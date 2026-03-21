## ¿Qué son las Imágenes?

Las imágenes Docker son **plantillas de solo lectura** que contienen:

- **Sistema operativo base** (Ubuntu, Alpine, etc.)
- **Aplicaciones y dependencias**
- **Configuración del entorno**
- **Metadatos e instrucciones**

### Arquitectura de Capas

```

[Capa 4] Aplicación y configuración [Capa 3] Dependencias y librerías [Capa 2] Herramientas del sistema [Capa 1] Sistema operativo base

````

**Ventaja del sistema de capas**: Las capas son **reutilizables** y se almacenan en caché, acelerando construcciones posteriores.

---

## Primera Imagen

### Crear un Dockerfile Básico

```dockerfile
# Dockerfile
FROM ubuntu:20.04

# Actualizar sistema
RUN apt-get update && apt-get install -y \
    curl \
    vim \
    && rm -rf /var/lib/apt/lists/*

# Comando por defecto
CMD ["bash"]
````

### Construir la Imagen

```bash
# Construir imagen
docker build -t mi-primera-imagen .

# Construir con tag específico
docker build -t mi-primera-imagen:v1.0 .

# Ver la imagen creada
docker images

# Ejecutar contenedor desde la imagen
docker run -it mi-primera-imagen
```

---

## Copiando Archivos

### Instrucción `COPY`

```dockerfile
FROM nginx:alpine

# Copiar archivos locales al contenedor
COPY index.html /usr/share/nginx/html/
COPY css/ /usr/share/nginx/html/css/
COPY js/ /usr/share/nginx/html/js/

# Copiar con permisos específicos
COPY --chown=nginx:nginx config.conf /etc/nginx/conf.d/
```

### Instrucción `ADD`

```dockerfile
FROM ubuntu:20.04

# ADD puede descomprimir archivos
ADD mi-archivo.tar.gz /app/

# ADD puede descargar desde URLs
ADD https://example.com/file.zip /tmp/

# Recomendación: usar COPY para archivos locales
COPY mi-archivo.txt /app/
```

**Diferencia entre `COPY` y `ADD`**:

- **`COPY`**: Solo copia archivos/directorios locales (recomendado)
- **`ADD`**: Tiene funcionalidades extra (descompresión, URLs) pero menos predecible

### Ejemplo Práctico: Aplicación Web

```dockerfile
FROM nginx:alpine

# Copiar contenido web
COPY ./html/ /usr/share/nginx/html/

# Exponer puerto
EXPOSE 80

# Nginx se ejecuta automáticamente
```

```bash
# Estructura del proyecto
./
├── Dockerfile
└── html/
    ├── index.html
    ├── style.css
    └── script.js

# Construir y ejecutar
docker build -t mi-web .
docker run -d -p 8080:80 mi-web
```

---

## Variables de Entorno

### Definir Variables en Dockerfile

```dockerfile
FROM node:16-alpine

# Variables de entorno
ENV NODE_ENV=production
ENV PORT=3000
ENV DB_HOST=localhost

# También se puede hacer en una línea
ENV NODE_ENV=production \
    PORT=3000 \
    DB_HOST=localhost

# Usar variables
RUN echo "Running in $NODE_ENV mode"

EXPOSE $PORT
```

### Variables de Construcción (`ARG`)

```dockerfile
FROM node:16-alpine

# Argumentos de construcción
ARG VERSION=latest
ARG BUILD_DATE

# Usar argumentos
LABEL version=$VERSION
LABEL build-date=$BUILD_DATE

# Convertir ARG en ENV
ENV APP_VERSION=$VERSION
```

```bash
# Construir con argumentos
docker build --build-arg VERSION=1.2.3 --build-arg BUILD_DATE=$(date) -t mi-app .
```

**Diferencia entre `ARG` y `ENV`**:

- **`ARG`**: Solo disponible durante la construcción
- **`ENV`**: Disponible durante construcción y ejecución

---

## Ejecutar Archivos

### Instrucción `RUN`

```dockerfile
FROM ubuntu:20.04

# Ejecutar comandos durante la construcción
RUN apt-get update
RUN apt-get install -y python3 python3-pip
RUN pip3 install flask

# Mejor práctica: combinar comandos
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    pip3 install flask && \
    rm -rf /var/lib/apt/lists/*
```

### Optimización de Capas

```dockerfile
# ❌ Crea muchas capas
FROM ubuntu:20.04
RUN apt-get update
RUN apt-get install -y python3
RUN apt-get install -y python3-pip
RUN pip3 install flask
RUN apt-get clean

# ✅ Crea una sola capa
FROM ubuntu:20.04
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    pip3 install flask && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
```

**Ventajas de combinar comandos**:

- Menos capas = imagen más pequeña
- Mejor uso de caché
- Limpieza en la misma capa

---

## `ENTRYPOINT` vs `CMD`

### `CMD` - Comando por Defecto

```dockerfile
FROM ubuntu:20.04

# CMD puede ser sobrescrito
CMD ["echo", "Hola Docker"]

# Al ejecutar:
# docker run mi-imagen              -> "Hola Docker"
# docker run mi-imagen echo "Adiós" -> "Adiós"
```

### `ENTRYPOINT` - Punto de Entrada

```dockerfile
FROM ubuntu:20.04

# ENTRYPOINT no puede ser sobrescrito
ENTRYPOINT ["echo", "Mensaje:"]

# Al ejecutar:
# docker run mi-imagen              -> "Mensaje:"
# docker run mi-imagen "Hola"       -> "Mensaje: Hola"
```

### Combinando `ENTRYPOINT` y `CMD`

```dockerfile
FROM ubuntu:20.04

# ENTRYPOINT define el comando base
ENTRYPOINT ["echo"]

# CMD define argumentos por defecto
CMD ["Hola Docker"]

# Al ejecutar:
# docker run mi-imagen              -> "Hola Docker"
# docker run mi-imagen "Adiós"      -> "Adiós"
```

**Cuándo usar cada uno**:

- **`CMD`**: Para comandos que el usuario puede sobrescribir fácilmente
- **`ENTRYPOINT`**: Para definir el ejecutable principal de la imagen
- **Combinados**: `ENTRYPOINT` para el comando, `CMD` para argumentos por defecto

---

## Dockerizar Script Python

### Ejemplo Completo

```python
# app.py
from flask import Flask
import os

app = Flask(__name__)

@app.route('/')
def hello():
    return f"Hola desde Python! Versión: {os.getenv('APP_VERSION', '1.0')}"

@app.route('/health')
def health():
    return {"status": "ok"}

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=int(os.getenv('PORT', 5000)))
```

```txt
# requirements.txt
Flask==2.3.3
```

```dockerfile
# Dockerfile
FROM python:3.11-slim

# Variables de entorno
ENV APP_VERSION=1.0
ENV PORT=5000

# Directorio de trabajo
WORKDIR /app

# Copiar requirements primero (mejor cache)
COPY requirements.txt .

# Instalar dependencias
RUN pip install --no-cache-dir -r requirements.txt

# Copiar código fuente
COPY app.py .

# Exponer puerto
EXPOSE $PORT

# Usuario no root (seguridad)
RUN useradd -m appuser
USER appuser

# Comando por defecto
CMD ["python", "app.py"]
```

```bash
# Construir y ejecutar
docker build -t python-app .
docker run -d -p 5000:5000 --name mi-python-app python-app

# Probar la aplicación
curl http://localhost:5000
curl http://localhost:5000/health
```

---

## Docker Hub

### Subir Imagen a Docker Hub

```bash
# 1. Crear cuenta en hub.docker.com
# 2. Iniciar sesión
docker login

# 3. Etiquetar imagen con tu usuario
docker tag mi-imagen tu-usuario/mi-imagen:latest

# 4. Subir imagen
docker push tu-usuario/mi-imagen:latest

# 5. Subir con múltiples tags
docker tag mi-imagen tu-usuario/mi-imagen:v1.0
docker push tu-usuario/mi-imagen:v1.0
```

### Automatizar con GitHub Actions

```yaml
# .github/workflows/docker.yml
name: Docker Build and Push

on:
  push:
    branches: [ main ]
    tags: [ 'v*' ]

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    
    - name: Login to Docker Hub
      uses: docker/login-action@v2
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}
    
    - name: Build and push
      uses: docker/build-push-action@v4
      with:
        context: .
        push: true
        tags: tu-usuario/mi-imagen:latest
```

---

## Dockerizar Script Node.js

### Ejemplo con Express

```javascript
// server.js
const express = require('express');
const app = express();
const port = process.env.PORT || 3000;

app.get('/', (req, res) => {
  res.json({
    message: 'Hola desde Node.js!',
    version: process.env.APP_VERSION || '1.0.0',
    timestamp: new Date().toISOString()
  });
});

app.get('/health', (req, res) => {
  res.json({ status: 'ok' });
});

app.listen(port, '0.0.0.0', () => {
  console.log(`Servidor corriendo en puerto ${port}`);
});
```

```json
{
  "name": "node-docker-app",
  "version": "1.0.0",
  "description": "Aplicación Node.js con Docker",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  },
  "devDependencies": {
    "nodemon": "^3.0.1"
  }
}
```

```dockerfile
# Dockerfile
FROM node:18-alpine

# Metadatos
LABEL maintainer="tu-email@example.com"
LABEL version="1.0"

# Variables de entorno
ENV NODE_ENV=production
ENV PORT=3000

# Directorio de trabajo
WORKDIR /app

# Copiar package.json primero (mejor cache)
COPY package*.json ./

# Instalar dependencias
RUN npm ci --only=production && npm cache clean --force

# Copiar código fuente
COPY server.js .

# Usuario no root
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nodeuser -u 1001
USER nodeuser

# Exponer puerto
EXPOSE $PORT

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:$PORT/health || exit 1

# Comando por defecto
CMD ["npm", "start"]
```

```bash
# Construir imagen optimizada
docker build -t node-app .

# Ejecutar con variables de entorno
docker run -d \
  --name mi-node-app \
  -p 3000:3000 \
  -e APP_VERSION=1.2.3 \
  -e NODE_ENV=production \
  node-app

# Verificar health check
docker ps  # Debería mostrar (healthy)
```

**Buenas prácticas aplicadas**:

- Uso de **Alpine** para imágenes más ligeras
- **Cache de dependencias** (copiar `package.json` primero)
- **Usuario no root** para seguridad
- **Health check** para monitoreo