## Introducción

Las operaciones sobre **RDD** se dividen en **transformaciones** (lazy) y **acciones** (eager).

---

## Transformaciones Comunes

**Operaciones lazy:**

Las transformaciones crean nuevos RDD **sin ejecutarse** inmediatamente.

```python
# map
numbers = sc.parallelize([1, 2, 3, 4, 5])
squared = numbers.map(lambda x: x ** 2)  # [1, 4, 9, 16, 25]

# filter
evens = numbers.filter(lambda x: x % 2 == 0)  # [2, 4]

# flatMap
words = sc.parallelize(["hello world", "spark is great"])
all_words = words.flatMap(lambda line: line.split(" "))

# distinct
data = sc.parallelize([1, 2, 2, 3, 3, 3])
unique = data.distinct()  # [1, 2, 3]

# union
rdd1 = sc.parallelize([1, 2, 3])
rdd2 = sc.parallelize([4, 5, 6])
combined = rdd1.union(rdd2)

# intersection
rdd1 = sc.parallelize([1, 2, 3, 4])
rdd2 = sc.parallelize([3, 4, 5, 6])
common = rdd1.intersection(rdd2)

# subtract
diff = rdd1.subtract(rdd2)  # [1, 2]
```

---

## Transformaciones de Agrupación

**Operaciones de reorganización:**

```python
# groupBy
data = sc.parallelize([1, 2, 3, 4, 5, 6])
grouped = data.groupBy(lambda x: x % 2)

# sample
sample_data = data.sample(withReplacement=False, fraction=0.5, seed=42)

# coalesce
coalesced = data.coalesce(2)

# repartition
repartitioned = data.repartition(10)
```

---

## Acciones Principales

**Operaciones eager:**

Las acciones **disparan** la evaluación y retornan resultados.

```python
# collect
result = numbers.collect()

# count
total = numbers.count()

# first
first_elem = numbers.first()

# take
first_three = numbers.take(3)

# takeSample
sample = numbers.takeSample(withReplacement=False, num=3)

# reduce
sum_all = numbers.reduce(lambda a, b: a + b)

# fold
sum_with_initial = numbers.fold(0, lambda a, b: a + b)

# aggregate
def seq_op(acc, value):
    return (acc[0] + value, acc[1] + 1)

def comb_op(acc1, acc2):
    return (acc1[0] + acc2[0], acc1[1] + acc2[1])

sum_count = numbers.aggregate((0, 0), seq_op, comb_op)
average = sum_count[0] / sum_count[1]
```

---

## Operaciones de Guardado

**Persistencia de datos:**

```python
# Guardar como archivo de texto
numbers.saveAsTextFile("output/numbers")

# Guardar como archivo de secuencia
pairs = numbers.map(lambda x: (x, x**2))
pairs.saveAsSequenceFile("output/pairs")

# Guardar con compresión
numbers.saveAsTextFile("output/compressed", 
                      compressionCodecClass="org.apache.hadoop.io.compress.GzipCodec")
```

---