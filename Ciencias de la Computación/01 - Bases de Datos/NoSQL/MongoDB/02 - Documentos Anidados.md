## Introducción a los Documentos Anidados

Los documentos anidados en MongoDB permiten crear estructuras de datos complejas y jerárquicas.

Un documento anidado es un documento BSON embebido dentro de otro documento como valor de un campo.

---

## Tipos de Documentos Anidados

### Objetos Simples

```javascript
db.usuarios.insertOne({
    nombre: "Juan Pérez",
    edad: 30,
    direccion: {
        calle: "Gran Vía 123",
        ciudad: "Madrid",
        codigo_postal: "28013",
        pais: "España"
    },
    contacto: {
        email: "juan@email.com",
        telefono: "+34123456789",
        redes_sociales: {
            twitter: "@juanperez",
            linkedin: "juan-perez-123"
        }
    }
})
```

---

### Arrays de Objetos

```javascript
db.empleados.insertOne({
    nombre: "Ana García",
    puesto: "Desarrolladora",
    experiencia: [
        {
            empresa: "TechCorp",
            puesto: "Junior Developer",
            tecnologias: ["JavaScript", "React"]
        },
        {
            empresa: "InnovaSoft",
            puesto: "Senior Developer",
            tecnologias: ["Python", "Django"]
        }
    ],
    habilidades: {
        programacion: ["JavaScript", "Python"],
        bases_datos: ["MongoDB", "PostgreSQL"]
    }
})
```

---

### Anidamiento Profundo

```javascript
db.empresa.insertOne({
    nombre: "TechInnovate S.L.",
    sede: {
        direccion: {
            calle: "Paseo Castellana 95",
            ciudad: "Madrid"
        },
        oficinas: [
            {
                planta: 5,
                departamentos: [
                    {
                        nombre: "Desarrollo",
                        empleados: 15
                    }
                ]
            }
        ]
    }
})
```

---

## Ventajas

- Mantener datos relacionados juntos
- Reducir número de consultas
- Transacciones atómicas en un solo documento
- Modelado natural de relaciones uno-a-uno y uno-a-pocos

---

## Consideraciones de Diseño

- Límite de **16MB** por documento
- Máximo **100 niveles** de anidamiento
- Consultas complejas pueden ser difíciles
- Crecimiento ilimitado afecta rendimiento

---

## Dot Notation

### Sintaxis Básica

```javascript
"direccion.ciudad"
"array.0.campo"
```

---

### Consultas

```javascript
// Por campo anidado
db.usuarios.find({"direccion.ciudad": "Madrid"})

// En array de objetos
db.empleados.find({"experiencia.empresa": "TechCorp"})

// Con operadores
db.empleados.find({
    "experiencia.fecha_inicio": {$gte: new Date("2021-01-01")}
})
```

---

## Actualizar Elementos

### $set

```javascript
db.usuarios.updateOne(
    {nombre: "Juan Pérez"},
    {$set: {"direccion.ciudad": "Barcelona"}}
)
```

---

### $inc

```javascript
db.estadisticas.updateOne(
    {usuario: "juan123"},
    {$inc: {"metricas.visitas.total": 1}}
)
```

---

### $unset

```javascript
db.usuarios.updateOne(
    {nombre: "Juan Pérez"},
    {$unset: {"direccion.codigo_postal": ""}}
)
```

---

### $rename

```javascript
db.usuarios.updateOne(
    {nombre: "Juan Pérez"},
    {$rename: {"direccion.codigo_postal": "direccion.cp"}}
)
```

---

## Listado de Documentos

### Proyección

```javascript
db.usuarios.find(
    {},
    {nombre: 1, "direccion.ciudad": 1, _id: 0}
)
```

---

### Ordenamiento

```javascript
db.usuarios.find().sort({"direccion.ciudad": 1})
```

---

### Paginación

```javascript
db.usuarios.find().skip(10).limit(5)
```

---

## Agregación

### Agrupar

```javascript
db.usuarios.aggregate([
    {
        $group: {
            _id: "$direccion.ciudad",
            usuarios: {$push: "$nombre"},
            total: {$sum: 1}
        }
    }
])
```

---

### Estadísticas

```javascript
db.empleados.aggregate([
    {$unwind: "$experiencia"},
    {
        $group: {
            _id: "$experiencia.empresa",
            total: {$sum: 1}
        }
    }
])
```

---

## ElemMatch

```javascript
db.estudiantes.find({
    materias: {
        $elemMatch: {
            nota: {$gt: 90},
            profesor: "García"
        }
    }
})
```

---

## Proyecciones

### Básicas

```javascript
db.usuarios.find(
    {},
    {nombre: 1, direccion: 1, _id: 0}
)
```

---

### Con $slice

```javascript
db.empleados.find(
    {},
    {nombre: 1, experiencia: {$slice: 2}}
)
```

---

### Con $elemMatch

```javascript
db.estudiantes.find(
    {},
    {
        nombre: 1,
        materias: {$elemMatch: {nota: {$gte: 90}}}
    }
)
```

---