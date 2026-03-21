## Introducción a Redis

**Redis (Remote Dictionary Server)** es una base de datos **en memoria** de tipo **clave-valor**, de código abierto y con persistencia opcional. Se utiliza como base de datos, sistema de caché y broker de mensajes.

---

## Instalación de Redis

### Debian/Ubuntu

```bash
sudo apt update
sudo apt install redis-server
```

#### Verificar Instalación

```bash
redis-cli ping
# Respuesta esperada: PONG
```

---

### Fedora/CentOS

```bash
sudo dnf install redis
sudo systemctl enable --now redis
```

---

### macOS (Homebrew)

```bash
brew install redis
brew services start redis
```

---

## Redis con Docker

### Imagen Oficial

```bash
docker run --name redis -p 6379:6379 -d redis
```

---

### Con Persistencia

```bash
docker run --name redis \
  -p 6379:6379 \
  -v redis-data:/data \
  -d redis redis-server --save 60 1 --loglevel warning
```

---

### Probar Conexión

```bash
docker exec -it redis redis-cli
```

---

## Conceptos Básicos de Redis

|Concepto|Descripción|
|---|---|
|**Clave-Valor**|Almacena datos como pares clave/valor|
|**In-Memory**|Los datos residen en **RAM** (muy rápido)|
|**Persistencia**|Puede guardar datos en disco (RDB o AOF)|
|**Tipos de datos**|Soporta múltiples estructuras más allá de strings|
|**Monohilo**|Corre en un **solo hilo**, optimizado|

---

## Tipos de Datos en Redis

### String

|Comando|Descripción|Ejemplo|
|---|---|---|
|`SET`|Establecer valor|`SET clave valor`|
|`GET`|Obtener valor|`GET clave`|

**Uso común:** Caché, contadores, configuraciones

---

### List

|Comando|Descripción|Ejemplo|
|---|---|---|
|`LPUSH`|Insertar al inicio|`LPUSH lista valor`|
|`RPUSH`|Insertar al final|`RPUSH lista valor`|
|`LRANGE`|Obtener rango|`LRANGE lista 0 -1`|

**Uso común:** Colas de mensajes, feeds, historiales

---

### Set

|Comando|Descripción|Ejemplo|
|---|---|---|
|`SADD`|Agregar elemento|`SADD set valor`|
|`SMEMBERS`|Listar todos|`SMEMBERS set`|
|`SREM`|Remover elemento|`SREM set valor`|

**Uso común:** Tags, categorías, elementos únicos

---

### Hash

|Comando|Descripción|Ejemplo|
|---|---|---|
|`HSET`|Establecer campo|`HSET hash campo valor`|
|`HGET`|Obtener campo|`HGET hash campo`|
|`HGETALL`|Obtener todos|`HGETALL hash`|

**Uso común:** Objetos, perfiles de usuario

---

### Sorted Set (ZSet)

|Comando|Descripción|Ejemplo|
|---|---|---|
|`ZADD`|Agregar con score|`ZADD zset score valor`|
|`ZRANGE`|Rango ascendente|`ZRANGE zset 0 -1`|
|`ZREM`|Remover elemento|`ZREM zset valor`|

**Uso común:** Leaderboards, rankings

---

### Bitmap

|Comando|Descripción|Ejemplo|
|---|---|---|
|`SETBIT`|Establecer bit|`SETBIT key offset 1`|
|`GETBIT`|Obtener bit|`GETBIT key offset`|

**Uso común:** Features flags, estadísticas binarias

---

### HyperLogLog

|Comando|Descripción|Ejemplo|
|---|---|---|
|`PFADD`|Agregar elementos|`PFADD key elemento`|
|`PFCOUNT`|Contar únicos|`PFCOUNT key`|

**Uso común:** Conteo probabilístico de elementos únicos

---