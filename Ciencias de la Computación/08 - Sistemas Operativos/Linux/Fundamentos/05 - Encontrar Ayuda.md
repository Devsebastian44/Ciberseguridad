# Fuentes de Documentación

## Páginas del Manual (man)

Uso básico:

```bash
man comando              # Manual del comando
man -k palabra_clave     # Buscar en manuales
man 5 passwd            # Sección específica
```

Secciones del manual:

1. Comandos de usuario
2. Llamadas al sistema
3. Funciones de biblioteca
4. Archivos especiales
5. Formatos de archivo
6. Juegos
7. Convenciones
8. Comandos de administración

Navegación en man:

- `Espacio`: Página siguiente
- `b`: Página anterior
- `/texto`: Buscar texto
- `q`: Salir

## Comando info

```bash
info comando             # Documentación info
info --help             # Ayuda del comando info
```

## Ayuda integrada

```bash
comando --help          # Ayuda rápida
comando -h              # Versión corta
which comando           # Ubicación del comando
whereis comando         # Ubicación y manual
```

## Documentación del Sistema

### Directorio /usr/share/doc

```bash
ls /usr/share/doc/      # Documentación de paquetes
cd /usr/share/doc/apache2/
```

### Archivos de configuración

```bash
ls /etc/                # Archivos de configuración
man 5 fstab            # Manual de formato de archivo
```

## Recursos Online

### Sitios web oficiales

- **kernel.org**: Documentación del kernel
- **tldp.org**: The Linux Documentation Project
- **debian.org/doc**: Documentación de Debian
- **ubuntu.com/server/docs**: Documentación de Ubuntu

### Comunidades y Foros

- **Stack Overflow**: Preguntas específicas
- **Reddit**: r/linux, r/linuxquestions
- **LinuxQuestions.org**: Foro especializado
- **Ask Ubuntu**: Preguntas sobre Ubuntu

## Comandos de Diagnóstico

### Información del sistema

```bash
uname -a                # Información del kernel
lsb_release -a          # Información de distribución
hostnamectl             # Información del host
```

### Procesos y recursos


```bash
ps aux                  # Procesos en ejecución
top                     # Monitor de procesos
htop                    # Monitor mejorado
df -h                   # Uso de disco
free -h                 # Uso de memoria
```

### Logs del sistema


```bash
journalctl              # Logs systemd
tail -f /var/log/syslog # Seguir log del sistema
dmesg                   # Mensajes del kernel
```

## Estrategias de Resolución de Problemas

### Metodología sistemática

1. **Identificar el problema**
2. **Recopilar información**
3. **Analizar logs**
4. **Buscar documentación**
5. **Probar soluciones**
6. **Documentar la solución**

### Herramientas de diagnóstico

```bash
strace comando          # Rastrear llamadas al sistema
ldd binario            # Dependencias de biblioteca
file archivo           # Tipo de archivo
```