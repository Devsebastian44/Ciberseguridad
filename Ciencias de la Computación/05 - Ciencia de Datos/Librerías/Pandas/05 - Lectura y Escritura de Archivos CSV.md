## Introducción

Los archivos **CSV (Comma Separated Values)** son archivos de texto plano donde los valores se separan por un delimitador, normalmente una **coma (`,`)** o un **punto y coma (`;`)**.  
Son ampliamente usados para intercambio de datos entre aplicaciones.

---

## Entender qué es un archivo CSV

- **Formato simple:** cada fila representa un registro.  
- **Separador:** por defecto es la coma, pero puede variar (punto y coma, tabulador, etc.).  
- **Cabecera:** normalmente la primera fila contiene los nombres de las columnas.  
- **Ejemplo:**

```csv
Nombre,Edad,Ciudad
Ana,23,Quito
Luis,30,Guayaquil
Pedro,25,Cuenca
````

---

## Leer un archivo CSV separado por comas

```python
import pandas as pd

df = pd.read_csv("datos.csv")
```

- Por defecto, `read_csv` usa la coma como separador.
- El DataFrame resultante tendrá columnas según la cabecera.

---

## Leer un archivo CSV separado por punto y coma

```python
df = pd.read_csv("datos.csv", sep=";")
```

- Se especifica el parámetro `sep=";"` para indicar el delimitador.
- Útil en archivos exportados desde Excel u otros sistemas.

---

## Leer sólo unas pocas líneas

```python
df = pd.read_csv("datos.csv", nrows=5)
```

- `nrows=5` → lee únicamente las primeras 5 filas.
- Útil para inspeccionar archivos grandes.

---

## Leer columnas específicas

```python
df = pd.read_csv("datos.csv", usecols=["Nombre", "Edad"])
```

- `usecols` → selecciona solo las columnas indicadas.
- Reduce memoria y carga de datos innecesarios.

## Usando índices de columnas

```python
df = pd.read_csv("datos.csv", usecols=[0, 1, 4])
```

- Aquí `0`, `1` y `4` representan las posiciones de las columnas en el archivo CSV.
- En el ejemplo anterior, se leerían las columnas:
    - `0 → Nombre`
    - `1 → Edad`
    - `4 → Ingreso`

Esto es útil cuando no conoces los nombres exactos de las columnas o cuando quieres seleccionar por posición.

---

## Escribir un archivo en formato CSV

```python
df.to_csv("datos_salida.csv", index=False)
```

- `index=False` → evita guardar la columna de índices.
- Se puede cambiar el separador:

```python
df.to_csv("datos_salida.csv", sep=";", index=False, encoding="utf-8")
```

- **Parámetros útiles:**
    - `sep` → define el delimitador.
    - `encoding` → define la codificación (ej. `"utf-8"`).
    - `header=False` → no guarda los nombres de columnas.
