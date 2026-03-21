## Declaración y Uso de Variables

```bash
#!/bin/bash

# Declaración básica (sin espacios alrededor del =)
nombre="Juan"
edad=25
precio=19.99

# Acceso a variables
echo "Nombre: $nombre"
echo "Edad: ${edad}"  # Recomendado usar llaves
echo "Precio: $precio"

# Variables con espacios
mensaje="Hola mundo desde Bash"
echo "$mensaje"
````

---

## Tipos de Variables

```bash
#!/bin/bash

# Cadenas de texto
cadena="Esto es una cadena"
cadena_vacia=""

# Números enteros
numero=42
negativo=-10

# Arrays
frutas=("manzana" "banana" "naranja")
echo "Primera fruta: ${frutas[0]}"
echo "Todas las frutas: ${frutas[@]}"

# Variables de solo lectura
readonly PI=3.14159
# PI=3.14  # Esto causaría un error

# Variables locales (dentro de funciones)
function ejemplo() {
    local var_local="Solo visible aquí"
    echo "$var_local"
}
```

---

## Operaciones con Variables

```bash
#!/bin/bash

# Longitud de cadena
texto="Hola mundo"
echo "Longitud: ${#texto}"

# Concatenación
nombre="Juan"
apellido="Pérez"
nombre_completo="${nombre} ${apellido}"
echo "$nombre_completo"

# Sustitución de cadenas
archivo="documento.txt"
sin_extension="${archivo%.txt}"  # documento
echo "Sin extensión: $sin_extension"

# Valores por defecto
echo "Usuario: ${USER:-'desconocido'}"
```