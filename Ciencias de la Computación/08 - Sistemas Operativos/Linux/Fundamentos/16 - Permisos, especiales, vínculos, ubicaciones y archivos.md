# Permisos especiales

## Sticky bit

```bash
# Aplicar sticky bit
chmod +t directorio/
chmod 1755 directorio/

# Ejemplo típico: /tmp
ls -ld /tmp
# drwxrwxrwt 10 root root 4096 ene 15 10:30 /tmp

# Función: Solo el propietario puede eliminar archivos
# Útil para directorios compartidos
```

## Setuid bit

```bash
# Aplicar setuid
chmod u+s archivo
chmod 4755 archivo

# Ejemplo: comando passwd
ls -l /usr/bin/passwd
# -rwsr-xr-x 1 root root 68208 jul 15 2021 /usr/bin/passwd

# Función: Se ejecuta con privilegios del propietario
# Peligroso si se mal usa
```

## Setgid bit

```bash
# Aplicar setgid a archivo
chmod g+s archivo
chmod 2755 archivo

# Aplicar setgid a directorio
chmod g+s directorio/
chmod 2755 directorio/

# Función en archivos: Se ejecuta con privilegios del grupo
# Función en directorios: Archivos nuevos heredan el grupo
```

## Combinación de bits especiales

```bash
# Combinaciones posibles
chmod 7755 archivo  # setuid + setgid + sticky
chmod 6755 archivo  # setuid + setgid
chmod 5755 archivo  # setuid + sticky
chmod 3755 archivo  # setgid + sticky

# Visualización
ls -l archivo
# Setuid: s en posición de x del usuario
# Setgid: s en posición de x del grupo
# Sticky: t en posición de x de otros
```


# Listas de control de acceso (ACL)

## Comandos básicos de ACL

```bash
# Ver ACL
getfacl archivo

# Establecer ACL
setfacl -m u:usuario:rwx archivo

# Establecer ACL para grupo
setfacl -m g:grupo:r-x archivo

# Establecer ACL por defecto
setfacl -d -m u:usuario:rwx directorio/

# Eliminar ACL específica
setfacl -x u:usuario archivo

# Eliminar todas las ACL
setfacl -b archivo

# Aplicar ACL recursivamente
setfacl -R -m u:usuario:rwx directorio/
```

## Ejemplos prácticos de ACL

```bash
# Dar acceso a usuario específico
setfacl -m u:juan:rw- archivo.txt

# Dar acceso a grupo específico
setfacl -m g:desarrolladores:rwx proyecto/

# Configurar ACL por defecto para directorio
setfacl -d -m u:juan:rwx proyectos/
setfacl -d -m g:equipo:r-x proyectos/

# Copiar ACL entre archivos
getfacl archivo1 | setfacl --set-file=- archivo2
```


# Vínculos (Enlaces)

## Enlaces duros (Hard links)

```bash
# Crear enlace duro
ln archivo enlace_duro

# Características:
# - Mismo inode que el archivo original
# - No se puede distinguir original de enlace
# - Solo funciona en mismo sistema de archivos
# - No funciona con directorios

# Ver inodes
ls -li archivo enlace_duro

# Contar enlaces duros
ls -l archivo  # Segunda columna muestra número de enlaces
```

## Enlaces simbólicos (Soft links)

```bash
# Crear enlace simbólico
ln -s archivo enlace_simbolico

# Enlace a directorio
ln -s /path/to/directory enlace_directorio

# Enlace absoluto
ln -s /home/usuario/archivo enlace_absoluto

# Enlace relativo
ln -s ../archivo enlace_relativo

# Características:
# - Diferente inode
# - Apunta al nombre del archivo
# - Funciona entre sistemas de archivos
# - Funciona con directorios
# - Se rompe si se elimina el original
```

## Gestión de enlaces

```bash
# Encontrar enlaces duros
find /path -samefile archivo

# Encontrar enlaces simbólicos
find /path -type l

# Encontrar enlaces simbólicos rotos
find /path -type l -exec test ! -e {} \; -print

# Eliminar enlace simbólico
rm enlace_simbolico
unlink enlace_simbolico

# Ver destino de enlace simbólico
readlink enlace_simbolico
ls -l enlace_simbolico
```


# Sistema de archivos y ubicaciones

## Jerarquía estándar (FHS)

```bash
# Directorios principales
/                    # Raíz del sistema
/bin                # Binarios esenciales
/boot               # Archivos de arranque
/dev                # Dispositivos
/etc                # Configuración del sistema
/home               # Directorios de usuarios
/lib                # Bibliotecas esenciales
/media              # Medios extraíbles
/mnt                # Montajes temporales
/opt                # Software opcional
/proc               # Sistema de archivos virtual
/root               # Directorio del superusuario
/run                # Datos variables en tiempo de ejecución
/sbin               # Binarios del sistema
/srv                # Datos de servicios
/sys                # Sistema de archivos virtual
/tmp                # Archivos temporales
/usr                # Recursos de usuario
/var                # Datos variables
```

