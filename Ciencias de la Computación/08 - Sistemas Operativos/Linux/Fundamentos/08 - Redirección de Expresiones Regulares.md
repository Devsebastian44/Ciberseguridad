# Redirección de Entrada y Salida

## Conceptos Básicos

Flujos estándar:

- **stdin (0)**: Entrada estándar
- **stdout (1)**: Salida estándar
- **stderr (2)**: Salida de error

## Redirección de Salida

```bash
# Redireccionar stdout a archivo
comando > archivo.txt           # Sobreescribir
comando >> archivo.txt          # Agregar

# Redireccionar stderr
comando 2> errores.txt          # Solo errores
comando 2>> errores.txt         # Agregar errores

# Redireccionar stdout y stderr
comando > salida.txt 2>&1       # Ambos al mismo archivo
comando &> salida.txt           # Forma abreviada
comando > salida.txt 2> errores.txt  # Archivos separados
```

## Redirección de Entrada

```bash
# Redireccionar stdin desde archivo
comando < archivo.txt

# Here document
comando << EOF
línea 1
línea 2
EOF

# Here string
comando <<< "texto directo"
```

## Ejemplos Prácticos

```bash
# Guardar lista de archivos
ls -la > lista_archivos.txt

# Agregar fecha al final de archivo
date >> log.txt

# Buscar errores en logs
grep "error" /var/log/syslog > errores.txt 2>&1

# Enviar contenido a comando
sort < nombres.txt

# Crear archivo con contenido
cat > archivo.txt << EOF
Contenido del archivo
Línea 2
Línea 3
EOF
```

Final de línea:

- `[]`: Clase de caracteres
- `()`: Agrupación
- `|`: Alternativa (OR)

## Clases de Caracteres

```bash
[abc]       # Cualquier carácter: a, b, o c
[a-z]       # Cualquier letra minúscula
[A-Z]       # Cualquier letra mayúscula
[0-9]       # Cualquier dígito
[a-zA-Z]    # Cualquier letra
[^abc]      # Cualquier carácter EXCEPTO a, b, o c
```

Clases predefinidas:

- `\d`: Dígitos [0-9]
- `\w`: Caracteres de palabra [a-zA-Z0-9_]
- `\s`: Espacios en blanco
- `\D`: No dígitos
- `\W`: No caracteres de palabra
- `\S`: No espacios en blanco

## Cuantificadores

```bash
a*          # Cero o más 'a'
a+          # Una o más 'a'
a?          # Cero o una 'a'
a{3}        # Exactamente 3 'a'
a{3,}       # 3 o más 'a'
a{3,5}      # Entre 3 y 5 'a'
```

## Comando grep

### Uso Básico

```bash
grep "patrón" archivo.txt       # Buscar patrón
grep -i "patrón" archivo.txt    # Ignorar mayúsculas/minúsculas
grep -v "patrón" archivo.txt    # Líneas que NO contienen patrón
grep -n "patrón" archivo.txt    # Mostrar números de línea
grep -r "patrón" directorio/    # Búsqueda recursiva
```

### Opciones Avanzadas

```bash
grep -c "patrón" archivo.txt    # Contar coincidencias
grep -l "patrón" *.txt          # Solo nombres de archivos
grep -w "palabra" archivo.txt   # Palabra completa
grep -A 3 "patrón" archivo.txt  # 3 líneas después
grep -B 3 "patrón" archivo.txt  # 3 líneas antes
grep -C 3 "patrón" archivo.txt  # 3 líneas antes y después
```

### Expresiones Regulares con grep

```bash
# Buscar líneas que empiecen con "Error"
grep "^Error" archivo.log

# Buscar líneas que terminen con "OK"
grep "OK$" archivo.log

# Buscar direcciones IP
grep "\b[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\b" archivo.txt

# Buscar direcciones de email
grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" archivo.txt

# Buscar números de teléfono
grep -E "\([0-9]{3}\) [0-9]{3}-[0-9]{4}" archivo.txt
```

## Comando sed

### Introducción a sed

`sed` (Stream Editor) es un editor de flujo que permite realizar transformaciones en texto.

