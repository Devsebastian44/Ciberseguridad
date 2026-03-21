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


# YAML y Workflows

## ¿Qué es YAML?

**YAML** significa *YAML Ain’t Markup Language*  
Es un lenguaje de serialización de datos, usado para escribir archivos de configuración.

### Comparación YAML vs JSON
| Característica  | YAML                             | JSON                 |
| --------------- | -------------------------------- | -------------------- |
| **Sintaxis**    | Legible, menos símbolos          | Estricta, con llaves |
| **Comentarios** | Sí (`#`)                         | No                   |
| **Tamaño**      | Compacto                         | Verboso              |
| **Parsing**     | Complejo                         | Fácil                |
| **Uso común**   | Configs (GitHub Actions, Docker) | APIs, JavaScript     |
### Características de YAML

1. **Formato clave-valor**  
2. **Indentación con espacios** (no tabs)  
3. **Tipos de datos**: strings, números, booleanos, null.  
4. **Texto multilínea**: Usa `|` (preserva saltos) o `>` (une líneas).

### Herramientas que usan YAML

- GitHub Actions
- Docker Compose
- Kubernetes
- Ansible

### Ejemplos

Tipos primitivos:

```yaml
ciudad: Madrid
edad: 25
activo: true  
descripcion: null
```

Listas:

```yaml
colores:
  - rojo
  - verde
  - azul
```

Mapas/Diccionarios:

```yaml
persona:
  nombre: Juan
  edad: 30
```

Lista de Valores:

```yaml
usuarios:
  - nombre: Ana
    edad: 30
  - nombre: Luis
    edad: 25
```

Modificadores string multimedia:

```yaml
mensaje: |
  Hola ,
  Esto es un texto multilínea,
```

```yaml
texto: >
  Esta es una línea
  que continuará en la siguiente
```

Herencia (anchors):

```yaml
defaults: &defaults
  color: blue
  size: medium

item1:
  <<: *defaults
  color: red  # Sobrescribe color

item2:
  <<: *defaults
  size: small  # Sobrescribe size

# item1 hereda de defaults y sobrescribe el color
```

### Ejemplo práctico: Docker Compose

```yaml
version: '3.8'
services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - .:/var/www/html
  php:
    image: php:8.2-fpm
    volumes:
      - .:/var/www/html
```

### Ejemplo completo:

```yaml
name: CI
on:
    push:
    branches: [ main ]
jobs:
    build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout repository to
    uses: actions/checkout@v3
    - name: Configurar Node.js
    uses: actions/setup-node@v3
    with:
    node-version: '18'
```


# Integración Continua con GitHub Actions

## Sección 1: Conceptos Fundamentales CI/CD

### CI/CD (Clase 3)

- **CI (Integración Continua):** 
  Proceso donde los desarrolladores integran cambios frecuentemente en el repositorio, disparando builds y pruebas automáticas.  
  **Beneficios:** 
  - Detección temprana de errores.  
  - Reduce conflictos entre ramas.  

- **CD (Entrega Continua):** 
  Extensión de CI que prepara el código para despliegue en entornos de staging/pre-producción. 
  **Características:**
  - Artefacto siempre listo para despliegue manual.  
  - Liberación confiable bajo demanda.  

- **CD (Despliegue Continuo):**
  Automatización completa hasta producción.  
  **Flujo:**
  `Cambio aprobado → Despliegue automático a producción`.  

### Beneficios de CI/CD (Clase 3)

- Entregas más rápidas y frecuentes.  
- Mejor calidad de software con pruebas automáticas.  
- Reducción de errores y conflictos.  
- Feedback inmediato.  

## Sección 2: GitHub Actions

### CI/CD

- **CI (Integración Continua):** Automatización de builds y pruebas.
- **CD (Despliegue Continuo):** Automatización de despliegues.

### Conceptos clave

1. **Workflow:** Archivo YAML en `.github/workflows/`.
2. **Eventos/Triggers:** Ejecutan workflows (ej: `push`, `pull_request`).
3. **Jobs/Steps:**

    - **Job:** Unidad de trabajo (ejecutada en paralelo o secuencialmente).
    - **Step:** Acción individual dentro de un job.
    
4. **Actions:** Bloques reutilizables (ej: `actions/checkout@v3`).
5. **Runners:** Entornos de ejecución (Ubuntu, Windows, macOS).

### Ejemplo de Workflow

```yaml
name: CI Pipeline
on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
      - name: Configurar Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
```

**Diagrama:** [[Integración.excalidraw]]  

### Pasos Clave en CD

1. **Promoción:** Mover código de QA a producción.
2. **Pruebas en Prod:** Soak tests, Canary releases.

## Sección 3: GitHub Actions Avanzado

### Temas Cubiertos

1. Variables de entorno

```yaml
env:
  NODE_ENV: production
```

2. Secretos

