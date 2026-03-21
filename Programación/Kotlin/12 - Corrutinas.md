# ¿Qué es Concurrencia?

La concurrencia es una propiedad de los sistemas que permite que varias tareas o procesos se ejecuten simultáneamente, de forma independiente y compartiendo los mismos recursos del sistema.

## Modelos de Concurrencia:

1. **1 Thread - Modelo síncrono**
2. **Multi-threaded - Modelo síncrono**
3. **1 Thread - Modelo asíncrono**
4. **Multi-threaded - Modelo asíncrono**

## Concurrencia y Código No Bloqueante

El código no bloqueante ofrece un rendimiento mucho mayor. El código bloqueante desperdicia alrededor del 90% de los ciclos de CPU esperando a que la red o el disco obtengan los datos.

## Concurrencia Estructurada

La concurrencia estructurada garantiza que todas las corrutinas se inicien, completen o cancelen de forma ordenada.

## Ventajas principales:

- Los hijos heredan el contexto de sus padres (pero también pueden sobrescribirlo)
- Un padre suspende hasta que todos los hijos hayan terminado
- Cuando se cancela el padre, sus corrutinas hijas también se cancelan
- Cuando un hijo genera un error, también destruye al padre

## ¿Qué son las Corrutinas?

Las corrutinas ayudan a administrar tareas de larga duración que, de lo contrario, podrían bloquear el subproceso principal.

**Corrutinas = Co + Rutinas**

- Co = cooperación
- Rutinas = funciones

### Beneficios de las Corrutinas

- **Simplicidad**: El código se lee como código secuencial, reduciendo la complejidad
- **Rendimiento**: Las corrutinas son livianas y no bloquean los subprocesos
- **Integración**: Bien integrado con Android y otras bibliotecas Kotlin

## Scope (Alcance)

Un scope de corrutina es un espacio donde se colocan corrutinas. Se utilizan para definir el ciclo de vida de las coroutinas y administrar su ejecución.

### Tipos de Coroutine Scope:

1. **RunBlocking**: Para pruebas unitarias e inicialización de la aplicación
2. **GlobalScope**: Ámbito global predefinido que dura mientras la aplicación esté en ejecución
3. **CoroutineScope**: Vinculado a componentes específicos (actividad, fragmento, modelo de vista)
4. **ViewModelScope**: Para clases ViewModel de Android
5. **LifecycleScope**: Para componentes de Android como Activity y Fragment

## Coroutine Context (Contexto)

El contexto contiene los datos necesarios para la corrutina. Es un conjunto indexado de elementos donde cada elemento tiene una clave única.

### Componentes del contexto:

- **Dispatcher**: Ayuda a las corrutinas a decidir el hilo de ejecución
- **Name**: Proporciona un nombre para la corrutina (útil para depuración)
- **ExceptionHandler**: Para manejar excepciones no detectadas
- **Job**: Representa el ciclo de vida de una corrutina


# Iniciar una Corrutina

## `launch` vs `async`:

- **`launch`**: Dispara y olvida - devuelve un `Job`
- **`async`**: Realiza una tarea y devuelve un resultado - devuelve una instancia de `Deferred<T>`

## Funciones Suspend

Las funciones de suspensión son funciones que pueden suspender una corrutina. Deben ser llamadas en una corrutina o por otras funciones de suspensión.

## `withContext`

Es una función de suspensión que permite cambiar el contexto de una corrutina.

## `join()`

Esta función se utiliza para esperar a que se completen varias corrutinas que se ejecutan simultáneamente.

## Cancelar una Corrutina

Cancelar una corrutina puede ser útil para:

- Interrumpir operaciones de larga duración innecesarias
- Liberar recursos del sistema
- Detener corrutinas que no responden

## Channels (Canales)

Los canales proporcionan un mecanismo de comunicación entre corrutinas con suspensión:

- **send**: Se suspende si ningún consumidor está listo
- **receive**: Se suspende hasta que haya nuevos datos disponibles

## Tipos de canales:

1. **Rendezvous (default)**: Capacidad 0, sin búfer
2. **Unlimited**: Capacidad ilimitada, `send` nunca se suspende
3. **Buffered**: Capacidad positiva pero limitada
4. **Conflated**: Búfer de tamaño 1, cada nuevo elemento reemplaza al anterior