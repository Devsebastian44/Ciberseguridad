# ¿Qué es Programación Reactiva?

La programación reactiva es un paradigma centrado en el manejo de flujos de datos asíncronos y en la reacción a los datos conforme están disponibles.

**Reactive Streams** es una especificación estándar para proporcionar un enfoque unificado para el manejo de flujos de datos asincrónicos con contrapresión.

## ¿Qué es Flow?

Un flujo es un tipo que puede emitir varios valores de manera secuencial, en lugar de suspender funciones que muestran solo un valor único.

## Flujo Frío vs Caliente

|Flujo Frío|Flujo Caliente|
|---|---|
|Emite datos solo cuando hay un recolector|Emite datos incluso cuando no hay recolectores|
|No almacena datos|Puede almacenar datos|
|No puede tener varios recolectores|Puede tener varios recolectores|

## Transmisiones de Datos

Hay tres entidades involucradas:

1. **Productor**: Produce datos que se agregan al flujo
2. **Intermediarios** (opcional): Modifican cada valor emitido en el flujo
3. **Consumidor**: Consume los valores del flujo

## Características de Flow

- **Asíncrono**: Diseñado para operaciones asíncronas
- **Integración perfecta**: Se integra con las corrutinas de Kotlin
- **Compatibilidad**: Puede componer múltiples operaciones de flujo
- **Cancelación**: Admite concurrencia estructurada
- **Manejo de errores**: Proporciona mecanismos integrados de manejo de errores

## Componentes Clave de Kotlin Flow

1. **Flow Builder**: Representa el flujo de datos
2. **Operator**: Funciones como `map`, `filter`, y `collect`
3. **Collector**: Recibe y procesa los valores emitidos


# Flow Builders

## Tipos de constructores:

1. **`flow{}`**: Forma más básica de crear un flujo
2. **`flowOf()`**: Crea un flujo a partir de un conjunto determinado de elementos
3. **`asFlow()`**: Función de extensión que convierte tipos en flujos
4. **`channelFlow{}`**: Crea un flujo usando el envío proporcionado por el constructor

## Operadores de Terminales

Los flujos son fríos y no producen valores hasta que se invoque un operador de terminal.

## Operadores principales:

- **`collect`**: Operador de terminal más básico
- **`first`**: Devuelve solo la primera emisión del flujo
- **`last`**: Devuelve solo la última emisión del flujo
- **`toList` y `toSet`**: Esperan hasta que se complete el flujo
- **`reduce`**: Acumula el valor comenzando con el primer elemento
- **`fold`**: Para realizar operaciones como sumar todos los valores emitidos

## Operadores Intermedios

Los operadores intermedios se aplican al flujo y devuelven un flujo descendente.

## Operadores principales:

- **`map`**: Transforma cada valor en otro valor
- **`filter`**: Selecciona valores que cumplen una condición
- **`take`**: Devuelve un flujo con los primeros elementos
- **`zip`**: Combina flujos
- **`dropWhile`**: Descarta elementos mientras se cumple una condición
- **`transform`**: Para transformaciones complejas
- **`withIndex`**: Añade índices a los elementos

## StateFlow y SharedFlow

**Hot Flow** no depende del colector. Comienza a emitir valores instantáneamente.

### SharedFlow

- Flujo caliente que puede tener múltiples colectores
- Emite valores independientemente de los colectores
- Útil para transmitir valores a varios recopiladores
- No tiene valor inicial
- Configurable caché de reproducción

### StateFlow

- Flujo caliente que representa un estado
- Contiene un solo valor a la vez
- Es un flujo combinado (conserva el valor más reciente)
- Útil para mantener una única fuente de verdad para un estado
- Siempre tiene un valor inicial
- Solo almacena el último valor emitido