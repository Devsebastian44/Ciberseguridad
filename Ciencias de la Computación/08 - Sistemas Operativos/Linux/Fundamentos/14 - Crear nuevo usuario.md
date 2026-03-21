# Comandos básicos para gestión de usuarios

## Crear usuario

```bash
# Crear usuario básico
useradd nombre_usuario

# Crear usuario con directorio home
useradd -m nombre_usuario

# Crear usuario con shell específico
useradd -m -s /bin/bash nombre_usuario

# Crear usuario con grupo primario
useradd -m -g grupo_primario nombre_usuario

# Crear usuario con grupos adicionales
useradd -m -G grupo1,grupo2 nombre_usuario

# Crear usuario con directorio home personalizado
useradd -m -d /home/custom_dir nombre_usuario

# Crear usuario con UID específico
useradd -m -u 1500 nombre_usuario

# Crear usuario con comentario
useradd -m -c "Nombre Completo" nombre_usuario

# Crear usuario completo
useradd -m -s /bin/bash -c "Juan Pérez" -G sudo,www-data juan
```

## Configurar contraseña

```bash
# Establecer contraseña
passwd nombre_usuario

# Forzar cambio de contraseña en próximo login
passwd -e nombre_usuario

# Deshabilitar contraseña
passwd -l nombre_usuario

# Habilitar contraseña
passwd -u nombre_usuario

# Eliminar contraseña
passwd -d nombre_usuario
```

## Modificar usuario existente

```bash
# Cambiar shell
usermod -s /bin/zsh nombre_usuario

# Agregar a grupos
usermod -a -G grupo1,grupo2 nombre_usuario

# Cambiar grupo primario
usermod -g nuevo_grupo nombre_usuario

# Cambiar directorio home
usermod -d /nuevo/home -m nombre_usuario

# Cambiar nombre de usuario
usermod -l nuevo_nombre nombre_actual

# Cambiar UID
usermod -u 1600 nombre_usuario

# Bloquear cuenta
usermod -L nombre_usuario

# Desbloquear cuenta
usermod -U nombre_usuario
```


# Archivos de configuración

## Archivo /etc/passwd

```bash
# Estructura: usuario:x:UID:GID:comentario:home:shell
root:x:0:0:root:/root:/bin/bash
juan:x:1000:1000:Juan Pérez:/home/juan:/bin/bash
```

## Archivo /etc/shadow

```bash
# Estructura: usuario:contraseña_hash:última_cambio:min_días:max_días:advertencia:inactivo:expiración
juan:$6$salt$hashedpassword:18900:0:99999:7:::
```

## Archivo /etc/group

```bash
# Estructura: grupo:x:GID:miembros
sudo:x:27:juan,maria
www-data:x:33:juan
```

## Archivo /etc/default/useradd

```bash
# Configuración por defecto para useradd
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```


# Configuración avanzada

## Plantillas de usuario (/etc/skel)

```bash
# Archivos que se copian al crear usuario
/etc/skel/.bashrc
/etc/skel/.bash_logout
/etc/skel/.profile

# Personalizar plantilla
cp archivo_config /etc/skel/
```

## Límites de usuario

```bash
# Configurar límites en /etc/security/limits.conf
usuario soft nofile 1024
usuario hard nofile 2048
@grupo soft nproc 100
@grupo hard nproc 200

# Ver límites actuales
ulimit -a

# Configurar límites temporalmente
ulimit -n 2048
```

## Configuración de login

```bash
# Archivo /etc/login.defs
MAIL_DIR        /var/mail
FAILLOG_ENAB    yes
LOG_UNKFAIL_ENAB    no
LOG_OK_LOGINS    no
SYSLOG_SU_ENAB    yes
SYSLOG_SG_ENAB    yes
CONSOLE_GROUPS    floppy:audio:cdrom
```


# Gestión de grupos

## Crear y modificar grupos

```bash
# Crear grupo
groupadd nombre_grupo

# Crear grupo con GID específico
groupadd -g 1500 nombre_grupo

# Modificar grupo
groupmod -n nuevo_nombre nombre_actual

# Cambiar GID
groupmod -g 1600 nombre_grupo

# Eliminar grupo
groupdel nombre_grupo
```

## Gestión de miembros

```bash
# Agregar usuario a grupo
usermod -a -G grupo usuario
gpasswd -a usuario grupo

# Eliminar usuario de grupo
gpasswd -d usuario grupo

# Establecer administrador de grupo
gpasswd -A admin_user grupo

# Listar miembros de grupo
getent group nombre_grupo
```


# Eliminar usuarios

## Eliminar usuario

```bash
# Eliminar usuario (conservar home)
userdel nombre_usuario

# Eliminar usuario y directorio home
userdel -r nombre_usuario

# Eliminar usuario y todos sus archivos
userdel -r -f nombre_usuario

# Verificar archivos huérfanos
find / -nouser -o -nogroup 2>/dev/null
```

## Limpieza manual

```bash
# Buscar archivos del usuario
find / -user nombre_usuario 2>/dev/null

# Buscar procesos del usuario
ps -u nombre_usuario

# Limpiar crontab
crontab -r -u nombre_usuario

# Limpiar mail
rm -rf /var/mail/nombre_usuario
```