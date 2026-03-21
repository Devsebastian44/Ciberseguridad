## Volúmenes Docker

Los volúmenes son el **mecanismo preferido para persistir datos** en Docker. Son gestionados completamente por Docker y viven fuera del filesystem del contenedor.

### ¿Por Qué Usar Volúmenes?

**Problema sin volúmenes:**

```bash
docker run -d --name db postgres:15
docker exec db psql -c "CREATE TABLE users..."
docker rm -f db
# ❌ ¡Todos los datos se pierden!
```

**Solución con volúmenes:**

```bash
docker run -d --name db -v pgdata:/var/lib/postgresql/data postgres:15
docker rm -f db
docker run -d --name db-new -v pgdata:/var/lib/postgresql/data postgres:15
# ✓ Los datos persisten entre contenedores
```

### Características Principales

- **Persistencia**: Sobreviven a la eliminación del contenedor
- **Independencia**: No dependen del ciclo de vida del contenedor
- **Compartición**: Múltiples contenedores pueden usar el mismo volumen
- **Portabilidad**: Fáciles de respaldar, restaurar y migrar
- **Rendimiento**: Mejor que bind mounts en Docker Desktop
- **Gestión**: Comandos dedicados para administrarlos

---

## Tipos de Almacenamiento

### Comparación de Métodos

|Característica|Volúmenes|Bind Mounts|tmpfs|
|---|---|---|---|
|**Gestión**|Docker|Usuario|Docker|
|**Ubicación**|`/var/lib/docker/volumes/`|Cualquier ruta|RAM|
|**Persistencia**|Sí|Sí|No (volátil)|
|**Rendimiento**|Alto|Medio|Muy alto|
|**Portabilidad**|Alta|Baja|N/A|
|**Uso ideal**|Producción, datos|Desarrollo|Datos temporales|
|**Respaldo**|Fácil|Manual|N/A|

### Cuándo Usar Cada Uno

**Volúmenes Docker** (Named Volumes):

- Bases de datos en producción
- Datos que deben persistir
- Compartir datos entre contenedores
- Facilitar backups y migraciones

**Bind Mounts**:

- Desarrollo local (hot reload)
- Archivos de configuración del host
- Compartir código fuente
- Logs accesibles desde el host

**tmpfs Mounts**:

- Datos sensibles temporales
- Cache de aplicación
- Archivos de sesión
- Build artifacts temporales

---

## Gestión de Volúmenes

### Comandos Básicos

```bash
# Crear volumen
docker volume create mi-volumen
docker volume create --driver local --opt type=none --opt device=/data --opt o=bind mi-vol

# Listar volúmenes
docker volume ls
docker volume ls -q                       # Solo nombres
docker volume ls --filter dangling=true   # Sin contenedor asociado

# Inspeccionar volumen
docker volume inspect mi-volumen
docker volume inspect --format '{{.Mountpoint}}' mi-volumen

# Eliminar volumen
docker volume rm mi-volumen
docker volume rm $(docker volume ls -q)   # Eliminar todos (¡cuidado!)

# Limpiar volúmenes huérfanos
docker volume prune
docker volume prune -f                     # Sin confirmación
```

### Información Detallada

```bash
# Ver ubicación física del volumen
docker volume inspect mi-volumen --format '{{.Mountpoint}}'
# Salida: /var/lib/docker/volumes/mi-volumen/_data

# Ver qué contenedores usan un volumen
docker ps -a --filter volume=mi-volumen

# Espacio usado por volúmenes
docker system df -v
```

---

## Usar Volúmenes en Contenedores

### Sintaxis de Montaje

```bash
# Sintaxis corta (-v)
docker run -v VOLUMEN:DESTINO[:OPCIONES] IMAGE

# Sintaxis larga (--mount) - recomendada
docker run --mount type=volume,source=VOLUMEN,target=DESTINO IMAGE
```

### Ejemplos Prácticos

