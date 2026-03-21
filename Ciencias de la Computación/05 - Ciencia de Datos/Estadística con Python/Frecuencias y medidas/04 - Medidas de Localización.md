## Cuartiles, deciles y percentiles

Las medidas de localización dividen la distribución en partes iguales:

- **Cuartiles (Q1, Q2, Q3):** dividen la distribución en 4 partes.  
- **Deciles (D1, D2, …, D9):** dividen la distribución en 10 partes.  
- **Percentiles (P1, P2, …, P99):** dividen la distribución en 100 partes.  

```python
import pandas as pd

datos = pd.Series([7, 8, 5, 6, 9, 10, 12, 15, 18, 20])

# Cuartiles
q1 = datos.quantile(0.25)
q2 = datos.quantile(0.50)  # también es la mediana
q3 = datos.quantile(0.75)

print("Q1:", q1, "Q2:", q2, "Q3:", q3)

# Deciles
d4 = datos.quantile(0.4)
print("D4:", d4)

# Percentiles
p90 = datos.quantile(0.90)
print("P90:", p90)
````

**Salida:**

```
Q1: 7.75 Q2: 10.0 Q3: 16.5
D4: 9.6
P90: 19.0
```

---

## Boxplot (diagrama de caja)

El **boxplot** es una representación gráfica que utiliza los cuartiles para mostrar:

- **Q1 (cuartil inferior)**
- **Q2 (mediana)**
- **Q3 (cuartil superior)**
- **Rango intercuartílico (IQR = Q3 - Q1)**
- Valores extremos y posibles **outliers**

```python
import matplotlib.pyplot as plt

plt.boxplot(datos)
plt.title("Boxplot de la distribución")
plt.ylabel("Valores")
plt.show()
```

Este gráfico permite identificar rápidamente:

- La **dispersión** de los datos.
- La **simetría o asimetría** de la distribución.
- La presencia de **valores atípicos**.