## Comando `grep`

`grep` (Global Regular Expression Print) es fundamental para buscar patrones en texto.

### Opciones principales

```bash
grep "patrón" archivo.txt          # Buscar patrón
grep -v "patrón" archivo.txt       # Líneas que NO contienen el patrón
grep -c "patrón" archivo.txt       # Contar coincidencias
grep -n "patrón" archivo.txt       # Mostrar número de línea
grep -i "patrón" archivo.txt       # Ignorar mayúsculas/minúsculas
grep -l "patrón" *.txt             # Solo nombres de archivos coincidentes
```

### Ejemplos prácticos

```bash
grep "root" /etc/passwd
grep -i "error" /var/log/syslog
grep -n "TODO" *.py

grep "^root" /etc/passwd           # Líneas que empiezan con "root"
grep "bash$" /etc/passwd           # Líneas que terminan con "bash"
grep "[0-9]" /etc/passwd           # Líneas con números

grep -r "función" /home/usuario/proyectos/
grep -r --include="*.py" "import" /usr/lib/python3/
```

---

## Tuberías (Pipes)

Las tuberías permiten conectar la salida de un comando con la entrada de otro.

### Sintaxis básica

```bash
comando1 | comando2 | comando3
```

### Ejemplos fundamentales

```bash
cat /etc/passwd | grep "root"
ps aux | grep "apache"
ls -la | grep "Nov"
```

---

## Combinaciones Poderosas

```bash
# Análisis de logs
cat /var/log/syslog | grep "error" | wc -l
tail -f /var/log/apache2/access.log | grep "404"

# Análisis de procesos
ps aux | grep -v grep | grep "python"
ps aux | sort -k3 -nr | head -10

# Análisis de archivos
find /home -name "*.txt" | xargs grep "password"
ls -la | awk '{print $1, $3, $9}'

# Análisis de red
netstat -tulpn | grep ":80"
cat /etc/passwd | cut -d: -f1 | sort
```

---

## Redirecciones

```bash
comando > archivo.txt      # Sobrescribir
comando >> archivo.txt     # Añadir al final
comando 2> error.log       # Solo errores
comando &> todo.log        # Salida y errores

comando < archivo.txt
grep "patrón" < archivo.txt
```

---

## Comandos Adicionales para Análisis

```bash
wc -l archivo.txt          # Contar líneas
wc -w archivo.txt          # Contar palabras
wc -c archivo.txt          # Contar caracteres

sort archivo.txt           # Ordenar
sort -u archivo.txt        # Ordenar y eliminar duplicados
uniq archivo.txt           # Eliminar duplicados consecutivos

cut -d: -f1 /etc/passwd    # Primera columna usando ':' como separador
cut -c1-10 archivo.txt     # Caracteres 1-10

sed 's/viejo/nuevo/g' archivo.txt
tr 'a-z' 'A-Z' < archivo.txt
```

---