```bash
# Crear volumen automáticamente (si no existe)
docker run -d --name db -v postgres-data:/var/lib/postgresql/data postgres:15

# Volumen de solo lectura
docker run -d --name app -v config-vol:/app/config:ro nginx

# Volumen con opciones específicas
docker run -d --name db \
  --mount type=volume,source=db-data,target=/var/lib/mysql,readonly=false \
  mysql:8

# Múltiples volúmenes
docker run -d --name app \
  -v app-data:/app/data \
  -v app-logs:/app/logs \
  -v app-config:/app/config:ro \
  mi-aplicacion

# Volumen con driver personalizado
docker volume create --driver local \
  --opt type=nfs \
  --opt o=addr=192.168.1.100,rw \
  --opt device=:/path/to/dir \
  nfs-volume
```

---

## Compartir Volúmenes entre Contenedores

### Patrón: Data Container

```bash
# Crear volumen compartido
docker volume create shared-logs

# Aplicación que escribe logs
docker run -d --name app \
  -v shared-logs:/var/log/app \
  mi-aplicacion

# Procesador de logs (ej: Logstash)
docker run -d --name logstash \
  -v shared-logs:/logs:ro \
  logstash:latest

# Visualizador de logs (ej: Graylog)
docker run -d --name viewer \
  -v shared-logs:/logs:ro \
  -p 9000:9000 \
  graylog/graylog
```

### Patrón: Sidecar Container

```bash
# Volumen para datos procesados
docker volume create processed-data

# Aplicación principal
docker run -d --name app \
  -v processed-data:/data \
  mi-app

# Sidecar para backup periódico
docker run -d --name backup-sidecar \
  -v processed-data:/data:ro \
  -v /backup:/backup \
  alpine sh -c "while true; do tar -czf /backup/data-$(date +%Y%m%d-%H%M%S).tar.gz /data; sleep 3600; done"
```

### Ejemplo Real: WordPress + MySQL

```bash
# Crear volúmenes
docker volume create wp-db-data
docker volume create wp-content

# Red dedicada
docker network create wordpress-net

# MySQL
docker run -d \
  --name wp-mysql \
  --network wordpress-net \
  -v wp-db-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=secretpass \
  -e MYSQL_DATABASE=wordpress \
  -e MYSQL_USER=wpuser \
  -e MYSQL_PASSWORD=wppass \
  mysql:8.0

# WordPress
docker run -d \
  --name wordpress \
  --network wordpress-net \
  -v wp-content:/var/www/html/wp-content \
  -p 8080:80 \
  -e WORDPRESS_DB_HOST=wp-mysql \
  -e WORDPRESS_DB_USER=wpuser \
  -e WORDPRESS_DB_PASSWORD=wppass \
  -e WORDPRESS_DB_NAME=wordpress \
  wordpress:latest
```

---

## Bind Mounts

### Sintaxis y Uso

```bash
# Sintaxis corta (-v)
docker run -v /ruta/host:/ruta/contenedor[:opciones] IMAGE

# Sintaxis larga (--mount) - más explícita
docker run --mount type=bind,source=/ruta/host,target=/ruta/contenedor IMAGE

# Usar directorio actual
docker run -v $(pwd):/app IMAGE          # Linux/Mac
docker run -v ${PWD}:/app IMAGE          # Windows PowerShell
docker run -v %cd%:/app IMAGE            # Windows CMD
```

### Casos de Uso Comunes

```bash
# Desarrollo web con hot reload
docker run -d --name dev-web \
  -v $(pwd)/src:/app/src \
  -v $(pwd)/public:/app/public \
  -v /app/node_modules \
  -p 3000:3000 \
  -e NODE_ENV=development \
  node:18-alpine npm run dev

# Compartir archivo de configuración
docker run -d --name nginx-custom \
  -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro \
  -v $(pwd)/html:/usr/share/nginx/html:ro \
  -p 80:80 \
  nginx:alpine

# Desarrollo con bases de datos
docker run -d --name postgres-dev \
  -v $(pwd)/postgres-data:/var/lib/postgresql/data \
  -v $(pwd)/init.sql:/docker-entrypoint-initdb.d/init.sql:ro \
  -p 5432:5432 \
  -e POSTGRES_PASSWORD=devpass \
  postgres:15

# Bind mount para logs
docker run -d --name app \
  -v /var/log/myapp:/app/logs \
  --log-driver json-file \
  mi-aplicacion
```

