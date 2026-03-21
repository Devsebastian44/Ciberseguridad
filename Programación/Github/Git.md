# Instalación y Configuración Inicial de Git

## Instalación de Git

### En Windows

1. Ir a la página oficial: [https://git-scm.com](https://git-scm.com)
2. Descargar el instalador para Windows.
3. Ejecutar el instalador y seguir los pasos.
4. Para verificar que Git está instalado correctamente, abrir la terminal (CMD o PowerShell) y ejecutar:

```bash
git --version
```

### En Linux (Debian/Ubuntu)

```bash
sudo apt update
sudo apt install git
```

Verificar la instalación:

```bash
git --version
```

## Configuración Inicial

Una vez instalado Git, es importante configurar tu identidad para que tus _commits_ estén correctamente asociados a ti.

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_email@ejemplo.com"
```

El flag `--global` aplica esta configuración a nivel global del sistema (para todos tus repositorios). Puedes omitirlo para configurarlo solo en un repositorio específico.

### Ver configuración actual

```bash
git config --list
```

## Configuración de Llaves SSH

Usar llaves SSH permite autenticarse con servicios como GitHub, GitLab, etc., sin ingresar usuario y contraseña cada vez.

### Verificar si ya tienes una llave SSH

```bash
ls -al ~/.ssh
```

Si ves archivos como `id_rsa` y `id_rsa.pub`, ya tienes una llave generada.

### Generar una nueva llave SSH

```bash
ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
```

Si tu sistema no soporta `ed25519`, puedes usar `rsa`:

```bash
ssh-keygen -t rsa -b 4096 -C "tu_email@ejemplo.com"
```

Presiona Enter para aceptar la ruta por defecto y opcionalmente añade una _passphrase_.

### Agregar la llave al agente SSH

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Copiar la llave pública

```bash
cat ~/.ssh/id_ed25519.pub
```

### Probar conexión

```bash
ssh -T git@github.com
```

Si todo está bien configurado, deberías ver un mensaje de bienvenida.

**Recomendación:** No compartir la llave privada (`id_ed25519`), solo la pública (`id_ed25519.pub`).


# Comandos Esenciales de Git

## Crear un nuevo repositorio

Inicializar un repositorio local

```bash
git init
```

Esto crea un nuevo repositorio de Git en el directorio actual.

## Agregar cambios

### Ver estado actual del repositorio

```bash
git status
```

Muestra los archivos modificados, agregados o eliminados, y si están en el área de _staging_.

### Agregar archivos al área de staging

```bash
git add nombre_archivo
```

### Agregar todos los archivos modificados:

```bash
git add .
```

### Guardar cambios (commit)

```bash
git commit -m "Mensaje descriptivo del cambio"
```

Un _commit_ guarda los cambios del área de staging en el historial del repositorio.

### Commit automático con `-a` (agrega y guarda en uno)

```bash
git commit -am "Mensaje del commit"
```

## Sincronizar cambios con repositorio remoto

### Conectar con un repositorio remoto

```bash
git remote add origin https://github.com/usuario/repositorio.git
```

### Subir cambios por primera vez

```bash
git push -u origin main
```

`-u` establece `origin` como remoto por defecto. Usa `main` o `master` según el nombre de tu rama principal.

### Subir cambios posteriores

```bash
git push
```

### Obtener los últimos cambios del repositorio remoto

```bash
git pull
```

## Clonar (copiar) un repositorio existente

```bash
git clone https://github.com/usuario/repositorio.git
```

Esto crea una copia del repositorio remoto en tu máquina local.


# Trabajo con Ramas en Git

Las **ramas** permiten trabajar en nuevas funcionalidades o correcciones de errores sin afectar el código principal.

## Ver ramas existentes

```bash
git branch
```

Muestra las ramas locales. La rama actual aparece con un asterisco `*`.

### Ver ramas remotas

```bash
git branch -r
```

### Ver todas las ramas (locales + remotas)

```bash
git branch -a
```

### Crear una nueva rama

```bash
git branch nombre_rama
```

Ejemplo:

```bash
git branch nueva-funcionalidad
```

## Cambiar de rama

```bash
git checkout nombre_rama
```

Desde Git 2.23+, puedes usar el comando moderno:

```bash
git switch nombre_rama
```

## Crear y cambiar a una nueva rama en un solo paso

```bash
git checkout -b nombre_rama
```

O con el comando moderno:

```bash
git switch -c nombre_rama
```

## Fusionar (merge) ramas

Para fusionar otra rama en la rama actual:

```bash
git merge nombre_rama
```

Ejemplo: estás en `main` y quieres fusionar `dev`:

```bash
git checkout main
git merge dev
```

Si hay conflictos, Git te pedirá que los resuelvas manualmente.

## Eliminar una rama

### Local

```bash
git branch -d nombre_rama
```

Usa `-D` si quieres forzar el borrado sin confirmar que ya fue fusionada.

```bash
git push origin --delete nombre_rama
```

## Rebase (opcional)

`rebase` reescribe la base de una rama para mantener un historial más lineal.

```bash
git checkout rama-secundaria
git rebase main
```

Usa `merge` para preservar historial y `rebase` para limpiar el historial. Usa `rebase` solo si sabes lo que haces, especialmente en proyectos colaborativos.


# Comandos Útiles en Git

Estos comandos te permiten inspeccionar, revisar y gestionar el estado del repositorio de forma más avanzada.

## `git status`

Muestra el estado actual del repositorio: archivos modificados, agregados, eliminados y si están o no en el área de staging.

```bash
git status
```

## `git log`

Muestra el historial de commits y hash en orden cronológico (más recientes primero).

```bash
git status
```

Formato compacto y resumido:

```bash
git log --oneline
```

Mostrar gráfico de ramas y commits:

```bash
git log --oneline --graph --all --decorate
```

## `git diff`

### Muestra las diferencias entre archivos:

Cambios en el _working directory_ que aún no se han agregado:

```bash
git diff
```

Cambios entre staging y último commit:

```bash
git diff --cached
```

Comparar entre dos ramas:

```bash
git diff rama1 rama2
```

## `git stash`

### Guarda temporalmente los cambios no _commiteados_ para dejar el área de trabajo limpia.

```bash
git stash
```

### Ver elementos almacenados:

```bash
git stash list
```

### Aplicar último stash:

```bash
git stash list
```

### Aplicar y eliminar stash:

```bash
git stash pop
```

### Eliminar un stash específico:

```bash
git stash drop stash@{0}
```

### Eliminar todos los stash:

```bash
git stash clear
```

## `git show`

Muestra información detallada de un commit específico o de un objeto de Git (etiqueta, rama, stash, etc.)

```bash
git show
```

Por defecto, muestra el último commit.

### Mostrar un commit en específico:

```bash
git show <hash_commit>
```

Ejemplo:

```bash
git show a1b2c3d
```


# `.gitignore` en Git

El archivo `.gitignore` permite indicarle a Git qué archivos o directorios **no deben ser rastreados ni versionados**. Es muy útil para excluir archivos temporales, de configuración local, o dependencias.

---

## ¿Cómo crear un archivo `.gitignore`?

En la raíz del repositorio, crea un archivo llamado:

```bash
.gitignore
```

Dentro del archivo, escribe una regla por línea con el archivo o carpeta que deseas ignorar.

## Ejemplos de reglas comunes

### Ignorar un archivo específico

```
archivo.txt
```

### Ignorar todos los archivos `.log`

```bash
*.log
```

### Ignorar una carpeta y su contenido

```bash
/carpeta/
```

### Ignorar todo en una carpeta excepto un archivo

```gitignore
/carpetatemporal/*
!/carpetatemporal/archivo_importante.txt
```

### Ignorar archivos en cualquier subdirectorio

```gitignore
**/*.tmp
```


# Conflictos en Git

Un **conflicto en Git** ocurre cuando Git no puede fusionar automáticamente los cambios entre ramas porque dos partes han modificado la misma línea de un archivo o han hecho cambios incompatibles.

## ¿Cuándo ocurren los conflictos?

- Durante un **merge**:
  
```bash
git merge nombre_rama
```

- Durante un **rebase**:

```bash
git rebase nombre_rama
```

- Al aplicar un **stash**:

```bash
git stash apply
```

## ¿Cómo saber si hay un conflicto?

1. Git te lo indicará claramente:

```bash
CONFLICT (content): Merge conflict in archivo.txt
Automatic merge failed; fix conflicts and then commit the result.
```

2. El archivo afectado mostrará secciones como estas:

```bash
<<<<<<< HEAD
Código en la rama actual
=======
Código en la rama que se está fusionando
>>>>>>> rama-feature
```

## ¿Cómo resolver un conflicto?

1. **Editar manualmente** el archivo para dejar solo la versión correcta (y eliminar los marcadores `<<<<<<<`, `=======`, `>>>>>>>`).
2. Una vez resuelto, marcarlo como solucionado:

```bash
git add archivo.txt
```

3. Luego finalizar el merge con:

```bash
git commit
```

Si el conflicto fue durante un rebase, usa:

```bash
git rebase --continue
```

## Cancelar el proceso de merge o rebase

- Cancelar un merge:

```bash
git merge --abort
```

- Cancelar un rebase:

```bash
git rebase --abort
```

## Buenas prácticas para evitar conflictos

- Haz **pull frecuentemente** antes de hacer cambios:

```bash
git pull origin main
```

- Evita modificar archivos que otros miembros están tocando simultáneamente.
- Divide los cambios en ramas pequeñas y bien definidas.
- Revisa tu `git status` constantemente para evitar sorpresas.


# Deshacer Cambios en Git

En Git existen varias formas de deshacer cambios dependiendo del **contexto**: si ya hiciste `commit`, si no lo hiciste, si ya lo subiste al remoto, etc.

## Deshacer cambios no guardados (working directory)

### Restaurar archivo modificado a su versión más reciente en el repositorio

```bash
git restore archivo.txt
```

## Sacar archivos del staging (deshacer `git add`)

```bash
git restore --staged archivo.txt
```

El archivo vuelve al working directory, ya no está en staging.

## Deshacer el último commit (local)

### Manteniendo los cambios en el working directory:

```bash
git reset --soft HEAD~1
```

### Quitando el commit y regresando los archivos al staging:

```bash
git reset --mixed HEAD~1
```

### Quitando el commit y todos los cambios (peligroso):

```bash
git reset --hard HEAD~1
```

Esto elimina los cambios sin posibilidad de recuperarlos si no tienes un backup.

## Deshacer un commit ya subido al remoto

### Usar `revert` para crear un nuevo commit que deshace el anterior:

```bash
git revert <hash_commit>
```

Ideal para entornos colaborativos. **No borra historial**, solo lo invierte.

### Eliminar un archivo del repositorio pero no del disco

```bash
git rm --cached archivo.txt
```

Muy útil si olvidaste añadir algo al `.gitignore`.


# Manipulación de la Historia en Git

Manipular la historia de Git te permite modificar, reorganizar o eliminar commits para mantener un historial limpio y coherente. Sin embargo, **debe hacerse con precaución**, especialmente en ramas compartidas.

## Modificar el último commit (`--amend`)

Permite corregir el último commit (mensaje o archivos).

```bash
git commit --amend -m "Nuevo mensaje"
```

Reescribe el historial. **Evita usarlo si ya hiciste push.**

## Reescribir historial con `git rebase`

### Reordenar, editar, combinar o eliminar commits recientes:

```bash
git rebase -i HEAD~n
```

Reemplaza `n` por la cantidad de commits que quieres editar (por ejemplo, `HEAD~3`).

### Acciones comunes dentro del rebase interactivo:

| Acción   | Descripción                      |
| -------- | -------------------------------- |
| `pick`   | Mantener el commit tal como está |
| `reword` | Cambiar solo el mensaje          |
| `edit`   | Cambiar el contenido del commit  |
| `squash` | Combinar con el commit anterior  |
| `drop`   | Eliminar el commit               |

### Ejemplo:

```bash
git rebase -i HEAD~3
```

## Eliminar commits con `git reset`

### Retroceder el HEAD y el historial (local):

```bash
git reset --soft HEAD~1   # Mantiene cambios en staging
git reset --mixed HEAD~1  # Mantiene cambios en working directory
git reset --hard HEAD~1   # Elimina todo (irreversible)
```

## Deshacer cambios de forma segura con `git revert`

Crea un nuevo commit que revierte uno anterior.

```bash
git revert <hash_commit>
```

Ideal para proyectos colaborativos. **No reescribe el historial**.

## Reorganizar commits con `cherry-pick`

Aplica un commit específico en otra rama:

```bash
git cherry-pick <hash_commit>
```

