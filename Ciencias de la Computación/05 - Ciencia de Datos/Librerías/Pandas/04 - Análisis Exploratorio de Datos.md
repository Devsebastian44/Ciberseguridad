## Introducción

El **análisis exploratorio de datos (EDA)** es el proceso de **examinar, describir y visualizar** un conjunto de datos para comprender su estructura, patrones y posibles problemas antes de aplicar modelos o análisis más avanzados.

---

## Identificar qué Hacer Durante un Proceso de Análisis Exploratorio

Durante un **EDA** se suelen realizar las siguientes tareas:

- **Inspección inicial:** cargar los datos y revisar su estructura (`df.head()`, `df.info()`).
- **Dimensiones:** verificar número de filas y columnas (`df.shape`).
- **Tipos de datos:** comprobar si las columnas tienen el tipo correcto (`df.dtypes`).
- **Valores faltantes:** identificar nulos (`df.isnull().sum()`).
- **Distribución de valores:** calcular estadísticas (`df.describe()`).
- **Valores únicos y frecuencias:** (`df["columna"].unique()`, `df["columna"].value_counts()`).
- **Visualización:** gráficos básicos para detectar tendencias y anomalías.

---

## Calcular el Promedio de Valores de un DataFrame

```python
df["columna"].mean()
```

**Características:**

- Calcula el **promedio** de una columna numérica.

---

**Para varias columnas:**

```python
df.mean(numeric_only=True)
```

---

## Agrupar los Datos Según una Columna Específica con groupby

```python
df.groupby("columna")["otra_columna"].mean()
```

**Ejemplo:**

```python
df.groupby("Ciudad")["Edad"].mean()
```

**Características:**

- Agrupa por **ciudad** y calcula el promedio de **edad**.
- También se pueden aplicar otras funciones: `sum()`, `count()`, `max()`, `min()`.

---

## Realizar Selecciones con el Método query

```python
df.query("Edad > 25 and Ciudad == 'Quito'")
```

**Características:**

- Sirve para consultar si algunos de los elementos de la lista están en el **dataset**
- Filtra filas con **condiciones** expresadas como string.
- Admite operadores **lógicos** (`and`, `or`) y **comparaciones** (`==`, `>`, `<`).

---

## Uso de not in con query

En Pandas podemos filtrar filas que **no pertenezcan** a un conjunto de valores usando `not in`.

Se utiliza el operador `~` (tilde) para **negar** la condición.

---

### Ejemplo con query

```python
df.query("Ciudad not in ['Quito','Guayaquil']")
```

**Características:**

- Devuelve todas las filas cuya columna `Ciudad` **no sea** ni `"Quito"` ni `"Guayaquil"`.

---

### Ejemplo con Operadores Booleanos

```python
df[~df["Ciudad"].isin(["Quito","Guayaquil"])]
```

**Cómo funciona:**

- `df["Ciudad"].isin([...])` → devuelve `True` si el valor **está** en la lista.
- `~` → **niega** la condición, seleccionando los valores que **no están** en la lista.

---

## Transformar Series en DataFrames

```python
serie = df["Edad"]
df_serie = serie.to_frame()
```

**Características:**

- Convierte una **Serie** en un **DataFrame**.

---

**Renombrar la columna:**

```python
df_serie = serie.to_frame(name="Edad")
```

---

## Ordenar Valores de un DataFrame con sort_values

```python
df.sort_values(by="Edad")
```

**Características:**

- Ordena por la columna `Edad` en orden **ascendente**.

---

**Orden descendente:**

```python
df.sort_values(by="Edad", ascending=False)
```

---

**Ordenar por varias columnas:**

```python
df.sort_values(by=["Ciudad", "Edad"])
```

---

## Graficar Barras Verticales y Horizontales

```python
df["Ciudad"].value_counts().plot(kind="bar")   # Barras verticales
df["Ciudad"].value_counts().plot(kind="barh")  # Barras horizontales
```

