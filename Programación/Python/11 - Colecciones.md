## Colecciones en Python

Son estructuras de datos que permiten almacenar múltiples elementos en una sola variable.  
Tipos principales: **listas, tuplas, conjuntos y diccionarios**.

---

## Listas (`list`)

Colecciones ordenadas y mutables que permiten duplicados.

### Sintaxis

```python
lista = [1, 2, 3]
```

### Ejemplos

```python
frutas = ['manzana', 'banana', 'naranja']
print(frutas[0])   # manzana
frutas[1] = 'uva'  # modificar
```

### Métodos comunes

```python
frutas.append('pera')     # agregar
frutas.remove('banana')   # eliminar
len(frutas)               # longitud
numeros.sort()            # ordenar
numeros.reverse()         # invertir
```

### Slicing

```python
numeros = [0,1,2,3,4,5,6,7,8,9]
print(numeros[2:5])   # [2,3,4]
print(numeros[::-1])  # lista invertida
```

---

## Tuplas (`tuple`)

Colecciones ordenadas e inmutables que permiten duplicados.

### Sintaxis

```python
tupla = (1, 2, 3)
```

### Ejemplos

```python
frutas = ('manzana', 'banana', 'naranja')
print(frutas[0])   # manzana
print(len(frutas)) # longitud
```

### Métodos útiles

```python
numeros = (1,2,3,1,1)
print(numeros.count(1))   # 3
print(frutas.index('banana')) # 1
```

---

## Conjuntos (`set`)

Colecciones desordenadas y mutables que no permiten duplicados.

### Sintaxis

```python
conjunto = {1, 2, 3}
```

### Operaciones

```python
a = {1,2,3,4}
b = {3,4,5,6}

print(a | b)  # unión
print(a & b)  # intersección
print(a - b)  # diferencia
print(a ^ b)  # diferencia simétrica
```

---

## Diccionarios (`dict`)

Colecciones desordenadas y mutables que almacenan pares clave-valor.

### Sintaxis

```python
diccionario = {'nombre': 'Juan', 'edad': 30}
```

### Ejemplos

```python
persona = {'nombre': 'Juan', 'edad': 30}
print(persona['nombre'])       # acceso
persona['edad'] = 31           # modificar
persona['ciudad'] = 'Madrid'   # agregar
```

### Métodos comunes

```python
persona.keys()     # claves
persona.values()   # valores
persona.items()    # pares clave-valor
persona.pop('edad')# eliminar
```

---

## Comparación de colecciones

|Característica|Lista|Tupla|Conjunto|Diccionario|
|---|---|---|---|---|
|Sintaxis|`[]`|`()`|`{}`|`{k:v}`|
|Ordenada|✅|✅|❌|✅ (desde 3.7)|
|Mutable|✅|❌|✅|✅|
|Duplicados|✅|✅|❌|❌ (claves)|
|Indexable|✅|✅|❌|✅ (por clave)|

---

## Elegir la colección adecuada

- **Lista** → secuencia ordenada y modificable
- **Tupla** → datos constantes e inmutables
- **Set** → elementos únicos, operaciones matemáticas
- **Diccionario** → pares clave-valor, búsqueda rápida

---