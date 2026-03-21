## Visualización con Pairplot de Seaborn

El **pairplot** permite explorar relaciones entre varias variables de manera simultánea.

```python
import seaborn as sns
import pandas as pd

# Ejemplo con dataset de casas
df = pd.DataFrame({
    'precio':[200000,250000,180000,300000,220000],
    'metros':[80,120,70,150,100],
    'habitaciones':[3,4,2,5,3],
    'antiguedad':[10,5,20,2,15]
})

sns.pairplot(df)
````

Este gráfico ayuda a identificar qué variables tienen mayor relación con el **precio de venta**.

---

## Regresión lineal múltiple

Cuando se incluyen varias variables explicativas, el modelo se expresa como:

```python
from sklearn.linear_model import LinearRegression

X = df[['metros','habitaciones','antiguedad']]
y = df['precio']

modelo = LinearRegression()
modelo.fit(X, y)

print("Intercepto (β0):", modelo.intercept_)
print("Coeficientes (βi):", modelo.coef_)
```

Cada coeficiente indica el impacto de la variable correspondiente en el precio.

---

## Comparación de modelos: R² y R² ajustado

- **R²**: proporción de variabilidad explicada por el modelo.
- **R² ajustado**: corrige el R² considerando el número de variables incluidas, penalizando la complejidad innecesaria.

```python
from sklearn.metrics import r2_score

y_pred = modelo.predict(X)
r2 = r2_score(y, y_pred)

n = X.shape[0]  # número de observaciones
p = X.shape[1]  # número de variables explicativas

r2_ajustado = 1 - (1-r2)*(n-1)/(n-p-1)

print("R²:", r2)
print("R² ajustado:", r2_ajustado)
```

---

## Multicolinealidad

La **multicolinealidad** ocurre cuando dos o más variables explicativas están altamente correlacionadas, lo que dificulta interpretar los coeficientes.

Ejemplo:

- `metros` y `habitaciones` pueden estar correlacionados.
- Esto puede inflar los errores estándar y afectar la estabilidad del modelo.

---

## Elección del modelo adecuado

Al seleccionar el modelo de regresión lineal múltiple se debe balancear:

- **Simplicidad**: evitar incluir demasiadas variables irrelevantes.
- **Precisión**: maximizar R² y R² ajustado.
- **Interpretabilidad**: que los coeficientes tengan sentido práctico y no estén distorsionados por multicolinealidad.