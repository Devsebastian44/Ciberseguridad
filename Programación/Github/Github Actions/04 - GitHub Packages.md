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