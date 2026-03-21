## Variables y la memoria RAM

Cuando se declara una variable, Python guarda su valor en una celda de la **memoria RAM**.

### Ejemplo

```python
edad = 30
```

La variable `edad` apunta a un objeto que contiene el valor `30`.

### Cambio de valor

```python
edad = 32
```

Se crea un nuevo objeto con valor `32` y la variable apunta a él.

---

## Dirección de Memoria

Cada variable en Python apunta a un **objeto** en memoria.

### Ejemplo

```python
edad = 30
```

```
edad ──────> [Objeto int: 30]
(Stack)      (Heap)
```

---

## Tipos de memoria

Python utiliza dos áreas principales:

|Área|Nombre|Qué almacena|
|---|---|---|
|**Stack**|Pila|Referencias de variables|
|**Heap**|Montón|Objetos con valores reales|

---

## Creación de distintos objetos

```python
altura = 1.75
```

La variable `altura` apunta a un objeto `float` en el **heap**.

---

## Modificación de valores

```python
edad = 32
```

- Se crea un nuevo objeto con valor `32`.
- El objeto anterior (`30`) queda sin referencia y puede ser eliminado por el **garbage collector**.

---

## Garbage Collector

El **GC** elimina automáticamente objetos sin referencias para optimizar memoria.

### Funciones principales

1. Detecta objetos sin referencias
2. Los marca para eliminación
3. Libera memoria automáticamente

---

## Conceptos clave

|Concepto|Descripción|
|---|---|
|**Stack**|Referencias a variables|
|**Heap**|Objetos con valores|
|**Referencia**|Dirección que conecta variable con objeto|
|**Objeto huérfano**|Objeto sin referencias|
|**Garbage Collector**|Libera memoria automáticamente|
|**Dirección hexadecimal**|Identificador único del objeto|

---

## Para recordar

- En Python, **todo es un objeto**.
- Las variables contienen **referencias**, no valores directos.
- Para simplificar, se puede pensar que “la variable almacena el valor”, aunque en realidad apunta al objeto.

---