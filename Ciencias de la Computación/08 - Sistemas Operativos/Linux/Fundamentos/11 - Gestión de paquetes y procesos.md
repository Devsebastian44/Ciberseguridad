# Gestión de paquetes

## Sistemas de paquetes principales

Debian/Ubuntu (APT):

```bash
# Actualizar lista de paquetes
apt update

# Actualizar paquetes instalados
apt upgrade

# Instalar un paquete
apt install nombre_paquete

# Desinstalar un paquete
apt remove nombre_paquete

# Desinstalar completamente (incluyendo configuración)
apt purge nombre_paquete

# Buscar paquetes
apt search término_búsqueda

# Información de un paquete
apt show nombre_paquete

# Listar paquetes instalados
apt list --installed
```

Red Hat/CentOS/Fedora (YUM/DNF):

```bash
# Actualizar paquetes
yum update  # o dnf update

# Instalar un paquete
yum install nombre_paquete

# Desinstalar un paquete
yum remove nombre_paquete

# Buscar paquetes
yum search término_búsqueda

# Información de un paquete
yum info nombre_paquete

# Listar paquetes instalados
yum list installed
```

# Gestión de repositorios

APT (Debian/Ubuntu):

```bash
# Archivos de repositorios
/etc/apt/sources.list
/etc/apt/sources.list.d/

# Agregar repositorio
add-apt-repository ppa:repositorio/nombre

# Llaves GPG
apt-key add archivo_llave.gpg
```

YUM/DNF (Red Hat):

```bash
# Archivos de repositorios
/etc/yum.repos.d/

# Listar repositorios
yum repolist

# Habilitar/deshabilitar repositorio
yum-config-manager --enable repositorio
yum-config-manager --disable repositorio
```


# Gestión de procesos

## Visualización de procesos

```bash
# Listar procesos activos
ps aux

# Árbol de procesos
pstree

# Procesos en tiempo real
top

# Versión mejorada de top
htop

# Información detallada de procesos
ps -ef

# Procesos de un usuario específico
ps -u usuario
```

## Control de procesos

```bash
# Ejecutar proceso en segundo plano
comando &

# Listar trabajos en segundo plano
jobs

# Traer trabajo al primer plano
fg %número_trabajo

# Enviar trabajo al segundo plano
bg %número_trabajo

# Terminar proceso por PID
kill PID

# Terminar proceso por nombre
killall nombre_proceso

# Forzar terminación de proceso
kill -9 PID

# Terminar proceso de forma elegante
kill -15 PID
```

## Señales del sistema

```bash
# Señales principales
SIGTERM (15)  # Terminación normal
SIGKILL (9)   # Terminación forzada
SIGHUP (1)    # Reiniciar proceso
SIGSTOP (19)  # Pausar proceso
SIGCONT (18)  # Continuar proceso pausado

# Enviar señal específica
kill -SIGNAL PID
```

## Prioridades de procesos

```bash
# Ejecutar con prioridad específica
nice -n 10 comando

# Cambiar prioridad de proceso activo
renice 5 PID

# Ver prioridades
ps -l
```

## Servicios del sistema (systemd)

```bash
# Listar servicios
systemctl list-units --type=service

# Estado de un servicio
systemctl status nombre_servicio

# Iniciar servicio
systemctl start nombre_servicio

# Detener servicio
systemctl stop nombre_servicio

# Reiniciar servicio
systemctl restart nombre_servicio

# Habilitar servicio al inicio
systemctl enable nombre_servicio

# Deshabilitar servicio al inicio
systemctl disable nombre_servicio

# Recargar configuración
systemctl daemon-reload
```