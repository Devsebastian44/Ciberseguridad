## Importar la biblioteca Pandas

La biblioteca **pandas** es esencial para la manipulación y análisis de datos en Python.

```python
import pandas as pd
````

---

## Leer y visualizar los datos

Podemos cargar un archivo CSV y revisar las primeras filas para comprender la estructura del dataset.

```python
# Cargar dataset
df = pd.read_csv("datos.csv")

# Visualizar las primeras filas
print(df.head())
```

---

## Verificar el tamaño del dataset

Es importante conocer cuántas filas y columnas tiene el dataset.

```python
# Dimensiones del dataset
print(df.shape)
```

Esto devuelve una tupla `(filas, columnas)`.

---

## Tabla con estadísticas descriptivas

Las estadísticas descriptivas permiten entender la distribución de los datos.

```python
# Estadísticas descriptivas
print(df.describe())
```

La tabla incluye métricas como: **media, desviación estándar, mínimo, máximo y cuartiles**.

---

## Matriz de correlación

La correlación mide la relación entre variables. Una matriz de correlación ayuda a identificar qué variables están más relacionadas.

```python
# Matriz de correlación
print(df.corr())
```

Visualización con un mapa de calor usando **seaborn**:

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Mapa de calor de correlaciones
sns.heatmap(df.corr(), annot=True, cmap="coolwarm")
plt.show()
```
