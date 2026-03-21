## ¿Qué es Docker?

Docker es una **plataforma de contenedorización** que permite empaquetar aplicaciones y sus dependencias en **contenedores ligeros y portables**.

### Ventajas Principales

- **Portabilidad**: Funciona igual en desarrollo, staging y producción
- **Eficiencia**: Comparte el kernel del SO, usa menos recursos que VMs
- **Consistencia**: Elimina el problema de "en mi máquina funciona"
- **Microservicios**: Ideal para arquitecturas distribuidas

---

## Virtualización vs Contenedorización

|Aspecto|Máquinas Virtuales|Contenedores Docker|
|---|---|---|
|**Tamaño**|2-10 GB|50-500 MB|
|**Inicio**|1-5 minutos|1-3 segundos|
|**Sistema Operativo**|SO completo por VM|Comparte kernel del host|
|**Rendimiento**|Overhead significativo|Casi nativo|

**Cuándo usar Contenedores:** Microservicios, CI/CD, desarrollo ágil, escalado rápido.

---

## Conceptos Fundamentales

### 1. Imagen (Image)

Plantilla de solo lectura con todo lo necesario para ejecutar una aplicación.

- Inmutable - no cambia una vez creada
- Basada en capas (layered filesystem)
- Se construye desde un Dockerfile
- Versionada mediante tags (ej: `nginx:1.21`, `node:18-alpine`)

### 2. Contenedor (Container)

Instancia ejecutable de una imagen. Es el proceso aislado corriendo tu aplicación.

**Estados:** `running`, `stopped`, `paused`, `exited`

### 3. Dockerfile

Archivo de texto con instrucciones para construir una imagen.

**Instrucciones comunes:**

- `FROM` - Imagen base
- `WORKDIR` - Directorio de trabajo
- `COPY` - Copiar archivos
- `RUN` - Ejecutar comandos al construir
- `CMD` - Comando por defecto al iniciar
- `EXPOSE` - Puerto que expone

### 4. Volúmenes (Volumes)

Mecanismo para persistir datos fuera del contenedor.

### 5. Redes (Networks)

Permiten comunicación entre contenedores (tipo `bridge` es el más común).

---

## Instalación

### Linux (Ubuntu/Debian)

```bash
# Instalación rápida
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Añadir usuario al grupo docker
sudo usermod -aG docker $USER
newgrp docker

# Verificar
docker --version
docker run hello-world
```

### Windows y macOS

1. Descargar **Docker Desktop** desde [docker.com](https://www.docker.com/products/docker-desktop) 
2. Instalar y reiniciar 
3. Verificar: `docker --version`

**Requisitos Windows:** Windows 10/11 Pro con WSL 2 habilitado

---

## Comandos Esenciales

### Gestión de Contenedores

```bash
# Ejecutar contenedor
docker run -d -p 8080:80 --name mi-nginx nginx

# Listar
docker ps                    # En ejecución
docker ps -a                 # Todos

# Gestionar
docker start <contenedor>
docker stop <contenedor>
docker rm <contenedor>

# Ejecutar comandos
docker exec -it <contenedor> bash

# Ver logs
docker logs -f <contenedor>
```

### Gestión de Imágenes

```bash
# Descargar
docker pull nginx:1.21

# Listar y eliminar
docker images
docker rmi nginx:1.21

# Construir imagen
docker build -t mi-app:1.0 .

# Limpiar
docker system prune -a
```

### Gestión de Volúmenes

```bash
# Crear
docker volume create mi-datos

# Usar volúmenes
docker run -v mi-datos:/app/data nginx       # Named volume
docker run -v /ruta/host:/app/data nginx     # Bind mount
```

---

## Ejemplo Práctico

### Dockerfile

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY . .
EXPOSE 3000
USER node
CMD ["node", "server.js"]
```

### Construcción y Ejecución

```bash
# Construir
docker build -t mi-web-app:1.0 .

# Ejecutar
docker run -d \
  --name mi-app \
  -p 3000:3000 \
  -e NODE_ENV=production \
  mi-web-app:1.0
```

---

## Buenas Prácticas

- Nunca ejecutes contenedores como root (usa `USER`)
- Usa imágenes base pequeñas (alpine, distroless)
- Aprovecha la caché de capas (COPY package.json antes que código)
- Usa .dockerignore para excluir archivos innecesarios
- Implementa health checks y restart policies en producción
- Un proceso por contenedor

---

## Solución de Problemas

```bash
# Ver logs de error
docker logs <contenedor>

# Limpiar espacio
docker system prune -a --volumes

# Ver uso de espacio
docker system df
```