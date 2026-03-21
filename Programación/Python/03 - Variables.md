## ¿Qué es una variable?

Una **variable** en Python es un nombre que se utiliza para almacenar un valor en memoria.  
Las variables son **dinámicas**, pueden contener distintos tipos de datos en cualquier momento.

### Tipos de datos comunes

|Tipo|Nombre en Python|Ejemplo|
|---|---|---|
|Cadenas de texto|`str`|`"Hola"`|
|Números enteros|`int`|`42`|
|Números decimales|`float`|`3.14`|
|Valores booleanos|`bool`|`True`, `False`|
|Listas|`list`|`[1, 2, 3]`|

---

## Sintaxis para definir una variable

```python
nombre = "María"
edad = 30
peso = 65.5
es_casado = False
```

### Explicación

- `nombre` → cadena (`str`)
- `edad` → entero (`int`)
- `peso` → decimal (`float`)
- `es_casado` → booleano (`bool`)

### Puntos importantes

- Booleanos: `True` y `False` con mayúscula inicial
- El operador `=` asigna valores
- Tipado dinámico: las variables pueden cambiar de tipo

---

## Reglas para nombres de variables

### Caracteres permitidos

- Letras (`A-Z`, `a-z`)
- Dígitos (`0-9`)
- Guiones bajos (`_`)

**Importante:**

- No pueden iniciar con número
- Deben comenzar con letra o guion bajo

### Palabras reservadas

No se pueden usar palabras clave como `if`, `for`, `class`, `return`.

```python
# Incorrecto
for = 5

# Correcto
contador = 5
```

### Sensibilidad a mayúsculas

```python
mi_nombre = "Marce"
Mi_Nombre = "Acosta"
```

Son variables distintas.

### Uso de Snake Case

Se recomienda usar **snake_case**:

```python
nombre_usuario = "Marce"
nombre_completo = "Marce Acosta"
```

### Nombres descriptivos

```python
# No recomendado
e = 28
n = "Carlos"

# Recomendado
edad = 28
nombre = "Carlos"
```

### Evitar nombres de un solo carácter

Prefiere nombres claros como `total_ventas` en lugar de `x`, `y`, `z`.

---

## Conceptos clave

|Concepto|Descripción|
|---|---|
|Variable|Nombre que almacena un valor|
|`=`|Operador de asignación|
|Tipado dinámico|Variables pueden cambiar de tipo|
|`True` / `False`|Valores booleanos|

---
