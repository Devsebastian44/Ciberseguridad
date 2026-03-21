## Introducción a la Estadística y sus Datos

## ¿Qué es la Estadística?

La **estadística** es la ciencia que se encarga de **recoger, organizar, analizar e interpretar datos** con el fin de tomar decisiones informadas.  
En programación y ciencia de datos, Python junto con librerías como **pandas** nos permite aplicar estos conceptos de manera práctica.

---

## Lectura de Datos en Python

En esta clase aprendimos a **leer un dataset en formato CSV** y convertirlo en un **DataFrame de pandas**.

```python
import pandas as pd

# Leer un archivo CSV
df = pd.read_csv("dataset.csv")

# Mostrar las primeras filas
print(df.head())
```

- **CSV (Comma Separated Values):** formato de texto plano donde los valores están separados por comas.
- **DataFrame:** estructura de datos de pandas similar a una tabla, con filas y columnas.

---

## Tipos de Variables en Estadística

Los datos en un dataset se clasifican en **variables**, que pueden ser de dos grandes tipos:

### 🔹 Variables Cualitativas (o categóricas)

Describen **atributos o categorías**. No son numéricas.

- **Nominales:** categorías sin orden específico.  
    Ejemplo: colores (`rojo`, `azul`, `verde`), género (`masculino`, `femenino`).

- **Ordinales:** categorías con un orden definido.  
    Ejemplo: nivel educativo (`primaria`, `secundaria`, `universidad`), satisfacción (`baja`, `media`, `alta`).

### 🔹 Variables Cuantitativas (o numéricas)

Representan **cantidades medibles**. Son numéricas.

- **Discretas:** toman valores enteros y contables.  
    Ejemplo: número de hijos, cantidad de autos.

- **Continuas:** pueden tomar cualquier valor dentro de un rango.  
    Ejemplo: altura, peso, temperatura.

---

## Ejemplo de Clasificación de Variables

|Variable|Tipo|Subtipo|
|---|---|---|
|Nombre|Cualitativa|Nominal|
|Nivel educativo|Cualitativa|Ordinal|
|Número de hijos|Cuantitativa|Discreta|
|Altura|Cuantitativa|Continua|
