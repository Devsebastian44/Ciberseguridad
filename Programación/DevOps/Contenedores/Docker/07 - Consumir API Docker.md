## API REST de Docker

Docker expone una **API REST** que permite interactuar programáticamente con el daemon de Docker.

```bash
# Habilitar API TCP (desarrollo únicamente)
dockerd -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock

# Listar contenedores via API
curl http://localhost:2375/containers/json

# Información del sistema
curl http://localhost:2375/info

# Crear contenedor via API
curl -X POST http://localhost:2375/containers/create \
  -H "Content-Type: application/json" \
  -d '{"Image": "nginx", "ExposedPorts": {"80/tcp": {}}}'
````

**Advertencia de seguridad**: Nunca expongas la API TCP en producción sin **autenticación TLS**.

---

## Usando Docker SDK

### Python

```python
import docker

# Conectar al daemon
client = docker.from_env()

# Listar contenedores
containers = client.containers.list()
for container in containers:
    print(f"ID: {container.id}, Name: {container.name}")

# Crear y ejecutar contenedor
container = client.containers.run(
    image="nginx",
    ports={'80/tcp': 8080},
    detach=True,
    name="mi-nginx"
)

# Obtener logs
logs = container.logs()
print(logs.decode())

# Detener y eliminar
container.stop()
container.remove()
```

### Node.js

```javascript
const Docker = require('dockerode');
const docker = new Docker();

// Listar contenedores
async function listContainers() {
  const containers = await docker.listContainers();
  containers.forEach(container => {
    console.log(`ID: ${container.Id}, Names: ${container.Names}`);
  });
}

// Crear contenedor
async function createContainer() {
  const container = await docker.createContainer({
    Image: 'nginx',
    ExposedPorts: { '80/tcp': {} },
    HostConfig: {
      PortBindings: { '80/tcp': [{ HostPort: '8080' }] }
    }
  });
  
  await container.start();
  return container;
}

listContainers();
```

---

## Docker Portainer

### ¿Qué es Portainer?

Portainer es una **interfaz web ligera** para gestionar Docker, Docker Swarm y Kubernetes de forma visual.

### Instalación

```bash
# Crear volumen para datos
docker volume create portainer_data

# Ejecutar Portainer
docker run -d -p 8000:8000 -p 9000:9000 \
  --name=portainer --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:latest

# Acceder a http://localhost:9000
```

### Funcionalidades

- **Dashboard** con estadísticas del sistema
- **Gestión de contenedores** (crear, iniciar, detener, eliminar)
- **Gestión de imágenes** (descargar, construir, eliminar)
- **Gestión de volúmenes** y redes
- **Monitoreo** de recursos
- **Gestión de stacks** (Docker Compose)
- **Terminal web** para contenedores
- **Gestión de usuarios** y permisos

---

## Docker Aplicaciones Gráficas

### Ejecutar Aplicaciones GUI

#### Linux (X11)

```bash
# Permitir conexiones X11
xhost +local:docker

# Ejecutar aplicación gráfica
docker run -it --rm \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  --name firefox \
  jess/firefox

# Ejemplo con editor de texto
docker run -it --rm \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -v $(pwd):/workspace \
  --name vscode \
  codercom/code-server:latest
```

#### macOS (con XQuartz)

```bash
# Instalar XQuartz
brew install --cask xquartz

# Configurar XQuartz
open -a XQuartz

# Ejecutar aplicación
docker run -it --rm \
  -e DISPLAY=host.docker.internal:0 \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  jess/firefox
```

#### Windows (con VcXsrv)

```bash
# Instalar VcXsrv
# Configurar display

docker run -it --rm \
  -e DISPLAY=host.docker.internal:0.0 \
  jess/firefox
```

### Ejemplo: Entorno de Desarrollo Completo

```dockerfile
# Dockerfile.dev
FROM ubuntu:20.04

# Evitar interacciones durante instalación
ENV DEBIAN_FRONTEND=noninteractive

# Instalar dependencias
RUN apt-get update && apt-get install -y \
    firefox \
    gedit \
    git \
    curl \
    wget \
    vim \
    python3 \
    python3-pip \
    nodejs \
    npm \
    && rm -rf /var/lib/apt/lists/*

# Crear usuario no root
RUN useradd -m -s /bin/bash developer
USER developer
WORKDIR /home/developer

# Comando por defecto
CMD ["firefox"]
```

```bash
# Construir imagen
docker build -f Dockerfile.dev -t dev-environment .

# Ejecutar entorno de desarrollo
docker run -it --rm \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -v $(pwd):/workspace \
  --name dev-env \
  dev-environment
```

---

## Entorno VS Code

### VS Code con Docker

**Extensión Remote-Containers:**

1. Instalar extensión **"Remote - Containers"**
2. Crear archivo `.devcontainer/devcontainer.json`
3. Abrir proyecto en contenedor

```json
{
  "name": "Node.js Development",
  "image": "node:16",
  "features": {
    "ghcr.io/devcontainers/features/git:1": {}
  },
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-vscode.vscode-typescript-next",
        "esbenp.prettier-vscode"
      ]
    }
  },
  "forwardPorts": [3000],
  "postCreateCommand": "npm install",
  "remoteUser": "node"
}
```

### Code-Server (VS Code en el navegador)

```bash
# Ejecutar code-server
docker run -it --rm \
  -p 8080:8080 \
  -v $(pwd):/home/coder/workspace \
  -e PASSWORD=mi-password \
  codercom/code-server:latest

# Acceder a http://localhost:8080
```

### Dockerfile para Entorno de Desarrollo

```dockerfile
FROM codercom/code-server:latest

# Cambiar a usuario root para instalaciones
USER root

# Instalar herramientas adicionales
RUN apt-get update && apt-get install -y \
    git \
    curl \
    wget \
    python3 \
    python3-pip \
    nodejs \
    npm \
    docker.io \
    && rm -rf /var/lib/apt/lists/*

# Instalar extensiones de VS Code
RUN code-server --install-extension ms-python.python
RUN code-server --install-extension ms-vscode.vscode-typescript-next
RUN code-server --install-extension bradlc.vscode-tailwindcss

# Configurar Git
RUN git config --global user.name "Developer"
RUN git config --global user.email "dev@example.com"

# Volver al usuario coder
USER coder

# Configurar workspace
WORKDIR /home/coder/workspace

# Comando por defecto
CMD ["code-server", "--bind-addr", "0.0.0.0:8080", "--auth", "password"]
```

```bash
# Construir imagen personalizada
docker build -t mi-code-server .

# Ejecutar con configuración personalizada
docker run -d \
  --name mi-ide \
  -p 8080:8080 \
  -v $(pwd):/home/coder/workspace \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -e PASSWORD=mi-password-seguro \
  mi-code-server
```

**Ventajas de Code-Server:**

- **Acceso desde cualquier lugar** via navegador
- **Consistencia** entre diferentes máquinas
- **Recursos del servidor** en lugar de la máquina local
- **Colaboración** simplificada