### Permisos y Propiedad

```bash
# Problema común: permisos incorrectos
docker run -v $(pwd)/data:/data alpine touch /data/file.txt
ls -l data/file.txt
# Salida: -rw-r--r-- 1 root root  # ⚠️ Creado como root

# Solución 1: Especificar usuario
docker run -u $(id -u):$(id -g) -v $(pwd)/data:/data alpine touch /data/file.txt

# Solución 2: En Dockerfile
FROM node:18-alpine
RUN addgroup -g 1000 appuser && adduser -D -u 1000 -G appuser appuser
USER appuser

# Solución 3: Cambiar permisos después
docker run -v $(pwd)/data:/data alpine sh -c "touch /data/file.txt && chown 1000:1000 /data/file.txt"
```

---

## tmpfs Mounts

### Uso de tmpfs (Linux únicamente)

```bash
# Crear tmpfs mount
docker run -d --name app --tmpfs /tmp:rw,noexec,nosuid,size=100m nginx

# Múltiples tmpfs
docker run -d --name app \
  --tmpfs /tmp:size=64m \
  --tmpfs /run:size=32m \
  mi-aplicacion

# Con --mount (sintaxis preferida)
docker run -d --name app \
  --mount type=tmpfs,destination=/tmp,tmpfs-size=100000000,tmpfs-mode=1770 \
  nginx
```

### Casos de Uso

```bash
# Cache temporal de aplicación
docker run -d --name api \
  -v api-data:/data \
  --tmpfs /tmp/cache:size=512m \
  mi-api

# Datos sensibles que no deben persistir
docker run -d --name secure-app \
  --tmpfs /app/secrets:size=10m,mode=700 \
  --read-only \
  mi-app-segura

# Build artifacts temporales
docker run --rm \
  -v $(pwd):/src \
  --tmpfs /build:exec \
  -w /src \
  gcc:latest make
```

---

## Backup y Restauración

### Backup de Volúmenes

```bash
# Método 1: Usando tar
docker run --rm \
  -v postgres-data:/data \
  -v $(pwd):/backup \
  alpine tar -czf /backup/postgres-backup-$(date +%Y%m%d).tar.gz /data

# Método 2: Exportar a archivo SQL (PostgreSQL)
docker exec postgres-db pg_dump -U admin mydb > backup.sql

# Método 3: Backup automático periódico
docker run -d --name backup-service \
  -v postgres-data:/data:ro \
  -v /backups:/backup \
  alpine sh -c "while true; do tar -czf /backup/backup-\$(date +%Y%m%d-%H%M).tar.gz /data; sleep 86400; done"
```

### Restauración de Volúmenes

```bash
# Método 1: Restaurar desde tar
docker run --rm \
  -v postgres-data:/data \
  -v $(pwd):/backup \
  alpine sh -c "rm -rf /data/* && tar -xzf /backup/postgres-backup-20240111.tar.gz -C /"

# Método 2: Restaurar desde SQL
docker exec -i postgres-db psql -U admin mydb < backup.sql

# Método 3: Copiar volumen completo
docker volume create postgres-data-new
docker run --rm \
  -v postgres-data:/from:ro \
  -v postgres-data-new:/to \
  alpine sh -c "cp -av /from/. /to"
```

### Migración de Volúmenes entre Hosts

```bash
# En host origen
docker run --rm \
  -v mi-volumen:/data \
  alpine tar -czf - /data | ssh user@destino "cat > volumen-backup.tar.gz"

# En host destino
docker volume create mi-volumen
cat volumen-backup.tar.gz | docker run --rm -i \
  -v mi-volumen:/data \
  alpine tar -xzf - -C /
```

