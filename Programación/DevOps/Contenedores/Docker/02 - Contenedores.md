## Comandos Básicos

### Gestión de Contenedores

```bash
# Listar contenedores en ejecución
docker ps

# Listar todos los contenedores (incluyendo detenidos)
docker ps -a

# Ejecutar un contenedor
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

# Detener un contenedor
docker stop CONTAINER_ID

# Iniciar un contenedor detenido
docker start CONTAINER_ID

# Reiniciar un contenedor
docker restart CONTAINER_ID

# Eliminar un contenedor
docker rm CONTAINER_ID

# Eliminar todos los contenedores detenidos
docker container prune

# Información detallada del contenedor
docker inspect CONTAINER_ID
````

### Ejemplos Prácticos

```bash
# Ejecutar nginx
docker run nginx

# Ejecutar nginx con nombre personalizado
docker run --name mi-nginx nginx

# Ejecutar nginx en segundo plano
docker run -d nginx

# Ejecutar nginx con puerto mapeado
docker run -d -p 8080:80 nginx
```

---

## Contenedores en Segundo Plano

### Modo Daemon (`-d`)

```bash
# Ejecutar contenedor en segundo plano
docker run -d nginx

# Ejecutar con nombre personalizado
docker run -d --name web-server nginx

# Ejecutar con reinicio automático
docker run -d --restart=always nginx

# Ejecutar con límites de recursos
docker run -d --memory=512m --cpus=1 nginx
```

### Opciones de Reinicio

```bash
# Nunca reiniciar
docker run -d --restart=no nginx

# Reiniciar siempre
docker run -d --restart=always nginx

# Reiniciar si falla
docker run -d --restart=on-failure nginx

# Reiniciar si falla (máximo 3 intentos)
docker run -d --restart=on-failure:3 nginx
```

**Políticas de reinicio:**

- **`no`**: No reinicia automáticamente (por defecto)
- **`always`**: Siempre reinicia el contenedor
- **`on-failure`**: Solo reinicia si el contenedor falla
- **`on-failure:N`**: Reinicia máximo N veces

---

## Modo Interactivo

### Ejecutar Contenedor Interactivo

```bash
# Ejecutar bash en Ubuntu
docker run -it ubuntu bash

# Ejecutar comandos específicos
docker run -it ubuntu ls -la

# Ejecutar Python interactivo
docker run -it python python3

# Conectar a contenedor en ejecución
docker exec -it CONTAINER_ID bash
```

### Ejemplo Práctico: Explorar un Contenedor

```bash
# Iniciar Ubuntu interactivo
docker run -it --name mi-ubuntu ubuntu bash

# Dentro del contenedor:
apt update
apt install curl
curl --version
exit

# Reconectar al mismo contenedor
docker start mi-ubuntu
docker exec -it mi-ubuntu bash
```

**Diferencia entre `run` y `exec`:**

- **`docker run`**: Crea y ejecuta un nuevo contenedor
- **`docker exec`**: Ejecuta un comando en un contenedor ya en ejecución

---

## Puertos

### Mapeo de Puertos

```bash
# Sintaxis básica
docker run -p HOST_PORT:CONTAINER_PORT IMAGE

# Ejemplos
docker run -d -p 8080:80 nginx        # Puerto 8080 del host al 80 del contenedor
docker run -d -p 3000:3000 node:alpine # Puerto 3000 del host al 3000 del contenedor
docker run -d -p 127.0.0.1:8080:80 nginx # Solo interfaz local

# Mapear múltiples puertos
docker run -d -p 8080:80 -p 8443:443 nginx

# Puerto aleatorio
docker run -d -P nginx  # Docker asigna puertos aleatorios
```

### Verificar Puertos

```bash
# Ver puertos mapeados
docker port CONTAINER_ID

# Ejemplo de salida
80/tcp -> 0.0.0.0:8080
```

---

## Logs

### Visualizar Logs

```bash
# Ver logs de un contenedor
docker logs CONTAINER_ID

# Ver logs en tiempo real
docker logs -f CONTAINER_ID

