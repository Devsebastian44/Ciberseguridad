Las cadenas (o *Strings*) en Kotlin son objetos que representan texto. Hay dos formas principales de construir textos combinando variables y valores: **concatenación** e **interpolación**.

## Concatenación

Consiste en unir varias cadenas utilizando el operador `+`.

### Ejemplo:

```kotlin
fun main() {
    val nombre = "Sebastián"
    val saludo = "Hola, " + nombre + "!"
    println(saludo)
}
```

- Cada vez que se usa `+`, Kotlin crea una nueva cadena combinando los valores.
- Es útil para casos sencillos, pero puede volverse poco legible con muchas variables.

## Interpolación de Cadenas

Es una forma más limpia y moderna de insertar variables dentro de una cadena utilizando `$`.

```kotlin
fun main() {
    val nombre = "Sebastián"
    val edad = 19
    val mensaje = "Hola, mi nombre es $nombre y tengo $edad años."
    println(mensaje)
}
```

- `$variable`: inserta directamente el valor de la variable.
- `${expresión}`: permite insertar expresiones completas dentro de la cadena.

```kotlin
fun main() {
    val nombre = "Sebastián"
    val edad = 19
    val mensaje = "Hola, mi nombre es $nombre y tengo $edad años."
    println(mensaje)
}
```

- `$variable`: inserta directamente el valor de la variable.
- `${expresión}`: permite insertar expresiones completas dentro de la cadena.

```kotlin
fun main() {
    val a = 5
    val b = 3
    println("La suma de $a y $b es ${a + b}")
}
```

### Diferencias Clave

|Característica|Concatenación|Interpolación|
|---|---|---|
|Símbolo|`+`|`$variable` o `${expresión}`|
|Legibilidad|Menor|Mayor|
|Rendimiento|Similar, pero depende del uso||
|Recomendación|Usar interpolación cuando sea posible|

## Buenas Prácticas

- Prefiere interpolación por claridad y limpieza de código.
- Usa `${}` cuando quieras evaluar una expresión dentro del texto.
- Si necesitas unir muchas cadenas dinámicamente, considera usar `StringBuilder`.


# Comillas Simples, Dobles y Triples en Kotlin

En Kotlin, hay tres formas principales de trabajar con texto y caracteres, cada una con un tipo de comillas diferente:

## Comillas Simples: `'` - Para caracteres (`Char`)

Se usan para declarar **un solo carácter**.

### Ejemplo:

```kotlin
fun main() {
    val letra: Char = 'A'
    println("Letra: $letra")
}
```

- Solo aceptan **un carácter**.
- No se puede usar para palabras o frases.
- No puedes escribir `'AB'` ni `'Hola'`, eso lanza error.

## Comillas Dobles: `"` - Para cadenas (`String`)

Se usan para declarar **texto o frases completas**.

```kotlin
fun main() {
    val nombre: String = "Sebastián"
    val saludo = "Hola, $nombre!"
    println(saludo)
}
```

- Soportan **interpolación**: `$variable` o `${expresión}`.
- Se pueden concatenar con `+`.

## Comillas Triples: `""" """` - Para texto multilínea

Se usan para declarar **strings multilínea**, sin necesidad de caracteres especiales para saltos de línea (`\n`).

### Ejemplo:


```kotlin
fun main() {
    val textoLargo = """
        Este es un texto
        que ocupa varias líneas,
        y se ve tal como está escrito.
    """.trimIndent()

    println(textoLargo)
}
```

- Mantiene el formato exacto del texto escrito.
- Útil para mensajes grandes, SQL, JSON, logs, etc.
- Puedes usar `.trimIndent()` o `.trimMargin()` para alinear mejor el texto.

## Comparación Rápida

| Tipo de comillas | Tipo de dato | Uso principal                             |
| ---------------- | ------------ | ----------------------------------------- |
| `'A'`            | `Char`       | Un solo carácter                          |
| `"Hola"`         | `String`     | Texto en una sola línea                   |
| `"""Texto"""`    | `String`     | Texto multilínea o sin escapar caracteres |


# Métodos Útiles para Cadenas en Kotlin

Kotlin provee una gran variedad de métodos para trabajar con cadenas (`String`). Aquí te muestro los más comunes y útiles para desarrollo diario.

## Métodos Básicos

### `.length`

Devuelve la longitud de la cadena.

```kotlin
val texto = "Kotlin"
println("Longitud: ${texto.length}") // 6
```

### `.uppercase()` y `.lowercase()`

Convierte todo el texto a mayúsculas o minúsculas.

```kotlin
val nombre = "Sebastián"
println(nombre.uppercase()) // SEBASTIÁN
println(nombre.lowercase()) // sebastián
```

### `.trim()`, `.trimStart()`, `.trimEnd()`

Elimina espacios en blanco (u otros caracteres) al inicio, final o ambos.

```kotlin
val sucio = "   texto   "
println(sucio.trim())       // "texto"
println(sucio.trimStart())  // "texto   "
println(sucio.trimEnd())    // "   texto"
```

### `.contains()`

Verifica si una cadena contiene otra.

```kotlin
val frase = "Hola mundo"
println(frase.contains("mundo")) // true
```

### `.replace(old, new)`

Reemplaza una parte de la cadena por otra.

```kotlin
val original = "Hola Kotlin"
val nuevo = original.replace("Kotlin", "Mundo")
println(nuevo) // Hola Mundo
```

### `.substring()`

Extrae una subcadena.

```kotlin
val texto = "Programador"
println(texto.substring(0, 4)) // "Prog"
```

### `.indexOf()` y `.lastIndexOf()`

Devuelve la posición de un carácter o texto (o -1 si no existe).

```kotlin
val texto = "Hola Kotlin"
println(texto.indexOf("K"))     // 5
println(texto.lastIndexOf("o")) // 9
```

## Otras Funciones Útiles

|Método|Descripción|
|---|---|
|`isEmpty()`|Verifica si la cadena está vacía|
|`isNotEmpty()`|Verifica si **no** está vacía|
|`startsWith()`|¿Comienza con...?|
|`endsWith()`|¿Termina con...?|
|`split()`|Divide en partes por un separador|
|`toIntOrNull()`|Convierte a entero (devuelve `null` si falla)|
|`reversed()`|Devuelve la cadena invertida|

### Ejemplo con varios métodos:


```kotlin
fun main() {
    val frase = "  Kotlin es Genial!  "

    println("Original: '$frase'")
    println("Sin espacios: '${frase.trim()}'")
    println("En mayúsculas: ${frase.uppercase()}")
    println("Empieza con 'Kotlin': ${frase.trim().startsWith("Kotlin")}")
    println("Cadena invertida: ${frase.reversed()}")
    println("Longitud: ${frase.length}")
}
```
