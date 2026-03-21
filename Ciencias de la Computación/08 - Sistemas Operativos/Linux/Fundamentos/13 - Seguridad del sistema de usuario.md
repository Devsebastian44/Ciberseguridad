# Principios básicos de seguridad

## Conceptos fundamentales

- **Principio de menor privilegio**: Otorgar solo los permisos mínimos necesarios
- **Defensa en profundidad**: Múltiples capas de seguridad
- **Autenticación**: Verificar identidad del usuario
- **Autorización**: Controlar acceso a recursos
- **Auditoría**: Registrar y monitorear actividades

## Vectores de amenaza comunes

- Acceso no autorizado
- Escalación de privilegios
- Inyección de código
- Ataques de fuerza bruta
- Malware y rootkits


# Seguridad del sistema

## Actualizaciones de seguridad

```bash
# Debian/Ubuntu
apt update && apt upgrade
apt list --upgradable

# Red Hat/CentOS
yum update
yum updateinfo list security

# Actualizaciones automáticas
unattended-upgrades  # Ubuntu
yum-cron            # CentOS
```

## Configuración del kernel

```bash
# Parámetros de seguridad del kernel
/etc/sysctl.conf

# Ejemplos de configuración
net.ipv4.ip_forward=0                    # Deshabilitar forwarding
net.ipv4.conf.all.accept_redirects=0     # No aceptar redirects
net.ipv4.conf.all.send_redirects=0       # No enviar redirects
net.ipv4.conf.all.accept_source_route=0  # No aceptar source routing
```

## Montaje seguro de sistemas de archivos

```bash
# Opciones de montaje en /etc/fstab
/dev/sda1 /tmp ext4 defaults,nodev,nosuid,noexec 0 2

# Opciones de seguridad:
# nodev   - No interpretar dispositivos
# nosuid  - No permitir bits SUID/SGID
# noexec  - No permitir ejecución de binarios
```


# Autenticación y autorización

## Configuración de contraseñas

```bash
# Política de contraseñas
/etc/login.defs

# Configuración PAM
/etc/pam.d/common-password

# Forzar cambio de contraseña
chage -d 0 usuario

# Información de expiración
chage -l usuario

# Configurar expiración
chage -M 90 -m 7 -W 14 usuario
```

## Sudo y privilegios

```bash
# Configurar sudo
visudo

# Ejemplos de configuración
usuario ALL=(ALL:ALL) ALL
%admin ALL=(ALL) ALL
usuario ALL=(ALL) NOPASSWD: /bin/systemctl restart apache2

# Usar sudo
sudo comando
sudo -u usuario comando
sudo -i  # Cambiar a root
```

## Autenticación de dos factores

```bash
# Instalar Google Authenticator
apt install libpam-google-authenticator

# Configurar para usuario
google-authenticator

# Configurar PAM
/etc/pam.d/sshd
auth required pam_google_authenticator.so
```


# Monitoreo y auditoría

## Logs del sistema

```bash
# Logs principales
/var/log/auth.log       # Autenticación
/var/log/syslog         # Sistema general
/var/log/kern.log       # Kernel
/var/log/apache2/       # Apache
/var/log/nginx/         # Nginx

# Herramientas de análisis
grep "Failed password" /var/log/auth.log
journalctl -u sshd
tail -f /var/log/syslog
```

## Auditoría del sistema (auditd)

```bash
# Instalar auditd
apt install auditd

# Configuración
/etc/audit/auditd.conf
/etc/audit/rules.d/

# Reglas de auditoría
auditctl -w /etc/passwd -p wa -k passwd_changes
auditctl -w /etc/shadow -p wa -k shadow_changes

# Buscar eventos
ausearch -k passwd_changes
aureport --auth
```

## Detección de intrusos

```bash
# Fail2ban
apt install fail2ban

# Configuración
/etc/fail2ban/jail.conf
/etc/fail2ban/jail.local

# Estado de fail2ban
fail2ban-client status
fail2ban-client status sshd
```


# Hardening del sistema

## Configuración SSH segura

```bash
# /etc/ssh/sshd_config
Port 2222                      # Cambiar puerto por defecto
PermitRootLogin no             # Deshabilitar login root
PasswordAuthentication no      # Solo autenticación por llaves
AllowUsers usuario1 usuario2   # Usuarios permitidos
Protocol 2                     # Usar protocolo SSH v2
```

## Deshabilitación de servicios innecesarios

```bash
# Listar servicios activos
systemctl list-units --type=service --state=active

# Deshabilitar servicio
systemctl disable nombre_servicio
systemctl stop nombre_servicio

# Puertos abiertos
netstat -tuln
ss -tuln
```

## Control de acceso obligatorio (SELinux/AppArmor)

SELinux:

```bash
# Estado de SELinux
getenforce
sestatus

# Configurar modo
setenforce 0  # Permisivo
setenforce 1  # Enforcing

# Contextos de archivos
ls -Z archivo
chcon -t httpd_exec_t archivo
```

AppArmor:

```bash
# Estado de AppArmor
apparmor_status

# Perfiles disponibles
ls /etc/apparmor.d/

# Habilitar perfil
apparmor_parser -r /etc/apparmor.d/usr.sbin.apache2
```