```yaml
steps:
  - name: Deploy
    env:
      API_KEY: ${{ secrets.API_KEY }}
```

3. Instalación de paquetes

```yaml
- run: npm install
```

4. Servicios (ej: Docker, Redis)

```yaml
services:
  redis:
    image: redis
    ports:
      - 6379:6379
```

5. Deploy

```yaml
- name: Deploy to AWS
  uses: aws-actions/configure-aws-credentials@v1
```


# Integración con GitHub Packages

## Conceptos Clave

### ¿Qué es un paquete?

- Pieza de software reutilizable descargable desde un registro global.
- Ejemplos: bibliotecas (pandas en Python), módulos (lodash en JavaScript).  

### ¿Qué es un registro de paquetes?

Permite a los desarrolladores compartir y usar fácilmente bibliotecas de código y usarlas en estaciones de trabajo de desarrollo

- **Públicos:** npm, PyPI, Docker Hub.
- **Privados:** GitHub Packages, Azure Artifacts.

### ¿Qué es un administrador de Paquetes?

Un administrador de paquetes es un software que te permite administrar las dependencias que tu proyecto necesita para funcionar de manera correcta.

### ¿Qué es GitHub Packages?

- Es un servicio de alojamiento y administración de paquetes de software.
    - Los paquetes pueden ser contenedores y otras dependencias
- Los paquetes pueden ser públicos o privados(organización)
- Los paquetes se pueden usar como dependencias en tus proyectos
- Puedes combinar tu código fuente y paquetes en un solo lugar.
    - Permite proporcionar una administración de permisos y facturación integradas
    - Permiten compartir las dependencias del proyecto dentro de forma pública o dentro de la organización

GitHub Packages puede hospedar:

  - npm
  - RubyGames
  - Gradle
  - Docker
  - NuGet
  - Registro de contenedores de GitHub optimizado para contenedores y soporta imágenes Docker y OCI

```yaml
# Ejemplo de configuración en package.json
{
  "publishConfig": {
    "registry": "https://npm.pkg.github.com"
  }
}
```

## Publicar y consumir un paquete en GitHub Packages

### Requisitos Previos

- **Node.js y npm instalados**:

```bash
node -v  # Debe mostrar v16.x o superior
npm -v   # Debe mostrar 8.x o superior
```

- **Cuenta en GitHub** y un repositorio creado (ej: `mi-paquete`).
- **Git instalado** y configurado:

```bash
mkdir mi-paquete && cd mi-paquete
```

### Inicializar el Proyecto

1. Crear una carpeta local:

```bash
mkdir mi-paquete && cd mi-paquete
```

2. Iniciar un proyecto npm:

```bash
npm init -y
```

Editar el `package.json` generado:

```json
{
  "name": "@tu-usuario/mi-paquete",  // Usar tu nombre de usuario/organización
  "version": "1.0.0",
  "main": "index.js",                // Punto de entrada del paquete
  "publishConfig": {
    "registry": "https://npm.pkg.github.com"  // Registrar en GitHub Packages
  }
}
```

3. Instala las dependencias:

```bash
npm install chart.js canvas chartjs-node-canvas
```

### Crear el Código del Paquete

1. Archivo principal (`estadisticas.js`):

```javascript
function promedio(arr) {
  return arr.reduce((a, b) => a + b, 0) / arr.length;
}

function desviacionEstandar(arr) {
  const media = promedio(arr);
  const sumaCuadrados = arr.reduce((acc, val) => acc + (val - media) ** 2, 0);
  return Math.sqrt(sumaCuadrados / arr.length);
}

module.exports = { promedio, desviacionEstandar };
```


2. Archivo de pruebas (`graficas.js`):

```javascript
const { ChartJSNodeCanvas } = require('chartjs-node-canvas');
const fs = require('fs');

const width = 800;
const height = 600;
const chartJSNodeCanvas = new ChartJSNodeCanvas({ width, height });

async function generarGrafico(nombreArchivo, labels, data) {
  const configuration = {
    type: 'bar',
    data: {
      labels,
      datasets: [{
        label: 'Datos',
        data,
        backgroundColor: 'rgba(75, 192, 192, 0.6)'
      }]
    }
  };

  const image = await chartJSNodeCanvas.renderToBuffer(configuration);
  fs.writeFileSync(nombreArchivo, image);
}

module.exports = { generarGrafico };
```

3. Archivo de pruebas (`test.js`):

```javascript
const { promedio, desviacionEstandar } = require('./estadisticas');
const { generarGrafico } = require('./graficas');

const datos = [10, 20, 30, 40, 50];

console.log('Promedio:', promedio(datos));
console.log('Desviación estándar:', desviacionEstandar(datos));

generarGrafico('grafico.png', ['A', 'B', 'C', 'D', 'E'], datos).then(() => {
  console.log('Gráfico generado.');
});
```

