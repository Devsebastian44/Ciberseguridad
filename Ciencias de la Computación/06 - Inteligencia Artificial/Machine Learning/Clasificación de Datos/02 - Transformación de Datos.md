## Uso de Scikit-Learn para transformaciones

La biblioteca **Scikit-Learn** ofrece herramientas para preparar los datos antes de aplicar modelos de clasificación.  
- Permite normalizar, escalar y codificar variables.  
- Facilita la separación entre variables explicativas (*features*) y la variable objetivo (*target*).  

**Ejemplo inicial:**

```python
import pandas as pd
from sklearn.model_selection import train_test_split

df = pd.read_csv("datos.csv")

# Separar variables explicativas y objetivo
X = df.drop("Clase", axis=1)  # Features
y = df["Clase"]               # Target
````

---

## Separación de variables explicativas y objetivo

- **Variables explicativas (X):** son las características que usamos para predecir.
- **Variable objetivo (y):** es la categoría que queremos clasificar.

Esta separación es esencial para entrenar cualquier modelo de Machine Learning.

---

## Transformación de variables categóricas con One Hot Encoding

Las variables categóricas deben convertirse a formato numérico para que los algoritmos las procesen.

- **One Hot Encoding** crea columnas binarias (0/1) para cada categoría.
- Evita que los modelos interpreten categorías como valores ordinales.

**Ejemplo con Scikit-Learn:**

```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(sparse_output=False)
X_encoded = encoder.fit_transform(X[["Genero"]])

# Convertir a DataFrame para visualizar
X_encoded_df = pd.DataFrame(X_encoded, columns=encoder.get_feature_names_out(["Genero"]))
print(X_encoded_df.head())
```

---

## Transformación de la variable objetivo con LabelEncoder

La variable objetivo también debe estar en formato numérico.

- **LabelEncoder** asigna un número entero a cada categoría.
- Ejemplo: _Aprobado → 0_, _Reprobado → 1_.

**Ejemplo en Python:**

```python
from sklearn.preprocessing import LabelEncoder

label_encoder = LabelEncoder()
y_encoded = label_encoder.fit_transform(y)

print(y_encoded[:10])  # Primeros 10 valores transformados
```