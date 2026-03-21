# Expresiones Lambda

Las expresiones lambda son funciones sin nombre que se pueden pasar y ejecutar más tarde.

## Características clave de las lambdas:

- **Anónimo**: No tienen nombre como las funciones regulares
- **Función literal**: Definidos sin la palabra clave `fun`
- **Expresiones**: Se pasan como parte de una expresión, a menudo como argumentos de funciones de orden superior
- **Sintaxis concisa**: Utiliza llaves `{}` para encerrar el cuerpo de la función

## Variaciones principales en lambdas:

1. En la función definir tipos en los parámetros y un tipo de retorno
2. En la función definir tipos en los parámetros y sin tipo de retorno (Unit)
3. Función sin parámetros y un tipo de retorno
4. Función sin parámetros y sin tipo de retorno (Unit)

## Palabra reservada Unit

El tipo `Unit` en Kotlin se usa para representar la ausencia de un valor significativo, similar a `void` en Java. Se usa comúnmente para indicar que una función no devuelve ningún valor útil.

## Higher-Order Functions (HOF)

Una función de orden superior es una función que toma una o más funciones como argumentos o devuelve una función como resultado.

### Ejemplos de funciones de orden superior en Kotlin:

**Operaciones en colección:**

- `filter()`
- `forEach()`
- `map()`
- `reduce()`

## Palabra reservada `it`

`it` es una forma abreviada de hacer referencia a un único parámetro en una expresión lambda. Cuando una expresión lambda tiene un único parámetro, Kotlin proporciona automáticamente este parámetro como `it`.

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val evenNumbers = numbers.filter { it % 2 == 0 } // Prints 2,4
```

### Ejemplo de `it`:

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val doubled = numbers.map { it * 2 }
println(doubled) // Output: [2, 4, 6, 8, 10]
```


# Modificador inline

Una función `inline` indica al compilador que inserte el cuerpo completo de la función donde sea que se use dicha función en el código.

## Notación Infix

Las funciones marcadas con la palabra clave `infix` también pueden llamarse mediante la notación infix (omitiendo el punto y los paréntesis).

### Requisitos para funciones infix:

- Deben ser funciones miembro o funciones de extensión
- Deben tener un solo parámetro
- El parámetro no debe aceptar un número variable de argumentos (varargs) y no debe tener un valor predeterminado

**Propósito**: Las funciones infix pueden hacer que nuestro código se parezca más a un lenguaje natural, mejorando la legibilidad.

### Tipos de notación infix:

1. Notación de función infix de la biblioteca estándar
2. Notación de función infix definida por el usuario


# Funciones de Alcance

Estas funciones permiten manipular objetos y ejecutar código en un contexto determinado, evitando la repetición de código y mejorando la legibilidad.

### Las cinco funciones de alcance principales:

- `let`
- `run`
- `with`
- `apply`
- `also`

### Usos comunes:

- **`let()`**: Transformar un objeto
- **`also()`**: Crear, pasar y evaluar un objeto
- **`run()`**: Inicializar y ejecutar
- **`apply()`**: Inicializar un objeto para su asignación
- **`with()`**: Funcionalmente es igual que la versión de la función de extensión de `run()`, ideal para inicializar y ejecutar

### Valor de retorno:

Las funciones de alcance se diferencian por el resultado que devuelven:

- `apply` y `also` devuelven el objeto de contexto
- `let`, `run`, y `with` devuelven el resultado lambda


# Tipos de Funciones

### Funciones Anónimas

Las funciones anónimas son útiles cuando necesitamos definir una función simple que se utilizará solo una vez en el programa.

```kotlin
val suma = fun(a: Int, b: Int): Int {
    return a + b
}
val resultado = suma(30, 50)
print(resultado)
```

### Funciones Lambda

Las funciones lambda son otra forma de escribir funciones anónimas pero implican características sintácticas que las hacen más cortas y concisas.

kotlin

```kotlin
val suma = { a: Int, b: Int -> a + b }
val resultado = suma(30, 50)
print(resultado)
```

### Funciones Regulares

```kotlin
fun suma(a: Int, b: Int): Int {
    return a + b
}
val resultado = suma(30, 50)
print(resultado)
```