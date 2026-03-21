## Introducción

NumPy es una de las librerías fundamentales de Python para el cálculo numérico y científico. Su principal aporte es el **manejo eficiente de arrays multidimensionales**, que permiten realizar operaciones matemáticas de manera rápida y vectorizada, sin necesidad de bucles explícitos.

---

## Crear arrays con secuencias numéricas

NumPy ofrece funciones para generar secuencias de números de manera eficiente:

- **`np.arange(start, stop, step)`**  
    Genera una secuencia con valores equidistantes según el paso indicado.

```python
import numpy as np
arr = np.arange(0, 10, 2)
print(arr)  # [0 2 4 6 8]
```

- **`np.linspace(start, stop, num)`**  
    Crea una secuencia de valores igualmente espaciados entre dos límites.

```python
arr = np.linspace(0, 1, 5)
print(arr)  # [0.   0.25 0.5  0.75 1.  ]
```

- **`np.ones(shape)` / `np.zeros(shape)`**  
    Arrays llenos de unos o ceros.

```python
np.ones((2,3))   # [[1. 1. 1.]
                 #  [1. 1. 1.]]
np.zeros(4)      # [0. 0. 0. 0.]
```

---

## Cargar archivos

NumPy permite leer y escribir datos en archivos de texto o binarios:

- **`np.loadtxt(filename, delimiter)`** 
    Carga datos desde un archivo de texto.

```python
data = np.loadtxt("datos.csv", delimiter=",")
print(data.shape)
```

- **`np.genfromtxt(filename, delimiter)`** 
    Similar a `loadtxt`, pero más flexible con datos faltantes.

```python
data = np.genfromtxt("datos.csv", delimiter=",", filling_values=0)
```

- **Guardar arrays**

```python
np.savetxt("salida.csv", arr, delimiter=",")
np.save("array.npy", arr)       # formato binario
np.load("array.npy")            # cargar binario
```

---

## Verificar las dimensiones de un array

Las dimensiones (shape) y el número de ejes (ndim) son esenciales:

- **`arr.shape`** → devuelve una tupla con las dimensiones.
- **`arr.ndim`** → número de dimensiones.
- **`arr.size`** → número total de elementos.

```python
arr = np.array([[1,2,3],[4,5,6]])
print(arr.shape)  # (2, 3)
print(arr.ndim)   # 2
print(arr.size)   # 6
```

---

## Realizar la transposición de un array

La transposición intercambia filas por columnas:

- **`arr.T`** → transpuesta rápida.
- **`np.transpose(arr)`** → equivalente.

```python
arr = np.array([[1,2,3],[4,5,6]])
print(arr.T)
# [[1 4]
#  [2 5]
#  [3 6]]
```

También se puede especificar el orden de los ejes:

```python
arr3d = np.arange(8).reshape(2,2,2)
print(np.transpose(arr3d, (1,0,2)))
```