---

## Redes Docker

### Drivers de Red

Docker soporta varios drivers de red con diferentes características:

|Driver|Descripción|Uso|
|---|---|---|
|**bridge**|Red aislada en el host (default)|Contenedores en mismo host|
|**host**|Usa red del host directamente|Alta performance, testing|
|**overlay**|Red entre múltiples hosts|Docker Swarm, Kubernetes|
|**macvlan**|Asigna MAC address al contenedor|Legacy apps, DHCP|
|**none**|Sin conectividad de red|Máximo aislamiento|

### Gestión de Redes

```bash
# Crear red
docker network create mi-red
docker network create --driver bridge mi-red-bridge
docker network create --driver overlay mi-red-swarm

# Listar redes
docker network ls
docker network ls --filter driver=bridge

# Inspeccionar red
docker network inspect mi-red
docker network inspect bridge --format '{{range .Containers}}{{.Name}} {{end}}'

# Eliminar red
docker network rm mi-red
docker network prune                      # Limpiar redes sin usar

# Ver qué contenedores están en una red
docker network inspect mi-red --format '{{range .Containers}}{{.Name}}: {{.IPv4Address}}{{println}}{{end}}'
```

### Crear Redes Personalizadas

```bash
# Red con subnet específica
docker network create --subnet=172.20.0.0/16 mi-red-custom

# Red con gateway personalizado
docker network create \
  --subnet=172.20.0.0/16 \
  --gateway=172.20.0.1 \
  mi-red-gw

# Red con múltiples subnets (IPv4 + IPv6)
docker network create \
  --subnet=172.20.0.0/16 \
  --subnet=2001:db8::/64 \
  --ipv6 \
  mi-red-dual

# Red con opciones avanzadas
docker network create \
  --driver bridge \
  --subnet 172.25.0.0/16 \
  --ip-range 172.25.5.0/24 \
  --gateway 172.25.0.1 \
  --opt com.docker.network.bridge.name=my-bridge \
  --opt com.docker.network.bridge.enable_icc=true \
  mi-red-avanzada
```

---

## Conectar Contenedores a Redes

### Uso Básico

```bash
# Conectar al crear el contenedor
docker run -d --name web --network mi-red nginx

# Conectar contenedor existente
docker network connect mi-red contenedor-existente

# Desconectar
docker network disconnect mi-red contenedor-existente

# Conectar con IP estática
docker network connect --ip 172.20.0.10 mi-red mi-contenedor

# Conectar con alias
docker network connect --alias webserver mi-red nginx-container
```

### Múltiples Redes

```bash
# Contenedor en múltiples redes
docker run -d --name app \
  --network frontend \
  nginx

docker network connect backend app

# Verificar redes del contenedor
docker inspect app --format '{{range $net, $config := .NetworkSettings.Networks}}{{$net}}: {{$config.IPAddress}}{{println}}{{end}}'
```

---

## Comunicación entre Contenedores

### DNS Automático en Redes Personalizadas

```bash
# Crear red
docker network create app-net

# Contenedor 1: Base de datos
docker run -d --name database --network app-net postgres:15

# Contenedor 2: Backend (puede usar "database" como hostname)
docker run -d --name backend --network app-net \
  -e DB_HOST=database \
  -e DB_PORT=5432 \
  mi-backend

# Contenedor 3: Frontend (puede usar "backend" como hostname)
docker run -d --name frontend --network app-net \
  -p 80:80 \
  -e API_URL=http://backend:3000 \
  mi-frontend

# Verificar conectividad
docker exec backend ping -c 2 database
docker exec frontend wget -O- http://backend:3000/health
```

### Ejemplo: Stack MERN Completo

