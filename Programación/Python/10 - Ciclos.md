## Ciclos en Python

Los ciclos permiten ejecutar un bloque de código repetidamente mientras se cumpla una condición o para cada elemento de una secuencia.

---

## Ciclo `for`

Itera sobre una secuencia (lista, tupla, cadena, rango, etc.).

### Sintaxis

```python
for variable in secuencia:
    instrucciones
```

### Ejemplo

```python
for i in range(5):
    print(i)  # 0,1,2,3,4
```

```python
frutas = ['manzana', 'banana', 'naranja']
for fruta in frutas:
    print(fruta)
```

---

## Función `range()`

Genera una secuencia de números.

### Sintaxis

```python
range(inicio, fin, paso)
```

### Ejemplos

```python
for i in range(2, 7): 
    print(i)  # 2..6

for i in range(0, 10, 2): 
    print(i)  # 0,2,4,6,8
```

---

## Ciclo `while`

Ejecuta un bloque mientras la condición sea verdadera.

### Sintaxis

```python
while condición:
    instrucciones
```

### Ejemplo

```python
contador = 0
while contador < 5:
    print(contador)
    contador += 1
```

---

## Sentencia `break`

Finaliza el ciclo inmediatamente.

```python
for i in range(10):
    if i == 5:
        break
    print(i)  # 0..4
```

---

## Sentencia `continue`

Salta a la siguiente iteración.

```python
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)  # 1,3,5,7,9
```

---

## Ciclos anidados

Un ciclo dentro de otro.

```python
for i in range(3):
    for j in range(3):
        print(f"i={i}, j={j}")
```

---

## Sentencia `else` en ciclos

El bloque `else` se ejecuta si el ciclo termina normalmente (sin `break`).

```python
for i in range(5):
    print(i)
else:
    print("Ciclo completado")
```

---
