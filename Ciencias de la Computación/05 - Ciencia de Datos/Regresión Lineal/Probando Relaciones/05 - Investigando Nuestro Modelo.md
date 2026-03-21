## Multicolinealidad

La **multicolinealidad** ocurre cuando dos o más variables explicativas están altamente correlacionadas.  
Consecuencias:  
- Dificulta interpretar los coeficientes.  
- Puede inflar errores estándar.  
- Reduce la estabilidad del modelo.  

---

## Factor de Inflación de la Varianza (VIF)

El **VIF** cuantifica el grado de multicolinealidad.  
- VIF = 1 → no hay correlación.  
- VIF entre 1 y 5 → aceptable.  
- VIF > 10 → problema serio de multicolinealidad.  

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor
import pandas as pd

X = df[['metros','habitaciones','antiguedad']]
vif_data = pd.DataFrame()
vif_data["Variable"] = X.columns
vif_data["VIF"] = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]

print(vif_data)
````

---

## Gráfico de valores predichos vs valores reales

Comparar valores predichos con los reales permite evaluar el ajuste del modelo.

```python
import matplotlib.pyplot as plt

y_pred = modelo.predict(X)

plt.scatter(y, y_pred)
plt.xlabel("Valores reales")
plt.ylabel("Valores predichos")
plt.title("Predichos vs Reales")
plt.plot([y.min(), y.max()], [y.min(), y.max()], color='red', linestyle='--')
plt.show()
```

Interpretación:

- Si los puntos se alinean cerca de la diagonal → buen ajuste.
- Si se dispersan mucho → limitaciones del modelo.

---

## Análisis de residuos y homocedasticidad

La **homocedasticidad** implica que la varianza de los residuos es constante.  
Se analiza graficando residuos vs valores predichos.

```python
residuos = y - y_pred

plt.scatter(y_pred, residuos)
plt.axhline(y=0, color='red', linestyle='--')
plt.xlabel("Valores predichos")
plt.ylabel("Residuos")
plt.title("Residuos vs Predichos")
plt.show()
```

Interpretación:

- Distribución aleatoria alrededor de cero → homocedasticidad.
- Patrón en forma de abanico → heterocedasticidad.

---

## Limitaciones del modelo

- El modelo puede no capturar bien precios de propiedades más caras.
- Posibles causas: falta de variables explicativas relevantes (ubicación, calidad de materiales, servicios cercanos).
- Es importante explorar nuevas variables para mejorar la precisión y la interpretabilidad.
