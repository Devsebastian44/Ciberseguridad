## Spark Shell (Scala)

El shell de Scala proporciona una interfaz interactiva REPL.

```bash
spark-shell
spark-shell --master local[4] --driver-memory 2g
```

### Comandos básicos

```scala
// SparkContext disponible como 'sc'
// SparkSession disponible como 'spark'

// Crear RDD
val data = sc.parallelize(1 to 100)

// Operaciones
val filtered = data.filter(_ % 2 == 0)
val result = filtered.collect()

// Leer archivo
val textFile = sc.textFile("README.md")
val wordCounts = textFile.flatMap(_.split(" "))
                        .map((_, 1))
                        .reduceByKey(_ + _)
```

---

## PySpark Shell

El shell de Python ofrece interfaz interactiva similar.

```bash
pyspark
pyspark --master local[4] --driver-memory 2g
```

### Comandos básicos

```python
# SparkContext disponible como 'sc'
# SparkSession disponible como 'spark'

# Crear RDD
data = sc.parallelize(range(1, 101))

# Operaciones
filtered = data.filter(lambda x: x % 2 == 0)
result = filtered.collect()

# Leer archivo
text_file = sc.textFile("README.md")
word_counts = text_file.flatMap(lambda line: line.split(" ")) \
                      .map(lambda word: (word, 1)) \
                      .reduceByKey(lambda a, b: a + b)
```

---

## Jupyter Notebook con PySpark

Configurar PySpark para trabajar con Jupyter.

```python
pip install findspark

import findspark
findspark.init()

import pyspark
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("JupyterApp").getOrCreate()
```

---

## Comandos útiles del shell

### Scala

```scala
:help      // Ayuda
:quit      // Salir
:type expr // Mostrar tipo de expresión
:load file // Cargar archivo Scala
```

### Python

```python
help()     # Ayuda
exit()     # Salir
%timeit    # Medir tiempo de ejecución (en Jupyter)
```

---
