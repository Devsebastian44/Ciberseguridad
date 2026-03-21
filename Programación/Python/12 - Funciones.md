## Funciones en Python

Las funciones son bloques de código reutilizables que realizan una tarea específica. Permiten organizar el código, evitar repetición y facilitar el mantenimiento.

---

## Definir una función

```python
def saludar():
    print("¡Hola, mundo!")

saludar()  # ¡Hola, mundo!
```

---

## Parámetros

### Un parámetro

```python
def hello(name):
    print("Hello " + name)

hello("Sebas")  # Hello Sebas
```

### Múltiples parámetros

```python
def add(number1, number2):
    return number1 + number2

print(add(10, 20))  # 30
```

---

## Return

La palabra clave `return` permite que una función devuelva un valor.

```python
def sumar(a, b):
    return a + b

resultado = sumar(5, 3)
print(resultado)  # 8
```

### Retornar múltiples valores

```python
def operaciones(a, b):
    suma = a + b
    resta = a - b
    multiplicacion = a * b
    return suma, resta, multiplicacion

s, r, m = operaciones(10, 5)
print(f"Suma: {s}, Resta: {r}, Multiplicación: {m}")
# Suma: 15, Resta: 5, Multiplicación: 50
```

---

## Parámetros por defecto

Los parámetros pueden tener valores por defecto que se usan si no se proporciona un argumento.

```python
def saludar(nombre="Usuario"):
    print(f"¡Hola, {nombre}!")

saludar()           # ¡Hola, Usuario!
saludar("Juan")     # ¡Hola, Juan!
```

---

## Tipos de argumentos

### Argumentos posicionales

Se pasan en el orden definido en la función.

```python
def presentar(nombre, edad, ciudad):
    print(f"{nombre} tiene {edad} años y vive en {ciudad}")

presentar("Juan", 30, "Madrid")
# Juan tiene 30 años y vive en Madrid
```

### Argumentos de palabra clave (keyword arguments)

Se pasan especificando el nombre del parámetro.

```python
def print_name(name, surname):
    print(f"{name} {surname}")

print_name(surname="Moure", name="Brais")  # Brais Moure
```

### Combinación

```python
presentar("Juan", ciudad="Madrid", edad=30)
# Juan tiene 30 años y vive en Madrid
```

---

## *args - Argumentos variables posicionales

`*args` permite pasar un número variable de argumentos posicionales. Los empaqueta en una tupla.

```python
def sumar_todos(*numeros):
    total = 0
    for numero in numeros:
        total += numero
    return total

print(sumar_todos(1, 2, 3))           # 6
print(sumar_todos(1, 2, 3, 4, 5))     # 15
```

---

## **kwargs - Argumentos variables de palabra clave

`**kwargs` permite pasar un número variable de argumentos de palabra clave. Los empaqueta en un diccionario.

```python
def mostrar_datos(**datos):
    for clave, valor in datos.items():
        print(f"{clave}: {valor}")

mostrar_datos(nombre="Juan", edad=30, ciudad="Madrid")
# nombre: Juan
# edad: 30
# ciudad: Madrid
```

---

## Combinación de *args y **kwargs

Se pueden combinar parámetros normales, `*args` y `**kwargs`.

```python
def funcion_completa(obligatorio, opcional="default", *args, **kwargs):
    print(f"Obligatorio: {obligatorio}")
    print(f"Opcional: {opcional}")
    print(f"Args: {args}")
    print(f"Kwargs: {kwargs}")

funcion_completa("A", "B", 1, 2, 3, x=10, y=20)
# Obligatorio: A
# Opcional: B
# Args: (1, 2, 3)
# Kwargs: {'x': 10, 'y': 20}
```

---

## Ámbito de variables (scope)

### Variables locales

Las variables definidas dentro de una función solo existen dentro de ella.

```python
def mi_funcion():
    variable_local = 10
    print(variable_local)

mi_funcion()  # 10
# print(variable_local)  # Error: no está definida fuera
```

### Variables globales

```python
variable_global = 100

def mi_funcion():
    print(variable_global)

mi_funcion()  # 100
```

### Modificar variables globales

```python
contador = 0

def incrementar():
    global contador
    contador += 1

incrementar()
print(contador)  # 1
```

---

## Funciones lambda

Funciones anónimas de una sola línea.

```python
multiplicar = lambda x: x * 2
print(multiplicar(4))  # 8

sumar = lambda a, b: a + b
print(sumar(5, 3))  # 8
```

### Uso con funciones integradas

```python
numeros = [1, 2, 3, 4, 5]

# Con map
cuadrados = list(map(lambda x: x ** 2, numeros))
print(cuadrados)  # [1, 4, 9, 16, 25]

# Con filter
pares = list(filter(lambda x: x % 2 == 0, numeros))
print(pares)  # [2, 4]

# Con sorted
palabras = ['python', 'es', 'genial']
ordenadas = sorted(palabras, key=lambda x: len(x))
print(ordenadas)  # ['es', 'genial', 'python']
```

---

## Funciones recursivas

Una función recursiva es aquella que se llama a sí misma.

### Factorial

```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * factorial(n - 1)

print(factorial(5))  # 120
```

### Fibonacci

```python
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(6))  # 8
```

---

## Closures

Un closure es una función que recuerda los valores del entorno donde fue creada.

```python
def crear_multiplicador(factor):
    def multiplicar(numero):
        return numero * factor
    return multiplicar

multiplicar_por_2 = crear_multiplicador(2)
print(multiplicar_por_2(10))  # 20
```

### Ejemplo con contador

```python
def crear_contador():
    contador = 0
    
    def incrementar():
        nonlocal contador
        contador += 1
        return contador
    
    return incrementar

contador1 = crear_contador()
print(contador1())  # 1
print(contador1())  # 2
```

---

## Decoradores

Los decoradores son funciones que modifican el comportamiento de otras funciones.

### Decorador simple

```python
def mi_decorador(funcion):
    def wrapper():
        print("Antes de ejecutar")
        funcion()
        print("Después de ejecutar")
    return wrapper

@mi_decorador
def saludar():
    print("¡Hola!")

saludar()
# Antes de ejecutar
# ¡Hola!
# Después de ejecutar
```

### Decorador con argumentos

```python
def mi_decorador(funcion):
    def wrapper(*args, **kwargs):
        print(f"Argumentos: {args}, {kwargs}")
        resultado = funcion(*args, **kwargs)
        return resultado
    return wrapper

@mi_decorador
def sumar(a, b):
    return a + b

sumar(5, 3)
# Argumentos: (5, 3), {}
```

### Ejemplo práctico: Medir tiempo

```python
import time

def medir_tiempo(funcion):
    def wrapper(*args, **kwargs):
        inicio = time.time()
        resultado = funcion(*args, **kwargs)
        fin = time.time()
        print(f"Tiempo: {fin - inicio:.4f} segundos")
        return resultado
    return wrapper

@medir_tiempo
def proceso_lento():
    time.sleep(1)
    print("Completado")

proceso_lento()
```

---

## Resumen

|Concepto|Descripción|
|---|---|
|`def`|Define una función|
|Parámetros|Valores que recibe la función|
|`return`|Devuelve un valor|
|Valores por defecto|Parámetros con valores predefinidos|
|`*args`|Argumentos posicionales variables (tupla)|
|`**kwargs`|Argumentos de palabra clave variables (dict)|
|`global`|Modificar variables globales|
|`lambda`|Funciones anónimas de una línea|
|Recursividad|Función que se llama a sí misma|
|Closures|Función que recuerda su entorno|
|Decoradores|Modifican comportamiento de funciones|
