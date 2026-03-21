## Estructura Básica

Todo script de Bash debe comenzar con el **shebang** (`#!`) que indica qué **intérprete** usar:

```bash
#!/bin/bash

# Este es un comentario
echo "Hola Mundo"
````

---

## Creación y Ejecución

### Paso 1: Crear el Archivo

```bash
nano mundo.sh
```

### Paso 2: Escribir el Contenido

```bash
#!/bin/bash

echo "Hola Mundo"
```

### Paso 3: Dar Permisos de Ejecución

```bash
chmod +x mundo.sh
```

### Paso 4: Ejecutar el Script

```bash
./mundo.sh
# o
bash mundo.sh
```

---

## Comentarios

Los comentarios son fundamentales para **documentar el código**:

```bash
#!/bin/bash

# Esto es un comentario de una línea
echo "Hola Mundo"

: '
Esto es un comentario
de múltiples líneas
'
```