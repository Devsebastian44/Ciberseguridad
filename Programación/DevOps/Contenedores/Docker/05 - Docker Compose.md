## ¿Qué es Docker Compose?

Docker Compose es una herramienta para **definir y ejecutar aplicaciones Docker multi-contenedor**. Utiliza un archivo YAML para configurar los servicios de tu aplicación, y con un solo comando, puedes crear e iniciar todos los servicios.

### Ventajas

- **Definición declarativa** de la infraestructura
- **Gestión de múltiples servicios** como una sola aplicación
- **Reproducibilidad** en diferentes entornos
- **Escalabilidad** fácil de servicios
- **Gestión de dependencias** entre contenedores

### Instalación

Docker Compose viene incluido con Docker Desktop. Para Linux:

```bash
# Instalar Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Verificar instalación
docker-compose --version
````

---

## Servicios

### Estructura Básica del `docker-compose.yml`

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    
  db:
    image: postgres:13
    environment:
      POSTGRES_PASSWORD: secretpassword
```

### Ejemplo Completo con Múltiples Servicios

```yaml
version: '3.8'

services:
  # Servidor web
  web:
    image: nginx:alpine
    container_name: web-server
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./html:/usr/share/nginx/html
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - api
    restart: unless-stopped

  # API backend
  api:
    build:
      context: ./api
      dockerfile: Dockerfile
    container_name: api-server
    ports:
      - "3000:3000"
    environment:
      NODE_ENV: production
      DB_HOST: db
      DB_PORT: 5432
    depends_on:
      - db
      - redis
    volumes:
      - ./api:/app
      - /app/node_modules
    restart: unless-stopped

  # Base de datos
  db:
    image: postgres:13
    container_name: postgres-db
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secretpassword
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    restart: unless-stopped

  # Cache Redis
  redis:
    image: redis:7-alpine
    container_name: redis-cache
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    restart: unless-stopped

volumes:
  postgres_data:
  redis_data:
```

### Comandos Básicos

```bash
# Iniciar todos los servicios
docker-compose up

# Iniciar en segundo plano
docker-compose up -d

# Iniciar servicios específicos
docker-compose up web db

# Detener servicios
docker-compose down

# Detener y eliminar volúmenes
docker-compose down -v

# Ver logs
docker-compose logs

# Ver logs de un servicio específico
docker-compose logs web

# Seguir logs en tiempo real
docker-compose logs -f

# Escalar servicios
docker-compose up --scale web=3

# Reconstruir imágenes
docker-compose build

# Reiniciar servicios
docker-compose restart
```

---

## Redes

### Redes Automáticas

Docker Compose crea automáticamente una **red** para tu aplicación:

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    # Puede comunicarse con 'api' por nombre
    
  api:
    image: node:alpine
    # Puede comunicarse con 'web' por nombre
```

**Ventaja**: Los servicios pueden comunicarse entre sí usando sus **nombres** como hostname.

### Redes Personalizadas

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    networks:
      - frontend
      - backend
    
  api:
    image: node:alpine
    networks:
      - backend
    
  db:
    image: postgres:13
    networks:
      - backend

networks:
  frontend:
    driver: bridge
  backend:
    driver: bridge
    internal: true  # Solo comunicación interna
```

### Redes Externas

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    networks:
      - default
      - external_network

networks:
  external_network:
    external: true
    name: mi-red-externa
```

---

## Volúmenes

### Volúmenes Nombrados

```yaml
version: '3.8'

services:
  db:
    image: postgres:13
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - postgres_logs:/var/log/postgresql
    
  web:
    image: nginx:alpine
    volumes:
      - web_content:/usr/share/nginx/html

volumes:
  postgres_data:
    driver: local
  postgres_logs:
    driver: local
  web_content:
    driver: local
```

### Bind Mounts

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    volumes:
      - ./html:/usr/share/nginx/html:ro  # Solo lectura
      - ./logs:/var/log/nginx:rw         # Lectura y escritura
      - /etc/localtime:/etc/localtime:ro # Sincronizar tiempo
```

### Volúmenes Externos

```yaml
version: '3.8'

services:
  db:
    image: postgres:13
    volumes:
      - external_data:/var/lib/postgresql/data

volumes:
  external_data:
    external: true
    name: mi-volumen-externo
```

---

## Variables de Entorno

