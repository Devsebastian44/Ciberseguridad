## Agregar título y etiquetas a los ejes en una figura

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
ax.plot([1, 2, 3], [10, 20, 30])

ax.set_title("Ejemplo de Gráfico")
ax.set_xlabel("Eje X")
ax.set_ylabel("Eje Y")

plt.show()
```

---

## Crear una figura con subplots en una dirección

```python
fig, axes = plt.subplots(nrows=1, ncols=3, figsize=(10, 4))

axes[0].plot([1, 2, 3], [1, 4, 9])
axes[1].plot([1, 2, 3], [2, 4, 6])
axes[2].plot([1, 2, 3], [3, 6, 9])

plt.show()
```

Aquí los subplots están en **una sola fila**.

---

## Crear una figura con subplots en dos direcciones

```python
fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(8, 6))

axes[0,0].plot([1,2,3],[1,2,3])
axes[0,1].plot([1,2,3],[1,4,9])
axes[1,0].plot([1,2,3],[2,4,6])
axes[1,1].plot([1,2,3],[3,6,9])

plt.show()
```

Aquí los subplots están en **dos filas y dos columnas**.

---

## Modificar el espaciado entre subplots

```python
fig, axes = plt.subplots(2, 2, figsize=(8, 6))
plt.subplots_adjust(wspace=0.4, hspace=0.6)  # espacio horizontal y vertical
plt.show()
```

---

## Diferentes escalas en el eje Y y distorsiones

```python
fig, axes = plt.subplots(1, 2, figsize=(10, 4))

# Primer subplot con escala normal
axes[0].plot([1, 2, 3], [10, 20, 30])
axes[0].set_title("Escala normal")

# Segundo subplot con valores mucho más grandes
axes[1].plot([1, 2, 3], [1000, 2000, 3000])
axes[1].set_title("Escala diferente")

plt.show()
```

Esto puede causar **distorsión visual** al comparar resultados.

---

## Aplicar la misma escala en el eje Y

```python
fig, axes = plt.subplots(1, 2, figsize=(10, 4))

axes[0].plot([1, 2, 3], [10, 20, 30])
axes[1].plot([1, 2, 3], [1000, 2000, 3000])

# Igualar escalas en Y
axes[0].set_ylim(0, 3000)
axes[1].set_ylim(0, 3000)

plt.show()
```

---

## Crear un título general en una figura con subplots

```python
fig, axes = plt.subplots(2, 2, figsize=(8, 6))

fig.suptitle("Comparación de Subplots", fontsize=16)

plt.show()
```