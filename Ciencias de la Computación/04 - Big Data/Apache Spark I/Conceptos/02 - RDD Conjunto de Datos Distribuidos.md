## Introducción

Los **RDD (Resilient Distributed Datasets)** son la abstracción fundamental de datos en Spark.

---

## Características

**Propiedades principales:**

1. **Resilientes:** tolerantes a fallos mediante linaje de transformaciones
2. **Distribuidos:** particionados a través del clúster
3. **Inmutables:** no se pueden modificar una vez creados
4. **Evaluación perezosa:** las transformaciones se evalúan solo cuando se necesitan

---

## Creación de RDD

**Métodos de creación:**

```python
# Parallelizar una colección
data = [1, 2, 3, 4, 5]
rdd = sc.parallelize(data)

# Desde archivo de texto
rdd = sc.textFile("path/to/file.txt")

# Desde archivo CSV
rdd = sc.textFile("data.csv").map(lambda line: line.split(","))
```

---

## Operaciones sobre RDD

### Transformaciones (Lazy Evaluation)

**Operaciones comunes:**

- **`map()`:** aplica una función a cada elemento
- **`filter()`:** filtra elementos según condición
- **`flatMap()`:** aplica función y aplana resultado
- **`union()`:** une dos RDD
- **`distinct()`:** elimina duplicados

---

### Acciones (Trigger Evaluation)

**Operaciones de ejecución:**

- **`collect()`:** retorna todos los elementos al driver
- **`count()`:** cuenta elementos
- **`first()`:** retorna el primer elemento
- **`take(n)`:** retorna los primeros n elementos
- **`reduce()`:** agrega elementos con una función

---

**Ejemplo completo:**

```python
numbers = sc.parallelize([1,2,3,4,5,6,7,8,9,10])

# Transformaciones
even_numbers = numbers.filter(lambda x: x % 2 == 0)
squared_numbers = even_numbers.map(lambda x: x ** 2)

# Acción
result = squared_numbers.collect()  # [4, 16, 36, 64, 100]
```

---

## Particionamiento de RDD

**Gestión de particiones:**

El particionamiento afecta el **rendimiento** y la **distribución** de datos.

```python
# Crear RDD con particiones específicas
rdd = sc.parallelize(data, numSlices=4)

# Verificar número de particiones
print(rdd.getNumPartitions())

# Reparticionar
rdd_repartitioned = rdd.repartition(8)
```