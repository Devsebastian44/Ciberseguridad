## Distribuciones de frecuencia con `value_counts()`

La función `value_counts()` de **pandas** permite obtener la frecuencia absoluta de cada categoría o valor en una serie.

```python
import pandas as pd

# Ejemplo: conteo de edades
edades = pd.Series([18, 20, 21, 20, 19, 18, 21, 22, 20])
frecuencia = edades.value_counts()
print(frecuencia)
````

**Salida:**

```
20    3
18    2
21    2
19    1
22    1
dtype: int64
```

- **Frecuencia absoluta:** número de veces que aparece cada valor.
- Se puede ordenar con `sort_index()` o `sort_values()`.

---

## Distribuciones cruzadas con `crosstab()`

La función `crosstab()` permite analizar la relación entre dos variables categóricas.

```python
# Ejemplo: género y preferencia de producto
datos = pd.DataFrame({
    'Genero': ['M', 'F', 'M', 'F', 'M', 'F'],
    'Producto': ['A', 'A', 'B', 'B', 'A', 'C']
})

tabla_cruzada = pd.crosstab(datos['Genero'], datos['Producto'])
print(tabla_cruzada)
```

**Salida:**

```
Producto  A  B  C
Genero            
F         1  1  1
M         2  1  0
```

---

## Distribuciones con clases personalizadas (`cut()` + `value_counts()`)

Cuando los datos son **continuos**, se agrupan en intervalos o clases.

```python
# Ejemplo: agrupar edades en intervalos
intervalos = pd.cut(edades, bins=[17, 19, 21, 23])
frecuencia_clases = intervalos.value_counts()
print(frecuencia_clases)
```

**Salida:**

```
(17, 19]    3
(19, 21]    4
(21, 23]    2
dtype: int64
```

---

## Regla de Sturges

La **Regla de Sturges** se utiliza para calcular el número óptimo de clases en un histograma:

[ k = 1 + \log_2(n) ]

donde:

- (k) = número de clases
- (n) = tamaño de la muestra

```python
import numpy as np

n = len(edades)
k = int(1 + np.log2(n))
print("Número óptimo de clases según Sturges:", k)
```

---

## Histogramas

El histograma es la representación gráfica de una distribución de frecuencias.

```python
import matplotlib.pyplot as plt

plt.hist(edades, bins=k, edgecolor='black')
plt.title("Histograma de Edades")
plt.xlabel("Edades")
plt.ylabel("Frecuencia")
plt.show()
```