### Definir Variables en el Compose

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    environment:
      - NGINX_HOST=localhost
      - NGINX_PORT=80
      - DEBUG=true
    
  db:
    image: postgres:13
    environment:
      POSTGRES_DB: ${DB_NAME:-myapp}
      POSTGRES_USER: ${DB_USER:-admin}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
```

### Archivo `.env`

```bash
# .env
DB_NAME=myapp
DB_USER=admin
DB_PASSWORD=secretpassword
API_PORT=3000
WEB_PORT=8080
NODE_ENV=production
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  web:
    image: nginx:alpine
    ports:
      - "${WEB_PORT}:80"
    
  api:
    build: ./api
    ports:
      - "${API_PORT}:3000"
    environment:
      - NODE_ENV=${NODE_ENV}
      - DB_HOST=db
    
  db:
    image: postgres:13
    environment:
      POSTGRES_DB: ${DB_NAME}
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
```

### Archivo de Variables Específico

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    env_file:
      - ./config/web.env
      - ./config/common.env
    
  api:
    build: ./api
    env_file:
      - ./config/api.env
      - ./config/common.env
```

---

## Stack Local

### Aplicación Web Completa

```yaml
# docker-compose.yml
version: '3.8'

services:
  # Proxy reverso
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./nginx/ssl:/etc/nginx/ssl
      - web_static:/usr/share/nginx/html
    depends_on:
      - web
      - api
    restart: unless-stopped

  # Frontend React
  web:
    build:
      context: ./frontend
      dockerfile: Dockerfile
      args:
        NODE_ENV: production
    volumes:
      - web_static:/app/build
    depends_on:
      - api
    restart: unless-stopped

  # Backend API
  api:
    build:
      context: ./backend
      dockerfile: Dockerfile
    environment:
      NODE_ENV: production
      DB_HOST: db
      DB_PORT: 5432
      DB_NAME: ${DB_NAME}
      DB_USER: ${DB_USER}
      DB_PASSWORD: ${DB_PASSWORD}
      REDIS_HOST: redis
      REDIS_PORT: 6379
      JWT_SECRET: ${JWT_SECRET}
    depends_on:
      - db
      - redis
    volumes:
      - ./backend:/app
      - /app/node_modules
    restart: unless-stopped

  # Base de datos principal
  db:
    image: postgres:13
    environment:
      POSTGRES_DB: ${DB_NAME}
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./database/init:/docker-entrypoint-initdb.d
    restart: unless-stopped

  # Cache Redis
  redis:
    image: redis:7-alpine
    command: redis-server --appendonly yes
    volumes:
      - redis_data:/data
    restart: unless-stopped

  # Monitoreo
  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./monitoring/prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    environment:
      GF_SECURITY_ADMIN_PASSWORD: ${GRAFANA_PASSWORD}
    volumes:
      - grafana_data:/var/lib/grafana
    depends_on:
      - prometheus
    restart: unless-stopped

volumes:
  postgres_data:
  redis_data:
  web_static:
  prometheus_data:
  grafana_data:

networks:
  default:
    driver: bridge
```

---

## Docker Compose Build

### Configuración de Build

```yaml
version: '3.8'

services:
  web:
    build:
      context: ./frontend        # Directorio de contexto
      dockerfile: Dockerfile     # Nombre del Dockerfile
      args:                      # Argumentos de construcción
        NODE_ENV: production
        BUILD_VERSION: ${BUILD_VERSION}
      target: production         # Stage específico en multi-stage
    image: mi-web:latest         # Nombre de la imagen resultante
    
  api:
    build:
      context: ./backend
      dockerfile: Dockerfile.prod
      cache_from:                # Imágenes para cache
        - mi-api:latest
        - node:16-alpine
    image: mi-api:${VERSION:-latest}
```

### Multi-stage Build

```dockerfile
# Dockerfile para frontend
FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine AS production
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  web:
    build:
      context: ./frontend
      target: production  # Usar stage específico
    ports:
      - "80:80"
```

### Comandos de Build

```bash
# Construir todas las imágenes
docker-compose build

# Construir imagen específica
docker-compose build web

# Construir sin cache
docker-compose build --no-cache

# Construir con argumentos
docker-compose build --build-arg NODE_ENV=production

# Construir y ejecutar
docker-compose up --build

# Reconstruir solo si hay cambios
docker-compose up --build web
```

**Opciones útiles**:

- **`--no-cache`**: Ignora caché y reconstruye desde cero
- **`--pull`**: Descarga versiones más recientes de imágenes base
- **`--parallel`**: Construye imágenes en paralelo