## Bucle `for`

```bash
#!/bin/bash

# Bucle for con rango
echo "Contando del 1 al 5:"
for i in {1..5}; do
    echo "Número: $i"
done

# Bucle for con lista
echo "Frutas:"
for fruta in manzana banana naranja; do
    echo "- $fruta"
done

# Bucle for con archivos
echo "Archivos .txt en el directorio:"
for archivo in *.txt; do
    if [ -f "$archivo" ]; then
        echo "- $archivo"
    fi
done

# Bucle for estilo C
echo "Bucle estilo C:"
for ((i=1; i<=5; i++)); do
    echo "Iteración $i"
done
````

---

## Bucle `while`

```bash
#!/bin/bash

# Bucle while básico
contador=1
while [ $contador -le 5 ]; do
    echo "Contador: $contador"
    ((contador++))
done

# Bucle while con lectura de archivo
echo "Leyendo archivo línea por línea:"
while IFS= read -r linea; do
    echo "Línea: $linea"
done < archivo.txt

# Bucle while infinito con break
contador=1
while true; do
    echo "Iteración $contador"
    if [ $contador -eq 3 ]; then
        echo "Saliendo del bucle"
        break
    fi
    ((contador++))
done
```

---

## Bucle `until`

```bash
#!/bin/bash

# Bucle until (contrario a while)
contador=1
until [ $contador -gt 5 ]; do
    echo "Contador: $contador"
    ((contador++))
done
```

**Diferencia con `while`**: El bucle **`until`** se ejecuta mientras la condición sea **falsa** (opuesto a `while`).

---

## Control de Bucles

```bash
#!/bin/bash

# Uso de break y continue
for i in {1..10}; do
    if [ $i -eq 5 ]; then
        echo "Saltando el 5"
        continue
    fi
    
    if [ $i -eq 8 ]; then
        echo "Terminando en 8"
        break
    fi
    
    echo "Número: $i"
done
```

### Comandos de Control

- **`break`**: Sale del bucle completamente
- **`continue`**: Salta a la siguiente iteración del bucle