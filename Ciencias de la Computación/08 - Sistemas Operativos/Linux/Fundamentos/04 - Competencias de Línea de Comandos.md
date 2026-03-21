# Introducción al Shell

El shell es la interfaz de línea de comandos que permite interactuar con el sistema operativo Linux mediante texto.

## Shells populares

- **Bash** (Bourne Again Shell): Shell por defecto en la mayoría de distribuciones
- **Zsh** (Z Shell): Shell avanzado con características adicionales
- **Fish** (Friendly Interactive Shell): Shell fácil de usar
- **Csh** (C Shell): Shell con sintaxis similar a C

## Estructura básica de comandos

```bash
comando [opciones] [argumentos]
```

## Comandos básicos de navegación

### `pwd` - Print Working Directory

```bash
pwd
# Muestra el directorio actual
```

### `cd` - Change Directory

```bash
cd /home/usuario          # Cambiar a directorio específico
cd ..                     # Subir un nivel
cd ~                      # Ir al directorio home
cd -                      # Ir al directorio anterior
```

### `ls` - List

```bash
ls                        # Listar archivos del directorio actual
ls -l                     # Listado detallado
ls -la                    # Incluir archivos ocultos
ls -lh                    # Tamaños en formato legible
```

## Comandos de manipulación de archivos

### `touch` - Crear archivos vacíos

```bash
touch archivo.txt
touch archivo1.txt archivo2.txt
```

### `mkdir` - Crear directorios

```bash
mkdir directorio
mkdir -p ruta/completa/directorio    # Crear directorios padre si no existen
```

### `cp` - Copiar archivos

```bash
cp archivo.txt copia.txt
cp archivo.txt /ruta/destino/
cp -r directorio/ /ruta/destino/     # Copiar directorios recursivamente
```

### `mv` - Mover/renombrar archivos

```bash
mv archivo.txt nuevo_nombre.txt
mv archivo.txt /ruta/destino/
```

### `rm` - Eliminar archivos

```bash
rm archivo.txt
rm -r directorio/                    # Eliminar directorios recursivamente
rm -f archivo.txt                    # Forzar eliminación
```

## Comandos de visualización de contenido

### `cat` - Mostrar contenido completo

```bash
cat archivo.txt
cat archivo1.txt archivo2.txt       # Concatenar archivos
```

### `less` y `more` - Visualizar por páginas

```bash
less archivo.txt
more archivo.txt
```

### `head` - Mostrar primeras líneas

```bash
head archivo.txt                     # Primeras 10 líneas
head -n 5 archivo.txt               # Primeras 5 líneas
```

### `tail` - Mostrar últimas líneas

```bash
tail archivo.txt                     # Últimas 10 líneas
tail -n 5 archivo.txt               # Últimas 5 líneas
tail -f archivo.log                 # Seguir archivo en tiempo real
```

## Comandos de búsqueda

### `find` - Buscar archivos y directorios

```bash
find /ruta -name "*.txt"            # Buscar archivos .txt
find /ruta -type d                  # Buscar solo directorios
find /ruta -type f -size +1M        # Buscar archivos mayores a 1MB
```

### `locate` - Búsqueda rápida

```bash
locate archivo.txt
updatedb                            # Actualizar base de datos
```

### `which` - Ubicación de comandos

```bash
which ls
which python
```

## Comandos de información del sistema

### `ps` - Procesos en ejecución

```bash
ps aux                              # Todos los procesos
ps aux | grep proceso               # Buscar proceso específico
```

### `top` - Monitor de procesos en tiempo real

```bash
top
htop                                # Versión mejorada (si está instalada)
```

### `df` - Espacio en disco

```bash
df -h                               # Formato legible
```

### `du` - Uso de disco por directorio

```bash
du -h directorio/
du -sh directorio/                  # Resumen
```

### `free` - Memoria disponible

```bash
free -h                             # Formato legible
```

## Atajos de teclado útiles

- **Ctrl + C**: Interrumpir proceso actual
- **Ctrl + Z**: Suspender proceso
- **Ctrl + L**: Limpiar pantalla
- **Tab**: Autocompletado
- **Ctrl + R**: Buscar en historial
- **Ctrl + A**: Ir al inicio de línea
- **Ctrl + E**: Ir al final de línea