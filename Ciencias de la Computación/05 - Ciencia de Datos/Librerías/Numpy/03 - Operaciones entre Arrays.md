## Operaciones

NumPy permite realizar operaciones matemáticas de manera vectorizada, es decir, elemento por elemento:

- **Suma y resta**

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
  
print(a + b)  # [5 7 9]
print(a - b)  # [-3 -3 -3]
```

- **Multiplicación y división**

```python
print(a * b)  # [ 4 10 18]
print(a / b)  # [0.25 0.4  0.5 ]
```

- **Operaciones con escalares**

```python
print(a * 2)  # [2 4 6]
print(b + 10) # [14 15 16]
```

- **Potencias con `np.power`**  
    Eleva cada elemento de un array a una potencia determinada.
```python
print(np.power(a, 2))   # [1 4 9]
print(np.power(b, 3))   # [64 125 216]
```

- **Raíz cuadrada con `np.sqrt`**  
    Calcula la raíz cuadrada de cada elemento.

```python
print(np.sqrt(a))  # [1.         1.41421356 1.73205081]
```
    

---

## Norma entre arrays y módulo `numpy.linalg`

El submódulo **`numpy.linalg`** contiene funciones para álgebra lineal: cálculo de normas, determinantes, inversas de matrices, valores propios, etc.

- **Norma Euclidiana (L2)**

```python
from numpy.linalg import norm
  
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
   
distancia = norm(a - b)
print(distancia)  # 5.196152422706632
```

- **Otras normas**
    - Norma L1 (suma de valores absolutos):

```python
distancia = norm(a - b, ord=1)
print(distancia)  # 9
```

- Norma infinita (máximo valor absoluto):

```python
distancia = norm(a - b, ord=np.inf)
print(distancia)  # 3
```

- **Funciones clave en `numpy.linalg`**
    - `norm(x)` → calcula normas vectoriales o matriciales.
    - `inv(A)` → inversa de una matriz.
    - `det(A)` → determinante de una matriz.
    - `eig(A)` → valores y vectores propios.
    - `lstsq(A, b)` → solución de mínimos cuadrados (usada en regresión lineal).

Ejemplo de inversa y determinante:

```python
A = np.array([[1, 2],
              [3, 4]])

print(np.linalg.inv(A))   # inversa
print(np.linalg.det(A))   # determinante
```

---

## Regresión Lineal
### ¿Qué es?

La **regresión lineal** es un método matemático y estadístico que busca encontrar una **recta** que describa la relación entre dos variables:

**y = m⋅x + c**

- x → variable independiente (ejemplo: temperatura).
- y → variable dependiente (ejemplo: ventas de helados).
- m → pendiente (cuánto cambia y cuando x aumenta en 1).
- c → intercepto (valor de y cuando x=0).

En palabras simples: la regresión lineal intenta dibujar una línea que pase lo más cerca posible de todos los puntos de tus datos.

### ¿Por qué sirve?

- **Predicción**: si conoces (x), puedes estimar (y).
- **Relación**: muestra cómo una variable influye en otra.
- **Ejemplo cotidiano**: más horas de estudio → mejor calificación.

### ¿Cómo se calcula?

El método más usado es el de **mínimos cuadrados**:

- Se busca la recta que minimice la suma de las distancias (errores) entre los puntos reales y la línea.
- Matemáticamente, se resuelve con álgebra lineal.

### `np.vstack`

- Significa _vertical stack_ (apilar verticalmente).
- Se usa para construir matrices a partir de vectores.
- En regresión lineal, nos permite crear la **matriz de diseño** con la variable x y una columna de unos para el intercepto.

Ejemplo:

```python
x = np.array([1, 2, 3])
unos = np.ones(len(x))
print(np.vstack([x, unos]).T)
```

Salida:

```
[[1. 1.]
 [2. 1.]
 [3. 1.]]
```

### `np.linalg`

- Es el submódulo de NumPy para **álgebra lineal**.
- Contiene funciones como:
    - `np.linalg.lstsq` → mínimos cuadrados (regresión lineal).
    - `np.linalg.norm` → cálculo de normas (distancias).
    - `np.linalg.inv` → inversa de matrices.
    - `np.linalg.det` → determinante.
    - `np.linalg.eig` → valores y vectores propios.

Ejemplo:

```python
A = np.array([[1, 2],
              [3, 4]])

print(np.linalg.inv(A))   # inversa
print(np.linalg.det(A))   # determinante
```

### Ejemplo paso a paso con NumPy

```python
import numpy as np
import matplotlib.pyplot as plt

# 1. Datos de ejemplo
x = np.array([1, 2, 3, 4, 5])   # Horas de estudio
y = np.array([2, 4, 5, 4, 5])   # Calificaciones

# 2. Construcción de la matriz de diseño
# Primera columna: valores de x
# Segunda columna: unos (para el intercepto c)
A = np.vstack([x, np.ones(len(x))]).T

# 3. Resolver con mínimos cuadrados
m, c = np.linalg.lstsq(A, y, rcond=None)[0]

print("Pendiente (m):", m)
print("Intercepto (c):", c)
print(f"Ecuación de la recta: y = {m:.2f}x + {c:.2f}")

# 4. Visualización
plt.scatter(x, y, color="blue", label="Datos reales")
plt.plot(x, m*x + c, color="red", label="Recta ajustada")
plt.xlabel("Horas de estudio")
plt.ylabel("Calificación")
plt.legend()
plt.title("Regresión Lineal desde cero")
plt.show()
```

## Interpretación del ejemplo

- La pendiente (m) indica cuánto sube la calificación por cada hora extra de estudio.
- El intercepto (c) indica la calificación esperada si no estudias nada.
- La recta roja es el modelo lineal que aproxima los puntos azules.