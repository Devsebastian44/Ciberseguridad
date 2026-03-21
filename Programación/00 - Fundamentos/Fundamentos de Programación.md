## 1. Introducción a la Programación
### 1.1 ¿Qué es la programación?

La programación es el proceso mediante el cual se crean instrucciones (código) para que una computadora realice tareas específicas. Estas instrucciones pueden ser dadas en distintos lenguajes de programación.

### 1.2 Lenguajes de Programación

Algunos de los lenguajes de programación más populares son Python, JavaScript, C++, Java, Ruby, entre otros.

### 1.3 Herramientas Necesarias

Para comenzar a programar, necesitarás un editor de texto y, en algunos casos, un compilador o un entorno de desarrollo integrado (IDE).

## 2. Variables y Tipos de Datos

### 2.1 ¿Qué es una variable?

Una variable es un espacio en la memoria de la computadora donde podemos almacenar valores.

### Ejemplo en Python:

```python
edad = 25 
nombre = "Sebastián"
```

### 2.2 Tipos de Datos Comunes

- **Enteros (int)**: Números enteros, como `1`, `2`, `-3`.
- **Punto flotante (float)**: Números con decimales, como `3.14`, `-1.5`.
- **Cadenas de texto (str)**: Secuencias de caracteres, como `"Hola Mundo"`.
- **Booleanos (bool)**: Valores `True` o `False`.

### Ejemplo en Python:

```python
let edad = 25;  // Número entero
let nombre = "Sebastián";  // Cadena de texto
let esEstudiante = true;  // Booleano
```

## 3. Operadores

### 3.1 Operadores Aritméticos

- **Suma**: `+`
- **Resta**: `-`
- **Multiplicación**: `*`
- **División**: `/`
- **Módulo**: `%` (resto de la división)

### Ejemplo en Python:

```python
suma = 5 + 3
producto = 4 * 2
```

### 3.2 Operadores de Comparación

- **Igual a**: `==`
- **Distinto a**: `!=`
- **Mayor que**: `>`
- **Menor que**: `<`
- **Mayor o igual que**: `>=`
- **Menor o igual que**: `<=`

### Ejemplo en Python:

```python
if (edad >= 18) {
    console.log("Eres adulto");
}
```

## 4. Estructuras de Control

### 4.1 Condicionales

#### 4.1.1 If - Else

Permiten ejecutar diferentes bloques de código según una condición.

### Ejemplo en Python:

```python
if (edad >= 18) {
    console.log("Eres adulto");
}
```

### Ejemplo en Javascript:

```javascript
if (edad >= 18) {
    console.log("Eres adulto");
} else {
    console.log("Eres menor de edad");
}
```

### 4.2 Bucles

#### 4.2.1 Bucle `for`

Usado para iterar sobre una secuencia de elementos.

#### Ejemplo en Python:

```python
for i in range(5):
    print(i)
```

### Ejemplo en Javascript:

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

#### 4.2.2 Bucle `while`

Se ejecuta mientras se cumpla una condición.

#### Ejemplo en Python:

```python
i = 0
while i < 5:
    print(i)
    i += 1
```

### Ejemplo en Javascript:

```javascript
let i = 0;
while (i < 5) {
    console.log(i);
    i++;
}
```

## 5. Funciones

### 5.1 ¿Qué es una función?

Una función es un bloque de código que realiza una tarea específica. Puede recibir entradas (argumentos) y devolver un valor.

#### Ejemplo en Python:

```python
def saludar(nombre):
    return f"Hola, {nombre}"

print(saludar("Sebastián"))
```

#### Ejemplo en JavaScript:

```javascript
function saludar(nombre) {
    return `Hola, ${nombre}`;
}

console.log(saludar("Sebastián"));
```

## 6. Arreglos y Listas

### 6.1 ¿Qué es un arreglo o lista?

Un arreglo o lista es una colección de elementos, los cuales pueden ser de cualquier tipo de dato.

#### Ejemplo en Python:

```python
frutas = ["manzana", "banana", "cereza"]
print(frutas[0])  # Imprime "manzana"
```

#### Ejemplo en Javascript:

```javascript
let frutas = ["manzana", "banana", "cereza"];
console.log(frutas[0]);  // Imprime "manzana"
```

## 7. Pseudocódigo y Diagramas de Flujo

### 7.1 Pseudocódigo

El pseudocódigo es una forma de escribir algoritmos en un lenguaje sencillo y comprensible por humanos.

#### Ejemplo en Pseudocódigo:

```arduino
Inicio
    Leer edad
    Si edad >= 18 entonces
        Imprimir "Eres adulto"
    Sino
        Imprimir "Eres menor de edad"
Fin
```

## 8. Ejercicios Prácticos

### 8.1 Ejercicio 1: Cálculo de la suma de dos números

Crea un programa que reciba dos números y calcule su suma.

#### Ejemplo en Pseudocódigo:

```java
Inicio
    Leer num1
    Leer num2
    suma = num1 + num2
    Imprimir suma
Fin
```

### 8.2 Ejercicio 2: Determinar si un número es par o impar

Crea un programa que reciba un número y determine si es par o impar.

#### Ejemplo en Pseudocódigo:

```java
Inicio
    Leer num
    Si num % 2 == 0 entonces
        Imprimir "Es par"
    Sino
        Imprimir "Es impar"
Fin
```







