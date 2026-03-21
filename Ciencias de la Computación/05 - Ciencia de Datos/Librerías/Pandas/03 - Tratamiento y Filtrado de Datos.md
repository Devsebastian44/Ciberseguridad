## Introducción

El **tratamiento** y **filtrado** de datos es una parte esencial del análisis, ya que permite limpiar, organizar y preparar la información para su uso en procesos posteriores.

---

## Verificar si una Base de Datos Tiene Datos Nulos

```python
df.isnull().sum()
```

**Características:**

- Devuelve el **número de valores nulos** por columna.

---

**Para verificar si existen nulos en todo el DataFrame:**

```python
df.isnull().values.any()
```

---
## Realizar diferentes selecciones en una base de datos

### Usando condiciones

```python
df[df["Edad"] > 25]
df[(df["Edad"] > 25) & (df["Ciudad"] == "Quito")]
df.query("Edad > 25 and Ciudad != 'Guayaquil'")
```

### Usando `.isin()`

```python
df[df["Ciudad"].isin(["Quito", "Cuenca"])]
```

- Filtra filas donde la columna tiene valores dentro de una lista o conjunto.
- Equivalente a un `IN` en SQL.

### Usando `.loc[]`

```python
# Seleccionar fila con índice 0
df.loc[0]

# Seleccionar filas con índice 0 y 2, y columnas específicas
df.loc[[0, 2], ["Nombre", "Ciudad"]]
```

- `.loc[]` → selección por etiquetas (nombres de filas/columnas).
- `.iloc[]` → selección por posición numérica.

---

## Tratar los Datos Nulos

**Reemplazar nulos por un valor específico:**

```python
df.fillna(0)   # Reemplaza nulos por 0
df.fillna("Desconocido")   # Reemplaza nulos por texto
```

---

**Reemplazar nulos con la media de la columna:**

```python
df["Edad"].fillna(df["Edad"].mean(), inplace=True)
```

---

**Eliminar filas con nulos:**

```python
df.dropna()   # Elimina filas con al menos un nulo
```

---

**Eliminar columnas con nulos:**

```python
df.dropna(axis=1)   # Elimina columnas con al menos un nulo
```

---

## Eliminar Filas y Columnas de un DataFrame

**Eliminar filas por índice:**

```python
df.drop([0, 1])   # Elimina las filas con índices 0 y 1
```

---

**Eliminar columnas por nombre:**

```python
df.drop(columns=["Ciudad", "Edad"])
```

---

**Eliminar filas por índice con inplace:**

```python
df.drop(axis=0, inplace=True)
```

---

## Realizar Diferentes Selecciones en una Base de Datos

**Seleccionar filas por condición:**

```python
df[df["Edad"] > 25]
```

---

**Seleccionar filas con múltiples condiciones:**

```python
df[(df["Edad"] > 25) & (df["Ciudad"] == "Quito")]
```

---

**Usar query:**

```python
df.query("Edad > 25 and Ciudad != 'Guayaquil'")
```

---

## Guardar Datos en Formato CSV

```python
df.to_csv("datos_limpios.csv", index=False)
```

**Características:**

- `index=False` evita guardar la **columna de índices**.

---

**Especificar codificación:**

```python
df.to_csv("datos_limpios.csv", index=False, encoding="utf-8")
```

---

## Guardar Datos en un Archivo Excel

```python
df.to_excel("datos_limpios.xlsx", index=False)
```

**Características:**

- **Excel (.xls / .xlsx):** formato de hoja de cálculo ampliamente usado.

---

**Parámetros útiles:**

- `sheet_name="Hoja1"` → define el **nombre** de la hoja.
- `index=False` → evita guardar la columna de **índices**.
- `engine="openpyxl"` → motor recomendado para archivos `.xlsx`.

---

**Ejemplo con nombre de hoja personalizado:**

```python
df.to_excel("datos_limpios.xlsx", sheet_name="Clientes", index=False)
```

---

## Guardar Datos en un Archivo JSON

```python
df.to_json("datos_limpios.json", orient="records", indent=2)
```

**Características:**

- **JSON (JavaScript Object Notation):** formato ligero para **intercambio** de datos.

---

**Parámetros útiles:**

- `orient="records"` → cada fila se convierte en un **objeto JSON**.
- `orient="columns"` → organiza los datos por **columnas**.
- `indent=2` → añade **sangría** para que el archivo sea más legible.
- `lines=True` → guarda en formato **NDJSON** (una fila por línea).

---

**Ejemplo con orientación por columnas:**

```python
df.to_json("datos_limpios.json", orient="columns", indent=4)
```

---

## Utilizar el Método replace para Reemplazar Valores

**Reemplazar un valor específico:**

```python
df["Ciudad"].replace("Quito", "QUITO", inplace=True)
```

---

**Reemplazar múltiples valores:**

```python
df["Ciudad"].replace({"Quito": "QUITO", "Guayaquil": "GYE"}, inplace=True)
```

---

**Reemplazar valores numéricos:**

```python
df["Edad"].replace({25: 30, 30: 35}, inplace=True)
```

---