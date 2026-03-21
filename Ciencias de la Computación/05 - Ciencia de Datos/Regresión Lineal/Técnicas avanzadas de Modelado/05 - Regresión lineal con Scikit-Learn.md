## Estimar el modelo lineal utilizando los datos de entrenamiento

Con **Scikit-Learn** podemos dividir el dataset en entrenamiento y prueba, y luego ajustar el modelo.

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

# Definir variables
X = df[["variable_independiente"]]
y = df["variable_dependiente"]

# Dividir en entrenamiento y prueba
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Ajustar modelo
modelo = LinearRegression()
modelo.fit(X_train, y_train)
````

---

## Obtener el coeficiente de determinación (R²) del modelo estimado

El coeficiente de determinación mide qué tan bien el modelo explica la variabilidad de los datos.

```python
r2_train = modelo.score(X_train, y_train)
print("R² en entrenamiento:", r2_train)
```

---

## Generar previsiones para los datos de prueba

```python
y_pred = modelo.predict(X_test)
```

---

## Obtener el coeficiente de determinación (R²) para las previsiones

```python
r2_test = modelo.score(X_test, y_test)
print("R² en prueba:", r2_test)
```

---

## Generar la predicción puntual del modelo

```python
# Predicción para un nuevo valor
nuevo_valor = [[50]]
prediccion = modelo.predict(nuevo_valor)
print("Predicción puntual:", prediccion)
```

---

## Invertir la transformación para obtener la estimación en reales

Si la variable dependiente fue transformada (ej. logarítmica), se debe aplicar la función inversa.

```python
import numpy as np

prediccion_real = np.exp(prediccion)
print("Predicción en escala real:", prediccion_real)
```

---

## Crear un simulador simple

Podemos simular valores de la variable dependiente para distintos valores de la independiente.

```python
import pandas as pd

valores = pd.DataFrame({"variable_independiente": range(10, 101, 10)})
valores["prediccion"] = modelo.predict(valores[["variable_independiente"]])
print(valores)
```

---

## Obtener el intercepto del modelo

```python
print("Intercepto:", modelo.intercept_)
```

---

## Obtener los coeficientes de regresión

```python
print("Coeficientes:", modelo.coef_)
```

---

## Crear un DataFrame para almacenar los coeficientes del modelo

```python
coeficientes = pd.DataFrame({
    "Variable": X.columns,
    "Coeficiente": modelo.coef_
})
print(coeficientes)
```

---

## Interpretar los coeficientes estimados

- El **intercepto** representa el valor esperado de la variable dependiente cuando todas las independientes son cero.
- Cada **coeficiente** indica el cambio esperado en la variable dependiente por unidad de cambio en la independiente, manteniendo las demás constantes.

---

## Analizar gráficamente los resultados del modelo

Podemos comparar las predicciones con los valores reales.

```python
import matplotlib.pyplot as plt

plt.scatter(y_test, y_pred)
plt.xlabel("Valores reales")
plt.ylabel("Predicciones")
plt.title("Comparación entre valores reales y predicciones")
plt.plot([y_test.min(), y_test.max()], [y_test.min(), y_test.max()], color="red", linestyle="--")
plt.show()
```