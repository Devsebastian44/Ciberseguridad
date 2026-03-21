## Modificar el tamaño de las fuentes del título y etiquetas

```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3], [10, 20, 30])
plt.title("Ventas", fontsize=18)
plt.xlabel("Año", fontsize=14)
plt.ylabel("Valor", fontsize=14)
plt.show()
```

---

## Modificar la posición del título

```python
plt.plot([1, 2, 3], [10, 20, 30])
plt.title("Ventas", loc="left")   # opciones: 'left', 'center', 'right'
plt.show()
```

---

## Cambiar el grosor de la línea

```python
plt.plot([1, 2, 3], [10, 20, 30], linewidth=3)
plt.show()
```

---

## Agregar marcadores a la línea

```python
plt.plot([1, 2, 3], [10, 20, 30], marker="o", linestyle="-")
plt.show()
```

---

## Agregar cuadrículas al fondo

```python
plt.plot([1, 2, 3], [10, 20, 30])
plt.grid(True, linestyle="--", alpha=0.7)
plt.show()
```

---

## Cambiar el color de solo una variable

```python
plt.plot([1, 2, 3], [10, 20, 30], color="red")
plt.show()
```

---

## Cambiar colores con varias categorías

```python
x = [1, 2, 3]
y1 = [10, 20, 30]
y2 = [5, 15, 25]

plt.plot(x, y1, color="blue", label="Categoría A")
plt.plot(x, y2, color="green", label="Categoría B")
plt.legend()
plt.show()
```

---

## Crear un gráfico de barras horizontal

```python
categorias = ["A", "B", "C"]
valores = [10, 20, 30]

plt.barh(categorias, valores, color="purple")
plt.show()
```

---

## Resaltar información en un gráfico

```python
x = [1, 2, 3, 4, 5]
y = [10, 20, 30, 40, 50]

plt.plot(x, y)
plt.scatter([3], [30], color="red", s=100, label="Punto destacado")
plt.legend()
plt.show()
```

---

## Agregar anotaciones de texto

```python
plt.plot(x, y)
plt.annotate("Máximo", xy=(5, 50), xytext=(4, 45),
             arrowprops=dict(facecolor="black", shrink=0.05))
plt.show()
```

---

## Eliminar el marco alrededor del gráfico

```python
fig, ax = plt.subplots()
ax.plot([1, 2, 3], [10, 20, 30])

# Ocultar bordes (spines)
for spine in ax.spines.values():
    spine.set_visible(False)

plt.show()
```

---

## Guardar las figuras

```python
plt.plot([1, 2, 3], [10, 20, 30])
plt.savefig("grafico.png", dpi=300, bbox_inches="tight")
```
