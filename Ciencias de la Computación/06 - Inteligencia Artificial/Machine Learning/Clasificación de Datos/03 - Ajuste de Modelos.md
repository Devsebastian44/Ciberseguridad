## Separación entre entrenamiento y prueba

Para evaluar correctamente un modelo, se divide el conjunto de datos en dos partes:  
- **Entrenamiento:** usado para ajustar el modelo.  
- **Prueba:** usado para medir el desempeño en datos no vistos.  

**Ejemplo en Python:**

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

print(X_train.shape, X_test.shape)
````

---

## Modelo base con DummyClassifier

El **DummyClassifier** sirve como referencia inicial.

- No aprende patrones, solo aplica reglas simples (ejemplo: siempre predice la clase más frecuente).
- Permite comparar si un modelo real aporta mejoras.

**Ejemplo:**

```python
from sklearn.dummy import DummyClassifier

dummy = DummyClassifier(strategy="most_frequent")
dummy.fit(X_train, y_train)

print("Score Dummy:", dummy.score(X_test, y_test))
```

---

## Modelo de árbol de decisión con DecisionTreeClassifier

El **árbol de decisión** es un modelo que divide los datos en ramas según condiciones.

- Fácil de interpretar.
- Útil para clasificación inicial.

**Ejemplo:**

```python
from sklearn.tree import DecisionTreeClassifier

tree = DecisionTreeClassifier(random_state=42)
tree.fit(X_train, y_train)

print("Score Árbol:", tree.score(X_test, y_test))
```

---

## Evaluación con el método score

El método `score` calcula la **tasa de acierto** (accuracy).

- Mide el porcentaje de predicciones correctas.
- Es una métrica básica para comparar modelos.

**Ejemplo:**

```python
accuracy = tree.score(X_test, y_test)
print("Exactitud del modelo:", accuracy)
```

---

## Visualización del árbol de decisión

La función `plot_tree` permite graficar las decisiones del árbol.

- Muestra cómo se dividen las ramas.
- Facilita la interpretación del modelo.

**Ejemplo:**

```python
import matplotlib.pyplot as plt
from sklearn.tree import plot_tree

plt.figure(figsize=(12,8))
plot_tree(tree, feature_names=X.columns, class_names=label_encoder.classes_, filled=True)
plt.show()
```