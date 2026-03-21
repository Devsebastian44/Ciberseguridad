## ¿Qué son los operadores en Python?

Son símbolos especiales que realizan tareas sobre valores o variables para producir un resultado.

```python
resultado = 5 + 3  # 8
```

---

## Operadores aritméticos

|Operador|Nombre|Ejemplo|Resultado|
|---|---|---|---|
|`+`|Suma|`5 + 3`|8|
|`-`|Resta|`10 - 4`|6|
|`*`|Multiplicación|`6 * 7`|42|
|`/`|División|`15 / 4`|3.75|
|`//`|División entera|`15 // 4`|3|
|`%`|Módulo|`15 % 4`|3|
|`**`|Exponenciación|`2 ** 3`|8|

---

## Operadores de asignación

|Operador|Equivalente|Ejemplo|
|---|---|---|
|`=`|Asignación simple|`x = 5`|
|`+=`|`x = x + y`|`x += 3`|
|`-=`|`x = x - y`|`x -= 2`|
|`*=`|`x = x * y`|`x *= 4`|
|`/=`|`x = x / y`|`x /= 2`|
|`//=`|`x = x // y`|`x //= 3`|
|`%=`|`x = x % y`|`x %= 5`|
|`**=`|`x = x ** y`|`x **= 2`|

---

## Operadores de comparación

|Operador|Nombre|Ejemplo|Resultado|
|---|---|---|---|
|`==`|Igual|`5 == 5`|True|
|`!=`|Diferente|`5 != 3`|True|
|`>`|Mayor|`7 > 3`|True|
|`<`|Menor|`3 < 7`|True|
|`>=`|Mayor o igual|`5 >= 5`|True|
|`<=`|Menor o igual|`3 <= 7`|True|

---

## Operadores lógicos

|Operador|Nombre|Ejemplo|Resultado|
|---|---|---|---|
|`and`|Y lógico|`True and False`|False|
|`or`|O lógico|`True or False`|True|
|`not`|Negación|`not True`|False|

**Ejemplo:**

```python
edad = 25
licencia = True
print(edad >= 18 and licencia)  # True
```

---

## Operadores de identidad

|Operador|Descripción|Ejemplo|
|---|---|---|
|`is`|Mismo objeto en memoria|`a is b`|
|`is not`|Objetos distintos|`a is not b`|

**Ejemplo:**

```python
x = [1,2,3]
y = [1,2,3]
print(x == y)   # True (mismo contenido)
print(x is y)   # False (objetos distintos)
```

---

## Operadores de membresía

|Operador|Descripción|Ejemplo|Resultado|
|---|---|---|---|
|`in`|Elemento presente|`'a' in 'casa'`|True|
|`not in`|Elemento ausente|`'z' not in 'casa'`|True|

**Ejemplo:**

```python
frutas = ['manzana', 'banana']
print('manzana' in frutas)  # True
print('uva' not in frutas)  # True
```

---
