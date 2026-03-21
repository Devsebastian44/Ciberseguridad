## Comprensión de Permisos

En Linux, cada archivo y directorio tiene permisos que determinan quién puede acceder y qué puede hacer.

```bash
ls -l archivo.txt     # Ver permisos de archivos
ls -la                # Todos los archivos incluyendo ocultos
ls -alh               # Con tamaños legibles
```

Ejemplo de salida:  
`-rwxr-xr-- 1 usuario grupo 1234 Nov 15 10:30 archivo.txt`  
Formato: `[tipo][propietario][grupo][otros] [enlaces] [propietario] [grupo] [tamaño] [fecha] [nombre]`

---

## Tipos de Permisos

|Símbolo|Significado|Valor Numérico|
|---|---|---|
|`r`|Read (leer)|4|
|`w`|Write (escribir)|2|
|`x`|Execute (ejecutar)|1|
|`-`|Sin permiso|0|

---

## Tipos de Archivos

|Símbolo|Tipo|
|---|---|
|`-`|Archivo regular|
|`d`|Directorio|
|`l`|Enlace simbólico|
|`c`|Dispositivo de caracteres|
|`b`|Dispositivo de bloques|

---

## Cambio de Permisos (`chmod`)

### Notación octal

```bash
chmod 755 archivo.txt    # rwxr-xr-x
chmod 644 archivo.txt    # rw-r--r--
chmod 700 directorio/    # rwx------
chmod 666 archivo.txt    # rw-rw-rw-
```

### Notación simbólica

```bash
chmod u+x archivo.txt    # Añadir ejecución al propietario
chmod g-w archivo.txt    # Quitar escritura al grupo
chmod o+r archivo.txt    # Añadir lectura a otros
chmod a+x archivo.txt    # Añadir ejecución a todos
```

### Cambios recursivos

```bash
chmod -R 755 directorio/
chmod -R u+x directorio/
```

---

## Combinaciones Comunes

```bash
chmod +x script.sh
chmod 755 script.sh

chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub

chmod 755 directorio/
chmod 700 directorio/
```

---

## Cambio de Propiedad (`chown` / `chgrp`)

```bash
chown usuario archivo.txt
chown usuario:grupo archivo.txt
chown -R usuario directorio/

chgrp grupo archivo.txt
chgrp -R grupo directorio/

chown root archivo.txt
chown www-data:www-data /var/www/html/
chown -R usuario:usuario /home/usuario/proyectos/
```

---

## Gestión de Grupos

```bash
groups
groups usuario
cat /etc/group

groupadd nombre_grupo
usermod -a -G nombre_grupo usuario
gpasswd -d usuario nombre_grupo
```

---

## Permisos Especiales

### SetUID, SetGID y Sticky Bit

```bash
chmod 4755 archivo     # SetUID
chmod u+s archivo

chmod 2755 archivo     # SetGID
chmod g+s archivo

chmod 1755 directorio  # Sticky Bit
chmod +t directorio

ls -ld /tmp            # Ejemplo: sticky bit en /tmp
```

---

## Ejemplos Prácticos

```bash
chown -R www-data:www-data /var/www/html/
chmod -R 755 /var/www/html/
chmod -R 644 /var/www/html/*.html

chmod +x script.sh
chmod 755 script.sh

chmod 600 /etc/ssh/ssh_host_rsa_key
chmod 644 /etc/ssh/ssh_host_rsa_key.pub

chmod 700 /home/usuario/
chmod 755 /home/usuario/public_html/

find /home -perm 777 -type f
find /etc -perm -4000 -type f
```

---

## Comandos de Verificación

```bash
ls -l archivo.txt
stat archivo.txt
stat -c "%a %n" archivo.txt

ls -l | awk '{print $3, $4, $9}'
find / -nouser -o -nogroup 2>/dev/null
```

---
