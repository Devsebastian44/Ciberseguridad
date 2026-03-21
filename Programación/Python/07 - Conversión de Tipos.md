## Conversión de tipos en Python

La conversión de tipos (casting) transforma un dato de un tipo a otro.

---

## De cadena a entero

```python
numero = int('10')
```

Convierte `'10'` en `10`.

---

## De cadena a flotante

```python
decimal = float('3.14')
```

Convierte `'3.14'` en `3.14`.

---

## De número a cadena

```python
texto = str(2025)
```

Convierte `2025` en `'2025'`.

---

## A valor booleano

```python
print(bool(0))     # False
print(bool(5))     # True
print(bool(''))    # False
print(bool('abc')) # True
print(bool([]))    # False
print(bool(None))  # False
```

---

## Tabla resumen

|Función|Desde|Hacia|Ejemplo|
|---|---|---|---|
|`int()`|str|int|`int('10') → 10`|
|`float()`|str|float|`float('3.14') → 3.14`|
|`str()`|int/float|str|`str(2025) → '2025'`|
|`bool()`|varios|bool|`bool(1) → True`|

---

## Reglas de conversión a booleano

|Valor|Resultado|
|---|---|
|`0`|False|
|Número distinto de 0|True|
|`''` (cadena vacía)|False|
|Cadena con contenido|True|
|`[]` (lista vacía)|False|
|`None`|False|

---

## Entrada de datos por consola

La función `input()` solicita información al usuario.

### Ejemplo

```python
nombre = input('Introduce tu nombre: ')
edad = int(input('Introduce tu edad: '))
print(f'Tu edad es: {edad}')
print(f'En un año tendrás: {edad + 1}')
```

---

## Conceptos clave

|Aspecto|Descripción|
|---|---|
|`input()`|Solicita datos al usuario|
|Retorno|Siempre devuelve `str`|
|Conversión|Usar `int()`, `float()`, etc.|
|Pausa|El programa espera hasta Enter|
|Interactividad|Permite programas dinámicos|

---
