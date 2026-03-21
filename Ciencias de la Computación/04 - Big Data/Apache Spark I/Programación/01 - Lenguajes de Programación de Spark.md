## Introducción

**Spark** soporta múltiples lenguajes de programación, siendo Scala y Python los más populares.

---

## Scala en Spark

**Lenguaje nativo de Spark:**

Scala es el lenguaje **nativo** de Spark y ofrece el mejor rendimiento.

---

### Ventajas

**Beneficios de Scala:**

- Rendimiento **óptimo** (sin overhead)
- Acceso **completo** a la API de Spark
- **Compilación estática** reduce errores
- **Interoperabilidad** con Java

---

### Sintaxis Básica

**Ejemplos de código:**

```scala
// Variables
val immutableVar = "Hello"
var mutableVar = "World"

// Funciones
def add(x: Int, y: Int): Int = x + y

// Colecciones
val numbers = List(1, 2, 3, 4, 5)
val doubled = numbers.map(_ * 2)

// Pattern matching
val message = numbers.length match {
  case 0 => "Empty list"
  case 1 => "Single element"
  case _ => "Multiple elements"
}
```

---

## Python en Spark (PySpark)

**API de Python:**

Python ofrece **facilidad de uso** y gran ecosistema.

---

### Ventajas

**Beneficios de Python:**

- Sintaxis **simple** y legible
- Gran ecosistema de **librerías**
- **Popularidad** en ciencia de datos
- Integración con **pandas, numpy, matplotlib**

---

### Configuración de PySpark

**Inicialización básica:**

```python
from pyspark.sql import SparkSession
from pyspark import SparkContext, SparkConf

# Crear SparkSession
spark = SparkSession.builder \
    .appName("MyApp") \
    .config("spark.executor.memory", "2g") \
    .getOrCreate()

# Obtener SparkContext
sc = spark.sparkContext
```

---

## Comparación de Rendimiento

**Scala vs Python:**

|Aspecto|Scala|Python|
|---|---|---|
|**Velocidad**|Excelente|Bueno (con overhead)|
|**Facilidad**|Moderado|Excelente|
|**Ecosistema**|Java/Scala|Python científico|
|**Debugging**|Compilación|Runtime|
|**Curva de aprendizaje**|Pronunciada|Suave|

---