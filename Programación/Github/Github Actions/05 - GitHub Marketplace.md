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