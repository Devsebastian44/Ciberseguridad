## Transformar los datos

Antes de aplicar el modelo de regresión, es común realizar transformaciones en los datos para mejorar la interpretación y el ajuste.

```python
import numpy as np

# Transformación logarítmica de la variable dependiente
df["variable_dependiente_log"] = np.log(df["variable_dependiente"])
````

---

## Aplicar la transformación logarítmica

La transformación logarítmica ayuda a estabilizar la varianza y reducir la influencia de valores atípicos.

```python
print(df[["variable_dependiente", "variable_dependiente_log"]].head())
```

---

## Distribución de frecuencias de la variable dependiente transformada

Podemos visualizar cómo cambia la distribución después de la transformación.

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.histplot(df["variable_dependiente_log"], bins=20, kde=True)
plt.title("Distribución de frecuencias de la variable dependiente transformada")
plt.show()
```

---

## Gráficos de dispersión entre las variables transformadas

Los gráficos de dispersión permiten observar la relación entre las variables después de la transformación.

```python
sns.scatterplot(x=df["variable_independiente"], y=df["variable_dependiente_log"])
plt.title("Gráfico de dispersión con variable dependiente transformada")
plt.show()
```

---

## Análisis de la dispersión entre las variables transformadas

- La transformación puede revelar relaciones lineales más claras.
- Una dispersión más compacta indica que la transformación fue efectiva.
- Comparar la dispersión antes y después de la transformación permite evaluar mejoras en la relación entre variables.

---

## Ajuste del modelo de regresión lineal con Statsmodels

La librería **statsmodels** permite ajustar modelos de regresión lineal y obtener un análisis estadístico detallado.

```python
import statsmodels.api as sm

# Definir variables
X = df[["variable_independiente"]]   # Variables independientes
y = df["variable_dependiente_log"]   # Variable dependiente transformada

# Agregar constante al modelo
X = sm.add_constant(X)

# Ajustar modelo
modelo = sm.OLS(y, X).fit()

# Resumen del modelo
print(modelo.summary())
```

El resumen incluye:

- Coeficientes estimados.
- Error estándar.
- Estadísticos t y p-valores.
- R² y R² ajustado.
- Pruebas de significancia global del modelo.