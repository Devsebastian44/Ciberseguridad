## Introducción

Las **colecciones paralelizadas** permiten convertir colecciones locales en RDD distribuidos.

---

## Colecciones Paralelizadas

### Ejemplos en Python

```python
# Crear RDD desde listas
numbers = sc.parallelize([1, 2, 3, 4, 5])
strings = sc.parallelize(["hello", "world", "spark"])

# Especificar número de particiones
data = sc.parallelize(range(1000), numSlices=10)

# Desde tuplas
pairs = sc.parallelize([("a", 1), ("b", 2), ("c", 3)])
```

---

### Ejemplos en Scala

```scala
val numbers = sc.parallelize(List(1, 2, 3, 4, 5))
val data = sc.parallelize(1 to 1000, numSlices = 10)
```

---

## Control de Particionamiento

**Gestión de particiones:**

```python
# Verificar particiones
print(f"Número de particiones: {rdd.getNumPartitions()}")

# Ver contenido de cada partición
def print_partition_content(index, iterator):
    print(f"Partición {index}: {list(iterator)}")

rdd.mapPartitionsWithIndex(print_partition_content).collect()
```

---

## Conjuntos de Datos Externos

### Archivos de Texto

**Lectura de archivos:**

```python
# Archivo único
text_rdd = sc.textFile("file:///path/to/file.txt")

# Múltiples archivos
text_rdd = sc.textFile("file:///path/to/directory/*.txt")

# Desde HDFS
hdfs_rdd = sc.textFile("hdfs://namenode:port/path/to/file")

# Desde S3
s3_rdd = sc.textFile("s3a://bucket/path/to/file")
```

---

### Archivos Estructurados

**Formatos comunes:**

```python
# JSON
json_rdd = sc.textFile("data.json").map(lambda x: json.loads(x))

# CSV
csv_rdd = sc.textFile("data.csv") \
           .map(lambda line: line.split(",")) \
           .filter(lambda row: len(row) > 1)

# Parquet (usando DataFrame)
df = spark.read.parquet("data.parquet")
parquet_rdd = df.rdd
```

---

### Bases de Datos

**Conexión JDBC:**

```python
# JDBC
df = spark.read \
    .format("jdbc") \
    .option("url", "jdbc:postgresql://localhost/test") \
    .option("dbtable", "employees") \
    .option("user", "username") \
    .option("password", "password") \
    .load()

jdbc_rdd = df.rdd
```

---

## Configuraciones Avanzadas

**Opciones de configuración:**

```python
# Configurar compresión
spark.conf.set("spark.sql.files.compressionCodecName", "gzip")

# Configurar encoding
text_rdd = sc.textFile("file.txt", use_unicode=True)

# Mínimo de particiones
text_rdd = sc.textFile("file.txt", minPartitions=8)
```