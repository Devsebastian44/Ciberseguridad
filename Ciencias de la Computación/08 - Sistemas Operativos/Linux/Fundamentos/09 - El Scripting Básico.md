# Introducción al Scripting

## ¿Qué es un Script?

Un script es un archivo de texto que contiene una serie de comandos que se ejecutan secuencialmente. Los scripts permiten automatizar tareas repetitivas y crear herramientas personalizadas.

## Ventajas del Scripting

- **Automatización**: Ejecutar tareas repetitivas sin intervención manual
- **Consistencia**: Mismos pasos cada vez
- **Eficiencia**: Ahorro de tiempo y esfuerzo
- **Documentación**: Los scripts sirven como documentación de procesos
- **Escalabilidad**: Fácil modificación y extensión


# Fundamentos de Bash Scripting

## Estructura Básica

```bash
#!/bin/bash
# Comentario: Descripción del script
# Autor: Tu nombre
# Fecha: Fecha de creación

# Código del script
echo "Hola, mundo!"
```

## El Shebang

```bash
#!/bin/bash         # Bash shell
#!/bin/sh           # Shell POSIX
#!/usr/bin/env bash # Bash usando env
#!/usr/bin/python3  # Python 3
```

## Hacer Ejecutable un Script

```bash
chmod +x script.sh      # Dar permisos de ejecución
./script.sh            # Ejecutar script
```


# Variables

## Declaración y Uso

```bash
#!/bin/bash

# Declaración de variables
NOMBRE="Juan"
EDAD=25
ARCHIVO="/tmp/datos.txt"

# Uso de variables
echo "Nombre: $NOMBRE"
echo "Edad: ${EDAD} años"
echo "Archivo: $ARCHIVO"

# Variables del sistema
echo "Usuario actual: $USER"
echo "Directorio home: $HOME"
echo "Ruta actual: $PWD"
```

## Variables Especiales

```bash
$0      # Nombre del script
$1, $2  # Argumentos posicionales
$#      # Número de argumentos
$@      # Todos los argumentos
$?      # Código de salida del último comando
$      # PID del proceso actual
```

## Ejemplo con Argumentos


```bash
#!/bin/bash

echo "Nombre del script: $0"
echo "Primer argumento: $1"
echo "Segundo argumento: $2"
echo "Número de argumentos: $#"
echo "Todos los argumentos: $@"

if [ $# -eq 0 ]; then
    echo "Uso: $0 <arg1> <arg2> ..."
    exit 1
fi
```


# Entrada y Salida

## Lectura de Entrada

```bash
#!/bin/bash

# Leer entrada del usuario
echo "Ingrese su nombre: "
read NOMBRE
echo "Hola, $NOMBRE!"

# Leer con prompt
read -p "Ingrese su edad: " EDAD
echo "Tienes $EDAD años"

# Leer contraseña (oculta)
read -s -p "Ingrese contraseña: " PASSWORD
echo
echo "Contraseña ingresada"
```

## Salida Formateada


```bash
#!/bin/bash

# Printf para formato avanzado
printf "Nombre: %-10s Edad: %d\n" "Juan" 25
printf "Precio: $%.2f\n" 19.99

# Colores en la salida
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m' # No Color

echo -e "${RED}Error${NC}: Archivo no encontrado"
echo -e "${GREEN}Éxito${NC}: Operación completada"
echo -e "${YELLOW}Advertencia${NC}: Espacio en disco bajo"
```


# Estructuras de Control

## Condicionales

```bash
#!/bin/bash

# Condicional simple
if [ $# -eq 0 ]; then
    echo "No se proporcionaron argumentos"
fi

# Condicional con else
if [ -f "$1" ]; then
    echo "El archivo existe"
else
    echo "El archivo no existe"
fi

# Condicional múltiple
if [ $1 -gt 10 ]; then
    echo "Mayor que 10"
elif [ $1 -eq 10 ]; then
    echo "Igual a 10"
else
    echo "Menor que 10"
fi
```

## Operadores de Comparación

Numéricos:

```bash
-eq     # Igual
-ne     # No igual
-lt     # Menor que
-le     # Menor o igual
-gt     # Mayor que
-ge     # Mayor o igual
```

Cadenas:

```bash
=       # Igual
!=      # No igual
-z      # Cadena vacía
-n      # Cadena no vacía
```

Archivos:

```bash
-f      # Es archivo regular
-d      # Es directorio
-r      # Es legible
-w      # Es escribible
-x      # Es ejecutable
-e      # Existe
```

## Estructura case


```bash
#!/bin/bash

case $1 in
    "start")
        echo "Iniciando servicio..."
        ;;
    "stop")
        echo "Deteniendo servicio..."
        ;;
    "restart")
        echo "Reiniciando servicio..."
        ;;
    *)
        echo "Uso: $0 {start|stop|restart}"
        exit 1
        ;;
esac
```


# Bucles

## Bucle for

```bash
#!/bin/bash

# For básico
for i in 1 2 3 4 5; do
    echo "Número: $i"
done

# For con rango
for i in {1..10}; do
    echo "Iteración: $i"
done

# For con archivos
for archivo in *.txt; do
    echo "Procesando: $archivo"
done

# For estilo C
for ((i=1; i<=10; i++)); do
    echo "Contador: $i"
done
```

## Bucle while

```bash
#!/bin/bash

# While básico
contador=1
while [ $contador -le 5 ]; do
    echo "Contador: $contador"
    ((contador++))
done

# Leer archivo línea por línea
while IFS= read -r linea; do
    echo "Línea: $linea"
done < archivo.txt
```

