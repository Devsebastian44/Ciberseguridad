## Preparar tus datos para la demanda del proyecto

Antes de estilizar tablas, es fundamental organizar los datos:

- **Importar librerías necesarias**:

```python
import pandas as pd
import numpy as np
```

- **Definir la fuente de datos**: puede ser un archivo CSV, Excel, JSON o incluso datos generados manualmente.

```python
datos = {
    "Producto": ["A", "B", "C", "D"],
    "Ventas": [120, 340, 560, 230],
    "Stock": [20, 15, 30, 10]
}
```

- **Convertir a DataFrame**:

```python
df = pd.DataFrame(datos)
```

---

## Construir un DataFrame para clasificar elementos

El **DataFrame** es la estructura central de Pandas para manejar datos tabulares.

- **Ejemplo de clasificación**:

```python
df["Categoria"] = np.where(df["Ventas"] > 300, "Alta", "Baja")
```

- Resultado:
    
    |Producto|Ventas|Stock|Categoria|
    |---|---|---|---|
    |A|120|20|Baja|
    |B|340|15|Alta|
    |C|560|30|Alta|
    |D|230|10|Baja|
    

---

## Trabajar con el objeto `style` para construir una visualización

El objeto `style` de Pandas permite aplicar **formato visual** a las tablas.

- **Resaltar valores máximos**:

```python
df.style.highlight_max(color="lightgreen")
```

- **Aplicar formato numérico**:

```python
df.style.format({
    "Ventas": "{:.0f}",
    "Stock": "{:.0f}"
})
```

- **Colorear según condición**:

```python
def color_categoria(val):
    return "background-color: lightblue" if val == "Alta" else "background-color: pink"

df.style.applymap(color_categoria, subset=["Categoria"])
```

---

## Exportar el objeto `style` a otros formatos

Una vez creada la visualización, se puede exportar:

- **HTML**:

```python
df.style.to_html("tabla_estilizada.html")
```

- **Excel**:

```python
df.style.to_excel("tabla_estilizada.xlsx", engine="openpyxl")
```

- **LaTeX** (para documentos académicos):

```python
df.style.to_latex("tabla_estilizada.tex")
```
