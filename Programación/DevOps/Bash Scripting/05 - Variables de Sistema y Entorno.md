## Variables Predefinidas

```bash
#!/bin/bash

echo "Nombre del script: $0"
echo "PID del proceso: $$"
echo "Código de salida del último comando: $?"
echo "Directorio actual: $PWD"
echo "Directorio home: $HOME"
echo "Usuario actual: $USER"
echo "Shell actual: $SHELL"
````

---

## Variables de Entorno Importantes

```bash
#!/bin/bash

# Variables de entorno comunes
echo "PATH: $PATH"
echo "HOME: $HOME"
echo "USER: $USER"
echo "SHELL: $SHELL"
echo "TERM: $TERM"
echo "LANG: $LANG"

# Crear variables de entorno
export MI_VARIABLE="valor"
export PATH="$PATH:/mi/directorio"
```

---

## Ejemplo Práctico

```bash
#!/bin/bash

echo "=== Información del Sistema ==="
echo "Script: $0"
echo "Usuario: $USER"
echo "PID: $$"
echo "Directorio: $PWD"
echo "Parámetros recibidos: $#"

if [ $# -gt 0 ]; then
    echo "Primer parámetro: $1"
fi
```