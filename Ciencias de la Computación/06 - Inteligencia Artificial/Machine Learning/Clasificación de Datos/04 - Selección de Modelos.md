## Normalización de datos

La normalización asegura que todas las variables estén en la misma escala.  
- Es importante porque algunos algoritmos, como KNN, dependen de distancias.  
- Se suele aplicar con **StandardScaler** o **MinMaxScaler** de Scikit-Learn.  

**Ejemplo:**
```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
````

---

## Modelo de vecinos más cercanos (KNN)

El **KNeighborsClassifier** clasifica observaciones según las clases de sus vecinos más cercanos.

- Se basa en la distancia entre puntos.
- El parámetro `n_neighbors` define cuántos vecinos se consideran.

**Ejemplo:**

```python
from sklearn.neighbors import KNeighborsClassifier

knn = KNeighborsClassifier(n_neighbors=5)
knn.fit(X_train_scaled, y_train)

print("Score KNN:", knn.score(X_test_scaled, y_test))
```

---

## Comparación de resultados de modelos

Comparar diferentes modelos permite elegir el más adecuado.

- Se evalúa con métricas como **accuracy** (`score`).
- Se pueden probar varios clasificadores y comparar sus resultados.

**Ejemplo:**

```python
print("Score Árbol:", tree.score(X_test, y_test))
print("Score KNN:", knn.score(X_test_scaled, y_test))
```

---

## Predicciones con nuevos datos

Una vez entrenado, el modelo puede predecir la clase de nuevas observaciones.

**Ejemplo:**

```python
nuevo_dato = [[1.70, 65]]  # Altura y peso
nuevo_dato_scaled = scaler.transform(nuevo_dato)

prediccion = knn.predict(nuevo_dato_scaled)
print("Predicción:", prediccion)
```

---

## Exportación de modelos con pickle

Guardar modelos entrenados permite reutilizarlos sin necesidad de reentrenar.

- Se usa la biblioteca **pickle** para serializar objetos en Python.

**Ejemplo:**

```python
import pickle

# Guardar modelo
with open("modelo_knn.pkl", "wb") as f:
    pickle.dump(knn, f)

# Cargar modelo
with open("modelo_knn.pkl", "rb") as f:
    modelo_cargado = pickle.load(f)

print("Score modelo cargado:", modelo_cargado.score(X_test_scaled, y_test))
```
```