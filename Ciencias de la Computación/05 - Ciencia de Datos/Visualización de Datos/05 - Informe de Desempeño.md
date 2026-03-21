## Construir una visualización simple y limpia con Pandas

El objetivo es mostrar un informe claro y profesional, sin sobrecargar la tabla.

```python
import pandas as pd

# Datos de ejemplo
datos = {
    "Empleado": ["Ana", "Luis", "Pedro", "María"],
    "Ventas": [1200, 1500, 1100, 1700],
    "Beneficio": [300, 400, 250, 500]
}

df = pd.DataFrame(datos)

# Visualización simple
df.style.format({
    "Ventas": "{:.0f}",
    "Beneficio": "{:.0f}"
})
```

Esto genera una tabla limpia con valores enteros.

---

### Alterar los bordes de la tabla

Podemos personalizar los bordes con CSS:

```python
df.style.set_table_styles(
    [{"selector": "td",
      "props": [("border", "1px solid black")]}]
)
```

Esto aplica un borde negro uniforme a todas las celdas.

---

### Destacar elementos específicos mediante selección

Podemos resaltar filas o columnas según condiciones:

```python
def resaltar_beneficio(val):
    return "background-color: lightgreen" if val > 400 else ""

df.style.applymap(resaltar_beneficio, subset=["Beneficio"])
```

Esto marca en verde los beneficios superiores a 400.

---

### Estructurar tablas académicas

Para informes académicos o profesionales, se pueden aplicar estilos más formales:

```python
df.style.set_table_styles({
    "": {"selector": "th",
         "props": [("background-color", "#f2f2f2"),
                   ("color", "black"),
                   ("font-weight", "bold"),
                   ("border", "1px solid gray")]}
})
```

Esto crea un encabezado con fondo gris claro y bordes definidos, ideal para documentos académicos.