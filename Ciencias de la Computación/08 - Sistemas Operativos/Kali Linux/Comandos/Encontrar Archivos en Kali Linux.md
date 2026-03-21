## Comando `updatedb` y `locate`

```bash
updatedb                          # Actualizar base de datos de archivos
locate nombre_archivo             # Buscar archivos por nombre
locate -i nombre_archivo          # Ignorar mayúsculas/minúsculas

# Ejemplos
locate "*.txt"
locate passwd
locate -i "python"
```

---

## Comando `which`

```bash
which python                      # Encontrar ejecutable en PATH
which ls
which -a python                   # Mostrar todas las rutas coincidentes

# Verificar si un comando existe
which curl && echo "curl está instalado"
```

---

## Comando `find`

El comando `find` es más potente y flexible:

### Sintaxis básica

```bash
find [directorio_inicio] [expresión] [opciones] [qué_buscar]
```

### Ejemplos

```bash
find /home -name "*.txt"          # Buscar por nombre
find . -name "archivo.py"
find / -iname "*.PDF"             # Ignorar mayúsculas/minúsculas

find /etc -type f                 # Solo archivos
find /etc -type d                 # Solo directorios

find /home -size +100M            # Archivos >100MB
find /tmp -size -1K               # Archivos <1KB

find /home -perm 755              # Permisos específicos
find /etc -perm -u+w              # Archivos con permisos de escritura

find /var/log -mtime -7           # Modificados últimos 7 días
find /tmp -atime +30              # Accedidos hace más de 30 días

# Ejecutar comandos sobre resultados
find /home -name "*.tmp" -exec rm {} \;
find /var/log -name "*.log" -exec gzip {} \;
```

---

## Ejemplos Prácticos de Búsqueda

```bash
find /etc -name "*.conf"          # Archivos de configuración
find /usr/bin -type f -executable # Archivos ejecutables
find / -size +500M -type f 2>/dev/null   # Archivos grandes

# Archivos duplicados por tamaño
find /home -type f -exec ls -la {} \; | sort -k5 -n

# Archivos sin propietario
find / -nouser -o -nogroup 2>/dev/null
```

---

