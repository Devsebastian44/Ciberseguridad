## Introducción

Pandas y Python permiten conectarse a bases de datos relacionales para leer, escribir y actualizar información mediante consultas SQL.  
Se puede trabajar con **SQLite** (local) o con motores más robustos como **MySQL** y **PostgreSQL** usando **SQLAlchemy**.

---

## Crear una base de datos local (SQLite con sqlite3)

```python
import sqlite3

conn = sqlite3.connect("mi_base.db")
cursor = conn.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS clientes (
    id INTEGER PRIMARY KEY,
    nombre TEXT,
    edad INTEGER,
    ciudad TEXT
)
""")
conn.commit()
````

---

## Escribir en una base de datos

```python
cursor.execute("INSERT INTO clientes (nombre, edad, ciudad) VALUES (?, ?, ?)", ("Ana", 23, "Quito"))
cursor.execute("INSERT INTO clientes (nombre, edad, ciudad) VALUES (?, ?, ?)", ("Luis", 30, "Guayaquil"))
conn.commit()
```

---

## Realizar lectura en una consulta SQL

```python
import pandas as pd

df = pd.read_sql("SELECT * FROM clientes", conn)
```

---

## Actualizar una base de datos

```python
cursor.execute("UPDATE clientes SET ciudad = ? WHERE nombre = ?", ("Cuenca", "Ana"))
conn.commit()
```

---

## Conexión con SQLAlchemy

**SQLAlchemy** es una librería que facilita la conexión con diferentes motores de bases de datos (SQLite, MySQL, PostgreSQL, etc.) y se integra muy bien con Pandas.

---

## Crear conexión con SQLAlchemy

```python
from sqlalchemy import create_engine

# Conexión a SQLite
engine = create_engine("sqlite:///mi_base.db")

# Conexión a MySQL
# engine = create_engine("mysql+pymysql://usuario:password@localhost:3306/mi_base")

# Conexión a PostgreSQL
# engine = create_engine("postgresql://usuario:password@localhost:5432/mi_base")
```

- `sqlite:///mi_base.db` → crea o conecta a una base local SQLite.
- `mysql+pymysql://...` → conecta a MySQL usando el driver `pymysql`.
- `postgresql://...` → conecta a PostgreSQL.

---

## Escribir en una base de datos con Pandas

```python
df = pd.DataFrame({
    "nombre": ["Pedro", "Maria"],
    "edad": [25, 28],
    "ciudad": ["Cuenca", "Quito"]
})

df.to_sql("clientes", con=engine, if_exists="append", index=False)
```

- **to_sql():** inserta un DataFrame en una tabla.
- `if_exists="append"` → añade registros sin borrar la tabla.
- `if_exists="replace"` → reemplaza la tabla completa.
- `index=False` → evita guardar la columna de índices.

---

## Leer datos con SQLAlchemy

```python
df = pd.read_sql("SELECT * FROM clientes", con=engine)
```

- Convierte el resultado de la consulta SQL en un DataFrame.
- Se pueden aplicar filtros y condiciones directamente en la consulta.

---

## Actualizar registros con SQLAlchemy

SQLAlchemy permite ejecutar consultas SQL directamente:

```python
with engine.connect() as conn:
    conn.execute("UPDATE clientes SET edad = 26 WHERE nombre = 'Pedro'")
    conn.commit()
```
