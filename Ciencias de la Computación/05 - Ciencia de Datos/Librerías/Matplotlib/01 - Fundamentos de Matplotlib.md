## Extraer una serie de datos de un DataFrame

Para graficar, normalmente trabajamos con datos de **Pandas**.

```python
import pandas as pd

# Ejemplo de DataFrame
df = pd.DataFrame({
    "Año": [2020, 2021, 2022, 2023],
    "Ventas": [100, 150, 200, 250]
})

# Extraer una serie
ventas = df["Ventas"]
años = df["Año"]
```

---

## Importar el módulo `pyplot`

```python
import matplotlib.pyplot as plt
```

---

## Graficar un gráfico básico

```python
plt.plot(años, ventas)
plt.show()
```

---

## Cambiar los _ticks_ de los ejes X e Y

```python
plt.plot(años, ventas)
plt.xticks([2020, 2021, 2022, 2023])  # ticks personalizados en X
plt.yticks([100, 150, 200, 250])      # ticks personalizados en Y
plt.show()
```

---

## Mostrar el gráfico

La función `plt.show()` **renderiza** el gráfico en pantalla.  
Es importante llamarla al final de la construcción del gráfico.

---

## Modificar el tamaño del gráfico

```python
plt.figure(figsize=(8, 5))  # ancho x alto en pulgadas
plt.plot(años, ventas)
plt.show()
```

---

## Agregar un título al gráfico

```python
plt.plot(años, ventas)
plt.title("Ventas por Año")
plt.show()
```

---

## Agregar etiquetas a los ejes

```python
plt.plot(años, ventas)
plt.xlabel("Año")
plt.ylabel("Ventas")
plt.show()
```

---

## Crear una figura

```python
fig = plt.figure(figsize=(6, 4))
ax = fig.add_subplot(111)  # 1 fila, 1 columna, primer gráfico
ax.plot(años, ventas)
plt.show()
```

---

## Modificar la frecuencia de los _ticks_ en el eje X

```python
import matplotlib.ticker as ticker

fig, ax = plt.subplots()
ax.plot(años, ventas)

# Configurar ticks cada 1 unidad
ax.xaxis.set_major_locator(ticker.MultipleLocator(1))

plt.show()
```
