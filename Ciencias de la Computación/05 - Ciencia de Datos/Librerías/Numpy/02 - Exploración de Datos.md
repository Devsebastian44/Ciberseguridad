## Realizar selecciones dentro de arrays

NumPy permite seleccionar elementos de un array de distintas formas:

- **Indexación simple**

```python
import numpy as np
 
arr = np.array([10, 20, 30, 40])
print(arr[0])   # 10
print(arr[-1])  # 40
```

- **Indexación múltiple**

```python
arr = np.array([10, 20, 30, 40])
print(arr[[0, 2]])  # [10 30]
```

- **Slicing (rebanado)**

```python
arr = np.arange(10)
print(arr[2:7])   # [2 3 4 5 6]
print(arr[:5])    # [0 1 2 3 4]
print(arr[::2])   # [0 2 4 6 8]
```

- **Selección booleana**

```python
arr = np.array([1, 2, 3, 4, 5])
print(arr[arr > 3])  # [4 5]
```

---

## Construir gráficos utilizando Matplotlib

Matplotlib es la librería estándar para visualización en Python. Se integra fácilmente con NumPy.

- **Gráfico de líneas**

```python
import matplotlib.pyplot as plt 
   
x = np.linspace(0, 10, 100)
y = np.sin(x)
  
plt.plot(x, y, label="Seno")
plt.xlabel("x")
plt.ylabel("y")
plt.title("Gráfico de Seno")
plt.legend()
plt.show()
```

- **Gráfico de dispersión**

```python
x = np.random.rand(50)
y = np.random.rand(50)
    
plt.scatter(x, y, color="red")
plt.title("Gráfico de dispersión")
plt.show()
```

- **Histograma**

```python
data = np.random.randn(1000)
plt.hist(data, bins=30, color="green")
plt.title("Histograma")
plt.show()
```


---

## Comparar arrays

NumPy permite comparar arrays elemento por elemento:

- **Comparación directa**

```python
a = np.array([1, 2, 3])
b = np.array([1, 4, 3])
    
print(a == b)   # [ True False  True]
print(a != b)   # [False  True False]
print(a < b)    # [False  True False]
```

- **Comparación global**

```python
np.array_equal(a, b)  # False
np.all(a == b)        # False
np.any(a == b)        # True
```

- **Comparación aproximada con** `np.allclose` Útil cuando se comparan arrays con valores de punto flotante que pueden diferir mínimamente.

```python
x = np.array([1.0, 2.0, 3.00001])
y = np.array([1.0, 2.0, 3.0])

print(np.allclose(x, y))  # True (diferencia dentro de tolerancia)
```

---

## Verificar la existencia de NaNs

Los valores **NaN (Not a Number)** aparecen en cálculos numéricos inválidos o datos faltantes.

- **Detectar NaNs**

```python
arr = np.array([1, np.nan, 3])
print(np.isnan(arr))  # [False  True False]
```

- **Filtrar NaNs**

```python
arr = np.array([1, np.nan, 3, np.nan])
print(arr[~np.isnan(arr)])  # [1. 3.]
```

- **Reemplazar NaNs**

```python
arr = np.array([1, np.nan, 3])
arr[np.isnan(arr)] = 0
print(arr)  # [1. 0. 3.]
```

## Calcular la media de un array

La función `np.mean` devuelve el promedio de los elementos de un array:

```python
arr = np.array([10, 20, 30, 40])
print(np.mean(arr))  # 25.0
```

También se puede calcular la media a lo largo de un eje específico:

```python
matriz = np.array([[1, 2, 3], [4, 5, 6]])

print(np.mean(matriz, axis=0))  # [2.5 3.5 4.5] (media por columnas)
print(np.mean(matriz, axis=1))  # [2. 5.]       (media por filas)
```