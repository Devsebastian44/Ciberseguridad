## Manejo de índices en cadenas

Las cadenas son secuencias de caracteres, cada uno con un índice que inicia en `0`.

### Ejemplo

```
Cadena: "Hola mundo"
H o l a   m u n d o
0 1 2 3 4 5 6 7 8 9
```

```python
cadena = 'Hola mundo'
print(cadena[0])  # H
print(cadena[9])  # o
```

---

## Inmutabilidad de cadenas

Las cadenas no pueden modificarse directamente, pero se pueden crear nuevas.

```python
cadena = 'Hola mundo'
nuevo = cadena.replace('Hola', 'Adios')
print(nuevo)  # Adios mundo
```

---

## Caracteres especiales

Se usan secuencias de escape:

|Secuencia|Descripción|Ejemplo|Resultado|
|---|---|---|---|
|`\n`|Salto de línea|`'Hola\nMundo'`|Hola<br>Mundo|
|`\t`|Tabulador|`'\tTexto'`|Texto|
|`\'`|Comilla simple|`'Juan\' Pérez'`|Juan' Pérez|
|`\"`|Comilla doble|`"Carla \"Gómez\""`|Carla "Gómez"|
|`\\`|Barra invertida|`'Ruta: C:\\user'`|Ruta: C:\user|

---

## Concatenación de cadenas

```python
a = 'Hola'
b = 'Mundo'
print(a + b)          # HolaMundo
print(a + ' ' + b)    # Hola Mundo
print(''.join([a, ' ', b])) # Hola Mundo
```

---

## Formateo de cadenas

### f-strings

```python
nombre = 'Juan'
edad = 30
print(f'Hola, me llamo {nombre} y tengo {edad} años')
```

### format()

```python
print('Hola, me llamo {} y tengo {} años'.format(nombre, edad))
```

---

## Métodos de cadenas

```python
cadena = ' Hola Mundo '
print(cadena.upper())   # HOLA MUNDO
print(cadena.lower())   # hola mundo
print(cadena.strip())   # Hola Mundo
```

|Método|Descripción|
|---|---|
|`upper()`|Convierte a mayúsculas|
|`lower()`|Convierte a minúsculas|
|`strip()`|Elimina espacios al inicio y final|

---

## Largo de una cadena

```python
cadena = 'Hola, Mundo!'
print(len(cadena))  # 12
```

---

## Subcadenas con slicing

```python
cadena = 'Hola, Mundo!'
print(cadena[0:4])   # Hola
print(cadena[6:11])  # Mundo
```

---

## Buscar subcadenas

```python
cadena = 'Hola, Mundo!'
print(cadena.find('Mundo'))  # 6
print(cadena.find('Hola'))   # 0
```

---

## Reemplazo de subcadenas

```python
cadena = 'Hola, mundo!'
print(cadena.replace('mundo', 'a todos'))  # Hola, a todos!
print(cadena.replace('Hola', 'Adios'))     # Adios, mundo!
```

---

## Multiplicación de cadenas

```python
texto = 'Hola '
print(texto * 3)  # Hola Hola Hola
```

---