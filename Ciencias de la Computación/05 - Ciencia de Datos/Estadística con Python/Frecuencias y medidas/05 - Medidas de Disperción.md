## Desviación media absoluta (DMA)

La **desviación media absoluta** mide el promedio de las distancias absolutas de cada dato respecto a la media:

```python
import pandas as pd

datos = pd.Series([10, 12, 13, 17, 20])

media = datos.mean()
dma = (abs(datos - media)).mean()

print("Media:", media)
print("Desviación Media Absoluta:", dma)
````

**Salida:**

```
Media: 14.4
Desviación Media Absoluta: 3.44
```

---

## Varianza

La **varianza** mide la dispersión de los datos respecto a la media, elevando las diferencias al cuadrado:

En **pandas**, se calcula con `.var()`.  
Por defecto, se usa el denominador (n-1) (muestra). Para la población completa, se puede ajustar con `ddof=0`.

```python
varianza_muestral = datos.var()        # n-1
varianza_poblacional = datos.var(ddof=0)  # n

print("Varianza muestral:", varianza_muestral)
print("Varianza poblacional:", varianza_poblacional)
```

---

## Desviación estándar

La **desviación estándar** es la raíz cuadrada de la varianza:

En **pandas**, se calcula con `.std()`.

```python
desviacion_muestral = datos.std()        # n-1
desviacion_poblacional = datos.std(ddof=0)  # n

print("Desviación estándar muestral:", desviacion_muestral)
print("Desviación estándar poblacional:", desviacion_poblacional)
```

---

## Interpretación

- **DMA:** útil para entender la dispersión promedio sin exagerar el efecto de valores extremos.
- **Varianza:** refleja la variabilidad, pero está en unidades al cuadrado.
- **Desviación estándar:** más interpretativa, ya que está en las mismas unidades que los datos originales.

Ejemplo:  
Si dos conjuntos tienen la misma media pero diferentes desviaciones estándar, el que tenga mayor desviación estándar será más **disperso**.