```bash
# Crear red dedicada
docker network create mern-stack

# MongoDB
docker run -d \
  --name mongodb \
  --network mern-stack \
  -v mongo-data:/data/db \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=secret \
  mongo:6

# Express Backend
docker run -d \
  --name backend \
  --network mern-stack \
  -v $(pwd)/backend:/app \
  -w /app \
  -e MONGODB_URI=mongodb://admin:secret@mongodb:27017/myapp?authSource=admin \
  -e PORT=5000 \
  node:18-alpine npm start

# React Frontend
docker run -d \
  --name frontend \
  --network mern-stack \
  -v $(pwd)/frontend:/app \
  -v /app/node_modules \
  -w /app \
  -p 3000:3000 \
  -e REACT_APP_API_URL=http://localhost:5000 \
  node:18-alpine npm start

# Nginx reverse proxy
docker run -d \
  --name nginx \
  --network mern-stack \
  -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro \
  -p 80:80 \
  nginx:alpine
```

---

## Red Bridge (Default)

### Características

La red `bridge` es la red por defecto cuando no se especifica ninguna.

```bash
# Contenedor en red bridge default
docker run -d --name web1 nginx

# Inspeccionar red bridge
docker network inspect bridge

# Ver IP del contenedor
docker inspect --format='{{.NetworkSettings.IPAddress}}' web1
```

### Limitaciones de la Red Bridge Default

```bash
# ❌ NO funciona: Los contenedores NO pueden comunicarse por nombre
docker run -d --name db postgres:15
docker run -d --name app mi-app
docker exec app ping db
# ping: db: Name or service not known

# ✓ Funciona: Usar red personalizada
docker network create mi-red
docker run -d --name db --network mi-red postgres:15
docker run -d --name app --network mi-red mi-app
docker exec app ping db
# PING db (172.18.0.2): 56 data bytes
```

**Recomendación:** Siempre usar redes personalizadas en lugar de la bridge default.

---

## Red Host

### Uso y Limitaciones

```bash
# Contenedor usa red del host directamente
docker run -d --name nginx-host --network host nginx

# No necesita -p porque usa puertos del host directamente
# nginx escuchará en localhost:80 automáticamente
```

### Cuándo Usar

**Ventajas:**

- Máximo rendimiento de red (sin NAT)
- No hay overhead de virtualización de red
- Acceso directo a interfaces del host

**Desventajas:**

- Sin aislamiento de red
- Conflictos de puertos con host
- No portable (solo Linux)
- Problemas de seguridad

**Casos de uso:**

```bash
# Monitoreo de red
docker run -d --name netdata --network host netdata/netdata

# Performance testing
docker run --rm --network host alpine ping -c 5 google.com

# Herramientas de red
docker run --rm --network host nicolaka/netshoot
```

---

## Red Overlay (Docker Swarm)

### Para Clústeres Multi-Host

```bash
# Crear red overlay (requiere Swarm mode)
docker swarm init
docker network create --driver overlay --attachable mi-overlay

# Desplegar servicios en la red overlay
docker service create --name web --network mi-overlay --replicas 3 nginx

# Los contenedores en diferentes hosts se comunican transparentemente
```

---

## Aislamiento y Seguridad

### Separar Aplicaciones con Redes

```bash
# Aplicación 1: Blog
docker network create blog-net
docker run -d --name blog-db --network blog-net postgres:15
docker run -d --name blog-app --network blog-net -p 8080:80 wordpress

# Aplicación 2: Tienda
docker network create shop-net
docker run -d --name shop-db --network shop-net mysql:8
docker run -d --name shop-app --network shop-net -p 8081:80 magento

# Las aplicaciones están completamente aisladas entre sí
```

### Red None (Sin Red)

```bash
# Contenedor sin conectividad de red
docker run -d --name isolated --network none alpine sleep infinity

# Útil para:
# - Procesamiento de datos sensibles
# - Builds seguros
# - Máximo aislamiento
```

---

## Troubleshooting de Redes

### Herramientas de Diagnóstico

