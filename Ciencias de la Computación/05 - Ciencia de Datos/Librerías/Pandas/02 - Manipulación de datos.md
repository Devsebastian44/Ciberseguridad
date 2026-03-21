## Introducción

La **manipulación de datos** en Pandas permite crear nuevas columnas, transformar valores y aplicar funciones personalizadas para enriquecer el análisis.

---

## Generar Columnas Numéricas

```python
df["Edad_en_meses"] = df["Edad"] * 12
df["Precio_con_IVA"] = df["Precio"] * 1.12
```

**Características:**

- **Derivadas numéricas:** crea columnas a partir de operaciones aritméticas.
- **Usos típicos:** porcentajes, escalas, conversiones.

---

## Insertar Columnas Categóricas

```python
df["Categoria"] = ["A", "B", "A", "C", "B"]
```

**Características:**

- **Etiquetas:** asigna categorías por fila.

---

### Clasificación por Rangos (cut)

```python
import pandas as pd

df["Grupo_Edad"] = pd.cut(df["Edad"], bins=[0, 18, 30, 50], labels=["Joven", "Adulto", "Mayor"])
```

**Qué hace cut:**

- **Segmenta valores continuos** en intervalos definidos por `bins`.
- **Devuelve una Serie categórica** con etiquetas (`labels`) por cada intervalo.
- **Opciones útiles:** `right=False` para intervalos cerrados a la izquierda, `include_lowest=True` para incluir el límite inferior, `duplicates="drop"` si hay bins repetidos.

---

**Ejemplo con percentiles usando qcut:**

```python
df["Ingreso_cuartil"] = pd.qcut(df["Ingreso"], q=4, labels=["Q1", "Q2", "Q3", "Q4"])
```

**Características:**

- **qcut:** crea intervalos por **cuantiles** (igual número de observaciones en cada grupo).

---

## Definir Columnas Binarias

```python
df["Mayor_de_25"] = (df["Edad"] > 25)
df["Mayor_de_25_int"] = (df["Edad"] > 25).astype(int)
```

**Características:**

- **Booleanos y enteros:** condiciones como True/False y conversión a 0/1.

---

## Realizar Operaciones entre Columnas

```python
df["Total"] = df["Cantidad"] * df["Precio"]
df["Margen"] = df["Ingreso"] - df["Costo"]
```

**Características:**

- **Combinaciones:** totales, diferencias, márgenes.

---

## Utilizar el Método apply

```python
df["Nombre_mayus"] = df["Nombre"].apply(str.upper)
df["Edad_clasificada"] = df["Edad"].apply(lambda x: "Mayor" if x >= 30 else "Menor")
```

**Qué es lambda:**

- Una **función anónima** que recibe un valor `x` y devuelve una cadena según una condición.

---

**Cómo funciona:**

- Evalúa `x >= 30`.
- Si la condición es **verdadera**, retorna `"Mayor"`.
- Si es **falsa**, retorna `"Menor"`.

---

**Aplicación:**

- **Por columna:** aplica funciones a cada valor.
- **Por filas/DataFrame:** `df.apply(func, axis=1)` para usar varias columnas en una fila.

---

## Crear Funciones Lambda

```python
df["Edad_doble"] = df["Edad"].apply(lambda x: x * 2)
```

**Características:**

- **Funciones en línea:** transformaciones rápidas sin definir funciones externas.

---

## Crear Columnas con assign

```python
df = df.assign(
    Edad_en_meses=lambda d: d["Edad"] * 12,
    Precio_con_IVA=lambda d: d["Precio"] * 1.12,
    Total=lambda d: d["Cantidad"] * d["Precio"]
)
```

**Qué hace assign():**

- **Crea y devuelve un nuevo DataFrame** con columnas añadidas sin modificar el original (a menos que reasignes).
- **Permite dependencias** entre nuevas columnas usando funciones `lambda` con el DataFrame como argumento.
- **Ventaja:** escritura **encadenable**, clara y reproducible.

---

**Encadenado con otras operaciones:**

```python
df = (
    df.assign(Descuento=lambda d: d["Precio"] * 0.10)
      .assign(Precio_final=lambda d: d["Precio"] - d["Descuento"])
)
```

**Cómo funciona:**

- `d` es el DataFrame original `df`.
- Se crea una nueva columna `"Descuento"` calculada como el **10%** de la columna `"Precio"`.
- `d` es el DataFrame **ya modificado** con la columna `"Descuento"`.
- Se crea la columna `"Precio_final"` restando el descuento al precio original.
- **Encadenamiento:** añade varias columnas de forma ordenada y legible.

---

## Eliminar Filas y Columnas

### Eliminar Filas por Índice

```python
df.drop([0, 1])   # Elimina las filas con índices 0 y 1
```

**Características:**

- Se pasa una **lista de índices** a eliminar.
- Por defecto, `axis=0` indica filas.
- Si quieres modificar el DataFrame directamente:

```python
df.drop([0, 1], inplace=True)
```

---

### Eliminar Columnas por Nombre

```python
df.drop(columns=["Ciudad", "Edad"])
```

**Características:**

- Se pasa una **lista de nombres** de columnas.
- Equivalente a `df.drop(["Ciudad","Edad"], axis=1)`.
- Con `inplace=True` se aplica directamente al DataFrame.

---

### Ejemplo Combinado

```python
df = pd.DataFrame({
    "Nombre": ["Ana", "Luis", "Pedro"],
    "Edad": [23, 30, 25],
    "Ciudad": ["Quito", "Guayaquil", "Cuenca"]
})

# Eliminar fila con índice 1
df = df.drop(1)

# Eliminar columna "Ciudad"
df = df.drop(columns="Ciudad")
```

**Resultado:**

|Nombre|Edad|
|---|---|
|Ana|23|
|Pedro|25|

---