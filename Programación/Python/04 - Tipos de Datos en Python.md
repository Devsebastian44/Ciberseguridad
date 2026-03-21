## Tipado dinámico

En Python no necesitas indicar explícitamente el tipo de dato: se detecta automáticamente.

### Ejemplo

```python
edad = 42       # int
pi = 3.1416     # float
mensaje = 'Hola' # str
```

**Ventajas:** código más limpio, flexible y rápido de escribir.

---

## Tipo `int` – Enteros

Representa números enteros sin parte decimal.

```python
numero1 = 42
numero2 = -109
```

**Características:** positivos/negativos, sin límite práctico más allá de la memoria.

---

## Tipo `float` – Decimales

Representa números reales con parte decimal.

```python
pi = 3.1416
altura = 1.75
```

**Importante:** se usa el punto `.` como separador decimal, no la coma.

---

## Tipo `str` – Cadenas de texto

Secuencias de caracteres entre comillas simples o dobles.

```python
saludo = "Hola mundo"
nombre = 'Juan'
```

**Uso recomendado:**

- Comillas dobles si el texto contiene comillas simples.
- Comillas simples si contiene comillas dobles.

---

## Tipo `bool` – Booleanos

Valores lógicos: `True` o `False` (con mayúscula inicial).

```python
activo = True
es_menor = False
```

**Resultado de comparaciones:**

```python
edad = 18
es_adulto = edad >= 18  # True
```

---

## Tipo `None` – Ausencia de valor

Indica que una variable no tiene valor asignado.

```python
resultado = None
```

**Características:** diferente de `0`, `False` o `""`. Útil para inicializar variables o indicar ausencia de retorno.

---

## Resumen de tipos básicos

|Tipo|Descripción|Ejemplo|
|---|---|---|
|`int`|Entero|`42`, `-10`|
|`float`|Decimal|`3.14`, `-0.5`|
|`str`|Texto|`"Hola"`|
|`bool`|Verdadero/Falso|`True`, `False`|
|`None`|Ausencia de valor|`None`|

---

## Verificar tipo de una variable

```python
print(type(42))       # <class 'int'>
print(type(3.14))     # <class 'float'>
print(type("Ana"))    # <class 'str'>
print(type(True))     # <class 'bool'>
print(type(None))     # <class 'NoneType'>
```

---
