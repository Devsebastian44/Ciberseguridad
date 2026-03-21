## Construir una tabla de distribución de valores

Podemos usar funciones como `value_counts` o `groupby` para generar distribuciones:

```python
import pandas as pd

# Datos de ejemplo
datos = {
    "Producto": ["A", "B", "A", "C", "B", "A", "C", "C"],
    "Ventas": [120, 340, 200, 560, 230, 150, 400, 300]
}

df = pd.DataFrame(datos)

# Distribución de productos
distribucion = df["Producto"].value_counts().reset_index()
distribucion.columns = ["Producto", "Frecuencia"]
distribucion
```

Resultado:

|Producto|Frecuencia|
|---|---|
|A|3|
|C|3|
|B|2|

---

## Estilizar todos los elementos de la tabla con CSS

Podemos aplicar estilos globales con `set_table_styles`:

```python
distribucion.style.set_table_styles(
    [{"selector": "td",
      "props": [("background-color", "lightyellow"),
                ("color", "black"),
                ("border", "1px solid gray")]}]
)
```

Esto aplica un fondo amarillo claro y bordes grises a todas las celdas.

---

## Añadir una visualización gráfica en la tabla

Podemos usar la función `bar` para representar valores con barras dentro de las celdas:

```python
distribucion.style.bar(subset=["Frecuencia"], color="lightblue")
```

Esto añade una barra proporcional al valor de cada frecuencia.

---

## Utilizar otras funciones built-in para estilizar tablas

Algunas funciones útiles para enriquecer la visualización:

- **`highlight_min` / `highlight_max`** → resaltar valores extremos.

```python
distribucion.style.highlight_min(color="lightcoral") \
            .highlight_max(color="lightgreen")
```

- **`background_gradient`** → aplicar gradiente de color.

```python
distribucion.style.background_gradient(cmap="coolwarm")
```

- **`format`** → personalizar formato de números.

```python
distribucion.style.format({"Frecuencia": "{:.0f}"})
```
