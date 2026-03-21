## Importar la biblioteca Seaborn

```python
import seaborn as sns
import matplotlib.pyplot as plt
```

---

## Definir el tema predeterminado

```python
sns.set_theme(style="darkgrid")  # opciones: "darkgrid", "whitegrid", "dark", "white", "ticks"
```

---

## Crear un gráfico de barras vertical

```python
import pandas as pd

df = pd.DataFrame({
    "Categoría": ["A", "B", "C"],
    "Valores": [10, 20, 30]
})

sns.barplot(x="Categoría", y="Valores", data=df)
plt.show()
```

---

## Crear un gráfico de barras horizontal

```python
sns.barplot(x="Valores", y="Categoría", data=df, orient="h")
plt.show()
```

---

## Agregar título y etiquetas a los ejes

```python
ax = sns.barplot(x="Categoría", y="Valores", data=df)
ax.set_title("Gráfico de Barras")
ax.set_xlabel("Categorías")
ax.set_ylabel("Valores")
plt.show()
```

---

## Usar Seaborn y Matplotlib juntos

```python
fig, ax = plt.subplots(figsize=(6,4))
sns.barplot(x="Categoría", y="Valores", data=df, ax=ax)
ax.set_title("Gráfico con Seaborn + Matplotlib")
plt.show()
```

---

## Cambiar colores utilizando paletas

```python
sns.barplot(x="Categoría", y="Valores", data=df, palette="pastel")
plt.show()

# otras paletas: "deep", "muted", "bright", "dark", "colorblind"
```

---

## Explorar diferentes temas

```python
sns.set_theme(style="whitegrid")
sns.barplot(x="Categoría", y="Valores", data=df)
plt.show()
```

---

## Eliminar bordes con `sns.despine()`

```python
sns.barplot(x="Categoría", y="Valores", data=df)
sns.despine()  # elimina los bordes superiores y derechos
plt.show()
```
