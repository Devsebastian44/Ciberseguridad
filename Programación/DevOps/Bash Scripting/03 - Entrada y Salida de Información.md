## Parámetros de Entrada

Los scripts pueden recibir información mediante **parámetros**:

```bash
#!/bin/bash

echo "El primer parámetro es: $1"
echo "El segundo parámetro es: $2"
echo "El número de parámetros es: $#"
echo "Todos los parámetros son: $*"
echo "Parámetros como array: $@"
echo "Nombre del script: $0"
````

### Variables de Parámetros

- **`$1, $2, $3...`**: Parámetros individuales
- **`$#`**: Número total de parámetros
- **`$*`**: Todos los parámetros como una cadena
- **`$@`**: Todos los parámetros como array
- **`$0`**: Nombre del script

---

## Lectura de Entrada del Usuario

```bash
#!/bin/bash

# Lectura básica
echo -n "¿Cuál es tu nombre? "
read nombre
echo "Hola, $nombre"

# Lectura con prompt
read -p "Ingresa tu edad: " edad
echo "Tienes $edad años"

# Lectura silenciosa (para contraseñas)
read -s -p "Ingresa tu contraseña: " password
echo -e "\nContraseña ingresada"

# Lectura con timeout
if read -t 10 -p "Tienes 10 segundos para responder: " respuesta; then
    echo "Respondiste: $respuesta"
else
    echo "Se agotó el tiempo"
fi
```

---

## Salida de Información

```bash
#!/bin/bash

# Salida estándar
echo "Mensaje normal"

# Salida con formato
printf "Nombre: %s, Edad: %d\n" "Juan" 25

# Redirección a archivo
echo "Contenido" > archivo.txt      # Sobrescribir
echo "Más contenido" >> archivo.txt # Agregar

# Salida de error
echo "Error: Algo salió mal" >&2
```