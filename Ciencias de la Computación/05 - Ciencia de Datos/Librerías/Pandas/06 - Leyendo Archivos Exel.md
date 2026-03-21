## Introducción

Los archivos **Excel (.xls / .xlsx)** son hojas de cálculo que permiten organizar datos en filas y columnas, con múltiples páginas (hojas) dentro de un mismo archivo.

---

## Entender qué es una hoja de cálculo

- **Hoja de cálculo:** tabla compuesta por filas y columnas.  
- **Archivo Excel:** puede contener varias hojas de trabajo (páginas).  
- **Extensiones comunes:** `.xls` (Excel antiguo) y `.xlsx` (Excel moderno).  
- **Uso típico:** almacenar datos tabulares, realizar cálculos, generar reportes.

---

## Leer un archivo en formato XLSX

```python
import pandas as pd

df = pd.read_excel("datos.xlsx")
````

- Por defecto lee la primera hoja del archivo.
- Se requiere el motor `openpyxl` para archivos `.xlsx`.

---

## Identificar páginas en una hoja de trabajo

```python
xls = pd.ExcelFile("datos.xlsx")
print(xls.sheet_names)
```

- `sheet_names` devuelve una lista con los nombres de todas las hojas disponibles.
- Ejemplo: `["Ventas", "Compras", "Clientes"]`.

---

## Leer páginas específicas de una hoja de trabajo

```python
df_ventas = pd.read_excel("datos.xlsx", sheet_name="Ventas")
df_clientes = pd.read_excel("datos.xlsx", sheet_name=2)  # por índice
```

- `sheet_name` puede ser el nombre de la hoja o su posición (0, 1, 2...).
- Permite acceder a diferentes páginas dentro del mismo archivo.

---

## Leer intervalos específicos de una hoja de trabajo

```python
df = pd.read_excel("datos.xlsx", sheet_name="Ventas", usecols="A:C", nrows=10)
```

- `usecols="A:C"` → selecciona columnas desde A hasta C.
- `nrows=10` → lee solo las primeras 10 filas.
- Útil para trabajar con fragmentos de datos grandes.

---

## Leer sólo unas pocas líneas de una hoja de cálculo

```python
df = pd.read_excel("datos.xlsx", nrows=5)
```

- Lee únicamente las primeras 5 filas de la hoja seleccionada.
- Ideal para inspeccionar archivos grandes.

---

## Escribir un archivo en formato XLSX

```python
df.to_excel("datos_salida.xlsx", index=False, sheet_name="Resultados")
```

- `index=False` → evita guardar la columna de índices.
- `sheet_name` → define el nombre de la hoja en el archivo de salida.
- Se requiere el motor `openpyxl` para escribir archivos `.xlsx`.

---

## Importar datos de Google Sheets

1. **Compartir la hoja en Google Sheets:**
    - Haz clic en _Compartir_ → _Copiar enlace_.
    - Asegúrate de que el archivo sea público o accesible con el enlace.

2. **Obtener el enlace en formato CSV o Excel:**
    - Para CSV: reemplaza en el enlace `edit#gid=0` por `export?format=csv`.
    - Para Excel: reemplaza por `export?format=xlsx`.

3. **Leer directamente con Pandas:**

```python
url = "https://docs.google.com/spreadsheets/d/ID_DE_TU_HOJA/export?format=csv"
df = pd.read_csv(url)
```

- Pandas puede leer directamente desde la URL si el archivo está compartido correctamente.