4. Archivos o carpetas que serán ignorados al realizar comandos (`.gitignore`):

```gitignore
# Node_modules
node_modules/

# Logs
logs/
*.log
npm-debug.log*

# OS files
.DS_Store
Thumbs.db

# Environment variables
.env
.env.*

# Output files
dist/
build/
coverage/

# Dependency directories
jspm_packages/

# Optional npm cache directory
.npm

# IDEs
.vscode/

# Test output
*.lcov

# Misc
*.tgz
```

4. Archivo para publicar paquete (`.github/workflows/publicar-paquete.yml`):

```yml
name: Publicar paquete en GitHub Packages
on:
  push:
    branches:
      - main
jobs:
  publicar-paquete:
    runs-on: ubuntu-latest

    permissions:
      contents: read
      packages: write

    steps:
      - name: Clonar repositorio
        uses: actions/checkout@v4

      # Configurar archivo .npmrc para publicar en GitHub Packages
      # La acción setup-node crea un archivo .npmrc en el runner. 
      # Cuando usas el input scope en la acción setup-node, el archivo .npmrc incluye el prefijo de ámbito.
      # Usa como referencia el token de la variable de entorno NODE_AUTH_TOKEN (GITHUB_TOKEN en realidad)
      - name: Configurar .npmrc
        uses: actions/setup-node@v4
        with:
          node-version: '22.x'
          registry-url: 'https://npm.pkg.github.com'
          # Usuario u organización propietaria del workflow
          scope: '@icebeam7'

      - name: Instalar dependencias usando versiones de package-lock.json
        run: npm ci
      - name: Publicar el paquete en GitHub Packages
        run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Confirma los cambios y haz push al repositorio

Ejecutar los siguientes comandos:

```bash
git add

git commit

git push
```

### 5. Consumir un paquete hospedado en GitHub Packages

- Ve a GitHub > Settings > Developer Settings > Personal Access Tokens.
- Primero, crear un token de acceso personal (PAT token) con el scope read:packages
- **¡Copia el token!** (No se mostrará nuevamente).
- Crea una nueva carpeta en una ubicación diferente y ábrela en VS Code
- Inicializa un nuevo proyecto de **Node.js**

```bash
npm init -y
```

- Crea un archivo **.npmrc** donde incluyas tu usuario de github (si estás consumiendo tu paquete) y el PAT token
- **IMPORTANTE:** NO HAGAS COMMIT DE ESTE ARCHIVO (contiene un valor sensible -el token-)

```bash
registry=https://registry.npmjs.org/
@tusuario:registry=https://npm.pkg.github.com/
//npm.pkg.github.com/:_authToken=ghp_TU-TOKEN
```

Reemplaza el usuario de github de la línea 2 y el token en la línea 3 con tus propios valores

- Instala el paquete en tu proyecto:

```bash
npm install
```

- Esto descarga el paquete desde GitHub Packages
- Observa que el paquete ha sido agregado en package.json (línea 13)
- Crea el archivo **generaGrafica.js**
- Reemplaza el usuario de la línea 1 y 2 si estás consumiendo tu paquete

```js
const { promedio, desviacionEstandar } = require('@icebeam7/paguete-estadistica/estadisticas');
const { generarGrafico } = require('@icebeam7/paguete-estadistica/graficas');

const datos = [12, 25, 33, 48, 60];
const etiquetas = ['Ene', 'Feb', 'Mar', 'Abr', 'May'];

console.log('Promedio:', promedio(datos));
console.log('Desviación estándar:', desviacionEstandar(datos));

