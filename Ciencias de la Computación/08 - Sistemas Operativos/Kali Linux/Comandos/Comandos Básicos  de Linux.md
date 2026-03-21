## Navegación y Gestión de Directorios

```bash
pwd                          # Directorio actual
ls                           # Listar archivos
ls -la                       # Lista detallada incluyendo ocultos
ls -alh                      # Lista con tamaños legibles

cd /ruta/del/directorio      # Cambiar directorio
cd ..                        # Directorio padre
cd ~                         # Home del usuario
cd -                         # Directorio anterior

mkdir nombre_directorio
mkdir -p ruta/completa/dir   # Crear directorios padre si no existen

rmdir nombre_directorio      # Eliminar directorio vacío
rm -rf nombre_directorio     # Eliminar recursivamente
```

---

## Gestión de Archivos

```bash
touch archivo.txt archivo2.txt         # Crear archivos
cp origen destino                      # Copiar archivo
cp -r dir_origen dir_destino           # Copia recursiva

mv origen nuevo_nombre                 # Renombrar
mv archivo /nueva/ruta/                # Mover

rm archivo                             # Eliminar
rm -f archivo                          # Forzar eliminación
rm -rf directorio                      # Eliminar recursivamente
```

---

## Visualización y Edición de Contenido

```bash
cat archivo.txt                        # Mostrar contenido
less archivo.txt                       # Paginado
head archivo.txt                       # Primeras 10 líneas
tail archivo.txt                       # Últimas 10 líneas
tail -f archivo.txt                    # Seguimiento en tiempo real

nano archivo.txt                       # Editor básico
vim archivo.txt                        # Editor avanzado
```

---

## Información del Sistema

```bash
df -h                                  # Espacio en disco
free -h                                # Memoria
ps aux                                 # Procesos
top                                    # Monitor en tiempo real
htop                                   # Monitor avanzado

ping google.com                        # Conectividad
hostname                               # Nombre del host

who                                    # Usuarios conectados
whoami                                 # Usuario actual
```

---

## Gestión de Paquetes

```bash
apt-get install paquete                # Instalar
apt install paquete                    # Versión corta

apt-get update                         # Actualizar repositorios
apt-get upgrade                        # Actualizar paquetes

apt-get remove paquete                 # Eliminar
apt-get purge paquete                  # Eliminar con configuraciones
```

---

## Compresión y Descompresión

```bash
zip archivo.zip archivos               # Comprimir
tar -czf archivo.tar.gz directorio/    # Comprimir tar.gz

unzip archivo.zip                      # Descomprimir zip
tar -xzf archivo.tar.gz                # Descomprimir tar.gz
```

---

## Utilidades Adicionales

```bash
comando --help                         # Ayuda rápida
man comando                            # Manual completo

clear                                  # Limpiar terminal

reboot                                 # Reiniciar
shutdown -h now                        # Apagar
shutdown -r now                        # Reiniciar

passwd                                 # Cambiar contraseña
```

---
