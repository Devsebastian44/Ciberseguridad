## Introducción

El manejo de datos temporales en Pandas se realiza con el tipo **datetime**, que permite trabajar con fechas y horas de manera eficiente para análisis y transformaciones.

---

## Identificar el tipo de datos datetime

```python
import pandas as pd

df = pd.DataFrame({"fechas": ["2024-01-01", "2024-02-15", "2024-03-10"]})

print(df.dtypes)
````

**Resultado:**

```
fechas    object
dtype: object
```

- Inicialmente las fechas suelen estar en formato `object` (texto).
- Para trabajar con ellas, se deben convertir al tipo `datetime64`.

---

## Transformar datos para el tipo datetime

```python
df["fechas"] = pd.to_datetime(df["fechas"])
print(df.dtypes)
```

**Resultado:**

```
fechas    datetime64[ns]
dtype: object
```

- **pd.to_datetime():** convierte cadenas en objetos de tipo fecha.
- Permite manejar operaciones temporales como diferencias, filtrado y agrupación.
- Se puede especificar el formato:

```python
df["fechas"] = pd.to_datetime(df["fechas"], format="%Y-%m-%d")
```

---

## Manipular columnas de tipo datetime a través de métodos

Una vez convertidas, se pueden usar atributos y métodos:

```python
df["año"] = df["fechas"].dt.year
df["mes"] = df["fechas"].dt.month
df["día"] = df["fechas"].dt.day
df["día_semana"] = df["fechas"].dt.day_name()
```

- **dt.year:** extrae el año.
- **dt.month:** extrae el mes.
- **dt.day:** extrae el día.
- **dt.day_name():** devuelve el nombre del día de la semana.

---

## Formatear fechas con `strftime`

El método `strftime` permite convertir fechas en cadenas con un formato específico.

python

```python
df["formato"] = df["fechas"].dt.strftime("%d/%m/%Y")
```

**Resultado:**

|fechas|formato|
|---|---|
|2024-01-01|01/01/2024|
|2024-02-15|15/02/2024|
|2024-03-10|10/03/2024|

### Códigos comunes de `strftime`

|Código|Significado|Ejemplo|
|---|---|---|
|`%Y`|Año completo|2024|
|`%y`|Año corto (2 dígitos)|24|
|`%m`|Mes (01-12)|02|
|`%B`|Nombre del mes|February|
|`%d`|Día del mes (01-31)|15|
|`%A`|Nombre del día|Thursday|
|`%H`|Hora (00-23)|14|
|`%M`|Minutos (00-59)|30|
|`%S`|Segundos (00-59)|45|

Ejemplo avanzado:

```python
df["custom"] = df["fechas"].dt.strftime("Día %d de %B del %Y")
```

**Resultado:**

| fechas     | custom                      |
| ---------- | --------------------------- |
| 2024-01-01 | Día 01 de January del 2024  |
| 2024-02-15 | Día 15 de February del 2024 |
| 2024-03-10 | Día 10 de March del 2024    |

---

## Agrupar datos por fechas con `groupby`

El método `groupby` permite agrupar registros por períodos de tiempo y aplicar funciones de agregación.

```python
df = pd.DataFrame({
    "fechas": pd.to_datetime(["2024-01-01", "2024-01-15", "2024-02-10", "2024-02-20"]),
    "ventas": [100, 200, 150, 300]
})

# Agrupar por mes y sumar ventas
df.groupby(df["fechas"].dt.month)["ventas"].sum()
```

**Resultado:**

|mes|ventas|
|---|---|
|1|300|
|2|450|

### Ejemplo agrupando por año y mes

```python
df.groupby([df["fechas"].dt.year, df["fechas"].dt.month])["ventas"].mean()
```

- Agrupa por año y mes.
- Calcula el promedio de ventas en cada período.    

### Ejemplo con resample (agrupación temporal)

Si la columna de fechas es el índice:

```python
df = df.set_index("fechas")

# Agrupar por mes y sumar
df.resample("M")["ventas"].sum()
```

- **resample("M")** → agrupa por mes.
    
- También se puede usar `"W"` (semana), `"D"` (día), `"Y"` (año).

---

## Operaciones con fechas

```python
# Diferencia entre fechas
df["diferencia_días"] = df["fechas"] - pd.to_datetime("2024-01-01")

# Filtrar por rango de fechas
df_filtrado = df[(df["fechas"] >= "2024-02-01") & (df["fechas"] <= "2024-02-28")]
```

- Se pueden realizar cálculos de diferencias (`Timedelta`).
- Filtrar registros por intervalos de tiempo.