```bash
# Verificar conectividad básica
docker exec CONTAINER ping google.com
docker exec CONTAINER ping otro-contenedor

# Ver configuración de red del contenedor
docker inspect CONTAINER --format '{{.NetworkSettings}}'

# Ver todas las IPs de un contenedor
docker inspect CONTAINER | jq '.[0].NetworkSettings.Networks'

# Probar resolución DNS
docker exec CONTAINER nslookup google.com
docker exec CONTAINER cat /etc/resolv.conf

# Verificar puertos abiertos
docker exec CONTAINER netstat -tulpn

# Usar contenedor de debugging con herramientas de red
docker run -it --rm --network container:CONTAINER nicolaka/netshoot

# Capturar tráfico de red
docker run --rm --net host \
  -v $(pwd):/data \
  nicolaka/netshoot tcpdump -i any -w /data/capture.pcap
```

### Problemas Comunes

```bash
# Problema: Contenedores no se ven entre sí
# Solución: Verificar que están en la misma red
docker network inspect mi-red

# Problema: No hay resolución DNS
# Solución: Usar red personalizada (no bridge default)
docker network create mi-red
docker run --network mi-red ...

# Problema: Puerto ya en uso
# Solución: Usar otro puerto del host
docker run -p 8081:80 nginx  # En lugar de 8080

# Problema: No puede alcanzar internet
# Solución: Verificar DNS y gateway
docker exec CONTAINER cat /etc/resolv.conf
docker network inspect bridge --format '{{.IPAM.Config}}'
```

---

## Buenas Prácticas

### Volúmenes

1. **Usar named volumes en producción**

```bash
# ✓ Correcto
docker run -v postgres-data:/var/lib/postgresql/data postgres:15
   
# ❌ Evitar volúmenes anónimos en producción
docker run -v /var/lib/postgresql/data postgres:15
```

2. **Implementar estrategia de backup**

```bash
# Backup diario automatizado
0 2 * * * docker run --rm -v db-data:/data -v /backups:/backup alpine tar czf /backup/db-$(date +\%Y\%m\%d).tar.gz /data
```

3. **Usar volúmenes para persistencia, bind mounts para desarrollo**

```bash
# Producción
docker run -v app-data:/app/data mi-app

# Desarrollo
docker run -v $(pwd)/src:/app/src mi-app
```

4. **Documentar volúmenes requeridos**

```dockerfile
# En Dockerfile
VOLUME ["/app/data", "/app/logs"]
```
    

### Redes

1. **Siempre usar redes personalizadas**

```bash
# ✓ Correcto - permite DNS entre contenedores
docker network create mi-app
docker run --network mi-app ...

# ❌ Evitar red bridge default
docker run ...  # Sin --network
```

2. **Una red por aplicación/stack**

```bash
docker network create wordpress-net
docker network create nextcloud-net
# Aislamiento entre aplicaciones
```

3. **Usar nombres descriptivos**

```bash
# ✓ Descriptivo
docker network create ecommerce-frontend
docker network create ecommerce-backend

# ❌ Genérico
docker network create net1
```
    
4. **Limitar exposición de puertos**
    
```bash
# ✓ Solo exponer lo necesario
docker run -p 127.0.0.1:5432:5432 postgres  # Solo localhost

# ❌ Exponer a internet innecesariamente
docker run -p 5432:5432 postgres
```

---

## Resumen de Comandos

### Volúmenes

```bash
docker volume create VOLUME
docker volume ls
docker volume inspect VOLUME
docker volume rm VOLUME
docker volume prune

docker run -v VOLUME:/path IMAGE
docker run --mount type=volume,src=VOL,dst=/path IMAGE
```

### Redes

```bash
docker network create NETWORK
docker network ls
docker network inspect NETWORK
docker network rm NETWORK
docker network prune

docker network connect NETWORK CONTAINER
docker network disconnect NETWORK CONTAINER

docker run --network NETWORK IMAGE
```

### Inspección

```bash
docker inspect CONTAINER
docker stats CONTAINER
docker exec CONTAINER ping HOST
docker logs CONTAINER
```