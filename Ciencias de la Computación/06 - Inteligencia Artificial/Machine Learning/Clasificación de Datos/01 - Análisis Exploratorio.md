## Identificación de la variable objetivo

La **variable objetivo** es aquella que queremos predecir o clasificar.  
- En problemas de clasificación, suele ser una variable categórica (ejemplo: *spam* vs *no spam*, *aprobado* vs *reprobado*).  
- Es fundamental reconocerla desde el inicio para orientar el análisis y los modelos.  

**Ejemplo en Python con Pandas:**

```python
import pandas as pd

df = pd.read_csv("datos.csv")
print(df.columns)  # Lista de columnas
objetivo = "Clase"  # Definimos la variable objetivo
````

---

## Verificación de datos nulos e inconsistentes

Antes de aplicar modelos, es necesario revisar la calidad de los datos.

- **Datos nulos:** valores faltantes que pueden sesgar el análisis.
- **Datos inconsistentes:** valores fuera de rango, duplicados o incorrectos.

**Ejemplo en Python:**

```python
# Verificar valores nulos
print(df.isnull().sum())

# Detectar valores duplicados
print(df.duplicated().sum())

# Reemplazar valores nulos con la media
df.fillna(df.mean(), inplace=True)
```

---

## Análisis exploratorio con gráficos

El análisis exploratorio permite **visualizar patrones y distribuciones**.  
Algunas técnicas comunes:

- Histogramas para distribución de variables.
- Diagramas de dispersión para relaciones entre variables.
- Gráficos de barras para frecuencias de categorías.

**Ejemplo con Matplotlib y Seaborn:**

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Histograma de una variable numérica
sns.histplot(df["Edad"], bins=10, kde=True)
plt.show()

# Gráfico de barras de la variable objetivo
sns.countplot(x="Clase", data=df)
plt.show()

# Diagrama de dispersión entre dos variables
sns.scatterplot(x="Altura", y="Peso", hue="Clase", data=df)
plt.show()
```