## Operadores Aritméticos

```bash
#!/bin/bash

a=10
b=3

# Operaciones básicas
echo "Suma: $((a + b))"
echo "Resta: $((a - b))"
echo "Multiplicación: $((a * b))"
echo "División: $((a / b))"
echo "Módulo: $((a % b))"
echo "Potencia: $((a ** 2))"

# Incremento y decremento
((a++))
echo "a después de incremento: $a"
((b--))
echo "b después de decremento: $b"
````

---

## Operadores de Comparación

### Comparaciones Numéricas

```bash
#!/bin/bash

a=10
b=20

if [ $a -eq $b ]; then echo "a es igual a b"; fi
if [ $a -ne $b ]; then echo "a no es igual a b"; fi
if [ $a -lt $b ]; then echo "a es menor que b"; fi
if [ $a -le $b ]; then echo "a es menor o igual que b"; fi
if [ $a -gt $b ]; then echo "a es mayor que b"; fi
if [ $a -ge $b ]; then echo "a es mayor o igual que b"; fi
```

### Operadores Disponibles

- **`-eq`**: igual a (equal)
- **`-ne`**: no igual a (not equal)
- **`-lt`**: menor que (less than)
- **`-le`**: menor o igual que (less or equal)
- **`-gt`**: mayor que (greater than)
- **`-ge`**: mayor o igual que (greater or equal)

---

## Operadores de Cadenas

```bash
#!/bin/bash

cadena1="Hola"
cadena2="Mundo"
cadena3=""

# Comparaciones de cadenas
if [ "$cadena1" = "$cadena2" ]; then echo "Cadenas iguales"; fi
if [ "$cadena1" != "$cadena2" ]; then echo "Cadenas diferentes"; fi
if [ -z "$cadena3" ]; then echo "Cadena vacía"; fi
if [ -n "$cadena1" ]; then echo "Cadena no vacía"; fi

# Longitud de cadena
echo "Longitud de '$cadena1': ${#cadena1}"

# Concatenación
resultado="${cadena1} ${cadena2}"
echo "Concatenación: $resultado"
```

---

## Operadores de Archivos

```bash
#!/bin/bash

archivo="test.txt"

# Verificaciones de archivos
if [ -e "$archivo" ]; then echo "El archivo existe"; fi
if [ -f "$archivo" ]; then echo "Es un archivo regular"; fi
if [ -d "$archivo" ]; then echo "Es un directorio"; fi
if [ -r "$archivo" ]; then echo "Es legible"; fi
if [ -w "$archivo" ]; then echo "Es escribible"; fi
if [ -x "$archivo" ]; then echo "Es ejecutable"; fi
if [ -s "$archivo" ]; then echo "El archivo no está vacío"; fi
```

### Operadores Disponibles

- **`-e`**: existe
- **`-f`**: es un archivo regular
- **`-d`**: es un directorio
- **`-r`**: es legible
- **`-w`**: es escribible
- **`-x`**: es ejecutable
- **`-s`**: no está vacío

---

## Operadores Lógicos

```bash
#!/bin/bash

a=5
b=10

# AND lógico
if [ $a -lt 10 ] && [ $b -gt 5 ]; then
    echo "Ambas condiciones son verdaderas"
fi

# OR lógico
if [ $a -eq 5 ] || [ $b -eq 5 ]; then
    echo "Al menos una condición es verdadera"
fi

# NOT lógico
if ! [ $a -eq $b ]; then
    echo "a no es igual a b"
fi
```

### Operadores Disponibles

- **`&&`**: AND lógico (ambas condiciones verdaderas)
- **`||`**: OR lógico (al menos una condición verdadera)
- **`!`**: NOT lógico (negación)