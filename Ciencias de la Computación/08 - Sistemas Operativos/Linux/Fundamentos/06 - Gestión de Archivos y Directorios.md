# Jerarquía del Sistema de Archivos

## Estructura FHS (Filesystem Hierarchy Standard)

```
/
├── bin/        # Binarios esenciales
├── boot/       # Archivos de arranque
├── dev/        # Archivos de dispositivos
├── etc/        # Archivos de configuración
├── home/       # Directorios de usuarios
├── lib/        # Bibliotecas compartidas
├── media/      # Puntos de montaje removibles
├── mnt/        # Puntos de montaje temporales
├── opt/        # Software opcional
├── proc/       # Sistema de archivos virtual
├── root/       # Directorio del root
├── sbin/       # Binarios del sistema
├── sys/        # Sistema de archivos virtual
├── tmp/        # Archivos temporales
├── usr/        # Programas de usuario
└── var/        # Datos variables
```

## Descripciones detalladas

Directorios principales:

**/bin** - Binarios esenciales

- Comandos básicos necesarios para el sistema
- Ejemplos: ls, cp, mv, rm, bash

**/etc** - Archivos de configuración

- Configuración del sistema
- Ejemplos: /etc/passwd, /etc/hosts, /etc/fstab

**/home** - Directorios de usuarios

- Cada usuario tiene su directorio personal
- Estructura: /home/usuario/

**/usr** - Programas de usuario

- /usr/bin: Binarios de usuario
- /usr/lib: Bibliotecas
- /usr/share: Datos compartidos

**/var** - Datos variables

- /var/log: Archivos de log
- /var/spool: Colas de impresión/correo
- /var/tmp: Archivos temporales

## Operaciones Básicas con Archivos

### Creación de Archivos

```bash
touch archivo.txt        # Crear archivo vacío
echo "texto" > archivo   # Crear con contenido
cat > archivo << EOF     # Crear con texto multilínea
Línea 1
Línea 2
EOF
```

### Propiedades de Archivos

```bash
ls -l archivo           # Información detallada
stat archivo           # Estadísticas completas
file archivo           # Tipo de archivo
```

Interpretación de ls -l:

```
-rw-r--r-- 1 usuario grupo 1024 Mar 15 10:30 archivo.txt
│││││││││  │ │       │     │    │         │
│││││││││  │ │       │     │    │         └─ Nombre
│││││││││  │ │       │     │    └─ Fecha/hora
│││││││││  │ │       │     └─ Tamaño
│││││││││  │ │       └─ Grupo
│││││││││  │ └─ Propietario
│││││││││  └─ Enlaces
└─────────── Permisos
```

## Búsqueda de Archivos

### Comando find

Búsqueda por nombre:

```bash
find /ruta -name "*.txt"     # Por extensión
find /ruta -name "archivo*"  # Por patrón
find /ruta -iname "*.TXT"    # Ignorar mayúsculas
```

Búsqueda por tipo:

```bash
find /ruta -type f           # Solo archivos
find /ruta -type d           # Solo directorios
find /ruta -type l           # Solo enlaces
```

Búsqueda por tamaño:

```bash
find /ruta -size +100M       # Mayores a 100MB
find /ruta -size -1k         # Menores a 1KB
find /ruta -size 50c         # Exactamente 50 bytes
```

Búsqueda por fecha:

```bash
find /ruta -mtime -7         # Modificados últimos 7 días
find /ruta -atime +30        # Accedidos hace más de 30 días
find /ruta -newer archivo    # Más nuevos que archivo
```

Acciones con find:

```bash
find /ruta -name "*.tmp" -delete     # Eliminar archivos
find /ruta -name "*.txt" -exec cat {} \;  # Ejecutar comando
find /ruta -name "*.log" -exec gzip {} \; # Comprimir archivos
```

### Comando locate

```bash
locate archivo           # Búsqueda rápida
updatedb                # Actualizar base de datos
```

### Comando which/whereis


```bash
which comando           # Ubicación de ejecutable
whereis comando         # Ubicación y manual
```

## Compresión y Archivos

### Comando tar

Crear archivos tar:

```bash
tar -cf archivo.tar directorio/     # Crear archivo tar
tar -czf archivo.tar.gz directorio/ # Crear y comprimir con gzip
tar -cjf archivo.tar.bz2 directorio/ # Crear y comprimir con bzip2
```

Extraer archivos tar:

```bash
tar -xf archivo.tar              # Extraer
tar -xzf archivo.tar.gz          # Extraer gzip
tar -xjf archivo.tar.bz2         # Extraer bzip2
tar -xf archivo.tar -C /destino/ # Extraer en directorio específico
```

Listar contenido:

```bash
tar -tf archivo.tar              # Listar contenido
tar -tvf archivo.tar             # Listar con detalles
```

### Otros comandos de compresión

```bash
gzip archivo.txt         # Comprimir con gzip
gunzip archivo.txt.gz    # Descomprimir gzip
zip archivo.zip *.txt    # Crear archivo zip
unzip archivo.zip        # Extraer archivo zip
```

## Enlaces (Links)

### Enlaces duros (Hard Links)

```bash
ln archivo enlace_duro   # Crear enlace duro
```

Características:

- Apuntan al mismo inode
- No se pueden crear entre sistemas de archivos
- No se pueden crear para directorios

### Enlaces simbólicos (Symbolic Links)

```bash
ln -s /ruta/original enlace_simbolico  # Crear enlace simbólico
```

Características:

- Apuntan al nombre del archivo
- Pueden cruzar sistemas de archivos
- Pueden apuntar a directorios
- Se rompen si se elimina el archivo original

## Montaje de Sistemas de Archivos

### Comando mount

```bash
mount /dev/sdb1 /mnt/usb    # Montar dispositivo
umount /mnt/usb             # Desmontar
mount -t ext4 /dev/sdb1 /mnt/disk  # Especificar tipo
```

### Archivo /etc/fstab

```bash
# Formato: dispositivo punto_montaje tipo opciones dump pass
/dev/sda1 / ext4 defaults 0 1
/dev/sda2 /home ext4 defaults 0 2
```