**Características:**

- `kind="bar"` → gráfico de **barras verticales**.
- `kind="barh"` → gráfico de **barras horizontales**.

---

## Personalizar Gráficos con xlabel y ylabel

Cuando generamos gráficos con Pandas (que internamente usa Matplotlib), podemos añadir **etiquetas** a los ejes para que el gráfico sea más claro.

---

### Ejemplo Básico

```python
import matplotlib.pyplot as plt

df["Ciudad"].value_counts().plot(kind="bar", color="skyblue")

plt.xlabel("Ciudad")       # Etiqueta para el eje X
plt.ylabel("Frecuencia")   # Etiqueta para el eje Y
plt.title("Cantidad de registros por ciudad")  # Título del gráfico
plt.show()
```

**Funciones:**

- **`plt.xlabel("texto")`** → define el nombre del **eje horizontal**.
- **`plt.ylabel("texto")`** → define el nombre del **eje vertical**.
- **`plt.title("texto")`** → añade un **título** al gráfico.

---

### Ejemplo con Barras Horizontales y Agrupación

```python
ax.set_xlabel("Precio promedio")   # Etiqueta eje X
ax.set_ylabel("Tipo de producto")  # Etiqueta eje Y
ax.set_title("Precio promedio por tipo de producto")
```

**Características:**

- Aquí usamos el objeto `ax` (Axes) que devuelve `.plot()` para personalizar directamente el gráfico.
- `set_xlabel`, `set_ylabel` y `set_title` funcionan igual que en Matplotlib, pero aplicados al gráfico generado por Pandas.

---

## Agrupación y Cálculo del Promedio

```python
df_tipo_precio = datos.groupby("Tipo")[["Valor"]].mean().sort_values("Valor")
```

**Cómo funciona:**

- **`datos.groupby("Tipo")`**  
    Agrupa el DataFrame `datos` según la columna `"Tipo"`.  
    Ejemplo: si `"Tipo"` tiene valores como _Casa_, _Departamento_, _Oficina_, se crean grupos para cada uno.
    
- **`[["Valor"]]`**  
    Selecciona solo la columna `"Valor"` para trabajar sobre ella después de agrupar.  
    Así se indica que solo se quiere calcular el promedio de esa columna.
    
- **`.mean()`**  
    Calcula el **promedio (media)** de la columna `"Valor"` para cada grupo `"Tipo"`.
    
- **`.sort_values("Valor")`**  
    Ordena los resultados de **menor a mayor** según el valor promedio obtenido.
    

---

## Generación del Gráfico

```python
df_tipo_precio.plot(kind="barh", figsize=(12,8), color="purple")
```

**Parámetros:**

- **`kind="barh"`**  
    Crea un gráfico de **barras horizontales** (`barh` = _bar horizontal_).
    
- **`figsize=(12,8)`**  
    Define el **tamaño** del gráfico (12 unidades de ancho y 8 de alto).
    
- **`color="purple"`**  
    Establece el color **púrpura** para las barras del gráfico.
    

---

## Visualizar Valores Únicos con unique

```python
df["Ciudad"].unique()
```

**Características:**

- Devuelve un **array** con los valores únicos de la columna.
- Útil para identificar **categorías** distintas.

---

## Utilizar value_counts para Contar Valores Únicos y Calcular Porcentajes

```python
df["Ciudad"].value_counts()
```

**Características:**

- Cuenta la **frecuencia** de cada valor único.

---

**Para porcentajes:**

```python
df["Ciudad"].value_counts(normalize=True) * 100
```

---

## Cambiar Nombres de Columnas

```python
df.rename(columns={"Nombre": "Cliente", "Edad": "Años"}, inplace=True)
```

**Características:**

- Cambia nombres de columnas **específicas**.

---

**Para renombrar todas las columnas:**

```python
df.columns = ["Cliente", "Años", "Ciudad"]
```

---