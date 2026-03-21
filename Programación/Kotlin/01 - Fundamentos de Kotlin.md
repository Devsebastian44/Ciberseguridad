El programa más básico en cualquier lenguaje es el famoso **Hola Mundo**. En Kotlin, este programa sirve para familiarizarnos con la estructura básica del lenguaje y cómo ejecutar código.

## Conceptos Clave

- Kotlin tiene una función principal llamada `main`, que es el punto de entrada de la aplicación.
- `println()` se usa para imprimir texto en la consola.
- `readLine()` permite capturar entrada del usuario desde la consola.

### Ejemplo:

```kotlin
fun main() {
    println("Hola, mundo!")
}
```

- `fun` es la palabra clave para definir una función.
- `main()` es la función principal. Kotlin no necesita parámetros obligatorios para esta función, pero puedes usarlos si lo deseas.
- `println()` imprime texto en la consola y hace un salto de línea al final.

### Ejemplo con entrada del usuario

```kotlin
fun main() {
    print("¿Cómo te llamas? ")
    val nombre = readLine()
    println("Hola, $nombre!")
}
```

- `readLine()` lee una línea desde la entrada estándar (teclado).
- La entrada siempre se interpreta como `String?` (puede ser `null`), por lo que si haces operaciones más complejas, es recomendable validarla o convertirla.

### Cómo Ejecutarlo

Si tienes el compilador de Kotlin instalado y agregado al `PATH`, guarda el archivo como `HolaMundo.kt` y ejecútalo con:

```bash
kotlinc HolaMundo.kt -include-runtime -d HolaMundo.jar
java -jar HolaMundo.jar
```

### Alternativa (Kotlin Script)

También puedes ejecutarlo directamente como script:

```bash
kotlinc -script HolaMundo.kts
```

En ese caso, usa extensión `.kts` y no necesitas `fun main()`, por ejemplo:

```kotlin
print("Ingresa tu nombre: ")
val nombre = readLine()
println("¡Hola, $nombre!")
```