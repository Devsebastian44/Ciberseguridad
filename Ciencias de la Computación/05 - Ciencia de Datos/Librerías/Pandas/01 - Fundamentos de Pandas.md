## Introducción

Pandas es una biblioteca poderosa para el **análisis** y **manipulación** de datos en Python. A continuación se presentan conceptos básicos y ejemplos prácticos, ampliados para cubrir CSV, Excel, JSON, HTML y conexiones a MySQL.

---

## Importar la Biblioteca Pandas

```python
import pandas as pd
```

- **Alias recomendado:** `pd` para escribir de forma concisa.
- **Uso típico:** `pd.DataFrame()`, `pd.read_csv()`, `pd.read_excel()`, `pd.read_json()`.

---

## Lectura de Archivos CSV

```python
df = pd.read_csv("datos.csv")
```

**Opciones importantes:**

- **Separador:** `sep=";"` si no es coma.
- **Codificación:** `encoding="utf-8"` para caracteres especiales.
- **Cabecera:** `header=0` o `names=[...]` si no hay encabezados.
- **Tipos:** `dtype={"col": "int64"}` para forzar tipos.
- **Fechas:** `parse_dates=["fecha"]` para parsear columnas de fecha.

---

**Ejemplo con opciones:**

```python
df = pd.read_csv("datos.csv", sep=";", encoding="utf-8", parse_dates=["fecha"])
```

---

## Identificar un DataFrame

```python
data = {
    "Nombre": ["Ana", "Luis", "Pedro"],
    "Edad": [23, 30, 25],
    "Ciudad": ["Quito", "Guayaquil", "Cuenca"]
}
df = pd.DataFrame(data)
```

**Características:**

- **Estructura:** tabla con filas (index) y columnas (labels).
- **Index personalizado:** `pd.DataFrame(data, index=["a","b","c"])`.

---

## Visualizar Primeras y Últimas Filas

```python
df.head()      # primeras 5
df.head(10)    # primeras 10
df.tail()      # últimas 5
df.tail(3)     # últimas 3
```

---

## Ver Cantidad de Filas y Columnas

```python
df.shape        # (filas, columnas)
df.columns      # saber cuales son las columnas
print(df.shape[0], df.shape[1])
```

**Alternativas:**

- **Filas:** `len(df)`
- **Columnas:** `len(df.columns)`

---

## Comprobar Tipos de Datos por Columna

```python
df.dtypes
```

**Opciones adicionales:**

- **Vista detallada:** `df.info()` muestra conteo de no nulos y memoria.
- **Conversión:** `df = df.astype({"Edad": "int64"})`

---

## Seleccionar una o Varias Columnas

```python
df["Nombre"]           # Serie
df[["Nombre", "Edad"]] # DataFrame
df.Nombre              # notación atributo (si nombre válido)
```

---

**Filtrar filas y columnas:**

- **`loc`:** `df.loc[filas, columnas]`
- **`iloc`:** `df.iloc[filas, columnas]`

```python
df.loc[df["Edad"] > 25, ["Nombre", "Edad"]]
df.iloc[:5, :2]
```

---

## Lectura de Archivos Excel xls y xlsx

```python
df = pd.read_excel("archivo.xlsx")
```

**Opciones importantes:**

- **Hoja específica:** `sheet_name="Ventas"` o por índice `sheet_name=0`.
- **Varias hojas:** devuelve dict si pasas lista de hojas.

---

**Ejemplo con opciones:**

```python
df_ventas = pd.read_excel("archivo.xlsx", sheet_name="Ventas")
hojas = pd.read_excel("archivo.xlsx", sheet_name=["Ventas", "Compras"])
```

---

**Opciones adicionales:**

- **Tipo de motor:** `engine="openpyxl"` para .xlsx, `engine="xlrd"` para .xls.
- **Seleccionar columnas:** `usecols=["Fecha","Total"]` o `usecols="A:C"`.
- **Parseo de fechas:** `parse_dates=["Fecha"]`.

```python
df = pd.read_excel("archivo.xls", sheet_name=0, usecols="A:D", parse_dates=["Fecha"])
```

---

## Lectura de JSON

```python
df = pd.read_json("datos.json")
```

**Orientación del JSON:**

- **Lista de objetos:** `[{"a":1,"b":2}, ...]` funciona directo.
- **Registros:** usar `orient="records"`.
- **Columnas:** `orient="columns"` para dict por columnas.

---

**Ejemplo con registros:**

```python
json_str = '[{"nombre":"Ana","edad":23},{"nombre":"Luis","edad":30}]'
df = pd.read_json(json_str, orient="records")
```

---

**Líneas JSON (NDJSON):**

```python
df = pd.read_json("eventos.ndjson", lines=True)
```

---

**Normalización de anidados:**

```python
from pandas import json_normalize

data = {
  "id": 1,
  "user": {"name": "Ana", "city": "Quito"},
  "items": [{"sku": "A1", "qty": 2}, {"sku": "B2", "qty": 1}]
}

df_user = json_normalize(data, sep="_")
df_items = json_normalize(data, record_path=["items"], meta=["id"])
```

---

## Lectura de Tablas HTML

```python
dfs = pd.read_html("https://ejemplo.com/tablas.html")
```

**Características:**

- **Devuelve:** lista de DataFrames por cada tabla encontrada.
- **Seleccionar una tabla:** `dfs[0]`.
- **Parseo con atributos:** `match="Ventas"`, `flavor="lxml"` o `"bs4"`.

---

**Ejemplo con filtros:**

```python
tablas = pd.read_html("archivo.html", match="Clientes")
df_clientes = tablas[0]
```

---

**Desde HTML en memoria:**

```python
html = """
<table>
  <tr><th>Nombre</th><th>Edad</th></tr>
  <tr><td>Ana</td><td>23</td></tr>
  <tr><td>Luis</td><td>30</td></tr>
</table>
"""
df = pd.read_html(html)[0]
```

---

## Lectura desde MySQL

### Conexión con SQLAlchemy

```python
from sqlalchemy import create_engine
engine = create_engine("mysql+pymysql://usuario:password@localhost:3306/base_datos")
```

**Consideraciones:**

- **Driver:** instalar `pymysql` o `mysqlclient`.
- **Seguridad:** evita hardcodear credenciales.

---

### Leer Tabla Completa

```python
df = pd.read_sql_table("clientes", con=engine)
```

**Opciones:**

- **Seleccionar columnas:** `columns=["id","nombre","ciudad"]`.

---

### Leer con Consulta SQL

```python
query = """
SELECT id, nombre, ciudad, fecha_registro
FROM clientes
WHERE ciudad = 'Quito' AND fecha_registro >= '2024-01-01'
"""
df = pd.read_sql(query, con=engine)
```

---

**Chunks para grandes volúmenes:**

```python
for chunk in pd.read_sql(query, con=engine, chunksize=10000):
    pass
```

**Opciones adicionales:**

- **Fechas y tipos:** `parse_dates=["fecha_registro"]`.

---

## Consejos Prácticos y Verificación Rápida

**Ruta correcta:**

Usa `Path` para manejar rutas.

```python
from pathlib import Path
ruta = Path("data") / "archivo.xlsx"
df = pd.read_excel(ruta)
```

---

**Vista general del DataFrame:**

```python
df.info()
df.sample(5)
df.describe()
```

---

**Guardar resultados:**

```python
df.to_csv("salida.csv", index=False)
df.to_excel("salida.xlsx", index=False)
df.to_json("salida.json", orient="records", indent=2)
```

---