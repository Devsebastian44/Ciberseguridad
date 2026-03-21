En Kotlin, podemos declarar **variables mutables** (que pueden cambiar su valor) y **constantes** o **variables inmutables** (cuyo valor no puede cambiar una vez asignado).

## Conceptos Clave

- `var`: declara una **variable mutable**.
- `val`: declara una **constante** o **variable inmutable**.
- Kotlin es un lenguaje **estáticamente tipado**, pero permite **inferencia de tipos**.

### Ejemplo:

```kotlin
fun main() {
    var nombre = "Sebastián"
    val edad = 19

    println("Nombre: $nombre")
    println("Edad: $edad")

    nombre = "Devsebastian44"
    // edad = 20  // Error: no se puede reasignar una val

    println("Nuevo nombre: $nombre")
}
```

- `var nombre = "Sebastián"`: la variable `nombre` puede cambiar.
- `val edad = 19`: la variable `edad` **no se puede modificar** después de su asignación inicial.
- `$variable`: se usa para interpolar el valor dentro de un `println`.

### Buenas Prácticas

- Usa `val` siempre que no necesites cambiar el valor.
- Solo usa `var` si sabes que el valor va a modificarse.
- Esto ayuda a escribir código **más seguro e inmutable**.

### Tipos de Datos Básicos

| Tipo      | Ejemplo         |
| --------- | --------------- |
| `Int`     | 1, 42, -7       |
| `Double`  | 3.14, -0.1      |
| `Boolean` | `true`, `false` |
| `String`  | "Hola", "123"   |
| `Char`    | 'A', 'z'        |
