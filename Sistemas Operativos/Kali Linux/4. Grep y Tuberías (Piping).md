# Comando `grep`

`grep` (Global Regular Expression Print) es fundamental para buscar patrones en texto:

## Opciones Principales

```bash
# Opciones básicas
grep "patrón" archivo.txt
grep -v "patrón" archivo.txt    # Líneas que NO contienen el patrón
grep -c "patrón" archivo.txt    # Contar líneas que contienen el patrón
grep -n "patrón" archivo.txt    # Mostrar número de línea
grep -i "patrón" archivo.txt    # Ignorar mayúsculas/minúsculas
grep -l "patrón" *.txt          # Solo nombres de archivos coincidentes
```

## Ejemplos Prácticos

```bash
# Buscar en archivos del sistema
grep "root" /etc/passwd
grep -i "error" /var/log/syslog
grep -n "TODO" *.py

# Buscar con expresiones regulares
grep "^root" /etc/passwd        # Líneas que empiezan con "root"
grep "bash$" /etc/passwd        # Líneas que terminan con "bash"
grep "[0-9]" /etc/passwd        # Líneas que contienen números

# Buscar recursivamente
grep -r "función" /home/usuario/proyectos/
grep -r --include="*.py" "import" /usr/lib/python3/
```

# Tuberías (Pipes)

Las tuberías permiten conectar la salida de un comando con la entrada de otro:

```bash
# Sintaxis básica
comando1 | comando2 | comando3

# Ejemplos fundamentales
cat /etc/passwd | grep "root"
ps aux | grep "apache"
ls -la | grep "Nov"
```

## Combinaciones Poderosas


```bash
# Análisis de logs
cat /var/log/syslog | grep "error" | wc -l  # Contar errores
tail -f /var/log/apache2/access.log | grep "404"

# Análisis de procesos
ps aux | grep -v grep | grep "python"
ps aux | sort -k3 -nr | head -10  # Top 10 procesos por CPU

# Análisis de archivos
find /home -name "*.txt" | xargs grep "password"
ls -la | awk '{print $1, $3, $9}'  # Permisos, propietario, nombre

# Análisis de red
netstat -tulpn | grep ":80"
cat /etc/passwd | cut -d: -f1 | sort  # Lista de usuarios ordenada
```

## Redirecciones


```bash
# Redireccionar salida
comando > archivo.txt    # Sobrescribir
comando >> archivo.txt   # Añadir al final
comando 2> error.log     # Solo errores
comando &> todo.log      # Salida y errores

# Redireccionar entrada
comando < archivo.txt
grep "patrón" < archivo.txt
```

## Comandos Adicionales para Análisis

```bash
# Contar líneas, palabras, caracteres
wc -l archivo.txt    # Líneas
wc -w archivo.txt    # Palabras
wc -c archivo.txt    # Caracteres

# Ordenar y eliminar duplicados
sort archivo.txt
sort -u archivo.txt  # Eliminar duplicados
uniq archivo.txt     # Eliminar duplicados consecutivos

# Cortar columnas
cut -d: -f1 /etc/passwd  # Primera columna usando ':' como separador
cut -c1-10 archivo.txt   # Caracteres 1-10

# Reemplazar texto
sed 's/viejo/nuevo/g' archivo.txt
tr 'a-z' 'A-Z' < archivo.txt  # Convertir a mayúsculas
```