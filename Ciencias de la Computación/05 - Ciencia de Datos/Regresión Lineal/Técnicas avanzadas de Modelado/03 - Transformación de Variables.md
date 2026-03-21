## Transformar los datos

La transformación de variables permite mejorar la interpretación y el ajuste del modelo, especialmente cuando los datos presentan asimetrías o valores extremos.

Ejemplo de transformación logarítmica:

```python
import numpy as np

# Transformación logarítmica de la variable dependiente
df["variable_dependiente_log"] = np.log(df["variable_dependiente"])
````

---

## Aplicar la transformación logarítmica

La transformación logarítmica ayuda a estabilizar la varianza y reducir la influencia de valores atípicos.

```python
# Visualizar primeras filas con la nueva variable
print(df[["variable_dependiente", "variable_dependiente_log"]].head())
```

---

## Distribución de frecuencias de la variable dependiente transformada

Podemos analizar cómo cambia la distribución después de la transformación.

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.histplot(df["variable_dependiente_log"], bins=20, kde=True)
plt.title("Distribución de frecuencias de la variable dependiente transformada")
plt.show()
```

---

## Gráficos de dispersión entre las variables transformadas

Los gráficos de dispersión permiten observar cómo se relacionan las variables después de la transformación.

```python
sns.scatterplot(x=df["variable_independiente"], y=df["variable_dependiente_log"])
plt.title("Gráfico de dispersión con variable dependiente transformada")
plt.show()
```

Para múltiples variables transformadas:

```python
sns.pairplot(df[["variable_dependiente_log", "variable_independiente"]])
plt.show()
```

---

### Análisis de la dispersión entre las variables transformadas

- La transformación puede revelar relaciones lineales más claras.
- Una dispersión más compacta indica que la transformación fue efectiva.
- Se debe comparar la dispersión antes y después de la transformación para evaluar mejoras en la relación entre variables.