## ¿Qué es MongoDB?

MongoDB es una base de datos NoSQL orientada a documentos que almacena datos en formato BSON.  
A diferencia de las bases de datos relacionales, usa colecciones y documentos en lugar de tablas y filas.

### Características principales

- Orientada a documentos (BSON)
- Esquema flexible
- Escalabilidad horizontal (sharding)
- Consultas ricas y agregaciones
- Indexación avanzada

### Conceptos básicos

- **Base de datos**: contenedor físico de colecciones
- **Colección**: grupo de documentos (similar a tabla)
- **Documento**: registro individual en BSON (similar a fila)
- **Campo**: par clave-valor (similar a columna)

---

## Instalación

### Windows

1. Descargar desde [mongodb.com](https://www.mongodb.com/try/download/community)
2. Ejecutar instalador `.msi`
3. Seguir asistente
4. Configurar como servicio

### macOS

```bash
brew tap mongodb/brew
brew install mongodb-community
brew services start mongodb-community
```

### Linux (Ubuntu)

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl start mongod
sudo systemctl enable mongod
```

### MongoDB Compass (GUI)

Interfaz gráfica oficial para MongoDB.

### Conexión

```bash
mongo    # shell antigua
mongosh  # nueva shell
```

---

## Crear Documentos

### Insertar uno

```javascript
db.usuarios.insertOne({
    nombre: "Juan Pérez",
    edad: 30,
    email: "juan@email.com",
    fecha_registro: new Date()
})
```

### Insertar múltiples

```javascript
db.usuarios.insertMany([
    {nombre: "Ana", edad: 25, ciudad: "Madrid"},
    {nombre: "Carlos", edad: 35, ciudad: "Barcelona"},
    {nombre: "María", edad: 28, ciudad: "Valencia"}
])
```

### Insert con validación

```javascript
try {
    db.productos.insertOne({nombre: "Laptop", precio: 899.99})
    print("Documento insertado exitosamente")
} catch (e) {
    print("Error: " + e)
}
```

---

## Consultas

### Básicas

```javascript
db.usuarios.find()
db.usuarios.find().pretty()
```

### Con criterios

```javascript
db.usuarios.find({nombre: "Juan Pérez"})
db.usuarios.find({edad: 30, ciudad: "Madrid"})
db.usuarios.find({edad: {$gte: 25}}, {nombre: 1, email: 1, _id: 0})
```

### Limitar y ordenar

```javascript
db.usuarios.find().limit(5)
db.usuarios.find().sort({edad: 1})
db.usuarios.find().sort({edad: -1}).limit(10).skip(5)
```

---

## Operadores Relacionales y Lógicos

### Comparación

```javascript
db.usuarios.find({edad: {$eq: 30}})
db.usuarios.find({edad: {$gt: 25}})
db.usuarios.find({edad: {$gte: 25}})
db.usuarios.find({edad: {$lt: 35}})
db.usuarios.find({edad: {$lte: 35}})
db.usuarios.find({edad: {$ne: 30}})
```

### $in y $nin

```javascript
db.usuarios.find({ciudad: {$in: ["Madrid","Barcelona"]}})
db.usuarios.find({ciudad: {$nin: ["Madrid","Barcelona"]}})
```

### Lógicos

```javascript
db.usuarios.find({$and: [{edad: {$gte: 25}}, {ciudad: "Madrid"}]})
db.usuarios.find({$or: [{edad: {$lt: 25}}, {edad: {$gt: 60}}]})
db.usuarios.find({edad: {$not: {$gte: 30}}})
db.usuarios.find({$nor: [{edad: {$lt: 25}}, {ciudad: "Madrid"}]})
```

---

## Expresiones Regulares

```javascript
db.usuarios.find({nombre: {$regex: "^Juan"}})
db.usuarios.find({email: {$regex: "gmail.com$"}})
db.usuarios.find({nombre: {$regex: "juan", $options: "i"}})
```

---

## Arrays y Documentos Anidados

### Arrays

```javascript
db.usuarios.find({hobbies: "deportes"})
db.usuarios.find({idiomas: {$all: ["español","francés"]}})
db.usuarios.find({"hobbies.0": "lectura"})
```

### Documentos anidados

```javascript
db.empleados.find({"direccion.ciudad": "Madrid"})
db.empleados.find({"contacto.email": /empresa.com$/})
```

---

## Actualizaciones

### Básicas

```javascript
db.usuarios.updateOne({nombre: "Juan"}, {$set: {edad: 31}})
db.usuarios.updateMany({ciudad: "Madrid"}, {$set: {pais: "España"}})
db.usuarios.replaceOne({nombre: "Juan"}, {nombre: "Juan García", edad: 32})
```

### Operadores

```javascript
$set, $unset, $inc, $mul, $min, $max
```

### Arrays

```javascript
$push, $addToSet, $pull, $pop
```

---

## Eliminaciones

```javascript
db.usuarios.deleteOne({nombre: "Juan"})
db.usuarios.deleteMany({activo: false})
db.usuarios.findOneAndDelete({email: "temporal@email.com"})
db.logs.drop()
```

---

## Cursores

```javascript
db.usuarios.find().limit(5)
db.usuarios.find().skip(10).limit(5)
db.usuarios.find().sort({edad: -1})
db.usuarios.countDocuments({activo: true})
```

---