### Operaciones Básicas

```bash
# Sustituir primera ocurrencia por línea
sed 's/antiguo/nuevo/' archivo.txt

# Sustituir todas las ocurrencias
sed 's/antiguo/nuevo/g' archivo.txt

# Sustituir ignorando mayúsculas/minúsculas
sed 's/antiguo/nuevo/gi' archivo.txt

# Modificar archivo in-place
sed -i 's/antiguo/nuevo/g' archivo.txt

# Crear backup antes de modificar
sed -i.bak 's/antiguo/nuevo/g' archivo.txt
```

### Operaciones Avanzadas

```bash
# Eliminar líneas vacías
sed '/^$/d' archivo.txt

# Eliminar líneas que contienen patrón
sed '/patrón/d' archivo.txt

# Imprimir líneas específicas
sed -n '5,10p' archivo.txt      # Líneas 5 a 10
sed -n '/patrón/p' archivo.txt  # Líneas que contienen patrón

# Agregar texto después de línea
sed '/patrón/a\Texto a agregar' archivo.txt

# Agregar texto antes de línea
sed '/patrón/i\Texto a agregar' archivo.txt

# Reemplazar línea completa
sed '/patrón/c\Nueva línea' archivo.txt
```

### Ejemplos Prácticos con sed

```bash
# Cambiar formato de fecha
sed 's/\([0-9]\{2\}\)\/\([0-9]\{2\}\)\/\([0-9]\{4\}\)/\3-\2-\1/g' archivo.txt

# Eliminar comentarios de configuración
sed '/^#/d' config.txt

# Convertir texto a mayúsculas
sed 's/.*/\U&/' archivo.txt

# Numerar líneas
sed = archivo.txt | sed 'N;s/\n/\t/'
```

## Comando awk

### Introducción a awk

`awk` es un lenguaje de programación orientado a patrones para procesamiento de texto.

### Estructura Básica

```bash
awk 'patrón { acción }' archivo.txt
```

### Operaciones Básicas

```bash
# Imprimir archivo completo
awk '{ print }' archivo.txt

# Imprimir columnas específicas
awk '{ print $1, $3 }' archivo.txt

# Imprimir líneas que contienen patrón
awk '/patrón/ { print }' archivo.txt

# Imprimir número de línea
awk '{ print NR, $0 }' archivo.txt

# Imprimir última columna
awk '{ print $NF }' archivo.txt
```

### Variables Integradas

```bash
NR          # Número de registro (línea)
NF          # Número de campos
FS          # Separador de campos
OFS         # Separador de salida
RS          # Separador de registros
ORS         # Separador de salida de registros
```

### Ejemplos Avanzados

```bash
# Sumar columna
awk '{ suma += $1 } END { print suma }' archivo.txt

# Promedio de columna
awk '{ suma += $1; count++ } END { print suma/count }' archivo.txt

# Contar líneas por patrón
awk '/error/ { errores++ } /warning/ { warnings++ } END { print "Errores:", errores, "Warnings:", warnings }' archivo.log

# Procesar CSV
awk -F',' '{ print $1 "\t" $2 }' archivo.csv

# Filtrar por condición
awk '$3 > 100 { print $1, $3 }' archivo.txt
```

## Combinando Herramientas

### Análisis de Logs

```bash
# Top 10 IPs en logs de Apache
awk '{ print $1 }' /var/log/apache2/access.log | \
    sort | \
    uniq -c | \
    sort -nr | \
    head -10

# Análisis de errores por hora
grep "error" /var/log/syslog | \
    sed 's/^\([^ ]* [^ ]* [^ ]*\).*/\1/' | \
    cut -d: -f1-2 | \
    sort | \
    uniq -c | \
    sort -nr
```

### Procesamiento de Datos

```bash
# Estadísticas de archivos por extensión
find /home -type f | \
    sed 's/.*\.//' | \
    sort | \
    uniq -c | \
    sort -nr

# Análisis de uso de comandos del historial
history | \
    awk '{ print $2 }' | \
    sort | \
    uniq -c | \
    sort -nr | \
    head -20
```