generarGrafico('./public/grafica.png', etiquetas, datos).then(() => {
    console.log('Gráfica generada exitosamente.");
});
```

- Crea la carpeta **public** y el archivo **index.html**

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8" />
    <title>Gráfica generada</title>
</head>
<body>
    <h1>Gráfica de datos</h1>
    <img src="grafica.png" alt="Gráfica generada">
</body>
</html>
```

- Crea el archivo servidor.js

```javascript
const express = require('express');
const app = express();
const PORT = 3000;

app.use(express.static('public'));

app.listen(PORT, () => {
    console.log('Servidor disponible en http://localhost:${PORT}');
});
```

- Instala Express:

```bash
npm install express
```

Ejecuta el proyecto, generando la gráfica y lanzando el servidor 

```bash
node
```

## Ventajas y Limitaciones del servicio

### Consideraciones

- GitHub Packages está disponible con GitHub Free, GitHub Pro, GitHub Free para organizaciones, GitHub Team, GitHub Enterprise Cloud y GitHub Enterprise Server 3.0 o superior

- El desarrollo de software se centraliza en GitHub.
    - Puedes integrar GitHub Packages con GitHub APIs, GitHub Actions y webhooks para crear un flujo de trabajo de DevOps de extremo a extremo que incluya tu código, CI y CD.

### Ventajas

- Integración con GitHub 
- Soporte para múltiples tipos de paquetes 
- Identidad y acceso unificados 
- Paquetes con nombres con espacio de nombres (namespacing) 
- Gratis para repositorios públicos 
- Auditoría y trazabilidad • Alojamiento privado • Ubicación del almacenamiento

### Limitaciones

- Cuotas de almacenamiento y ancho de banda
- Ecosistema limitado en comparación con registries públicos
- Configuración de autenticación
- Interfaz limitada
- Desafíos en la resolución de dependencias
- Latencia geográfica
- Sin control de acceso por paquete
- No es ideal para distribución pública

### ¿Cuándo conviene usar GitHub Packages?

- Tu código está en GitHub.
- Necesitas una forma sencilla de publicar paquetes privados.
- Quieres versionar y liberar herramientas internas junto con el código fuente.
- Estás construyendo un flujo DevOps centrado en GitHub Actions

## GitHub Container Registry

### GitHub Container Registry (GHCR)

- Un servicio de GitHub diseñado específicamente para almacenar y gestionar imágenes de contenedores (como Docker), de forma más especializada y avanzada que el sistema general de GitHub Packages.
- Aunque técnicamente forma parte de GitHub Packages, GHCR se introdujo como una mejora con enfoque exclusivo en contenedores.
- Puedes almacenar y administrar imágenes Docker y OCI en el registro de contenedores.
- GHCR almacena imágenes de contenedor dentro de tu organización o cuenta personal, y te permite asociar una imagen con un repositorio.
- Puede elegir si desea heredar permisos de un repositorio o establecer permisos granulares independientemente de un repositorio.
- También puede acceder a imágenes de contenedores públicos de forma anónima.

## GitHub Container Registry vs Docker Hub

| Característica          | GitHub Container Registry (GitHub Packages)            | Docker Hub                                            |
| ----------------------- | ------------------------------------------------------ | ----------------------------------------------------- |
| **Tipo de hosting**     | Integrado con repositorios GitHub                      | Especializado en imágenes Docker                      |
| **Soporte de paquetes** | Sí (npm, Maven, NuGet, RubyGems, etc.)                 | No, solo imágenes Docker                              |
| **Integración CI/CD**   | Muy buena con GitHub Actions (nativo)                  | Compatible pero no nativo                             |
| **Control de acceso**   | Hereda permisos del repositorio GitHub                 | Gestión separada de permisos                          |
| **Autenticación**       | Usa GITHUB_TOKEN                                       | Usa tokens de acceso o Docker Hub login               |
| **Visibilidad**         | Sigue la visibilidad del repositorio (público/privado) | Configuración independiente por repositorio/namespace |


# GitHub Marketplace
## ¿Qué es GitHub Marketplace?

Plataforma para descubrir, comprar e integrar herramientas que amplían GitHub.

- GitHub Marketplace es una plataforma que permite a los desarrolladores y equipos descubrir, comprar e integrar herramientas y aplicaciones que amplían la funcionalidad de GitHub.
- Ofrece una amplia gama de herramientas, desde herramientas de CI/CD y modelos de IA hasta aplicaciones de gestión de proyectos.
- Acceso centralizado a herramientas desde tu cuenta de GitHub. 
- Integración perfecta con tus repositories y workflows.
- Amplia variedad de aplicaciones
- Modelos de precios flexibles
- Facturación simplificada

### Categorías principales:

- **Actions**: Automatización de workflows.  
- **Apps**: Integraciones con herramientas externas (Jira, Slack).  
- **Copilot Extensions**: Extienden GitHub Copilot (ej: Stack Overflow, Docker).  
- **Modelos de IA**: Integración con IA para desarrollo.  

### Ejemplo de Actions populares

- `actions/checkout`: Clona repositorios.  
- `JamesIves/github-pages-deploy-action`: Despliega en GitHub Pages.  
- `Super-Linter`: Valida código con múltiples linters.  

## Publicando GitHub Actions personalizadas

- Las acciones son tareas individuales que puedes usar para personalizar los flujos de trabajo de desarrollo.
- Puedes crear acciones propias escribiendo un código personalizado que interactúe con tu repositorio de la manera que desees, incluida la integración con las API de GitHub y cualquier API de terceros disponible públicamente.
- Por ejemplo, una acción puede publicar módulos npm, enviar alertas por SMS cuando se crean problemas urgentes o implementar código listo para producción.

### Archivo de metadatos

- Las acciones requieren un archivo de metadatos para definir las entradas, salidas y puntos de entrada para tu acción.
- El nombre del archivo de metadatos debe ser action.yml
- Elementos:
    - name, description, inputs, outputs, runs

```bash
name: 'Hello World'
description: 'Greet someone and record the time'
inputs:
  who-to-greet:  # id of input
    description: 'Who to greet'
    required: true
    default: 'World'
outputs:
  time: # id of output
    description: 'The time we greeted you'
runs:
  using: 'node20'
  main: 'index.js'
```

### Archivo README

Un archivo README para ayudar a las personas a que aprendan a usar tu acción. 

Puedes incluir esta información en README.md:

- Una descripción detallada de lo que hace la acción.
- Argumentos obligatorios de entrada y salida.
- Argumentos opcionales de entrada y salida. 
- Secretos que utiliza la acción.
- Variables de entorno que utiliza la acción.
- Un ejemplo de cómo usar tu acción en un flujo de trabajo.

```markdown
# Hello world javascript action

This action prints "Hello World" or "Hello" + the name of a person to greet to the log.

## Inputs

### `who-to-greet`

**Required** The name of the person to greet. Default `"World"`.

## Outputs

### `time` You, 9 minutes ago • My first action is ready …

The time we greeted you.

## Example usage

| **yaml**    |    |
|---|---|
| uses: actions/ejemplo-actionsjs@v1    |    |
| with:    |    |
| who-to-greet: 'Mona the Octocat'   |    |

Como regla general, el archivo incluir todo lo que un usuario acción.

Si cree que podría ser informado...
```

Como regla general, el archivo README.md debe incluir todo lo que un usuario debe saber para usar la acción. Si cree que podría ser información útil, inclúyela en README.md.

## Tipos de acciones personalizadas

### Docker Container Actions

- Los contenedores Docker empaquetan el entorno con el código GitHub Actions. 
- Esto crea una unidad de trabajo más consistente y confiable, ya que el consumidor de la acción no necesita preocuparse por las herramientas o las dependencias. 
- Un contenedor Docker te permite usar versiones específicas de un sistema operativo, dependencias, herramientas y código.
- Para las acciones que se deben ejecutar en una configuración de entorno específica, Docker es una opción ideal ya que puedes personalizar el sistema operativo y las herramientas.
- Debido a la latencia para crear y recuperar el contenedor, las acciones del contenedor Docker son más lentas que las acciones de JavaScript.
- Las acciones de contenedor de Docker solo pueden ejecutarse en ejecutores con un sistema operativo Linux. 
- Los runners auto-hospedados deberán utilizar un sistema operativo Linux y tener Docker instalado para ejecutar las acciones de contenedores de Docker.

Pasos para crear una Docker Container Action:

- Cree un elementoDockerfilea fin de definir los comandos para ensamblar la imagen de Docker. 
- Cree un archivo de metadatosaction.ymlpara definir las entradas y salidas de la acción. En el archivo, establezca:
    - runs: using: docker
    - runs: image: Dockerfile
- Cree un archivo **entrypoint.sh** para describir la imagen de Docker. 
- Confirme e inserte la acción en GitHub con los archivos siguientes: **action.yml, entrypoint.sh, Dockerfile y README.md.**

### JavaScript Actions

- Las JavaScript Actions separan el código de acción del entorno que se usa para ejecutar la acción. Por este motivo, el código de acción se simplifica y se puede ejecutar más rápido que las acciones dentro de un contenedor de Docker.
- Como requisito previo para crear y usar acciones de JavaScript empaquetadas, debe descargar Node.js, que incluye npm. 
- Como paso opcional (pero recomendado), use el módulo GitHub Actions Toolkit de Node.js, que es una recopilación de paquetes de Node.js que le permite crear rápidamente acciones de JavaScript con más coherencia.

Pasos para crear una JavaScript Action: 

- Cree un archivo de metadatos **action.yml** para definir las entradas y salidas de la acción, así como para indicarle al runner de acciones cómo empezar a ejecutar esta acción de JavaScript.
- Cree un archivoindex.js con información de contexto sobre los paquetes del kit de herramientas, el enrutamiento y otras funciones de la acción.
- Confirme e inserte la acción en GitHub con los archivos siguientes: **action.yml, index.js, node_modules, package.json, package lock.json y README.md.**

### Composite Actions 

- Las acciones de pasos de ejecución compuestos permiten reutilizar acciones mediante scripts de shell. Incluso puede combinar varios lenguajes de shell dentro de la misma acción. 
- Si tiene muchos scripts de shell para automatizar varias tareas, ahora puede convertirlos fácilmente en una acción y reutilizarlos para diferentes flujos de trabajo.
- A veces es más fácil escribir un script de shell que usar JavaScript o encapsular el código en un contenedor de Docker.


# Desarrollo Moderno con GitHub

## Integración de GitHub Actions con Azure

### Beneficios Clave de Azure

- **Escalabilidad elástica:** Ajuste automático de recursos según demanda.  
- **Seguridad empresarial:** Certificaciones ISO, SOC y cifrado de datos.  
- **Catálogo de servicios:** +200 servicios (IA, almacenamiento, cómputo).  
- **Alta disponibilidad:** SLA del 99.9% para servicios críticos.  

### Servicios Populares para Despliegue

1. **Azure App Service:** Hosting para aplicaciones web.  
2. **Azure Functions:** Computación sin servidor (serverless).  
3. **AKS (Azure Kubernetes Service):** Orquestación de contenedores.  
4. **Máquinas Virtuales:** Infraestructura como servicio (IaaS).  

**Tier Gratuito:** $200 USD de crédito para nuevos usuarios.

### Automatización total de CI/CD

Cada vez que hay un cambio en el código, se pueden disparar despliegues automáticos en Azure. Menos errores manuales y más consistencia.

### Acciones específicas de Azure

Microsoft provee acciones oficiales para App Service, AKS, Container Apps, etc. Se ahorra tiempo porque no necesitas escribir scripts complejos.

### Conexión nativa entre GitHub y Azure

Al ser ambos de Microsoft, la integración es directa y confiable.

## Sección 2: Beneficios de GitHub Actions + Azure

### Automatización CI/CD

- **Despliegue automático** en Azure ante cambios en el código (`push`/`pull_request`).  
- **Reducción de errores manuales:**  

```yaml
  - name: Deploy to Azure App Service
    uses: azure/webapps-deploy@v2
    with:
      app-name: 'mi-app'
      slot-name: 'production'
      publish-profile: ${{ secrets.AZURE_PUBLISH_PROFILE }}
```

### Acciones Oficiales de Azure

- **Pre-configuradas** para servicios como:
    - `azure/login@v1`: Autenticación en Azure.
    - `azure/aks-set-context@v1`: Gestión de Kubernetes.

### Ejemplo para AKS:

```yaml
- name: Deploy to AKS
  uses: azure/aks-deploy@v1
  with:
    resource-group: 'my-rg'
    cluster-name: 'my-cluster'
    namespace: 'prod'
```

## Sección 3: Configuración Práctica

### Pasos para Integración

1. Crear un Service Principal en Azure:

```bash
az ad sp create-for-rbac --name "github-actions-sp" --role contributor
```

2. Workflow de Ejemplo (App Service):

```bash
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}
      - run: az webapp up --name mi-app --resource-group my-rg
```


# Mejores Prácticas
## Organizar los steps de forma clara

- Usa nombres descriptivos para cada paso.
- Agrupa los pasos por propósito: `build`, `test`, `deploy`.

## ¿Qué es `needs`?

Es la palabra clave en GitHub Actions para definir **dependencias entre jobs**. Un job solo se ejecutará cuando los jobs de los que depende (`needs`) hayan terminado (éxito o fallo, según configuración).

```bash
jobs:
  job1:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Job 1"

  job2:
    needs: job1  # Dependencia simple
    runs-on: ubuntu-latest
    steps:
      - run: echo "Job 2 se ejecuta después de Job 1"

  job3:
    needs: [job1, job2]  # Dependencia múltiple
    runs-on: ubuntu-latest
    steps:
      - run: echo "Job 3 espera a Job 1 y Job 2"
```

## Casos de Uso

1. Dependencia con jobs exitosos (Comportamiento por defecto)

```yml
job2:
  needs: job1  # Job 2 solo se ejecuta si Job 1 tiene éxito
```

2. Dependencia con jobs exitosos (Comportamiento por defecto)

```yml
job2:
  needs: job1
  if: always()  # Se ejecuta aunque Job 1 falle
```

3. Dependencia de múltiples jobs

```yml
job4:
  needs: [job1, job2, job3]  # Espera a 3 jobs
```

### Configuraciones Avanzadas

Matriz de jobs con dependencias

```yml
jobs:
  build:
    strategy:
      matrix:
        os: [ubuntu-latest, macos-latest]
    runs-on: ${{ matrix.os }}
    steps:
      - run: echo "Build en ${{ matrix.os }}"

  test:
    needs: build  # Espera a TODOS los jobs de la matriz
    runs-on: ubuntu-latest
    steps:
      - run: echo "Tests"
```

### Dependencia condicional

```yml
deploy:
  needs:
    - build
    - test  # Solo si test tiene éxito (comportamiento por defecto)
```

**Diagrama:** [[needs.excalidraw]]

## Nunca harcodear información

- Utiliza variables para información repetitiva o configurable.
- Usa secretos para datos sensibles como contraseñas o tokens.
- Evita exponer información confidencial en logs o archivos.

## Trabajar con artefactos

- Guarda archivos importantes generados durante el workflow: logs, reportes de pruebas, binarios.
- Facilita el debugging al permitir revisar qué salió mal después de la ejecución.

## Usa versiones concretas

- Especifica versiones exactas para acciones, dependencias y herramientas.
- Evita que actualizaciones automáticas rompan tu pipeline.

## Define las ramas a escuchar en los eventos

- Limita la ejecución de workflows a ramas específicas usando:

```yaml
  on:
    push:
      branches: [ main, develop ]
    pull_request:
      branches: [ main ]
```

- Evita disparar workflows innecesarios en ramas que no son relevantes.

## Crear acciones reusables

- Encapsula lógica común en custom actions para evitar duplicidad.
- Usa parámetros flexibles para adaptar la acción a diferentes contextos.

## Crear workflows reusables

- Utiliza `reusable workflows` para compartir lógica entre múltiples workflows.
- Centraliza y simplifica el mantenimiento de procesos complejos.

## Revisar las GitHub Actions de terceros

- Verifica que las acciones de terceros sean seguras y estén mantenidas activamente.
- Revisa issues abiertos, frecuencia de actualizaciones y reputación del autor.

## Uso de Cache

- Aprovecha la caché para evitar reinstalar dependencias en cada ejecución.
- Reduce tiempos de ejecución y consumo de minutos facturables en planes privados.

```yaml
- uses: actions/cache@v3
  with:
    path: ~/.npm
    key: ${{ runner.os }}-npm-${{ hashFiles('**/package-lock.json') }}
```

## Configurar permisos mínimos al GITHUB_TOKEN

- Limita los permisos del `GITHUB_TOKEN` para reducir riesgos de seguridad.

```yaml
permissions:
  contents: read
  issues: write
```

## Añadir un badge del status del workflow en tu README

- Mejora la visibilidad del estado del pipeline.

```yaml
![CI Status](https://github.com/usuario/repo/actions/workflows/main.yml/badge.svg)
```

## Recomendaciones de monitoreo y debugging

- Usa `echo` para agregar logs en pasos clave.
- Sube artefactos como reportes de pruebas para facilitar el análisis.

## Hacer uso de notificaciones

- Configura alertas en Slack, Teams o correo para fallos críticos.
- `issues`: Se activa cuando se crea, se edita o se cierra un problema

### Ejemplo:

Para comentarios en _issues_:

```yaml
on:
  issue_comment:
    types: [created, edited]  # Se activa al crear/editar un comentario
```

Para comentarios en _pull requests_:

```yaml
on:
  pull_request_review_comment:
    types: [created]  # Comentarios en revisiones de PRs
```

Para cualquier actividad en _issues_ (incluyendo comentarios):

```yaml
on:
  issues:
    types: [opened, commented]  # Issue nuevo o comentado
```

## Hacer uso de paralelismo

- Ejecuta tareas independientes en paralelo para acelerar el workflow.

```yaml
jobs:
  test:
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest]
```

## Hacer uso de matrix

- Prueba en múltiples entornos o combinaciones automáticamente.

```yaml
strategy:
  matrix:
    node-version: [14.x, 16.x, 18.x]
    os: [ubuntu-latest, windows-latest]
```

## Utiliza Dependabot para actualizar Actions

- Habilita Dependabot para mantener tus acciones actualizadas.

```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
```

## Hacer uso de concurrencia

- Evita ejecuciones redundantes del mismo workflow.

```yaml
concurrency: 
  group: ${{ github.ref }}
  cancel-in-progress: true
```

## Hacer uso de servicios

- Levanta contenedores para servicios como bases de datos en segundos.

```yaml
services:
  redis:
    image: redis
    ports:
      - 6379:6379
```

## Usar self-hosted runners

- Aprovecha máquinas más potentes o con configuraciones personalizadas.
- Elimina tiempos de espera en colas de runners públicos.


# Fundamentos de GitHub para Empresas

## ¿Qué es GitHub Enterprise?

GitHub Enterprise es una edición de GitHub diseñada para empresas y organizaciones grandes que requieren más control, seguridad, personalización y soporte. Está pensada para equipos que gestionan múltiples repositorios y flujos de trabajo complejos, con necesidades específicas de cumplimiento y gobernanza.

**Diagrama:** [[Github Enterprise.excalidraw]]

### GitHub Enterprise

- Edición de GitHub diseñada para empresas y organizaciones grandes.
    - Se requiere más control, seguridad, personalización y soporte.
    - Pensada para equipos que gestionan múltiples repositorios, flujos de trabajo complejos.
    - Necesidades específicas de cumplimiento y gobernanza.

### Modelos:

- GitHub Enterprise Cloud
- GitHub Enterprise Server

## Características principales

- Seguridad Empresarial  
- Cumplimiento y control  
- CI/CD integrado  
- Métricas y reportes  
- SLA y nivel de soporte empresarial  
- Integración con herramientas empresariales  
- Incluye todas las características del plan de tarifa GitHub Team  

**Mantenimiento y Automatización**

## GitHub Online Services SLA

Este SLA aplica a Cloud, Cloud-ENU y GitHub AE. GitHub se compromete a mantener al menos un 39% de tiempo de actividad ("Uptime") para el servicio aplicable.

https://github.com/customer-terms/github-online-services-sla

### Cálculo de Uptime

| Service Feature    | Uptime Calculation    | Definitions    | Service Credits Calculation |
|---|---|---|---|
| Issues, Pull Requests, Git Operations | (total minutes in a calendar quarter - Downtime) / total minutes in a calendar quarter | "Downtime" es cuando la tasa de error excede el 5% en un minuto dado | 10% del monto |

## GitHub Enterprise login process with IDP using SAML SSO

Flujo de autenticación:
1. Usuario accede a `github.com/username`
2. Identidad vinculada con SSO a través del Identity Provider (IdP)
3. SAML SSO se habilita y aplica en GitHub Enterprise Cloud

## Categorías

### Mantenimiento (Upkeep)

- GitHub Enterprise Support  
- Autenticación con SAML SSO  
- GitHub Connect  
- Control de acceso personalizado para GitHub Pages

Las características de mantenimiento facilitan tareas administrativas para que los colaboradores pongan manos a la obra con el trabajo real.

El rol del administrador de una organización de GitHub es minimizar la fricción que los usuarios sienten al interactuar con GitHub.

### Características de mantenimiento incluidas:

- Soporte técnico de GitHub Enterprise
- Autenticación con SAML SSO
- GitHub Connect
- Control de acceso a sitios de GitHub Pages
- Otras características, según el modelo elegido

### Automatización

- GitHub Advanced Security  
- Minutos de GitHub Actions  
- Actualizaciones automáticas de seguridad y de versión  

### Elementos de automatización para CI/CD

- GitHub Actions
- Construcción de pipelines
- Automatización de pruebas
- Entrega continua
- Flexibilidad de herramientas
- Automatización de versión de release
- Seguridad
- Monitoreo y Notificaciones

## Rulesets

### Tipos de reglas:

- **Branch PR Rules**: 1 regla activa (38 ramas)  
- **Repository rulesets**: 3 reglas activas (38 ramas)  
- **Tag Rules**: 2 reglas desactivadas  
- **Test Rules**: 4 reglas en evaluación  

## ¿Cuándo conviene usar GitHub Enterprise?

- Necesidad de gobernanza y control sobre equipos y repositorios  
- Requerimientos de seguridad avanzada  
- Soporte técnico garantizado  
- Cumplimiento de normas regulatorias  
- Escalabilidad para cientos/miles de desarrolladores  

## Modelos de GitHub Enterprise

- GHEC: GitHub Enterprise Cloud
- GHES: GitHub Enterprise Server

### GitHub Enterprise Cloud (GHEC)

- Alojado por GitHub en la nube  
- Ofrece las mismas capacidades que GitHub.com, pero con características adicionales como:
    - Single Sign-On (SSO)
    - Auditoría avanzada
    - Políticas de seguridad organizacionales
    - GitHub Connect (integración con GitHub Enterprise Server)
    - Organizaciones y Teams
### GHEC con Residencia de Datos

Para organizaciones que deben cumplir con normativas de protección
de datos.

- Regiones de residencia de datos: Estados Unidos, Europa, …
- Tipos de datos cubiertos: contenido del repositorio, metadatos.
- Cifrado y seguridad: encriptación de datos, cumplimiento de estándares de seguridad (ISO 27001, SOC 2, …)
- Almacenamiento regional y conmutación por error:
    - Datos almacenados en la región con alta disponibilidad y recuperación ante desastres
    - Si algunos tipos de datos de copia de seguridad se replican fuera de la región, permanecen encriptados

### GitHub Enterprise Server (GHES)

- Instalado y gestionado en los servidores propios de la empresa.

- Características clave:
    - Control total sobre la infraestructura y los datos.
    - Seguridad, privacidad y residencia.
    - Personalización y control.
    - Rendimiento optimizado
    - Cumplimiento con políticas corporativas o regulatorias.

- Se accede a través de una URL personalizada (por ejemplo,
git.miempresa.com).

### Componentes (GHES)

- Aplicación de GitHub
- Panel administrativo
- Herramientas de admistración del sistema
- Copia de seguridad y recuperación ante desastres
- Registro y monitoreo

## Modelos de usuarios

### Estándar

- Usuarios gestionan sus propias cuentas  
- Administradores tienen control limitado  

### Enterprise Managed User (EMU)

- Los administradores tienen control sobre la cuenta de usuario:
    - Nombres de usuario, correo electrónico, ciclo de vida (creación, desactivación)
    - Métrodos de autenticación: controlada via proveedor de identidades de la empresa (SAML, SCIM)

- Los usuarios administrados solo pueden unirse a la empresa a la
que pertenecen, no se pueden unir de forma independiente a
otras organizaciones.

- Las cuentas de usuario están totalmente administradas por la
empresa.

### ¿Cuándo utilizar el modelo EMU?

- Onboarding de nuevos empleados a la organización.
- Offboarding de empleados.
- Reducir la filtración de Propiedad Intelectual (IP)
- Administración de consultores
