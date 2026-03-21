## Introducción

El agrupamiento de datos en Pandas permite reorganizar, transformar y analizar conjuntos de datos en diferentes formatos (wide vs. long) y aplicar funciones de agregación para obtener resúmenes útiles.

---

## Transformación de datos del formato wide a long

```python
import pandas as pd

df = pd.DataFrame({
    "id": [1, 2],
    "enero": [100, 200],
    "febrero": [150, 250]
})

df_long = df.melt(id_vars="id", var_name="mes", value_name="ventas")
````

---

## Diferencias entre formato wide y long

- **Wide:** columnas representan variables (ej. meses).
- **Long:** filas representan observaciones, más flexible para análisis.

---

## Crear agrupaciones de datos con `groupby`

```python
df = pd.DataFrame({
    "ciudad": ["Quito", "Quito", "Cuenca", "Cuenca", "Guayaquil"],
    "ventas": [100, 200, 150, 300, 400]
})

grupo = df.groupby("ciudad")["ventas"].sum()
```

---

## Dataset de ejemplo

```python
import pandas as pd

df = pd.DataFrame({
    "ciudad": ["Quito", "Quito", "Cuenca", "Cuenca", "Guayaquil"],
    "ventas": [100, 200, 150, 300, 400],
    "empleados": [10, 15, 8, 12, 20]
})
````

---

## Ejemplo con `sum`

```python
df.groupby("ciudad").sum()
```

**Resultado:**

|ciudad|ventas|empleados|
|---|---|---|
|Cuenca|450|20|
|Guayaquil|400|20|
|Quito|300|25|

---

## Ejemplo con `mean`

```python
df.groupby("ciudad").mean()
```

**Resultado:**

|ciudad|ventas|empleados|
|---|---|---|
|Cuenca|225.0|10.0|
|Guayaquil|400.0|20.0|
|Quito|150.0|12.5|

---

## Ejemplo con `median`

```python
df.groupby("ciudad").median()
```

**Resultado:**

|ciudad|ventas|empleados|
|---|---|---|
|Cuenca|225.0|10.0|
|Guayaquil|400.0|20.0|
|Quito|150.0|12.5|

---

## Ejemplo con `min`

```python
df.groupby("ciudad").min()
```

**Resultado:**

|ciudad|ventas|empleados|
|---|---|---|
|Cuenca|150|8|
|Guayaquil|400|20|
|Quito|100|10|

---

## Ejemplo con `max`

```python
df.groupby("ciudad").max()
```

**Resultado:**

|ciudad|ventas|empleados|
|---|---|---|
|Cuenca|300|12|
|Guayaquil|400|20|
|Quito|200|15|

---

## Ejemplo con `std` (desviación estándar)

```python
df.groupby("ciudad").std()
```

**Resultado:**

|ciudad|ventas|empleados|
|---|---|---|
|Cuenca|106.06|2.82|
|Guayaquil|NaN|NaN|
|Quito|70.71|3.53|

---

## Ejemplo con `var` (varianza)

```python
df.groupby("ciudad").var()
```

**Resultado:**

|ciudad|ventas|empleados|
|---|---|---|
|Cuenca|11250.0|8.0|
|Guayaquil|NaN|NaN|
|Quito|5000.0|12.5|

---
## Nota importante

- Si el DataFrame contiene **solo columnas numéricas**, no es necesario `numeric_only`.
- **`numeric_only=True`** → ignora columnas no numéricas.
- **`numeric_only=False`** → intenta incluir todas las columnas (puede dar error si hay texto).
- Si no se especifica, Pandas puede lanzar advertencias en versiones recientes.

---
## Construir gráficos de barras con `plot`

```python
import matplotlib.pyplot as plt

df.groupby("ciudad")["ventas"].sum().plot(kind="bar")
plt.title("Ventas por ciudad")
plt.ylabel("Total ventas")
plt.show()
```