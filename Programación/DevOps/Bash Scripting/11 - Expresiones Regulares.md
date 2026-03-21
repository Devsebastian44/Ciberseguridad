## Uso con `grep`

### Búsqueda Básica

```bash
#!/bin/bash

# Búsqueda simple
grep "patrón" archivo.txt

# Búsqueda con expresiones regulares
grep -E "^[0-9]+$" archivo.txt          # Solo números
grep -E "^[a-zA-Z]+@[a-zA-Z]+\.[a-zA-Z]+$" archivo.txt  # Email básico
grep -E "^[0-9]{3}-[0-9]{3}-[0-9]{4}$" archivo.txt     # Teléfono
````

**Opciones de `grep`:**

- **`-E`**: Habilita expresiones regulares extendidas
- **`-o`**: Muestra solo la parte que coincide
- **`-i`**: Ignora mayúsculas/minúsculas

---

## Validación con Expresiones Regulares

### Función para Validar Email

```bash
validar_email() {
    local email=$1
    if [[ $email =~ ^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$ ]]; then
        echo "Email válido: $email"
        return 0
    else
        echo "Email inválido: $email"
        return 1
    fi
}

# Uso
validar_email "usuario@ejemplo.com"
validar_email "email_invalido"
```

### Función para Validar Teléfono

```bash
validar_telefono() {
    local telefono=$1
    if [[ $telefono =~ ^[0-9]{3}-[0-9]{3}-[0-9]{4}$ ]]; then
        echo "Teléfono válido: $telefono"
        return 0
    else
        echo "Teléfono inválido: $telefono"
        return 1
    fi
}

# Uso
validar_telefono "123-456-7890"
validar_telefono "123456789"
```

**Operador `=~`**: Permite comparar contra **expresiones regulares** dentro de `[[ ]]`

---

## Manipulación de Texto

### Comandos Básicos

```bash
#!/bin/bash

# Reemplazar texto con sed
sed 's/antiguo/nuevo/g' archivo.txt

# Extraer información con awk
awk '{print $1}' archivo.txt           # Primera columna
awk -F',' '{print $2}' archivo.csv     # Segunda columna de CSV
```

### Función para Limpiar Datos

```bash
limpiar_datos() {
    local archivo=$1
    
    # Eliminar líneas vacías
    sed -i '/^$/d' "$archivo"
    
    # Eliminar espacios al inicio y final
    sed -i 's/^[ \t]*//;s/[ \t]*$//' "$archivo"
    
    echo "Datos limpiados en $archivo"
}
```

### Función para Extraer URLs

```bash
extraer_urls() {
    local archivo=$1
    grep -oE 'https?://[^[:space:]]+' "$archivo"
}
```

**Herramientas principales:**

- **`sed`**: Editor de flujo para transformar texto
- **`awk`**: Procesamiento de patrones y columnas
- **`grep -o`**: Extrae solo las coincidencias