# Programación Sincrónica

Ejecuta las tareas en un orden predeterminado, donde cada operación espera a que la anterior se complete antes de continuar.

## Características clave:

1. El código se ejecuta en orden secuencial
2. Cada instrucción espera a que la anterior termine antes de ejecutarse
3. Las tareas bloquean el hilo principal hasta su finalización
4. Los errores son más fáciles de rastrear y solucionar

```kotlin
fun tarea1Sincrona() {
    println("Obtener datos")
    Thread.sleep(10000)
}

fun tarea2Sincrona() {
    println("Calcular IVA")
}

tarea1Sincrona() // Se ejecuta y esperamos 10 segundos
tarea2Sincrona()
```

## Programación Asíncrona

Las tareas se ejecutan sin esperar a que finalicen las tareas anteriores.

### Características clave:

1. Las tareas se ejecutan sin esperar a que finalicen las tareas anteriores
2. Se pueden ejecutar varias tareas simultáneamente, mejorando la eficiencia
3. Ideal para gestionar tareas de larga duración (solicitudes de red)
4. Sin bloqueo para un mejor rendimiento
5. La ejecución no lineal dificulta el seguimiento de errores

## Enfoques de Programación Asíncrona en Kotlin

1. **Thread**
2. **Callbacks**
3. **Future y Promesas**
4. **Corrutinas**

### Thread

Cuando iniciamos cualquier programa Kotlin, inmediatamente comienza a ejecutarse un Thread, llamado Thread Principal.

```kotlin
val thread = Thread {
    Thread.sleep(10000)
    System.out.println("Obtuve datos")
}
thread.start()
```

### Callbacks

Los callbacks son funciones que se pasan como argumentos a otras funciones y se ejecutan después de que se completa la primera función.

**Problema**: Callback hell - cuando hay demasiadas callbacks anidadas, el código se vuelve difícil de leer y manejar excepciones.

### Multithreading vs Programación Asíncrona

**Multithreading - Tareas limitadas por la CPU:**

- Procesamiento de grandes conjuntos de datos
- Representación o transformación de imágenes
- Cálculos matemáticos complejos
- Operaciones en segundo plano

**Programación asíncrona - Tareas vinculadas a E/S:**

- Consultas de bases de datos
- Comunicación de red (solicitudes HTTP, llamadas API)
- E/S de archivo
- Operaciones basadas en retardos (temporizadores)

### Future y Promise

La idea detrás de los futuros o promesas es que cuando hacemos una llamada, se nos promete que en algún momento la llamada devolverá un objeto Promise. En Kotlin, se implementan mediante `CompletableFuture` en Java.