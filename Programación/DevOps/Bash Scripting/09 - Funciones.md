## Declaración y Uso Básico

```bash
#!/bin/bash

# Función básica
saludar() {
    echo "¡Hola desde la función!"
}

# Función con parámetros
saludar_usuario() {
    local nombre=$1
    local edad=$2
    echo "Hola $nombre, tienes $edad años"
}

# Función con valor de retorno
sumar() {
    local a=$1
    local b=$2
    local resultado=$((a + b))
    echo $resultado
}

# Llamadas a funciones
saludar
saludar_usuario "Juan" 25
resultado=$(sumar 5 3)
echo "5 + 3 = $resultado"
````

**Características de las funciones:**

- Los **parámetros** se acceden con `$1`, `$2`, etc.
- Las **variables locales** se declaran con `local`
- Los **valores de retorno** se envían con `echo` y se capturan con `$()`

---

## Funciones Avanzadas

### Función con Variables Locales

```bash
#!/bin/bash

procesar_datos() {
    local datos=$1
    local procesados=""
    
    echo "Procesando: $datos"
    # Lógica de procesamiento aquí
    procesados="Datos procesados: $datos"
    echo "$procesados"
}

# Uso
procesar_datos "mis datos"
```

### Función con Múltiples Valores de Retorno

```bash
obtener_info_sistema() {
    local usuario=$(whoami)
    local fecha=$(date)
    local directorio=$(pwd)
    
    echo "$usuario|$fecha|$directorio"
}

# Capturar múltiples valores
IFS='|' read -r usuario fecha directorio <<< "$(obtener_info_sistema)"
echo "Usuario: $usuario"
echo "Fecha: $fecha"
echo "Directorio: $directorio"
```

### Función Recursiva (Factorial)

```bash
factorial() {
    local n=$1
    if [ $n -le 1 ]; then
        echo 1
    else
        local temp=$((n - 1))
        local temp_result=$(factorial $temp)
        echo $((n * temp_result))
    fi
}

# Uso
echo "Factorial de 5: $(factorial 5)"
```

**Nota sobre recursividad**: La función se llama a sí misma hasta alcanzar la **condición base** (`n <= 1`).