# Ver últimas 100 líneas
docker logs --tail 100 CONTAINER_ID

# Ver logs con timestamps
docker logs -t CONTAINER_ID

# Combinar opciones
docker logs -f --tail 50 -t CONTAINER_ID
```

### Ejemplo Práctico

```bash
# Ejecutar nginx
docker run -d --name web-server nginx

# Ver logs
docker logs web-server

# Generar tráfico (desde otra terminal)
curl http://localhost:8080

# Ver logs en tiempo real
docker logs -f web-server
```

**Opciones útiles:**

- **`-f`**: Sigue los logs en tiempo real (follow)
- **`--tail N`**: Muestra las últimas N líneas
- **`-t`**: Agrega timestamps a cada línea

---

## Inspeccionar Contenedores

### Comando Inspect

```bash
# Información completa del contenedor
docker inspect CONTAINER_ID

# Información específica con formato
docker inspect --format='{{.State.Status}}' CONTAINER_ID

# IP del contenedor
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' CONTAINER_ID

# Variables de entorno
docker inspect --format='{{.Config.Env}}' CONTAINER_ID
```

### Información Útil

```bash
# Estado del contenedor
docker inspect --format='{{.State.Status}}' CONTAINER_ID

# Fecha de creación
docker inspect --format='{{.Created}}' CONTAINER_ID

# Imagen utilizada
docker inspect --format='{{.Config.Image}}' CONTAINER_ID

# Comando ejecutado
docker inspect --format='{{.Config.Cmd}}' CONTAINER_ID

# Puertos expuestos
docker inspect --format='{{.Config.ExposedPorts}}' CONTAINER_ID
```

---

## Variables de Entorno

### Definir Variables de Entorno

```bash
# Una variable
docker run -e VARIABLE=valor IMAGE

# Múltiples variables
docker run -e VAR1=valor1 -e VAR2=valor2 IMAGE

# Desde archivo
docker run --env-file .env IMAGE
```

### Ejemplos Prácticos

```bash
# MySQL con variables de entorno
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=mi-password \
  -e MYSQL_DATABASE=mi-db \
  -e MYSQL_USER=mi-usuario \
  -e MYSQL_PASSWORD=mi-user-password \
  mysql:8.0

# Node.js con variables de entorno
docker run -d \
  --name mi-app \
  -e NODE_ENV=production \
  -e PORT=3000 \
  -p 3000:3000 \
  node:alpine
```

### Archivo `.env`

```bash
# Crear archivo .env
cat > .env << EOF
DB_HOST=localhost
DB_PORT=5432
DB_NAME=myapp
DB_USER=admin
DB_PASSWORD=secret123
EOF

# Usar archivo .env
docker run -d --env-file .env postgres:13
```

**Ventajas del archivo `.env`:**

- Organiza configuraciones en un solo lugar
- Facilita el manejo de múltiples variables
- Mejora la seguridad al no exponer credenciales en comandos

---

## Contenedores sin Servicio

### Contenedores de Utilidad

```bash
# Ejecutar comando y salir
docker run --rm ubuntu echo "Hola Docker"

# Procesar archivos
docker run --rm -v $(pwd):/data ubuntu find /data -name "*.txt"

# Contenedor temporal para debugging
docker run --rm -it ubuntu bash
```

### Ejemplos de Contenedores Utilitarios

```bash
# Comprimir archivos
docker run --rm -v $(pwd):/data ubuntu tar -czf /data/backup.tar.gz /data/*.txt

# Generar documentación
docker run --rm -v $(pwd):/docs pandoc/latex README.md -o manual.pdf

# Ejecutar tests
docker run --rm -v $(pwd):/app -w /app node:alpine npm test

# Análisis de seguridad
docker run --rm -v $(pwd):/app -w /app node:alpine npm audit
```

**Opción `--rm`:**

- Elimina automáticamente el contenedor cuando termina su ejecución
- Útil para contenedores de un solo uso
- Mantiene el sistema limpio sin contenedores innecesarios