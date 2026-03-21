## Coeficiente de correlación

El **coeficiente de correlación de Pearson (r)** mide la fuerza y dirección de la relación lineal entre dos variables.

- Valores cercanos a **+1** → correlación positiva fuerte  
- Valores cercanos a **-1** → correlación negativa fuerte  
- Valores cercanos a **0** → ausencia de correlación lineal  

**Ejemplo en Python:**

```python
import pandas as pd

# Datos de ejemplo
data = {'x':[1,2,3,4,5], 'y':[2,4,5,4,5]}
df = pd.DataFrame(data)

# Calcular correlación
correlacion = df['x'].corr(df['y'])
print("Coeficiente de correlación:", correlacion)
````

---

## Intensidad y dirección de la correlación

- **Dirección**: positiva (ambas variables aumentan) o negativa (una aumenta y la otra disminuye).
- **Intensidad**: depende de qué tan cerca está el valor de r a ±1.

Ejemplo interpretativo:

- r = 0.85 → relación positiva fuerte
- r = -0.60 → relación negativa moderada

---

## Gráfico de dispersión y linealidad

El **gráfico de dispersión** permite visualizar si los puntos siguen una tendencia lineal.

```python
import matplotlib.pyplot as plt

plt.scatter(df['x'], df['y'])
plt.xlabel("Variable explicativa (X)")
plt.ylabel("Variable respuesta (Y)")
plt.title("Gráfico de dispersión")
plt.show()
```

Si los puntos se alinean en torno a una recta, existe linealidad.

---

## Variables en regresión lineal

- **Variable explicativa (X)**: la que usamos para predecir.
- **Variable respuesta (Y)**: la que queremos explicar o estimar.

Ejemplo:

- X = horas de estudio
- Y = calificación obtenida

---

## Ajuste de la recta con Plotly

Plotly permite visualizar la mejor línea de ajuste de manera interactiva.

```python
import plotly.express as px
import numpy as np

# Datos
x = np.array([1,2,3,4,5])
y = np.array([2,4,5,4,5])

# Ajuste lineal
coef = np.polyfit(x, y, 1)
recta = np.poly1d(coef)

# Crear gráfico
fig = px.scatter(x=x, y=y, labels={'x':'Variable explicativa', 'y':'Variable respuesta'})
fig.add_scatter(x=x, y=recta(x), mode='lines', name='Línea de ajuste')
fig.show()
```