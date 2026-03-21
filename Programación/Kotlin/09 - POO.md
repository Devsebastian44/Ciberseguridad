Kotlin es un lenguaje orientado a objetos, lo que significa que puedes usar clases, objetos, herencia, interfaces, constructores, modificadores, etc.

## Elementos básicos de la POO

- **Clases**: plantillas para crear objetos.
- **Objetos**: instancias de clases.
- **Atributos o propiedades**: variables dentro de una clase.
- **Métodos**: funciones que pertenecen a una clase.
- **Constructores**: inicializan objetos.
- **Encapsulamiento, herencia, abstracción y polimorfismo**: pilares fundamentales.

## Clases y objetos

Una clase es una plantilla. Un objeto es una instancia de esa clase.

```kotlin
class Persona {
    var nombre: String = "Desconocido"
    var edad: Int = 0

    fun saludar() {
        println("Hola, soy $nombre y tengo $edad años")
    }
}

fun main() {
    val persona = Persona()
    persona.nombre = "Sebastián"
    persona.edad = 19
    persona.saludar()
}
```

## Constructores

Kotlin permite declarar el constructor primario directamente en la cabecera:

```kotlin
class Persona(val nombre: String, var edad: Int) {
    fun presentarse() {
        println("Soy $nombre y tengo $edad años")
    }
}
```

Crear una instancia:

```kotlin
val p = Persona("Sebastián", 19)
p.presentarse()
```

## Propiedades y métodos

- **Propiedades** = atributos o variables de una clase.
- **Métodos** = funciones dentro de una clase.

```kotlin
class Circulo(val radio: Double) {
    fun area(): Double = Math.PI * radio * radio
    fun perimetro(): Double = 2 * Math.PI * radio
}
```

## Herencia

Usamos `open` para que una clase pueda ser heredada:

```kotlin
open class Animal {
    fun respirar() = println("Respirando...")
    open fun sonido() = println("Haciendo un sonido")
}

class Perro : Animal() {
    override fun sonido() = println("Guau guau")
}
```

## `init` (bloque de inicialización)

Se ejecuta cuando se instancia un objeto:

```kotlin
class Usuario(val nombre: String) {
    init {
        println("Usuario $nombre creado")
    }
}
```

## `data class` (clases de datos)

Clases pensadas para contener datos. Kotlin genera automáticamente `toString`, `equals`, `hashCode`, y `copy`.

```kotlin
data class Usuario(val nombre: String, val email: String)

val user = Usuario("Sebastián", "seb@ejemplo.com")
println(user)
```

## Variables de instancia (propiedades)

```kotlin
class Persona {
    var nombre: String = "Sin nombre"
    var edad: Int = 0
}

val p = Persona()
p.nombre = "Sebastián"
p.saludar()
```

## Variables de instancia

Son las propiedades que pertenecen a cada objeto creado a partir de una clase.

```kotlin
class Auto {
    var color: String = "Rojo"
    var velocidad: Int = 0
}
```

## Constructores

### Constructor primario

```kotlin
class Usuario(val nombre: String, var edad: Int)

val user = Usuario("Ana", 20) // Llamada
```

### Constructor con lógica (`init` block)

```kotlin
class Animal(val nombre: String) {
    init {
        println("Animal creado: $nombre")
    }
}
```

### Constructor secundario

```kotlin
class Libro {
    var titulo: String

    constructor(titulo: String) {
        this.titulo = titulo
    }
}
```

### Getter y Setter personalizados

```kotlin
class Producto {
    var precio: Int = 0
        get() = field
        set(value) {
            field = if (value >= 0) value else 0
        }
}
```

### Encapsulamiento

Controlas el acceso a propiedades y métodos usando modificadores:

- `public` (por defecto)
- `private`
- `protected`
- `internal`

```kotlin
class CuentaBancaria {
    private var saldo: Double = 0.0

    fun depositar(cantidad: Double) {
        if (cantidad > 0) saldo += cantidad
    }

    fun mostrarSaldo() = println("Saldo actual: $saldo")
}
```

### Herencia

```kotlin
open class Animal(val nombre: String) {
    fun comer() = println("$nombre está comiendo")
}

class Perro(nombre: String) : Animal(nombre) {
    fun ladrar() = println("Guau!")
}
```

## Abstracción

### Clase abstracta

```kotlin
abstract class Figura {
    abstract fun area(): Double
}

class Circulo(val radio: Double) : Figura() {
    override fun area() = Math.PI * radio * radio
}
```

## Polimorfismo

Permite usar clases hijas a través de una referencia de la clase padre.

```kotlin
fun mostrarArea(figura: Figura) {
    println("Área: ${figura.area()}")
}

val c = Circulo(5.0)
mostrarArea(c) // Polimorfismo
```

## `companion object` (como `static`) y patrón `Factory`

```kotlin
class Config {
    companion object {
        const val VERSION = "1.0"
        fun saludar() = println("Hola desde companion")
    }
}

Config.saludar()
```

Patrón de diseño `Factory`

```kotlin
class Usuario private constructor(val nombre: String) {
    companion object Factory {
        fun crear(nombre: String): Usuario = Usuario(nombre)
    }
}

val u = Usuario.crear("Sebastián")
```

## `data class`

Clase para representar modelos de datos con funcionalidades automáticas (`equals`, `toString`, `copy`, etc.)

```kotlin
data class Cliente(val id: Int, val nombre: String)

val c1 = Cliente(1, "Mario")
val c2 = c1.copy(nombre = "Juan")
```

## `inner class`

Clases anidadas con acceso a la clase externa.

```kotlin
class Computadora(val marca: String) {
    inner class Procesador {
        fun info() = "Procesador de $marca"
    }
}
```

## `sealed class`

Usada para jerarquías de clases limitadas, especialmente útil en `when`.

```kotlin
sealed class Resultado
class Exito(val data: String) : Resultado()
class Error(val mensaje: String) : Resultado()

fun manejarResultado(r: Resultado) = when (r) {
    is Exito -> println("Éxito: ${r.data}")
    is Error -> println("Error: ${r.mensaje}")
}
```

## `enum class`

Enumeraciones de constantes.

```kotlin
enum class Dia {
    LUNES, MARTES, MIERCOLES, JUEVES, VIERNES
}

val dia = Dia.LUNES
println("Hoy es $dia")
```