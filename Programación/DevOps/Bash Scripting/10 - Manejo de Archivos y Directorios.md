## Operaciones Básicas con Archivos

```bash
#!/bin/bash

# Crear archivo
touch archivo.txt

# Escribir en archivo
echo "Contenido inicial" > archivo.txt
echo "Línea adicional" >> archivo.txt

# Leer archivo
while IFS= read -r linea; do
    echo "Línea: $linea"
done < archivo.txt

# Verificar existencia
if [ -f "archivo.txt" ]; then
    echo "El archivo existe"
    
    # Obtener información del archivo
    echo "Tamaño: $(wc -c < archivo.txt) bytes"
    echo "Líneas: $(wc -l < archivo.txt)"
    echo "Permisos: $(ls -l archivo.txt | cut -d' ' -f1)"
fi
````

**Operadores de redirección:**

- **`>`**: Sobrescribe el archivo
- **`>>`**: Agrega contenido al final del archivo

---

## Operaciones con Directorios

```bash
#!/bin/bash

# Crear directorio
mkdir -p mi_directorio/subdirectorio

# Listar contenido
echo "Contenido del directorio actual:"
ls -la

# Navegar entre directorios
cd mi_directorio
echo "Ahora estoy en: $(pwd)"
cd ..

# Encontrar archivos
echo "Archivos .txt en el directorio:"
find . -name "*.txt" -type f

# Copiar y mover archivos
cp archivo.txt copia_archivo.txt
mv copia_archivo.txt mi_directorio/

# Eliminar archivos y directorios
rm -f archivo_temporal.txt
rmdir directorio_vacio
rm -rf directorio_con_contenido
```

**Comandos importantes:**

- **`mkdir -p`**: Crea directorios incluyendo padres si no existen
- **`find`**: Busca archivos según criterios
- **`rm -rf`**: Elimina recursivamente (¡usar con precaución!)

---

## Procesamiento de Archivos

### Función para Procesar Archivos CSV

```bash
#!/bin/bash

procesar_csv() {
    local archivo=$1
    local contador=0
    
    while IFS=, read -r col1 col2 col3; do
        if [ $contador -eq 0 ]; then
            echo "Encabezados: $col1, $col2, $col3"
        else
            echo "Fila $contador: $col1 | $col2 | $col3"
        fi
        ((contador++))
    done < "$archivo"
}

# Uso
if [ -f "datos.csv" ]; then
    procesar_csv "datos.csv"
fi
```

### Función para Hacer Backup de Archivos

```bash
hacer_backup() {
    local archivo=$1
    local backup_dir="backup_$(date +%Y%m%d)"
    
    mkdir -p "$backup_dir"
    
    if [ -f "$archivo" ]; then
        cp "$archivo" "$backup_dir/"
        echo "Backup creado: $backup_dir/$archivo"
    else
        echo "Error: El archivo $archivo no existe"
    fi
}

# Uso
hacer_backup "archivo_importante.txt"
```

**Características:**

- **`IFS=,`**: Define el separador de campos (coma para CSV)
- **`date +%Y%m%d`**: Formatea la fecha (ej: 20250109)
- **`read -r`**: Lee líneas sin interpretar caracteres de escape