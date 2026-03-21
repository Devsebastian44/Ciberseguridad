Kotlin proporciona un conjunto robusto de estructuras de datos llamadas **colecciones**. Estas se dividen principalmente en tres tipos:

## `List`: Lista ordenada

Una `List` contiene elementos en un orden específico y puede tener duplicados.

### Inmutable (`listOf`)

```kotlin
val frutas = listOf("Manzana", "Banana", "Uva")
println(frutas[0])          // Manzana
println("Total: ${frutas.size}") // 3
```

### Mutable (`mutableListOf`)

```kotlin
val numeros = mutableListOf(1, 2, 3)
numeros.add(4)
numeros.remove(2)
println(numeros) // [1, 3, 4]
```

## `Set`: Conjunto sin duplicados

Un `Set` no permite elementos repetidos y no garantiza un orden específico.

### Inmutable (`listOf`)

```kotlin
val letras = setOf("A", "B", "C", "A")
println(letras) // [A, B, C]
```

### Mutable (`mutableSetOf`)

```kotlin
val set = mutableSetOf(1, 2, 3)
set.add(3) // No se agrega porque ya existe
set.add(4)
println(set) // [1, 2, 3, 4]
```

## `Map`: Pares clave - valor

Un `Map` guarda pares `clave - valor`, como un diccionario.

### Inmutable (`mapOf`)

```kotlin
val edades = mapOf("Sebastián" to 19, "Ana" to 21)
println(edades["Sebastián"]) // 19
```

### Mutable (`mutableMapOf`)

```kotlin
val personas = mutableMapOf("Juan" to 30)
personas["Lucía"] = 25
personas.remove("Juan")
println(personas) // {Lucía=25}
```

### Recorrer colecciones

Con `for`:

```kotlin
val frutas = listOf("Manzana", "Banana", "Uva")
for (fruta in frutas) {
    println(fruta)
}
```

Con `forEach`:

```kotlin
frutas.forEach { fruta ->
    println(fruta.uppercase())
}
```

## Métodos útiles

|Método|Tipo|Descripción|
|---|---|---|
|`.add()`|mutable|Agrega elemento|
|`.remove()`|mutable|Elimina elemento|
|`.contains(x)`|ambos|¿Contiene elemento?|
|`.isEmpty()`|ambos|¿Está vacía?|
|`.size`|ambos|Tamaño de la colección|
|`.keys` / `.values`|Map|Devuelve claves o valores|
