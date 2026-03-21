## División de la base de datos

Para evaluar el modelo, se separan los datos en **conjunto de entrenamiento** y **conjunto de prueba**.

```python
from sklearn.model_selection import train_test_split

X = df[['x']]  # variable explicativa
y = df['y']    # variable respuesta

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
````

- **Entrenamiento**: se ajusta el modelo.
- **Prueba**: se evalúa el desempeño del modelo en datos no vistos.

---

## Coeficientes de regresión lineal simple

La recta de regresión se expresa como:

```python
from sklearn.linear_model import LinearRegression

modelo = LinearRegression()
modelo.fit(X_train, y_train)

print("Intercepto (β0):", modelo.intercept_)
print("Pendiente (β1):", modelo.coef_[0])
```

---

## Coeficiente de determinación R²

El **R²** mide la proporción de la variabilidad de Y explicada por el modelo.

- Valores cercanos a **1** → el modelo explica bien los datos.
- Valores cercanos a **0** → el modelo explica poco la variabilidad.

```python
r2_train = modelo.score(X_train, y_train)
print("R² en entrenamiento:", r2_train)
```

---

## Análisis de residuos

Los **residuos** son las diferencias entre los valores observados y los valores predichos por el modelo.

```python
import matplotlib.pyplot as plt

y_pred_train = modelo.predict(X_train)
residuos = y_train - y_pred_train

plt.scatter(X_train, residuos)
plt.axhline(y=0, color='red', linestyle='--')
plt.xlabel("Variable explicativa (X)")
plt.ylabel("Residuos")
plt.title("Análisis de residuos")
plt.show()
```

Un buen modelo muestra residuos distribuidos aleatoriamente alrededor de cero.

---

## Evaluación en el conjunto de prueba

Es fundamental calcular el R² en el conjunto de prueba para verificar la capacidad de generalización del modelo.

```python
r2_test = modelo.score(X_test, y_test)
print("R² en prueba:", r2_test)
```