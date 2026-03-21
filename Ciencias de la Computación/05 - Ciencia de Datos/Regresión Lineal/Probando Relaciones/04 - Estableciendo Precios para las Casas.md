## R² en datos de prueba

El R² en el conjunto de prueba indica qué tan bien el modelo generaliza a datos no vistos.

```python
from sklearn.metrics import r2_score

y_pred_test = modelo.predict(X_test)
r2_test = r2_score(y_test, y_pred_test)

print("R² en prueba:", r2_test)
````

---

## Comparación de métricas de entrenamiento y prueba

Es importante comparar el R² en entrenamiento y prueba:

- Si el R² en entrenamiento es mucho mayor que en prueba → posible **sobreajuste**.
- Si ambos valores son similares → el modelo generaliza bien.

```python
r2_train = modelo.score(X_train, y_train)
r2_test = modelo.score(X_test, y_test)

print("R² entrenamiento:", r2_train)
print("R² prueba:", r2_test)
```

---

## Predicción de nuevos valores

El método `predict` permite estimar el precio de nuevas casas a partir de sus características.

```python
# Ejemplo: nueva casa con 120 metros, 4 habitaciones y 10 años de antigüedad
nueva_casa = [[120, 4, 10]]
precio_estimado = modelo.predict(nueva_casa)

print("Precio estimado:", precio_estimado[0])
```

---

## Guardar el modelo con Pickle

La biblioteca **pickle** permite guardar el modelo entrenado para reutilizarlo sin necesidad de volver a entrenar.

```python
import pickle

# Guardar modelo
with open("modelo_regresion.pkl", "wb") as archivo:
    pickle.dump(modelo, archivo)
```

---

## Cargar el modelo desde Pickle

Se puede recuperar el modelo en su estado original para realizar predicciones.

```python
# Leer modelo guardado
with open("modelo_regresion.pkl", "rb") as archivo:
    modelo_cargado = pickle.load(archivo)

# Usar el modelo cargado
precio_estimado = modelo_cargado.predict(nueva_casa)
print("Precio estimado con modelo cargado:", precio_estimado[0])
```
