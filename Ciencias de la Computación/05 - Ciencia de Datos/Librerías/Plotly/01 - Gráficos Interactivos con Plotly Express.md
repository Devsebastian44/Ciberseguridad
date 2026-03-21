## 1. Importar el módulo `express`

```python
import plotly.express as px
```

---

## 2. Crear un gráfico de líneas interactivo

```python
import pandas as pd

df = pd.DataFrame({
    "Año": [2020, 2021, 2022, 2023],
    "Ventas": [100, 150, 200, 250]
})

fig = px.line(df, x="Año", y="Ventas", title="Ventas por Año")
fig.show()
```

---

## 3. Explorar funcionalidades de Plotly

- Zoom interactivo.
- Hover con información detallada.
- Exportar imágenes.
- Guardar en HTML.
- Personalización de colores, estilos y tamaños.

---

## 4. Modificar el tamaño de un gráfico

```python
fig = px.line(df, x="Año", y="Ventas", title="Ventas por Año")
fig.update_layout(width=800, height=500)
fig.show()
```

---

## 5. Rotar los _ticks_ del eje X

```python
fig.update_layout(xaxis=dict(tickangle=-45))
fig.show()
```

---

## 6. Agregar título y etiquetas a los ejes

```python
fig.update_layout(
    title="Ventas por Año",
    xaxis_title="Año",
    yaxis_title="Ventas"
)
fig.show()
```

---

## 7. Personalizar gráficos

```python
fig.update_traces(line=dict(dash="dot", width=3))
fig.show()
```

---

## 8. Cambiar colores y agregar marcadores

```python
fig = px.line(df, x="Año", y="Ventas", markers=True)
fig.update_traces(line_color="red", marker=dict(size=10, symbol="circle"))
fig.show()
```

---

## 9. Guardar gráficos en formato HTML

```python
fig.write_html("grafico_interactivo.html")
```

---

# ✅ Resumen de la Clase

- **Importar express** → `import plotly.express as px`.
- **Gráfico de líneas interactivo** → `px.line()`.
- **Modificar tamaño** → `update_layout(width, height)`.
- **Rotar ticks** → `tickangle`.
- **Título y etiquetas** → `xaxis_title`, `yaxis_title`.
- **Personalización** → `update_traces()`.
- **Colores y marcadores** → `line_color`, `markers=True`.
- **Guardar en HTML** → `write_html()`.

---

¿Quieres que integre estas clases de **Matplotlib y Plotly** en un **índice unificado de visualización de datos** para tu repositorio, de modo que tengas todo centralizado y navegable en Obsidian?