## Procesamiento en Paralelo

```bash
#!/bin/bash

# Función para procesar archivo
procesar_archivo() {
    local archivo=$1
    echo "Procesando $archivo..."
    sleep 2  # Simular procesamiento
    echo "Terminado $archivo"
}

# Procesamiento en paralelo
archivos=("archivo1.txt" "archivo2.txt" "archivo3.txt")

for archivo in "${archivos[@]}"; do
    procesar_archivo "$archivo" &
done

# Esperar a que terminen todos los procesos
wait
echo "Todos los archivos procesados"
````

**Conceptos clave:**

- **`&`**: Ejecuta el comando en **segundo plano** (background)
- **`wait`**: Espera a que todos los procesos en background terminen
- **Ventaja**: Procesa múltiples archivos simultáneamente, reduciendo el tiempo total

---

## Menús Interactivos

### Menú Principal

```bash
#!/bin/bash

# Menú principal
mostrar_menu() {
    clear
    echo "================================"
    echo "    SISTEMA DE GESTIÓN"
    echo "================================"
    echo "1. Gestionar usuarios"
    echo "2. Gestionar archivos"
    echo "3. Información del sistema"
    echo "4. Configuración"
    echo "5. Salir"
    echo "================================"
}
```

### Submenú de Usuarios

```bash
menu_usuarios() {
    while true; do
        clear
        echo "=== GESTIÓN DE USUARIOS ==="
        echo "1. Listar usuarios"
        echo "2. Agregar usuario"
        echo "3. Eliminar usuario"
        echo "4. Volver al menú principal"
        
        read -p "Selecciona una opción: " opcion
        
        case $opcion in
            1) listar_usuarios ;;
            2) agregar_usuario ;;
            3) eliminar_usuario ;;
            4) break ;;
            *) echo "Opción inválida" ;;
        esac
        
        read -p "Presiona Enter para continuar..."
    done
}
```

### Bucle Principal

```bash
while true; do
    mostrar_menu
    read -p "Selecciona una opción: " opcion
    
    case $opcion in
        1) menu_usuarios ;;
        2) echo "Funcionalidad de archivos" ;;
        3) echo "Información del sistema" ;;
        4) echo "Configuración" ;;
        5) echo "¡Hasta luego!"; exit 0 ;;
        *) echo "Opción inválida" ;;
    esac
    
    read -p "Presiona Enter para continuar..."
done
```

**Características:**

- **`clear`**: Limpia la pantalla para mejor presentación
- **Navegación anidada**: Menús dentro de menús
- **`break`**: Sale del submenú y vuelve al menú principal

---

## Configuración Externa

### Archivo de Configuración (config.conf)

```bash
# Ejemplo de config.conf
DB_HOST=localhost
DB_USER=admin
DB_PASS=secreto
DEBUG=true
```

### Cargar Configuración

```bash
#!/bin/bash

cargar_config() {
    local config_file=$1
    
    if [ ! -f "$config_file" ]; then
        echo "Error: Archivo de configuración no encontrado: $config_file"
        return 1
    fi
    
    # Cargar variables del archivo
    source "$config_file"
    
    echo "Configuración cargada desde $config_file"
}
```

### Validar Configuración

```bash
validar_config() {
    local errores=0
    
    if [ -z "$DB_HOST" ]; then
        echo "Error: DB_HOST no definido"
        ((errores++))
    fi
    
    if [ -z "$DB_USER" ]; then
        echo "Error: DB_USER no definido"
        ((errores++))
    fi
    
    if [ $errores -gt 0 ]; then
        echo "Errores en la configuración: $errores"
        return 1
    fi
    
    return 0
}
```

### Uso

```bash
if cargar_config "config.conf"; then
    if validar_config; then
        echo "Conectando a $DB_HOST como $DB_USER"
    else
        exit 1
    fi
else
    exit 1
fi
```

**Ventajas de configuración externa:**

- **Separación**: Configuración separada del código
- **Flexibilidad**: Cambios sin modificar el script
- **Seguridad**: Credenciales fuera del código fuente
- **`source`**: Importa variables desde un archivo externo