## Introducción

El tratamiento de datos textuales en Pandas permite limpiar, transformar y analizar cadenas de caracteres.  
Se pueden aplicar funciones nativas de Pandas, expresiones regulares y técnicas de tokenización.

---

## Manipular elementos textuales en un DataFrame

```python
import pandas as pd

df = pd.DataFrame({"nombres": [" Ana ", "Luis", "Pedro "]})

# Limpiar espacios y convertir a minúsculas
df["nombres"] = df["nombres"].str.strip().str.lower()
````

- **str.strip():** elimina espacios en blanco.
- **str.lower():** convierte a minúsculas.
- **str.upper():** convierte a mayúsculas.
- **str.replace():** reemplaza texto.

---

## Trabajar con expresiones regulares (regex)

```python
df = pd.DataFrame({"emails": ["ana@gmail.com", "luis@hotmail.com", "pedro@yahoo.com"]})

# Extraer el dominio del email
df["dominio"] = df["emails"].str.extract(r"@(\w+)\.")
```

- **str.extract():** extrae patrones con regex.
- **r"@(\w+).":** busca texto entre `@` y `.`.
- Regex permite validar, buscar y transformar cadenas complejas.

Ejemplo de validación de números:

```python
df["es_numero"] = df["nombres"].str.match(r"^\d+$")
```

---

## Transformar textos en listas

```python
df = pd.DataFrame({"frases": ["hola mundo", "aprendiendo pandas"]})

df["tokens"] = df["frases"].str.split(" ")
```

**Resultado:**

|frases|tokens|
|---|---|
|hola mundo|["hola", "mundo"]|
|aprendiendo pandas|["aprendiendo","pandas"]|

- **str.split():** divide cadenas en listas según un delimitador.
- Útil para preparar datos para análisis de texto.

---

## Realizar el proceso de tokenización de strings

La **tokenización** consiste en dividir un texto en unidades (tokens), como palabras o frases.

Ejemplo con `apply`:

```python
df["tokens"] = df["frases"].apply(lambda x: x.split())
```

Ejemplo con librería `nltk`:

```python
import nltk
nltk.download("punkt")
from nltk.tokenize import word_tokenize

df["tokens"] = df["frases"].apply(word_tokenize)
```

- **word_tokenize:** divide en palabras considerando puntuación.
- Útil para análisis de lenguaje natural (NLP).
