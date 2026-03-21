## Construir una visualización basada en variables temporales

Cuando trabajamos con grandes volúmenes de datos, las **variables temporales** (fechas, horas) son clave para organizar la información.

```python
import pandas as pd

# Datos de ejemplo con fechas
datos = {
    "Fecha": pd.date_range("2024-01-01", periods=6, freq="M"),
    "Ventas": [200, 340, 560, 230, 400, 300],
    "Beneficio": [50, 80, 120, 40, 90, 70]
}

df = pd.DataFrame(datos)

# Agrupar por año
df["Año"] = df["Fecha"].dt.year
df.groupby("Año")[["Ventas", "Beneficio"]].sum()
```

Esto permite visualizar tendencias anuales o mensuales.

---

## Modelar una tabla dinámica

Las **tablas dinámicas** (`pivot_table`) permiten resumir grandes cantidades de datos:

```python
pivot = pd.pivot_table(df,
                       values="Ventas",
                       index="Año",
                       columns=df["Fecha"].dt.month,
                       aggfunc="sum",
                       fill_value=0)
pivot
```

Resultado: una tabla con ventas por año y mes.

---

## Fijar la columna de índice

Para mejorar la navegación en tablas grandes, podemos fijar índices:

```python
df.set_index("Fecha", inplace=True)
df.head()
```

Esto convierte la columna `Fecha` en índice, facilitando operaciones temporales.

---

## Mejorar la visualización de una tabla con muchos datos

El objeto `style` ayuda a destacar información en tablas extensas:

```python
df.style.background_gradient(cmap="Blues") \
        .highlight_max(color="lightgreen") \
        .highlight_min(color="lightcoral")
```

Esto aplica gradientes y resalta valores extremos.

---

## Diferenciar los métodos `pivot_table` y `pivot`

|Método|Características principales|
|---|---|
|**pivot**|Reorganiza datos sin aplicar funciones de agregación. Requiere que los valores sean únicos en la combinación de índices y columnas.|
|**pivot_table**|Permite aplicar funciones de agregación (`sum`, `mean`, `count`, etc.). Maneja duplicados y valores faltantes con mayor flexibilidad.|

Ejemplo comparativo:

```python
# pivot: reorganiza datos
df.pivot(index="Año", columns=df["Fecha"].dt.month, values="Ventas")

# pivot_table: agrega datos
df.pivot_table(values="Ventas", index="Año", columns=df["Fecha"].dt.month, aggfunc="sum")
```