## Subdirectorios importantes

```bash
# /usr - Recursos de usuario
/usr/bin            # Binarios de usuario
/usr/sbin           # Binarios de administración
/usr/lib            # Bibliotecas
/usr/local          # Software instalado localmente
/usr/share          # Datos compartidos
/usr/src            # Código fuente

# /var - Datos variables
/var/log            # Archivos de log
/var/cache          # Caché de aplicaciones
/var/lib            # Datos de aplicaciones
/var/mail           # Correo electrónico
/var/spool          # Colas de trabajos
/var/tmp            # Archivos temporales persistentes
/var/www            # Contenido web
```

## Archivos de configuración importantes

```bash
# Sistema
/etc/passwd         # Información de usuarios
/etc/shadow         # Contraseñas encriptadas
/etc/group          # Información de grupos
/etc/hosts          # Resolución local de nombres
/etc/hostname       # Nombre del sistema
/etc/resolv.conf    # Configuración DNS
/etc/fstab          # Tabla de sistemas de archivos

# Red
/etc/network/interfaces     # Configuración de red (Debian)
/etc/sysconfig/network-scripts/  # Red (Red Hat)
/etc/ssh/sshd_config       # Configuración SSH
/etc/iptables/rules.v4     # Reglas de firewall

# Servicios
/etc/systemd/system/       # Servicios systemd
/etc/init.d/              # Scripts de inicio (SysV)
/etc/cron.d/              # Tareas programadas
/etc/logrotate.d/         # Rotación de logs
```


# Montaje de sistemas de archivos

## Comandos de montaje

```bash
# Montar sistema de archivos
mount /dev/sda1 /mnt/disco

# Montar con opciones específicas
mount -t ext4 -o rw,noatime /dev/sda1 /mnt/disco

# Desmontar
umount /mnt/disco

# Montaje de red (NFS)
mount -t nfs servidor:/ruta /mnt/nfs

# Montaje de red (SMB/CIFS)
mount -t cifs //servidor/recurso /mnt/smb -o username=usuario
```

## Archivo /etc/fstab

```bash
# Estructura: dispositivo punto_montaje tipo opciones dump pass
/dev/sda1 / ext4 defaults 0 1
/dev/sda2 /home ext4 defaults 0 2
/dev/sda3 swap swap defaults 0 0
tmpfs /tmp tmpfs defaults,noatime,mode=1777 0 0

# Opciones comunes:
# defaults: rw,suid,dev,exec,auto,nouser,async
# noatime: no actualizar tiempo de acceso
# nodev: no interpretar dispositivos
# nosuid: no permitir bits suid/sgid
# noexec: no permitir ejecución
```

## Información de sistemas de archivos

```bash
# Mostrar montajes activos
mount
df -h

# Información detallada
findmnt
lsblk

# Uso de espacio
du -sh directorio/
du -h --max-depth=1 directorio/

# Espacio libre
df -h
df -i  # Inodes
```


# Cuotas de disco

## Configuración de cuotas

```bash
# Habilitar cuotas en /etc/fstab
/dev/sda1 /home ext4 defaults,usrquota,grpquota 0 2

# Crear archivos de cuotas
quotacheck -cum /home

# Activar cuotas
quotaon /home

# Configurar cuotas para usuario
edquota usuario

# Configurar cuotas para grupo
edquota -g grupo
```

## Gestión de cuotas

```bash
# Ver cuotas de usuario
quota usuario

# Ver cuotas de grupo
quota -g grupo

# Reporte de cuotas
repquota /home

# Establecer cuotas directamente
setquota usuario 100000 110000 1000 1100 /home

# Desactivar cuotas
quotaoff /home
```


# Casos prácticos y resolución de problemas

## Configuración de directorio compartido

```bash
# Crear directorio compartido
mkdir /shared/proyecto
chown :equipo /shared/proyecto
chmod 2775 /shared/proyecto

# Configurar ACL por defecto
setfacl -d -m g:equipo:rwx /shared/proyecto
setfacl -d -m o::r-x /shared/proyecto

# Verificar configuración
getfacl /shared/proyecto
```

## Migración de datos preservando permisos

```bash
# Copiar preservando permisos
cp -p archivo destino
cp -a directorio/ destino/

# Rsync preservando todo
rsync -avH origen/ destino/

# Tar preservando permisos
tar -czpf archivo.tar.gz directorio/
tar -xzpf archivo.tar.gz
```

## Auditoría de permisos

```bash
# Encontrar archivos con permisos 777
find /path -type f -perm 777

# Encontrar archivos con setuid
find /path -type f -perm -4000

# Encontrar archivos sin propietario
find /path -nouser -o -nogroup

# Encontrar archivos modificados recientemente
find /path -type f -mtime -7

# Verificar permisos de archivos críticos
ls -l /etc/passwd /etc/shadow /etc/sudoers
```