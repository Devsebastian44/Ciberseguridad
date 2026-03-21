## Introducción

Las **variables compartidas** y **Pair RDD** permiten gestionar datos de forma eficiente en operaciones distribuidas.

---

## Variables Broadcast

**Compartir datos de solo lectura:**

Las variables broadcast permiten compartir eficientemente datos de **solo lectura**.

```python
lookup_table = {"A": 1, "B": 2, "C": 3}
broadcast_lookup = sc.broadcast(lookup_table)

def map_values(x):
    return broadcast_lookup.value.get(x, 0)

data = sc.parallelize(["A", "B", "C", "D"])
mapped = data.map(map_values)  # [1, 2, 3, 0]

broadcast_lookup.unpersist()
```

---

## Acumuladores

**Agregar información desde workers:**

Los acumuladores permiten **agregar información** desde los workers.

```python
counter = sc.accumulator(0)

def process_line(line):
    global counter
    if "ERROR" in line:
        counter.add(1)
    return line.upper()

log_lines = sc.textFile("log.txt")
processed = log_lines.map(process_line)

processed.count()
print(f"Líneas con ERROR: {counter.value}")
```

---

### Acumuladores Personalizados

**Crear acumuladores custom:**

```python
from pyspark.util import AccumulatorParam

class ListAccumulatorParam(AccumulatorParam):
    def zero(self, value):
        return []
    def addInPlace(self, list1, list2):
        list1.extend(list2)
        return list1

list_accum = sc.accumulator([], ListAccumulatorParam())

def collect_errors(line):
    if "ERROR" in line:
        list_accum.add([line])
    return line

log_lines.map(collect_errors).count()
print(f"Errores encontrados: {list_accum.value}")
```

---

## Pair RDD (Pares Clave-Valor)

**RDD con tuplas clave-valor:**

Los Pair RDD son RDD que contienen **tuplas de clave-valor**.

```python
pairs = sc.parallelize([("a", 1), ("b", 2), ("c", 3)])
data = sc.parallelize(["hello", "world", "hello", "spark"])
word_pairs = data.map(lambda word: (word, 1))
```

---

### Transformaciones Específicas

**Operaciones sobre Pair RDD:**

```python
# Reducir por clave
word_counts = word_pairs.reduceByKey(lambda a, b: a + b)

# Agrupar por clave
grouped = word_pairs.groupByKey()

# Transformar valores
doubled_values = pairs.mapValues(lambda x: x * 2)

# Extraer claves y valores
all_keys = pairs.keys()
all_values = pairs.values()

# Ordenar por clave
sorted_pairs = pairs.sortByKey()

# Joins
rdd1 = sc.parallelize([("a", 1), ("b", 2)])
rdd2 = sc.parallelize([("a", 10), ("b", 20)])
joined = rdd1.join(rdd2)
left_joined = rdd1.leftOuterJoin(rdd2)
right_joined = rdd1.rightOuterJoin(rdd2)
cogrouped = rdd1.cogroup(rdd2)
```

---

## Particionamiento para Pair RDD

**Optimización de distribución:**

```python
# Hash partitioning
hash_partitioned = pairs.partitionBy(4)

# Range partitioning
range_partitioned = pairs.sortByKey().partitionBy(4)

# Verificar partitioner
print(hash_partitioned.partitioner)

# Persistir con particionamiento
hash_partitioned.persist()
```

---

## Análisis de Logs

**Ejemplo práctico:**

```python
logs = sc.textFile("access.log")
ips = logs.map(lambda line: line.split()[0])

# Contar IPs
ip_counts = ips.map(lambda ip: (ip, 1)) \
              .reduceByKey(lambda a, b: a + b)

# Top 10 IPs
top_ips = ip_counts.takeOrdered(10, key=lambda x: -x[1])

# Guardar resultados
ip_counts.saveAsTextFile("output/ip_analysis")
```