## Bucle until

```bash
#!/bin/bash

# Until (contrario a while)
contador=1
until [ $contador -gt 5 ]; do
    echo "Contador: $contador"
    ((contador++))
done
```


# Funciones

## Definición y Uso

```bash
#!/bin/bash

# Definir función
saludar() {
    echo "Hola, $1!"
}

# Función con múltiples parámetros
calcular_area() {
    local base=$1
    local altura=$2
    local area=$((base * altura))
    echo $area
}

# Función con valor de retorno
es_par() {
    local numero=$1
    if [ $((numero % 2)) -eq 0 ]; then
        return 0  # Verdadero
    else
        return 1  # Falso
    fi
}

# Uso de funciones
saludar "Juan"
area=$(calcular_area 5 3)
echo "El área es: $area"

if es_par 4; then
    echo "4 es par"
fi
```

## Variables Locales

```bash
#!/bin/bash

variable_global="Global"

mi_funcion() {
    local variable_local="Local"
    echo "Dentro de la función: $variable_local"
    echo "Dentro de la función: $variable_global"
}

mi_funcion
echo "Fuera de la función: $variable_global"
# echo "Fuera de la función: $variable_local"  # Error
```


# Manejo de Errores

## Códigos de Salida

```bash
#!/bin/bash

# Verificar éxito de comando
if cp archivo1.txt archivo2.txt; then
    echo "Copia exitosa"
else
    echo "Error al copiar archivo"
    exit 1
fi

# Verificar código de salida
comando
if [ $? -eq 0 ]; then
    echo "Comando exitoso"
else
    echo "Comando falló"
fi
```

## Manejo de Errores con trap

```bash
#!/bin/bash

# Función de limpieza
cleanup() {
    echo "Limpiando archivos temporales..."
    rm -f /tmp/temp_$
    exit 1
}

# Configurar trap
trap cleanup EXIT INT TERM

# Crear archivo temporal
TEMP_FILE="/tmp/temp_$"
touch $TEMP_FILE

# Simular trabajo
echo "Trabajando..."
sleep 5
echo "Trabajo completado"
```

## Ejemplos Prácticos

### Script de Backup

```bash
#!/bin/bash

# Script de backup automatizado
# Autor: Admin
# Fecha: 2025

# Configuración
BACKUP_DIR="/backup"
SOURCE_DIR="/home/usuario"
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_FILE="backup_$DATE.tar.gz"
LOG_FILE="/var/log/backup.log"

# Función de log
log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a $LOG_FILE
}

# Verificar que existe el directorio fuente
if [ ! -d "$SOURCE_DIR" ]; then
    log_message "ERROR: Directorio fuente no existe: $SOURCE_DIR"
    exit 1
fi

# Crear directorio de backup si no existe
if [ ! -d "$BACKUP_DIR" ]; then
    mkdir -p $BACKUP_DIR
    log_message "INFO: Directorio de backup creado: $BACKUP_DIR"
fi

# Crear backup
log_message "INFO: Iniciando backup de $SOURCE_DIR"
tar -czf $BACKUP_DIR/$BACKUP_FILE $SOURCE_DIR

# Verificar que el backup se creó correctamente
if [ $? -eq 0 ]; then
    log_message "INFO: Backup creado exitosamente: $BACKUP_FILE"
    
    # Mostrar tamaño del backup
    SIZE=$(du -h $BACKUP_DIR/$BACKUP_FILE | cut -f1)
    log_message "INFO: Tamaño del backup: $SIZE"
else
    log_message "ERROR: Fallo al crear backup"
    exit 1
fi

# Eliminar backups antiguos (más de 7 días)
DELETED=$(find $BACKUP_DIR -name "backup_*.tar.gz" -mtime +7 -delete -print | wc -l)
if [ $DELETED -gt 0 ]; then
    log_message "INFO: Eliminados $DELETED backups antiguos"
fi

log_message "INFO: Proceso de backup completado"
```

### Script de Monitoreo del Sistema

```bash
#!/bin/bash

# Script de monitoreo del sistema
# Verifica recursos y envía alertas

# Configuración
THRESHOLD_CPU=80
THRESHOLD_MEMORY=85
THRESHOLD_DISK=90
LOG_FILE="/var/log/system_monitor.log"

# Función de log
log_alert() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - ALERT: $1" | tee -a $LOG_FILE
}

# Verificar uso de CPU
check_cpu() {
    CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | cut -d'%' -f1)
    CPU_USAGE=${CPU_USAGE%.*}  # Eliminar decimales
    
    if [ $CPU_USAGE -gt $THRESHOLD_CPU ]; then
        log_alert "Uso de CPU alto: ${CPU_USAGE}%"
    fi
}

# Verificar uso de memoria
check_memory() {
    MEMORY_USAGE=$(free | grep Mem | awk '{printf "%.0f", $3/$2 * 100.0}')
    
    if [ $MEMORY_USAGE -gt $THRESHOLD_MEMORY ]; then
        log_alert "Uso de memoria alto: ${MEMORY_USAGE}%"
    fi
}

# Verificar uso de disco
check_disk() {
    df -h | grep -E '^/dev/' | while read line; do
        USAGE=$(echo $line | awk '{print $5}' | cut -d'%' -f1)
        PARTITION=$(echo $line | awk '{print $6}')
        
        if [ $USAGE -gt $THRESHOLD_DISK ]; then
            log_alert "Uso de disco alto en $PARTITION: ${USAGE}%"
        fi
    done
}

# Ejecutar verificaciones
check_cpu
check_memory
check_disk

echo "Monitoreo completado - $(date)"
```