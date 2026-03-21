## Condicionales - `if/else`

### Estructura Básica `if`

```bash
#!/bin/bash

numero=15

if [ $numero -gt 10 ]; then
    echo "El número es mayor que 10"
fi
````

### Estructura `if-else`

```bash
if [ $numero -eq 10 ]; then
    echo "El número es 10"
else
    echo "El número no es 10"
fi
```

### Estructura `if-elif-else`

```bash
if [ $numero -lt 10 ]; then
    echo "Menor que 10"
elif [ $numero -eq 10 ]; then
    echo "Igual a 10"
else
    echo "Mayor que 10"
fi
```

---

## Condicionales - `case`

```bash
#!/bin/bash

opcion=$1

case $opcion in
    "1")
        echo "Seleccionaste la opción 1"
        ;;
    "2")
        echo "Seleccionaste la opción 2"
        ;;
    "3"|"tres")
        echo "Seleccionaste la opción 3 o 'tres'"
        ;;
    *)
        echo "Opción no válida"
        ;;
esac
```

**Características del `case`:**

- Permite **múltiples patrones** con `|`
- El patrón **`*`** actúa como el caso por defecto
- Cada caso termina con **`;;`**

---

## Ejemplo Práctico de Menú

```bash
#!/bin/bash

echo "=== MENÚ PRINCIPAL ==="
echo "1. Mostrar fecha"
echo "2. Mostrar usuarios"
echo "3. Mostrar espacio en disco"
echo "4. Salir"
read -p "Selecciona una opción: " opcion

case $opcion in
    1)
        echo "Fecha actual: $(date)"
        ;;
    2)
        echo "Usuarios conectados:"
        who
        ;;
    3)
        echo "Espacio en disco:"
        df -h
        ;;
    4)
        echo "¡Hasta luego!"
        exit 0
        ;;
    *)
        echo "Opción no válida"
        exit 1
        ;;
esac
```