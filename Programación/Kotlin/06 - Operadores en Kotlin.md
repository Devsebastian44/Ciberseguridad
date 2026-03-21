Los **operadores** permiten realizar operaciones sobre variables y valores. Kotlin soporta una gran variedad agrupada por categorías:

## Operadores Aritméticos

Se utilizan para realizar operaciones matemáticas:

| Operador | Descripción         | Ejemplo        |
|----------|---------------------|----------------|
| `+`      | Suma                | `a + b`        |
| `-`      | Resta               | `a - b`        |
| `*`      | Multiplicación      | `a * b`        |
| `/`      | División             | `a / b`        |
| `%`      | Módulo (residuo)    | `a % b`        |

```kotlin
val a = 10
val b = 3
println(a + b) // 13
println(a % b) // 1
```

## Operadores de Asignación

Asignan o modifican valores:

|Operador|Equivalente a|Ejemplo|
|---|---|---|
|`=`|—|`x = 5`|
|`+=`|`x = x + y`|`x += 3`|
|`-=`|`x = x - y`|`x -= 2`|
|`*=`|`x = x * y`|`x *= 4`|
|`/=`|`x = x / y`|`x /= 2`|
|`%=`|`x = x % y`|`x %= 3`|

## Operadores Relacionales (Comparación)

Devuelven un valor booleano (`true` o `false`).

|Operador|Descripción|Ejemplo|
|---|---|---|
|`==`|Igual a|`a == b`|
|`!=`|Distinto de|`a != b`|
|`>`|Mayor que|`a > b`|
|`<`|Menor que|`a < b`|
|`>=`|Mayor o igual que|`a >= b`|
|`<=`|Menor o igual que|`a <= b`|

## Operadores Lógicos

Se usan con condiciones booleanas.

|Operador|Nombre|Uso|
|---|---|---|
|`&&`|AND|`cond1 && cond2`|
|`||`|
|`!`|NOT|`!condicion`|

```kotlin
val edad = 19
val esMayor = edad >= 18
val tieneID = true

if (esMayor && tieneID) {
    println("Puede entrar")
}
```

## Operadores de Incremento y Decremento

|Operador|Descripción|Uso|
|---|---|---|
|`++`|Incrementa en 1|`x++` o `++x`|
|`--`|Decrementa en 1|`x--` o `--x`|

```kotlin
var x = 5
println(x++) // 5
println(x)   // 6
```

## Operadores de Bits

Manipulan los bits directamente (avanzado).

|Operador|Descripción|
|---|---|
|`shl(bits)`|Desplazamiento a la izquierda|
|`shr(bits)`|Desplazamiento a la derecha|
|`and()`|AND bit a bit|
|`or()`|OR bit a bit|
|`xor()`|XOR bit a bit|
|`inv()`|Inversión de bits|

```kotlin
val binario = 4 // 0100
println(binario shl 1) // 8 (1000)
println(binario shr 1) // 2 (0010)
```

## Operadores de Rango

Sirven para iterar o verificar si un valor está dentro de un rango.

```kotlin
val numero = 5

if (numero in 1..10) {
    println("Está en el rango")
}

for (i in 1..5) {
    println(i) // 1 2 3 4 5
}
```

| Operador | Descripción              |
| -------- | ------------------------ |
| `in`     | Está en el rango         |
| `..`     | Crea un rango ascendente |
| `downTo` | Rango descendente        |
| `step`   | Incremento personalizado |

### `?` (Safe Call Operator)

Evita una excepción si el valor es `null`.

```kotlin
val nombre: String? = null
println(nombre?.length) // null, en vez de lanzar excepción
```

### `!!` (Not-null Assertion Operator)

Lanza una excepción si el valor es `null`.

```kotlin
val nombre: String? = null
println(nombre!!.length) // NullPointerException
```

### `?:` (Elvis Operator)

Devuelve un valor por defecto si es `null`.

```kotlin
val nombre: String? = null
val longitud = nombre?.length ?: 0
println(longitud) // 0
```

### `let` + Safe Call

Ejecuta un bloque solo si el valor no es `null`.

```kotlin
val nombre: String? = "Sebastián"
nombre?.let {
    println("Hola, $it") // Hola, Sebastián
}
```


# Precedencia de Operadores en Kotlin

La **precedencia** determina el orden en que se evalúan los operadores cuando hay múltiples en una misma expresión. También influye la **asociatividad** (de izquierda a derecha o viceversa).

## Tabla de Precedencia (de mayor a menor)

| Nivel | Operadores                                  | Descripción                       | Asociatividad       |           |                     |
| ----- | ------------------------------------------- | --------------------------------- | ------------------- | --------- | ------------------- |
| 1     | `()`                                        | Paréntesis                        | -                   |           |                     |
| 2     | `++`, `--`, `+` (unario), `-` (unario), `!` | Unarios / lógica negada           | Derecha a izquierda |           |                     |
| 3     | `*`, `/`, `%`                               | Aritmética (multiplicación, etc.) | Izquierda a derecha |           |                     |
| 4     | `+`, `-`                                    | Aritmética (suma y resta)         | Izquierda a derecha |           |                     |
| 5     | `..`, `in`, `!in`                           | Rangos e inclusión                | Izquierda a derecha |           |                     |
| 6     | `<`, `>`, `<=`, `>=`                        | Comparación                       | Izquierda a derecha |           |                     |
| 7     | `==`, `!=`                                  | Igualdad                          | Izquierda a derecha |           |                     |
| 8     | `&&`                                        | Lógico AND                        | Izquierda a derecha |           |                     |
| 9     | `                                           |                                   | `                   | Lógico OR | Izquierda a derecha |
| 10    | `?:`                                        | Elvis (null safety)               | Derecha a izquierda |           |                     |
| 11    | `=` , `+=`, `-=`, `*=`, `/=`, `%=`          | Asignación                        | Derecha a izquierda |           |                     |
| 12    | `as`, `as?`, `is`, `!is`                    | Conversión y comprobación de tipo | Izquierda a derecha |           |                     |

## Ejemplo práctico

```kotlin
val resultado = 10 + 2 * 5
println(resultado) // 20, no 60
// Porque: 2 * 5 = 10 → luego: 10 + 10 = 20
```

## Ejemplo con paréntesis

```kotlin
val resultado = (10 + 2) * 5
println(resultado) // 60
// Se fuerza el orden usando paréntesis
```

### Asignación y encadenamiento

```kotlin
var x: Int
var y: Int
x = y = 5 // ❌ Error en Kotlin
// Kotlin no permite múltiples asignaciones encadenadas
```
