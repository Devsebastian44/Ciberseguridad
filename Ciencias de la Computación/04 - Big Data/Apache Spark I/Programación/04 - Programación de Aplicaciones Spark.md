## Introducción

**SparkContext** es el punto de entrada principal para todas las funcionalidades de Spark.

Representa la conexión al **clúster** y se usa para crear RDD, acumuladores y variables broadcast.

---

## SparkContext

### Responsabilidades

**Funciones principales:**

1. **Configuración** de parámetros de la aplicación
2. **Conexión** al clúster (YARN, Mesos, Standalone)
3. **Distribución** de tareas a los executors
4. **Gestión** de recursos (memoria y CPU)
5. **Tolerancia** a fallos

---

### Arquitectura

```
Driver Program
├── SparkContext
│   ├── Cluster Manager (YARN/Mesos/Standalone)
│   └── Executors
│       ├── Task 1
│       ├── Task 2
│       └── Cache/Storage
```

---

## Crear SparkContext

**Inicialización básica y avanzada:**

```python
from pyspark import SparkContext, SparkConf

# Configuración básica
conf = SparkConf().setAppName("MyApp").setMaster("local[2]")
sc = SparkContext(conf=conf)

# Configuración avanzada
conf = SparkConf() \
    .setAppName("AdvancedApp") \
    .setMaster("local[4]") \
    .set("spark.executor.memory", "2g") \
    .set("spark.executor.cores", "2") \
    .set("spark.sql.adaptive.enabled", "true")

sc = SparkContext(conf=conf)
```

---

## SparkSession vs SparkContext

**Diferencias y relación:**

```python
# SparkSession (recomendado en Spark 2.0+)
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("MyApp") \
    .config("spark.executor.memory", "2g") \
    .getOrCreate()

# Obtener SparkContext
sc = spark.sparkContext
```

---

## Propiedades Importantes

**Información del contexto:**

```python
print(f"App Name: {sc.appName}")
print(f"Spark Version: {sc.version}")
print(f"Master URL: {sc.master}")
print(f"Default Parallelism: {sc.defaultParallelism}")

# Configuraciones
for key, value in sc.getConf().getAll():
    print(f"{key}: {value}")

# Estado del contexto
print(f"Is stopped: {sc._jsc.sc().isStopped()}")
```

---

## Inicialización por Lenguaje

### Python (PySpark)

**Ejemplo completo:**

```python
pip install pyspark

from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("PythonSparkApp") \
    .master("local[*]") \
    .config("spark.driver.memory", "2g") \
    .config("spark.executor.memory", "2g") \
    .getOrCreate()

sc = spark.sparkContext

data = sc.parallelize([1, 2, 3, 4, 5])
result = data.map(lambda x: x * 2).collect()
print(result)

spark.stop()
```

---

### Scala

**Ejemplo completo:**

```scala
import org.apache.spark.{SparkConf, SparkContext}
import org.apache.spark.sql.SparkSession

object ScalaSparkApp {
  def main(args: Array[String]): Unit = {
    val conf = new SparkConf()
      .setAppName("ScalaSparkApp")
      .setMaster("local[*]")
    
    val sc = new SparkContext(conf)
    
    val spark = SparkSession.builder()
      .appName("ScalaSparkApp")
      .master("local[*]")
      .getOrCreate()
    
    val data = sc.parallelize(List(1, 2, 3, 4, 5))
    val result = data.map(_ * 2).collect()
    println(result.mkString(", "))
    
    sc.stop()
  }
}
```

---

### Java

**Ejemplo completo:**

```java
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaSparkContext;
import org.apache.spark.sql.SparkSession;
import java.util.Arrays;
import java.util.List;

public class JavaSparkApp {
    public static void main(String[] args) {
        SparkConf conf = new SparkConf()
            .setAppName("JavaSparkApp")
            .setMaster("local[*]");
        
        JavaSparkContext sc = new JavaSparkContext(conf);
        
        SparkSession spark = SparkSession.builder()
            .appName("JavaSparkApp")
            .master("local[*]")
            .getOrCreate();
        
        List<Integer> data = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> result = sc.parallelize(data)
                                 .map(x -> x * 2)
                                 .collect();
        System.out.println(result);
        
        sc.stop();
        spark.stop();
    }
}
```

---****