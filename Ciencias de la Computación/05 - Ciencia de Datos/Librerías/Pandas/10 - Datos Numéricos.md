## Introducción

En Pandas podemos transformar listas, convertir texto en números y aplicar funciones a columnas o a todo el DataFrame para manipular datos de manera eficiente.

---

## Identificar y transformar elementos dentro de listas con `explode`

Cuando una columna contiene listas, `explode` separa cada elemento en una nueva fila:

```python
import pandas as pd

df = pd.DataFrame({
    "id": [1, 2],
    "valores": [[10, 20, 30], [40, 50]]
})

df_exploded = df.explode("valores")
````

**Resultado:**

|id|valores|
|---|---|
|1|10|
|1|20|
|1|30|
|2|40|
|2|50|

- **explode:** convierte listas en filas individuales.
- Útil para normalizar datos anidados.

---

## Transformar datos textuales en numéricos con `astype`

```python
df = pd.DataFrame({"edad": ["23", "30", "25"]})
df["edad"] = df["edad"].astype(int)
```

- Convierte cadenas en enteros.
- También se puede usar `float`, `str`, `bool`, etc.
- Útil para asegurar tipos correctos antes de cálculos.

---

## Tratar textos con datos numéricos usando `apply`

```python
df = pd.DataFrame({"precio": ["$100", "$200", "$300"]})

df["precio_num"] = df["precio"].apply(lambda x: int(x.replace("$", "")))
```

- **apply:** aplica una función a cada elemento de la columna.
- Aquí se eliminan símbolos y se convierten a enteros.
- Útil para limpiar datos textuales con números.

---

## Tratar varias columnas elemento por elemento con `applymap`

```python
df = pd.DataFrame({
    "A": ["1", "2", "3"],
    "B": ["4", "5", "6"]
})

df_num = df.applymap(int)
```

**Resultado:**

|A|B|
|---|---|
|1|4|
|2|5|
|3|6|

- **applymap:** aplica una función a **cada elemento del DataFrame**.
- Útil para transformar múltiples columnas a la vez.
- Diferencia con `apply`:
    - `apply` → trabaja por columna o fila.
    - `applymap` → trabaja por cada celda.
