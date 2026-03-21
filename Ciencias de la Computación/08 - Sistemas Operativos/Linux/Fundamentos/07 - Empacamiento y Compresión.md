# Conceptos Fundamentales

## Diferencia entre Empacamiento y Compresión

**Empacamiento (Archiving):**

- Combinar múltiples archivos en uno solo
- No reduce el tamaño total
- Facilita el transporte y organización

**Compresión:**

- Reduce el tamaño de los datos
- Aplica algoritmos para eliminar redundancia
- Puede aplicarse a archivos individuales o empaquetados

## Herramientas de Empacamiento

### TAR (Tape Archive)

**Opciones principales:**

- `c`: Crear archivo
- `x`: Extraer archivo
- `t`: Listar contenido
- `v`: Verbose (detallado)
- `f`: Especificar archivo
- `z`: Comprimir con gzip
- `j`: Comprimir con bzip2
- `J`: Comprimir con xz

Ejemplos prácticos:

```bash
# Crear archivo tar
tar -cvf backup.tar /home/usuario/documentos/

# Crear archivo tar comprimido con gzip
tar -czvf backup.tar.gz /home/usuario/documentos/

# Crear archivo tar comprimido con bzip2
tar -cjvf backup.tar.bz2 /home/usuario/documentos/

# Extraer archivo tar
tar -xvf backup.tar

# Extraer archivo tar comprimido
tar -xzvf backup.tar.gz

# Listar contenido sin extraer
tar -tvf backup.tar

# Extraer archivos específicos
tar -xvf backup.tar archivo1.txt archivo2.txt

# Agregar archivos a un tar existente
tar -rvf backup.tar nuevos_archivos/

# Excluir archivos durante la creación
tar -cvf backup.tar --exclude='*.tmp' /home/usuario/
```

## Algoritmos de Compresión

### GZIP

Características:

- Compresión rápida
- Buena relación velocidad/tamaño
- Estándar en sistemas Unix/Linux

```bash
gzip archivo.txt         # Comprimir (reemplaza original)
gzip -k archivo.txt      # Comprimir manteniendo original
gzip -r directorio/      # Comprimir recursivamente
gunzip archivo.txt.gz    # Descomprimir
gzip -d archivo.txt.gz   # Descomprimir alternativo
gzip -t archivo.txt.gz   # Verificar integridad
```

### BZIP2

Características:

- Mayor compresión que gzip
- Más lento que gzip
- Mejor para archivos grandes

```bash
bzip2 archivo.txt        # Comprimir
bunzip2 archivo.txt.bz2  # Descomprimir
bzip2 -k archivo.txt     # Mantener original
bzip2 -t archivo.txt.bz2 # Verificar integridad
```

### XZ

Características:

- Mejor compresión que bzip2
- Más lento que bzip2
- Recomendado para archivos de distribución

```bash
xz archivo.txt           # Comprimir
unxz archivo.txt.xz      # Descomprimir
xz -k archivo.txt        # Mantener original
xz -t archivo.txt.xz     # Verificar integridad
```

## Herramientas de Archivo ZIP

### Comando zip

```bash
zip archivo.zip *.txt           # Crear archivo zip
zip -r directorio.zip directorio/ # Recursivo
zip -9 archivo.zip *.txt        # Máxima compresión
zip -e archivo.zip *.txt        # Con contraseña
zip -u archivo.zip nuevo.txt    # Actualizar archivo existente
```

### Comando unzip

```bash
unzip archivo.zip               # Extraer todo
unzip archivo.zip -d /destino/  # Extraer en directorio específico
unzip -l archivo.zip            # Listar contenido
unzip -t archivo.zip            # Verificar integridad
unzip archivo.zip archivo.txt   # Extraer archivo específico
```

## Herramientas Especializadas

### RAR

```bash
rar a archivo.rar *.txt         # Crear archivo rar
unrar x archivo.rar             # Extraer archivo rar
unrar l archivo.rar             # Listar contenido
```

### 7zip

```bash
7z a archivo.7z *.txt           # Crear archivo 7z
7z x archivo.7z                 # Extraer
7z l archivo.7z                 # Listar contenido
```

## Estrategias de Backup

### Backup Completo

```bash
# Backup completo del sistema
tar -czf backup_completo_$(date +%Y%m%d).tar.gz \
    --exclude='/proc' \
    --exclude='/sys' \
    --exclude='/tmp' \
    --exclude='/dev' \
    --exclude='/mnt' \
    --exclude='/media' \
    /

# Backup de directorios específicos
tar -czf backup_home_$(date +%Y%m%d).tar.gz /home/
tar -czf backup_etc_$(date +%Y%m%d).tar.gz /etc/
```

### Backup Incremental

```bash
# Primer backup completo
tar -czf backup_completo.tar.gz /home/usuario/

# Backups incrementales (archivos modificados)
find /home/usuario/ -newer backup_completo.tar.gz -type f | \
    tar -czf backup_incremental_$(date +%Y%m%d).tar.gz -T -
```

## Verificación de Integridad

### Checksums

```bash
# Crear checksums
md5sum archivo.tar.gz > archivo.md5
sha256sum archivo.tar.gz > archivo.sha256

# Verificar checksums
md5sum -c archivo.md5
sha256sum -c archivo.sha256
```

### Verificación de Archivos Comprimidos

```bash
# Verificar integridad sin extraer
gzip -t archivo.tar.gz
tar -tzf archivo.tar.gz > /dev/null
zip -T archivo.zip
```