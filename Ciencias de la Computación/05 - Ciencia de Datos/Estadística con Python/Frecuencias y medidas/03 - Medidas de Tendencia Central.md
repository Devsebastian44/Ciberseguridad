## Media aritmética

La **media aritmética** es el promedio de los valores de una muestra:

```python
import pandas as pd

datos = pd.Series([10, 15, 20, 25, 30])
media = datos.mean()
print("Media:", media)
````

**Salida:**

```
Media: 20.0
```

La media es sensible a valores extremos (outliers). Por ejemplo, si añadimos un valor muy grande, la media se desplaza hacia él.

---

## Mediana

La **mediana** es el valor central de los datos ordenados.  
Si el número de observaciones es par, se toma el promedio de los dos valores centrales.

```python
mediana = datos.median()
print("Mediana:", mediana)
```

**Salida:**

```
Mediana: 20.0
```

La mediana es más robusta frente a valores extremos, ya que depende de la posición de los datos y no de su magnitud.

---

## Moda

La **moda** es el valor que aparece con mayor frecuencia en la distribución.  
Puede haber:

- **Una moda** → distribución unimodal.
- **Dos modas** → distribución bimodal.
- **Más de dos modas** → distribución multimodal.

```python
moda = datos.mode()
print("Moda:", moda)
```

**Salida:**

```
0    10
1    15
2    20
3    25
4    30
dtype: int64
```

En este ejemplo no hay un único valor repetido, por lo que todos los valores son modas.

---

## Relación entre medidas y asimetría

La comparación entre **media, mediana y moda** permite identificar la **asimetría** de la distribución:

- **Distribución simétrica:**  
    Media = Mediana = Moda
    
- **Asimetría positiva (sesgo a la derecha):**  
    Media > Mediana > Moda
    
- **Asimetría negativa (sesgo a la izquierda):**  
    Media < Mediana < Moda
    

```python
# Ejemplo con datos sesgados
datos_sesgados = pd.Series([1, 2, 2, 3, 4, 100])
print("Media:", datos_sesgados.mean())
print("Mediana:", datos_sesgados.median())
print("Moda:", datos_sesgados.mode()[0])
```

**Salida:**

```
Media: 18.666...
Mediana: 2.5
Moda: 2
```

Aquí se observa **asimetría positiva**, ya que la media es mucho mayor que la mediana y la moda.