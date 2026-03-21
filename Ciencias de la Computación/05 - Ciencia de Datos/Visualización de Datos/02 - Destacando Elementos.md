## Agrupar datos por valor total de ventas y beneficio obtenido

Podemos construir una visualización agrupando datos con `groupby`:

```python
import pandas as pd

# Datos de ejemplo
datos = {
    "Pedido": [1, 2, 3, 4, 5],
    "Cliente": ["Ana", "Luis", "Ana", "Pedro", "Luis"],
    "Ventas": [200, 150, 300, 400, 250],
    "Beneficio": [50, 40, 80, 120, 60]
}

df = pd.DataFrame(datos)

# Agrupar por cliente
agrupado = df.groupby("Cliente")[["Ventas", "Beneficio"]].sum()
agrupado
```

Resultado:

|Cliente|Ventas|Beneficio|
|---|---|---|
|Ana|500|130|
|Luis|400|100|
|Pedro|400|120|

---

## Destacar valores mínimos y máximos

Pandas incluye funciones **built-in** para resaltar extremos:

```python
agrupado.style.highlight_min(color="lightcoral") \
        .highlight_max(color="lightgreen")
```

Esto marcará en rojo los valores más bajos y en verde los más altos.

---

## Aplicar gradiente de color con `background_gradient`

El gradiente ayuda a visualizar magnitudes de forma progresiva:

```python
agrupado.style.background_gradient(cmap="Blues")
```

- `cmap` define la paleta de colores (ejemplo: `"Blues"`, `"Greens"`, `"coolwarm"`).

---

## Estilizar encabezados con propiedades CSS

Podemos personalizar el encabezado de la tabla:

```python
agrupado.style.set_table_styles({
    "": {"selector": "th",
         "props": [("background-color", "black"),
                   ("color", "white"),
                   ("font-weight", "bold")]}
})
```

Esto aplica un fondo negro y texto blanco a los encabezados.

---

## Otras funciones built-in para estilizar

Algunas funciones útiles:

- **`highlight_null`** → resalta valores nulos.

```python
df.style.highlight_null(null_color="yellow")
```

- **`bar`** → agrega barras proporcionales en las celdas.

```python
agrupado.style.bar(subset=["Ventas"], color="lightblue")
```

- **`format`** → personaliza el formato de los números.

```python
agrupado.style.format("{:.2f}")
```
