## Tipos de Sistemas de Archivos

El sistema de archivos en Linux determina cómo se organizan y almacenan los datos en el disco.

### Ext (Extended File System)

- **Ext**: primer sistema de archivos de Linux, obsoleto por limitaciones
- **Ext2**: soporta hasta 2 TB de almacenamiento
- **Ext3**: mejora de Ext2 con compatibilidad hacia atrás, sin soporte de snapshots
- **Ext4**: rápido y eficiente, soporta archivos grandes. **Recomendado por defecto en Linux**

### Otros sistemas de archivos

- **JFS**: desarrollado por IBM, problemas de corrupción
- **XFS**: creado en 2001 por Silicon Graphics, lento con archivos pequeños
- **Btrfs**: sistema B-Tree de Oracle, diseñado como reemplazo de Ext
- **Swap**: no es un sistema de archivos real, usado como respaldo de RAM

---

## Estructura de Directorios en Linux (FHS)

La estructura sigue el estándar **Filesystem Hierarchy Standard (FHS)**:

|Directorio|Descripción|
|---|---|
|`/`|Raíz del sistema de archivos|
|`/bin`|Comandos básicos (`ls`, `mv`)|
|`/boot`|Archivos del cargador de arranque|
|`/dev`|Dispositivos físicos (USB, DVD)|
|`/etc`|Configuraciones de paquetes|
|`/home`|Carpeta personal de cada usuario|
|`/lib`|Bibliotecas de paquetes|
|`/media`|Dispositivos externos montados|
|`/mnt`|Punto de montaje para redes/sistemas|
|`/opt`|Paquetes opcionales|
|`/root`|Carpeta home del usuario root|
|`/sbin`|Binarios exclusivos de root|
|`/srv`|Datos servidos por el sistema|
|`/tmp`|Archivos temporales|
|`/usr`|Utilidades y archivos compartidos|
|`/var`|Registros y datos variables|
|`/proc`|Información del sistema creada en memoria por el kernel|

---
