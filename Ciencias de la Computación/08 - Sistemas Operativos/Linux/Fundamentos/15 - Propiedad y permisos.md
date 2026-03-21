# Conceptos básicos

## Tipos de permisos

- **r (read)**: Permiso de lectura
- **w (write)**: Permiso de escritura
- **x (execute)**: Permiso de ejecución

## Categorías de usuarios

- **u (user/owner)**: Propietario del archivo
- **g (group)**: Grupo propietario
- **o (others)**: Otros usuarios


# Visualización de permisos

## Comando ls

```bash
# Listar permisos detallados
ls -l archivo

# Ejemplo de salida:
# -rwxr-xr-- 1 usuario grupo 1024 ene 15 10:30 archivo
# │││││││││
# │││││││└─ Otros: lectura
# ││││││└── Otros: no escritura
# │││││└─── Otros: no ejecución
# ││││└──── Grupo: lectura
# │││└───── Grupo: no escritura
# ││└────── Grupo: ejecución
# │└─────── Usuario: lectura
# └──────── Usuario: escritura y ejecución
```

## Interpretación de permisos

```bash
# Primer carácter indica tipo:
# - : archivo regular
# d : directorio
# l : enlace simbólico
# c : dispositivo de caracteres
# b : dispositivo de bloque
# s : socket
# p : pipe (FIFO)

# Siguientes 9 caracteres: permisos
# rwx rwx rwx
# ┬─┬ ┬─┬ ┬─┬
# │ │ │ │ │ └─ Otros
# │ │ │ └─────── Grupo
# │ └─────────── Usuario
```


# Cambio de permisos

## Método simbólico

```bash
# Agregar permisos
chmod u+x archivo         # Agregar ejecución al usuario
chmod g+w archivo         # Agregar escritura al grupo
chmod o+r archivo         # Agregar lectura a otros
chmod a+x archivo         # Agregar ejecución a todos

# Quitar permisos
chmod u-x archivo         # Quitar ejecución al usuario
chmod g-w archivo         # Quitar escritura al grupo
chmod o-r archivo         # Quitar lectura a otros

# Establecer permisos exactos
chmod u=rwx archivo       # Usuario: lectura, escritura, ejecución
chmod g=r archivo         # Grupo: solo lectura
chmod o= archivo          # Otros: sin permisos

# Combinaciones
chmod u+x,g-w,o=r archivo
chmod a-x archivo
```

## Método numérico (octal)

```bash
# Valores numéricos:
# r = 4, w = 2, x = 1

# Ejemplos comunes:
chmod 755 archivo    # rwxr-xr-x
chmod 644 archivo    # rw-r--r--
chmod 600 archivo    # rw-------
chmod 777 archivo    # rwxrwxrwx
chmod 000 archivo    # ---------

# Cálculo:
# Usuario: rwx = 4+2+1 = 7
# Grupo: r-x = 4+0+1 = 5
# Otros: r-x = 4+0+1 = 5
# Resultado: 755
```

## Permisos recursivos

```bash
# Aplicar permisos recursivamente
chmod -R 755 directorio/

# Solo directorios
find directorio/ -type d -exec chmod 755 {} \;

# Solo archivos
find directorio/ -type f -exec chmod 644 {} \;
```


# Cambio de propiedad

## Comando chown

```bash
# Cambiar propietario
chown usuario archivo

# Cambiar grupo
chown :grupo archivo

# Cambiar propietario y grupo
chown usuario:grupo archivo

# Cambiar recursivamente
chown -R usuario:grupo directorio/

# Preservar enlaces simbólicos
chown -h usuario archivo_enlace

# Cambiar solo si es propietario actual
chown --from=usuario_actual nuevo_usuario archivo
```

## Comando chgrp

```bash
# Cambiar grupo
chgrp grupo archivo

# Cambiar grupo recursivamente
chgrp -R grupo directorio/

# Cambiar grupo preservando enlaces
chgrp -h grupo enlace_simbolico
```


# Permisos por defecto

## Umask

```bash
# Ver umask actual
umask

# Establecer umask
umask 022

# Configurar umask permanentemente
# En ~/.bashrc o ~/.profile
umask 022

# Cálculo de umask:
# Permisos máximos: 666 (archivos), 777 (directorios)
# Umask 022: 666-022=644 (archivos), 777-022=755 (directorios)
```

## Permisos por defecto para directorios

```bash
# Permisos por defecto con ACL
setfacl -d -m u::rwx,g::r-x,o::r-x directorio/

# Ver permisos por defecto
getfacl directorio/
```


# Casos prácticos

## Configuración típica de archivos

```bash
# Archivos de configuración
chmod 644 /etc/config_file

# Scripts ejecutables
chmod 755 /usr/local/bin/script.sh

# Archivos privados
chmod 600 ~/.ssh/id_rsa

# Archivos de log
chmod 644 /var/log/application.log

# Directorio web
chmod 755 /var/www/html/
chmod 644 /var/www/html/*.html
```

## Configuración de directorios compartidos

```bash
# Crear directorio compartido
mkdir /shared
chown :equipo /shared
chmod 2775 /shared  # Bit setgid

# Configurar para que archivos nuevos hereden grupo
chmod g+s /shared
```

## Resolución de problemas comunes

```bash
# Archivo no ejecutable
chmod +x archivo

# Directorio sin acceso
chmod 755 directorio/

# Archivos con permisos incorrectos después de copia
find directorio/ -type f -exec chmod 644 {} \;
find directorio/ -type d -exec chmod 755 {} \;

# Restaurar permisos de home
chmod 755 /home/usuario
chown -R usuario:usuario /home/usuario
```