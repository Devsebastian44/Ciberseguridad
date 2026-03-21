Las estructuras de control permiten controlar el flujo de ejecución de un programa según condiciones o repeticiones.

## Condicionales

### `if`, `else if`, `else`

```kotlin
val edad = 18

if (edad >= 18) {
    println("Eres mayor de edad")
} 

else if (edad >= 13) {
    println("Eres adolescente")
} 

else {
    println("Eres menor")
}
```

## `when`: el `switch` mejorado

Más limpio y poderoso que `switch` de otros lenguajes.

```kotlin
val dia = 3

val nombreDia = when (dia) {
    1 -> "Lunes"
    2 -> "Martes"
    3 -> "Miércoles"
    4 -> "Jueves"
    5 -> "Viernes"
    6, 7 -> "Fin de semana"
    else -> "Día inválido"
}

println(nombreDia)
```

También puede evaluarse por rangos o condiciones:

```kotlin
val nota = 8

val resultado = when {
    nota >= 9 -> "Excelente"
    nota >= 7 -> "Bueno"
    nota >= 5 -> "Suficiente"
    else -> "Reprobado"
}
```

## Bucles

### `while`

Ejecuta mientras la condición sea verdadera.

```kotlin
var contador = 1

while (contador <= 5) {
    println("Número $contador")
    contador++
}
```

### `do...while`

Ejecuta al menos una vez, incluso si la condición es falsa.

```kotlin
var i = 1

do {
    println("Valor: $i")
    i++
} while (i <= 3)
```

### `for` con rangos, listas y pasos

En un rango:

```kotlin
for (i in 1..5) {
    println(i) // 1 2 3 4 5
}
```

Descendente:

```kotlin
for (i in 5 downTo 1) {
    println(i) // 5 4 3 2 1
}
```

Con paso personalizado:

```kotlin
for (i in 1..10 step 2) {
    println(i) // 1 3 5 7 9
}
```

Sobre una lista:

```kotlin
val frutas = listOf("Manzana", "Banana", "Uva")

for (fruta in frutas) {
    println(fruta)
}
```

## Control de flujo en bucles

### `break`

Sale del bucle inmediatamente.

```kotlin
for (i in 1..10) {
    if (i == 4) break
    println(i)
}
// 1 2 3
```

### `continue`

Salta a la siguiente iteración.

```kotlin
for (i in 1..5) {
    if (i == 3) continue
    println(i)
}
// 1 2 4 5
```

## Manejo de Excepciones

### `try`, `catch`, `finally`

Se usa para capturar y manejar errores en tiempo de ejecución.

```kotlin
try {
    val resultado = 10 / 0
    println("Resultado: $resultado")
} 

catch (e: ArithmeticException) {
    println("Error: división por cero")
} 

finally {
    println("Esto siempre se ejecuta")
}
```

Puedes lanzar errores personalizados con `throw`:

```kotlin
val edad = -1

if (edad < 0) {
    throw IllegalArgumentException("La edad no puede ser negativa")
}
```
