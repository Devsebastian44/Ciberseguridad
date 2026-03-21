## Introducción a las Listas

En MongoDB, las listas se representan como **arrays** dentro de los documentos.

Los arrays pueden contener cualquier tipo de dato: strings, números, objetos, otros arrays, etc.

---

### Estructura Básica

```javascript
db.usuarios.insertMany([
    {
        nombre: "Juan Pérez",
        hobbies: ["lectura", "deportes", "música"],
        puntuaciones: [85, 92, 78, 96],
        direcciones: [
            {tipo: "casa", ciudad: "Madrid", calle: "Gran Vía 123"},
            {tipo: "trabajo", ciudad: "Madrid", calle: "Serrano 45"}
        ],
        tags: ["premium", "activo", "verificado"]
    },
    {
        nombre: "Ana García",
        hobbies: ["cocina", "viajes", "fotografía"],
        puntuaciones: [88, 91, 85],
        direcciones: [{tipo: "casa", ciudad: "Barcelona", calle: "Ramblas 67"}],
        tags: ["nuevo", "activo"]
    },
    {
        nombre: "Carlos López",
        hobbies: ["deportes", "tecnología"],
        puntuaciones: [92, 89, 94, 87, 91],
        direcciones: [],
        tags: ["premium", "verificado", "vip"]
    }
])
```

---

## Tipos de Arrays

```javascript
{colores: ["rojo", "azul", "verde"]}
{numeros: [1, 2, 3, 4, 5]}
{productos: [{nombre: "Laptop", precio: 899.99}, {nombre: "Mouse", precio: 25.50}]}
{datos: ["texto", 123, true, new Date(), {objeto: "valor"}]}
{matriz: [[1, 2], [3, 4], [5, 6]]}
```

---

## Búsqueda por Elementos

### Elemento Específico

```javascript
db.usuarios.find({hobbies: "deportes"})
db.usuarios.find({tags: "premium"})
db.usuarios.find({puntuaciones: 92})
```

---

### Coincidencia Exacta del Array

```javascript
db.usuarios.find({hobbies: ["lectura", "deportes", "música"]})
db.usuarios.find({tags: ["premium", "activo", "verificado"]})
```

---

### Arrays de Objetos

```javascript
db.usuarios.find({"direcciones.ciudad": "Madrid"})
db.usuarios.find({"direcciones.tipo": "casa"})
db.pedidos.find({"productos.precio": 899.99})
```

---

## Múltiples Condiciones

### $all

```javascript
db.usuarios.find({hobbies: {$all: ["deportes", "música"]}})
db.usuarios.find({tags: {$all: ["premium", "verificado"]}})
db.usuarios.find({puntuaciones: {$all: [85, 92]}})
```

---

### $in / $nin

```javascript
db.usuarios.find({hobbies: {$in: ["lectura", "cocina", "tecnología"]}})
db.usuarios.find({tags: {$in: ["premium", "vip"]}})
db.usuarios.find({hobbies: {$nin: ["deportes", "música"]}})
db.usuarios.find({tags: {$nin: ["nuevo", "inactivo"]}})
```

---

## Operadores Relacionales con Listas

### Comparación

```javascript
db.usuarios.find({puntuaciones: {$gt: 90}})
db.usuarios.find({puntuaciones: {$lt: 80}})
db.usuarios.find({puntuaciones: {$gte: 85, $lte: 95}})
```

---

### $elemMatch

```javascript
db.usuarios.find({
    direcciones: {$elemMatch: {ciudad: "Madrid", tipo: "casa"}}
})
db.pedidos.find({
    productos: {$elemMatch: {categoria: "Electrónicos", precio: {$gt: 500}}}
})
```

---

## Insertar Elementos en Listas

### $push / $each

```javascript
db.usuarios.updateOne({nombre: "Juan Pérez"}, {$push: {hobbies: "jardinería"}})
db.usuarios.updateOne({nombre: "Ana García"}, {$push: {puntuaciones: {$each: [87, 93, 91]}}})
```

---

### $addToSet

```javascript
db.usuarios.updateOne({nombre: "Carlos López"}, {$addToSet: {tags: {$each: ["premium", "vip"]}}})
```

---

## Ordenar Elementos

```javascript
db.usuarios.updateOne(
    {nombre: "Ana García"},
    {$push: {puntuaciones: {$each: [94], $sort: -1}}}
)
```

---

## Eliminar Elementos

### $pull / $pullAll / $pop

```javascript
db.usuarios.updateOne({nombre: "Juan Pérez"}, {$pull: {hobbies: "lectura"}})
db.usuarios.updateOne({nombre: "Ana García"}, {$pullAll: {puntuaciones: [85, 78]}})
db.usuarios.updateOne({nombre: "Carlos López"}, {$pop: {tags: 1}})
```

---

## Actualizar por Índice

```javascript
db.usuarios.updateOne({nombre: "Juan Pérez"}, {$set: {"hobbies.0": "natación"}})
db.usuarios.updateOne({nombre: "Ana García"}, {$set: {"puntuaciones.1": 95}})
db.usuarios.updateOne({nombre: "Carlos López"}, {$set: {"tags.$": "premium-plus"}})
```

---

## Obtener Elementos

```javascript
db.usuarios.find({nombre: "Juan Pérez"}, {hobbies: {$slice: 2}})
db.usuarios.find({nombre: "Ana García"}, {puntuaciones: {$slice: -3}})
```

---

## Búsqueda por Tamaño

```javascript
db.usuarios.find({hobbies: {$size: 3}})
db.usuarios.find({puntuaciones: {$size: 5}})
db.usuarios.find({tags: {$size: 2}})
```

---