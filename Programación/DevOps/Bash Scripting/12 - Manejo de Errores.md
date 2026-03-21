## Códigos de Salida

```bash
#!/bin/bash

# Función que puede fallar
operacion_riesgosa() {
    local archivo=$1
    
    if [ ! -f "$archivo" ]; then
        echo "Error: El archivo $archivo no existe" >&2
        return 1
    fi
    
    # Realizar operación
    echo "Operación exitosa en $archivo"
    return 0
}

# Manejo de errores
if operacion_riesgosa "archivo_inexistente.txt"; then
    echo "Operación completada exitosamente"
else
    echo "La operación falló"
    exit 1
fi
````

**Códigos de salida:**

- **`0`**: Éxito
- **`1-255`**: Error (1 es el más común para errores generales)
- **`>&2`**: Redirige la salida al **error estándar** (stderr)

---

## Trap para Manejo de Señales

```bash
#!/bin/bash

# Función de limpieza
cleanup() {
    echo "Limpiando archivos temporales..."
    rm -f /tmp/mi_script_$$*
    echo "Limpieza completada"
    exit 0
}

# Configurar trap
trap cleanup EXIT INT TERM

# Crear archivo temporal
temp_file="/tmp/mi_script_$$"
echo "Trabajando con archivo temporal: $temp_file"
touch "$temp_file"

# Simular trabajo
echo "Ejecutando operación larga..."
sleep 5

echo "Operación completada"
```

**Señales comunes:**

- **`EXIT`**: Cuando el script termina
- **`INT`**: Ctrl+C (interrupción)
- **`TERM`**: Señal de terminación
- **`$$`**: PID del proceso actual

---

## Logging

```bash
#!/bin/bash

# Configuración de logging
LOG_FILE="/var/log/mi_script.log"
DEBUG=true

# Función de logging
log() {
    local level=$1
    local message=$2
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    echo "[$timestamp] [$level] $message" >> "$LOG_FILE"
    
    if [ "$DEBUG" = true ]; then
        echo "[$timestamp] [$level] $message" >&2
    fi
}

# Funciones de logging específicas
log_info() {
    log "INFO" "$1"
}

log_error() {
    log "ERROR" "$1"
}

log_debug() {
    if [ "$DEBUG" = true ]; then
        log "DEBUG" "$1"
    fi
}

# Uso del logging
log_info "Script iniciado"
log_debug "Procesando archivo de configuración"

if [ ! -f "config.txt" ]; then
    log_error "Archivo de configuración no encontrado"
    exit 1
fi

log_info "Script completado exitosamente"
```

**Niveles de logging:**

- **`INFO`**: Información general
- **`ERROR`**: Errores que requieren atención
- **`DEBUG`**: Información detallada para desarrollo