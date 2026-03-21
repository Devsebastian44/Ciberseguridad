Kotlin es un lenguaje **estáticamente tipado**, lo que significa que el tipo de cada variable se determina en tiempo de compilación. Aunque permite inferencia de tipos, es importante conocer los tipos básicos y cómo convertir entre ellos.

### Tipos de Datos Primitivos

| Tipo      | Descripción                  | Ejemplo        |
|-----------|------------------------------|----------------|
| `Byte`    | 8 bits, enteros pequeños      | `val x: Byte = 1` |
| `Short`   | 16 bits                       | `val x: Short = 2` |
| `Int`     | 32 bits (por defecto entero) | `val x: Int = 10` |
| `Long`    | 64 bits                      | `val x: Long = 100L` |
| `Float`   | 32 bits con punto flotante   | `val x: Float = 3.14f` |
| `Double`  | 64 bits con punto flotante   | `val x: Double = 2.718` |
| `Char`    | Carácter Unicode             | `val x: Char = 'A'` |
| `Boolean` | Verdadero o falso            | `val x: Boolean = true` |
| `String`  | Cadena de texto              | `val x: String = "Hola"` |

### Ejemplo Básico

```kotlin
fun main() {
    val entero: Int = 42
    val decimal: Double = 3.14
    val letra: Char = 'K'
    val mensaje: String = "Kotlin"
    val logico: Boolean = true

    println("Entero: $entero")
    println("Decimal: $decimal")
    println("Letra: $letra")
    println("Mensaje: $mensaje")
    println("Lógico: $logico")
}
```

## Conversión de Tipos

En Kotlin **no hay conversión implícita entre tipos numéricos**, por lo tanto debes hacer conversiones explícitas con funciones como:

- `toInt()`
- `toDouble()`
- `toFloat()`
- `toLong()`
- `toString()`
- `toBoolean()`

### Ejemplo de Conversión

```kotlin
fun main() {
    val numeroComoString = "123"
    val numero: Int = numeroComoString.toInt()
    val decimal: Double = numero.toDouble()

    println("Número como String: $numeroComoString")
    println("Convertido a Int: $numero")
    println("Convertido a Double: $decimal")
}
```

### Conversión y Nulos

Cuando conviertes cadenas a números, asegúrate de que la cadena contenga un valor válido. Si no, el programa lanzará una excepción.

```kotlin
val entrada = readLine()
val numero = entrada?.toIntOrNull()  // Devuelve null si falla
if (numero != null) {
    println("Número ingresado: $numero")
} else {
    println("No ingresaste un número válido.")
}
```

### Buenas Prácticas

- Usa `toIntOrNull()`, `toDoubleOrNull()`, etc., para evitar errores en tiempo de ejecución.
- Evita conversiones innecesarias para mantener el rendimiento.
- Prefiere `val` para inmutabilidad a menos que necesites cambiar el valor.
