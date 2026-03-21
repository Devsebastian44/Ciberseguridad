## Generar secuencias de números aleatorios

NumPy incluye el submódulo `numpy.random` para generar números aleatorios:

- **Números aleatorios uniformes**

```python
import numpy as np
 
arr = np.random.rand(5)   # 5 números entre 0 y 1
print(arr)
```

- **Números enteros aleatorios**

```python
arr = np.random.randint(1, 10, size=5)  # 5 enteros entre 1 y 9
print(arr)
```

- **Distribución normal**

```python
arr = np.random.randn(5)  # 5 números con distribución normal (media=0, var=1)
print(arr)
```

**Distribución uniforme en un rango específico con** `np.random.uniform` Genera números aleatorios dentro de un intervalo definido [low,high).

``` python
arr = np.random.uniform(10, 20, size=5)  # 5 números entre 10 y 20
print(arr)
```

---

## Garantizar la reproducibilidad de resultados

Cuando trabajamos con números aleatorios, es importante poder **reproducir** los mismos resultados.  
Para esto se usa la **semilla** (`seed`):

```python
np.random.seed(42)   # Fija la semilla
arr1 = np.random.rand(3)
arr2 = np.random.rand(3)

print(arr1)
print(arr2)
```

Cada vez que se ejecute este código con la misma semilla, se obtendrá los mismos números.

---

## Agrupar arrays

NumPy permite combinar arrays de distintas formas:

- **Concatenar horizontalmente (`hstack`)**

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(np.hstack([a, b]))  # [1 2 3 4 5 6]
```

- **Concatenar verticalmente (`vstack`)**

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(np.vstack([a, b]))
# [[1 2 3]
#  [4 5 6]]
```

- **Concatenar por columnas (`column_stack`)**

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
    
print(np.column_stack([a, b]))
# [[1 4]
#  [2 5]
#  [3 6]]
```
    

---

## Guardar archivos

NumPy permite guardar arrays en distintos formatos:

- **Guardar en texto**

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
np.savetxt("datos.txt", arr, delimiter=",")
```

- **Guardar en formato binario (`.npy`)**

```python
np.save("datos.npy", arr)
```

- **Cargar archivos**

```python
data_txt = np.loadtxt("datos.txt", delimiter=",")
data_npy = np.load("datos.npy")

print(data_txt)
print(data_npy)
```



