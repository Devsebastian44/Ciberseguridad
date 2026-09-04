# Conceptos fundamentales

## ¿Qué es GitHub Actions?

GitHub Actions es una herramienta de **GitHub** que permite **automatizar tareas relacionadas a un repositorio**. Entre sus principales usos están:

- Integración continua (CI)
- Entrega continua (CD)
- Automatización de tareas como pruebas, despliegue, linting, entre otros.

Se basa en archivos YAML (`.yml`) que definen los *workflows*, y estos pueden ejecutarse en respuesta a eventos como pushes, pull requests, issues, releases, etc.

## ¿Cómo funciona?

GitHub Actions permite crear **Workflows** que se ejecutan ante eventos específicos como:

- `push`
- `merge`
- `pull_request (PR)`

## Casos de uso comunes

- Automatización de **builds**
- **Pruebas** (testing)
- Envío de **notificaciones** (Slack, correo, Notion, Asana, etc.)
- Escaneo de seguridad

## Conceptos clave

### Workflows

- Conjunto de procesos automatizados.
- Se define en un archivo `.yml` dentro del directorio `.github/workflows`.

### Triggers

- Evento que dispara la ejecución del workflow.
- Se define con la palabra clave `on`.

### Jobs

- Unidad de trabajo dentro de un workflow.
- Por defecto, se ejecutan en **paralelo**.
- Cada job se ejecuta en un **runner**.
- Se definen con la clave `jobs`.

### Steps

- Pasos dentro de un job.
- Se ejecutan **secuencialmente** en el mismo runner.
- Se definen usando `steps`, y pueden usar:
  - `name`
  - `uses` o `run`
  - Variables de entorno

### Runners

- Entorno (máquina virtual) donde se ejecutan los jobs.
- GitHub provee imágenes actualizadas de:
  - `ubuntu`
  - `windows`
  - `macos`
- Se especifica con `runs-on`.

| Componente | Descripción                        |
| ---------- | ---------------------------------- |
| `on`       | Evento(s) que disparan el workflow |
| `jobs`     | Conjunto de tareas ejecutadas      |
| `steps`    | Pasos dentro de cada job           |
| `runs-on`  | Runner donde se ejecuta el job     |
| `uses`     | Acción reutilizable predefinida    |
| `run`      | Comando shell a ejecutar           |

## Eventos que pueden activar un Workflow

- `push`: Al hacer push a una rama
- `pull_request`: Cuando se crea o actualiza un PR
- `schedule`: Tareas cron programadas
- `workflow_dispatch`: Ejecución manual
- `release`: Al publicar una nueva release
-  Otros: `fork`, `check_suite`

### Ejemplo con **`push`**:

Al hacer `push` a una rama

```yml
on:
  push:
    branches: [ "main" ]
```

Se ejecuta cada vez que haces `git push origin main`.

### Ejemplo con **`pull_request`**:

Cuando se crea o actualiza un PR

```yml
on:
  pull_request:
    branches: [ "main" ]
```

Se activa si alguien abre un PR contra `main` o actualiza un PR existente (con nuevos commits).

### Ejemplo con **`workflow_dispatch`**:

Ejecución manual desde la UI

```yml
on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Entorno a desplegar'
        required: true
        default: 'staging'
```

Permite ejecutar el workflow manualmente desde la pestaña **Actions** de GitHub, incluso con parámetros personalizados.

### Ejemplo con **`release`**:

Al publicar una nueva release

```yml
on:
  release:
    types: [published]
```

Se activa cuando creas una nueva release en GitHub (desde `Releases > Draft a new release`).

### Otros eventos comunes:

**`fork`** - Cuando alguien hace fork al repositorio

```yml
on: fork
```

Útil para workflows de bienvenida a nuevos contribuidores.

**`check_suite`** - Relacionado con pruebas de integración

```yml
on:
  check_suite:
    types: [completed]
```

Se usa en flujos avanzados de CI (ej: reaccionar a resultados de pruebas externas).