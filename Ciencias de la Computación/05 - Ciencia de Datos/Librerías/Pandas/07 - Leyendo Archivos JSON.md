## Introducción

El formato **JSON (JavaScript Object Notation)** es un estándar ligero para intercambio de datos.  
Se basa en pares clave-valor y estructuras anidadas, muy usado en aplicaciones web y APIs.

---

## Comprender qué es el formato JSON

- **Texto plano estructurado:** usa llaves `{}` para objetos y corchetes `[]` para listas.  
- **Claves y valores:** `"clave": valor`.  
- **Tipos soportados:** cadenas, números, booleanos, listas, objetos.  

Ejemplo:

```json
[
  {"nombre": "Ana", "edad": 23},
  {"nombre": "Luis", "edad": 30}
]
````

---

## Leer un archivo en formato JSON

```python
import pandas as pd

df = pd.read_json("datos.json")
```

- Convierte el archivo JSON en un DataFrame.
- Funciona bien con listas de objetos (registros).

---

## Normalizar datos de un archivo JSON

Cuando el JSON tiene estructuras anidadas, se usa `json_normalize`:

```python
from pandas import json_normalize

data = {
  "id": 1,
  "usuario": {"nombre": "Ana", "ciudad": "Quito"},
  "items": [{"sku": "A1", "cantidad": 2}, {"sku": "B2", "cantidad": 1}]
}

df_usuario = json_normalize(data, sep="_")
df_items = json_normalize(data, record_path=["items"], meta=["id"])
```

- **sep="_":** aplana claves anidadas (`usuario_nombre`, `usuario_ciudad`).
- **record_path:** extrae listas internas como tablas.
- **meta:** conserva claves externas como referencia.

---

## Escribir un archivo en formato JSON

```python
df.to_json("datos_salida.json", orient="records", indent=2)
```

- **orient="records":** cada fila se convierte en un objeto JSON.
- **orient="columns":** organiza los datos por columnas.
- **indent=2:** añade sangría para legibilidad.
- **lines=True:** guarda en formato NDJSON (una fila por línea).

Ejemplo con columnas:

```python
df.to_json("datos_salida.json", orient="columns", indent=4)
```

---

## Obtener archivos JSON de las API

Muchas APIs devuelven datos en formato JSON.  
Podemos consumirlos con `requests` y luego convertirlos en DataFrame:

```python
import requests

url = "https://api.ejemplo.com/datos"
response = requests.get(url)
data = response.json()

df = pd.json_normalize(data)
```

- **requests.get(url):** obtiene la respuesta de la API.
- **.json():** convierte la respuesta en un diccionario/lista de Python.
- **pd.json_normalize():** transforma estructuras anidadas en DataFrame o en un formato de tabla con múltiples columnas.