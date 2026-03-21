## Introducción

El **Multi-Index** en Pandas permite trabajar con agrupaciones jerárquicas de datos, facilitando análisis más complejos y flexibles.

---

## Crear agrupaciones a partir de más de una información simultáneamente

```python
import pandas as pd

df = pd.DataFrame({
    "ciudad": ["Quito", "Quito", "Cuenca", "Cuenca", "Guayaquil"],
    "año": [2024, 2025, 2024, 2025, 2024],
    "ventas": [100, 200, 150, 300, 400]
})

grupo = df.groupby(["ciudad", "año"])["ventas"].sum()
````

**Resultado:**

|ciudad|año|ventas|
|---|---|---|
|Cuenca|2024|150|
|Cuenca|2025|300|
|Guayaquil|2024|400|
|Quito|2024|100|
|Quito|2025|200|

---

## Seleccionar datos en DataFrames Multi-Index

```python
# Seleccionar ventas de Quito en 2025
grupo.loc[("Quito", 2025)]
```

---

## Cambiar la posición de los niveles jerárquicos de los índices

```python
grupo_swapped = grupo.swaplevel()
```

- **swaplevel():** intercambia el orden de los niveles del índice.
- Útil para reorganizar jerarquías.

---

## Seleccionar índices donde el valor sea máximo con `idxmax()`

```python
maximo = grupo.idxmax()
print(maximo)
```

**Resultado:**

```
('Guayaquil', 2024)
```

- Devuelve la combinación de índices donde el valor es máximo.

---

## Crear tablas dinámicas con `pivot_table()`

```python
tabla = pd.pivot_table(
    df,
    values="ventas",
    index="ciudad",
    columns="año",
    aggfunc="sum",
    fill_value=0
)
```

**Resultado:**

|ciudad|2024|2025|
|---|---|---|
|Cuenca|150|300|
|Guayaquil|400|0|
|Quito|100|200|

- **pivot_table():** reorganiza datos en formato tabla dinámica.
- Permite aplicar funciones de agregación (`sum`, `mean`, etc.).

---

## Crear múltiples gráficos desde un DataFrame con múltiples columnas usando `subplots`

```python
import matplotlib.pyplot as plt

tabla.plot(kind="bar", subplots=True, layout=(1,2), figsize=(10,4))
plt.show()
```

- **subplots=True:** genera un gráfico por cada columna.
- **layout=(1,2):** organiza los gráficos en 1 fila y 2 columnas.
- Útil para comparar visualmente diferentes períodos o categorías.