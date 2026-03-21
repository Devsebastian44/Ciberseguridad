# Introducción al hardware en Linux

Linux interactúa directamente con el hardware de la computadora a través del kernel. Entender cómo Linux detecta, configura y gestiona el hardware es fundamental para cualquier administrador de sistemas.

## Arquitectura del sistema

### Componentes principales

- **CPU (Procesador)**: Ejecuta instrucciones y procesa datos
- **RAM (Memoria)**: Almacenamiento temporal de datos y programas
- **Almacenamiento**: Discos duros, SSD, dispositivos de almacenamiento
- **Dispositivos de entrada/salida**: Teclado, mouse, monitor, impresoras
- **Placa base**: Conecta todos los componentes

### El kernel y el hardware

El kernel de Linux actúa como intermediario entre el software y el hardware:

- **Drivers**: Controladores que permiten al kernel comunicarse con dispositivos específicos
- **Módulos**: Código cargable que extiende la funcionalidad del kernel
- **Interrupciones**: Mecanismo para que el hardware comunique eventos al kernel


# Comandos para inspeccionar hardware

## Información general del sistema


```bash
# Información general del sistema
uname -a

# Información detallada del hardware
lshw

# Información del procesador
lscpu

# Información de la memoria
free -h

# Información del sistema
dmidecode
```

## Dispositivos conectados

```bash
# Listar dispositivos PCI
lspci

# Listar dispositivos USB
lsusb

# Listar dispositivos de bloque
lsblk

# Información de discos
fdisk -l
```

## Información específica de hardware

```bash
# Información de la CPU
cat /proc/cpuinfo

# Información de la memoria
cat /proc/meminfo

# Información de particiones
cat /proc/partitions

# Estado de los módulos del kernel
lsmod

# Información de dispositivos
cat /proc/devices
```


# Gestión de módulos del kernel

## Comandos básicos

```bash
# Cargar un módulo
modprobe nombre_modulo

# Descargar un módulo
modprobe -r nombre_modulo

# Información de un módulo
modinfo nombre_modulo

# Dependencias de módulos
depmod
```

## Configuración persistente

```bash
# Archivo de configuración de módulos
/etc/modules

# Configuración de parámetros de módulos
/etc/modprobe.d/
```


# Directorios importantes del sistema

## Sistema de archivos /proc

```bash
# Información del sistema en tiempo real
/proc/cpuinfo
/proc/meminfo
/proc/version
/proc/filesystems
```

## Sistema de archivos /sys

```bash
# Interfaz moderna para el kernel
/sys/block/      # Dispositivos de bloque
/sys/class/      # Clases de dispositivos
/sys/devices/    # Jerarquía de dispositivos
```

## Directorio /dev

```bash
# Archivos de dispositivos
/dev/sda1        # Primera partición del primer disco
/dev/tty1        # Terminal virtual
/dev/null        # Dispositivo nulo
/dev/zero        # Dispositivo de ceros
```