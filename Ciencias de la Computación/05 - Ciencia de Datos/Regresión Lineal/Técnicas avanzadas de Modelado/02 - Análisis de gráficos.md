## Configuración del formato de los gráficos

Para personalizar los gráficos utilizamos **matplotlib** y **seaborn**, ajustando estilo, tamaño y colores.

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Configuración general
plt.style.use("seaborn")
plt.figure(figsize=(8,6))
````

---

## Construcción del box-plot de la variable dependiente

El **box-plot** permite visualizar la dispersión, la mediana y posibles valores atípicos de la variable dependiente.

```python
sns.boxplot(y=df["variable_dependiente"])
plt.title("Box-Plot de la variable dependiente")
plt.show()
```

---

## Distribución de frecuencias de la variable dependiente

La distribución de frecuencias muestra cómo se distribuyen los valores de la variable dependiente.

```python
sns.histplot(df["variable_dependiente"], bins=20, kde=True)
plt.title("Distribución de frecuencias de la variable dependiente")
plt.show()
```

---

## Gráficos de dispersión entre las variables del dataset

Los gráficos de dispersión permiten analizar la relación entre dos variables.

```python
sns.scatterplot(x=df["variable_independiente"], y=df["variable_dependiente"])
plt.title("Gráfico de dispersión")
plt.show()
```

Para múltiples variables, podemos usar **pairplot**:

```python
sns.pairplot(df)
plt.show()
```

---

## Análisis de la dispersión entre las variables

El análisis de dispersión nos ayuda a identificar patrones, tendencias lineales y posibles relaciones entre variables.

- Una nube de puntos alineada sugiere una relación lineal.
- Una dispersión amplia indica baja correlación.
- La presencia de valores atípicos puede afectar el ajuste de la recta.