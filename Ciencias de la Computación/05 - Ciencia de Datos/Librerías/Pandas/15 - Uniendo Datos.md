## Introducción

El proceso de unión y manipulación de datos en Pandas permite filtrar, transformar, combinar y visualizar información de manera flexible.

---

## Filtrar valores que contengan parte de una string con `str.contains()`

```python
import pandas as pd

df = pd.DataFrame({
    "nombre": ["Ana", "Luis", "Pedro", "Maria"],
    "ciudad": ["Quito", "Guayaquil", "Cuenca", "Quito"]
})

# Filtrar filas donde la ciudad contenga "qui"
df_filtrado = df[df["ciudad"].str.contains("qui", case=False)]
````

**Resultado:**

|nombre|ciudad|
|---|---|
|Ana|Quito|
|Luis|Guayaquil|
|Maria|Quito|

---

## Crear columnas basadas en otras columnas con `assign()`

```python
df = df.assign(
    ciudad_mayus = df["ciudad"].str.upper(),
    nombre_ciudad = df["nombre"] + " - " + df["ciudad"]
)
```

- **assign():** crea nuevas columnas derivadas de otras.
- Se pueden aplicar funciones directamente.

---

## Utilizar expresiones regulares para buscar patrones textuales

```python
# Extraer solo nombres que empiezan con "A" o "M"
df_regex = df[df["nombre"].str.contains(r"^(A|M)", regex=True)]
```

- **regex:** permite buscar patrones complejos en cadenas.
- Ejemplo: `^` inicio, `(A|M)` letras permitidas.

---

## Reemplazar parte de una string con `replace()`

```python
df["ciudad"] = df["ciudad"].replace("Quito", "QUITO")
```

- **replace():** sustituye valores en columnas.
- Puede usarse con diccionarios para múltiples reemplazos:

```python
df["ciudad"] = df["ciudad"].replace({"Quito": "QUITO", "Cuenca": "CUENCA"})
```

---

## Unir DataFrames con `merge()`

```python
df1 = pd.DataFrame({
    "id": [1, 2, 3],
    "nombre": ["Ana", "Luis", "Pedro"]
})

df2 = pd.DataFrame({
    "id": [1, 2, 4],
    "ciudad": ["Quito", "Guayaquil", "Cuenca"]
})

df_merge = pd.merge(df1, df2, on="id", how="inner")
```

**Resultado (inner join):**

|id|nombre|ciudad|
|---|---|---|
|1|Ana|Quito|
|2|Luis|Guayaquil|

- **how="inner":** solo coincidencias.
- **how="left":** todos los de la izquierda.
- **how="right":** todos los de la derecha.
- **how="outer":** todos los registros.

---

## Crear gráficos interactivos con Plotly

```python
import plotly.express as px

# Gráfico de barras
fig_bar = px.bar(df_merge, x="nombre", y="id", color="ciudad", title="IDs por nombre y ciudad")
fig_bar.show()

# Gráfico de dispersión
fig_scatter = px.scatter(df_merge, x="id", y="nombre", color="ciudad", title="Dispersión de IDs")
fig_scatter.show()
```

- **px.bar():** gráfico de barras interactivo.
- **px.scatter():** gráfico de dispersión interactivo.
- Plotly permite zoom, hover y exportación dinámica.