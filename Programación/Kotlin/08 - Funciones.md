Una **función** es un bloque de código reutilizable que realiza una tarea. Kotlin facilita la creación de funciones de forma clara y expresiva.

## Declaración básica de funciones

```kotlin
fun saludar() {
    println("Hola desde una función")
}

saludar() // Para llamar la funcion
```

## Funciones con parámetros

```kotlin
fun saludar(nombre: String) {
    println("Hola, $nombre")
}

saludar("Sebastián")
```

## Funciones con valor de retorno

```kotlin
fun sumar(a: Int, b: Int): Int {
    return a + b
}

val resultado = sumar(3, 5)
println("Resultado: $resultado") // 8
```

También puedes usar la forma **reducida** si el cuerpo es una sola línea:

```kotlin
fun multiplicar(a: Int, b: Int) = a * b
```

## Parámetros por defecto

```kotlin
fun saludar(nombre: String = "visitante") {
    println("Hola, $nombre")
}

saludar()         // Hola, visitante
saludar("Juan")   // Hola, Juan
```

## Argumentos nombrados

Puedes llamar a los parámetros por su nombre, sin importar el orden.

```kotlin
fun mostrarInfo(nombre: String, edad: Int) {
    println("$nombre tiene $edad años")
}

mostrarInfo(edad = 19, nombre = "Sebastián")
```

## Funciones `Unit` (sin retorno)

`Unit` es equivalente a `void` en otros lenguajes. Se puede omitir:

```kotlin
fun imprimirMensaje(mensaje: String): Unit {
    println(mensaje)
}
```

O simplemente:

```kotlin
fun imprimirMensaje(mensaje: String) {
    println(mensaje)
}
```

## Funciones anidadas

Puedes declarar una función dentro de otra:

```kotlin
fun operacion(a: Int, b: Int) {
    fun suma(x: Int, y: Int) = x + y
    println("Resultado: ${suma(a, b)}")
}
```

### Funciones de una sola expresión

```kotlin
fun cuadrado(x: Int) = x * x
```

### Funciones lambda (funciones como variables)

```kotlin
val saludar = { println("Hola desde una lambda") }
saludar()
```

Con parámetros:

```kotlin
val sumar = { a: Int, b: Int -> a + b }
println(sumar(3, 4)) // 7
```

## Funciones de orden superior

Una función que recibe otra como parámetro:

```kotlin
fun operar(a: Int, b: Int, operacion: (Int, Int) -> Int): Int {
    return operacion(a, b)
}

val resultado = operar(5, 3) { x, y -> x + y }
println(resultado) // 8
```

## Funciones `inline`

Se utiliza para optimizar funciones de orden superior (el compilador reemplaza el código en tiempo de compilación):

```kotlin
inline fun medirTiempo(bloque: () -> Unit) {
    val inicio = System.currentTimeMillis()
    bloque()
    val fin = System.currentTimeMillis()
    println("Tiempo: ${fin - inicio}ms")
}

medirTiempo {
    Thread.sleep(500)
}
```

### Funciones locales y alcance

```kotlin
fun ejemplo() {
    val x = 5

    fun mostrarX() {
        println(x) // Accede a variables externas
    }

    mostrarX()
}
```

### Retorno temprano con `return`

```kotlin
fun verificarEdad(edad: Int) {
    if (edad < 18) return
    println("Eres mayor de edad")
}
```

### Ejemplo completo

```kotlin
fun main() {
    fun saludar(nombre: String = "usuario"): String {
        return "Hola, $nombre"
    }

    val mensaje = saludar("Sebastián")
    println(mensaje)
}
```

## Buenas prácticas

- Usa nombres descriptivos  
- Evita funciones largas  
- Prefiere funciones puras (sin efectos secundarios)  
- Usa `val` y `fun` para inmutabilidad y claridad
