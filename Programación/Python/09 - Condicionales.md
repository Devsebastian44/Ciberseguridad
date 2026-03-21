## Condicionales en Python

Los condicionales permiten ejecutar diferentes bloques de código según se cumplan o no ciertas condiciones.

---

## Estructura `if`

Ejecuta un bloque de código solo si la condición es verdadera.

### Sintaxis

```python
if condición:
    instrucciones
```

### Ejemplo

```python
edad = 18
if edad >= 18:
    print("Eres mayor de edad")
```

---

## Estructura `if-else`

Permite ejecutar un bloque si la condición es verdadera y otro si es falsa.

### Sintaxis

```python
if condición:
    instrucciones_si_verdadero
else:
    instrucciones_si_falso
```

### Ejemplo

```python
numero = 7
if numero % 2 == 0:
    print("El número es par")
else:
    print("El número es impar")
```

---

## Estructura `if-elif-else`

Evalúa múltiples condiciones en secuencia. Se ejecuta el bloque de la primera condición verdadera.

### Sintaxis

```python
if condición1:
    instrucciones1
elif condición2:
    instrucciones2
else:
    instrucciones_por_defecto
```

### Ejemplo

```python
calificacion = 85

if calificacion >= 90:
    print("Calificación: A")
elif calificacion >= 80:
    print("Calificación: B")
elif calificacion >= 70:
    print("Calificación: C")
elif calificacion >= 60:
    print("Calificación: D")
else:
    print("Calificación: F")
```

---