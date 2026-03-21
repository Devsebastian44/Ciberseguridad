## ¿Qué son las APIs?

> **API (Application Programming Interface)** es un conjunto de reglas que permiten la interacción entre sistemas de software.

---

## Propósitos de las APIs

### APIs de Datos

Acceso CRUD a bases de datos.

```
GET /users          → Leer usuarios
POST /users         → Crear usuario
PUT /users/123      → Actualizar usuario
DELETE /users/123   → Eliminar usuario
```

### APIs de Funciones

Funcionalidades específicas integrables:

- Procesamiento de pagos (Stripe, PayPal)
- Mapas (Google Maps)
- Envío de emails (SendGrid)
- Autenticación (Auth0, Firebase)

### APIs de Sistema Operativo

Interacción con hardware y recursos del sistema.

---

## Clasificación de APIs

### Según Nivel de Acceso

#### **APIs Públicas**

- Disponibles para cualquier desarrollador
- Ejemplos: Twitter API, GitHub API, OpenWeather API

#### **APIs Privadas**

- Uso interno organizacional
- Mayor seguridad y control

#### **APIs de Socio**

- Acceso restringido a socios comerciales
- Colaboraciones B2B

---

### Según Protocolo

#### **REST (RESTful APIs)**

**Principios:**

- Stateless (sin estado)
- Cliente-Servidor
- Cacheable
- Interfaz uniforme

**Métodos HTTP:**

```
GET     → Obtener recursos
POST    → Crear recursos
PUT     → Actualizar completamente
PATCH   → Actualizar parcialmente
DELETE  → Eliminar recursos
```

**Ejemplo:**

```http
GET /api/users/123
Authorization: Bearer token123

Response:
{
  "id": 123,
  "name": "Juan Pérez",
  "email": "juan@ejemplo.com"
}
```

#### **SOAP**

- Basado en XML
- Mayor seguridad (WS-Security)
- Común en sistemas bancarios y enterprise

#### **GraphQL**

- Un solo endpoint
- Cliente solicita exactamente los datos necesarios
- Reduce over-fetching y under-fetching

```graphql
query {
  user(id: 123) {
    name
    email
    posts {
      title
    }
  }
}
```

---

### Según Formato de Datos

#### **JSON (Recomendado para Web)**

```json
{
  "id": 123,
  "name": "Juan Pérez",
  "active": true
}
```

#### **XML (Enterprise)**

```xml
<user>
  <id>123</id>
  <name>Juan Pérez</name>
  <active>true</active>
</user>
```

---

## Seguridad en APIs

### Métodos de Autenticación

#### **JWT (JSON Web Tokens)**

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

**Ventajas:**

- Stateless
- Auto-contenido
- Puede llevar información del usuario

#### **API Keys**

```http
GET /api/weather?city=Madrid
X-API-Key: abc123def456
```

**Uso:** Identificación de aplicaciones, rate limiting, tracking

⚠️ **Advertencias:**

- No usar para autenticación de usuarios
- No exponer en código cliente
- Rotar periódicamente

#### **OAuth 2.0**

Para aplicaciones de terceros que necesitan acceso delegado.

---

### Mejores Prácticas de Seguridad

```
✅ HTTPS obligatorio
✅ Rate Limiting
✅ CORS configurado
✅ Validación de entrada
✅ No exponer datos sensibles
```

---

## Diseño de una API REST

### Paso 1: Definir Propósito y Recursos

Identificar los recursos principales y sus relaciones.

**Ejemplo:** API de Blog

- Posts (`/posts`)
- Comentarios (`/comments`)
- Usuarios (`/users`)

---

### Paso 2: Diseñar Rutas y Métodos

#### **Principios para URLs**

```
✅ Usa nombres en plural
   /users (no /user)

✅ Estructura jerárquica
   /posts/5/comments/12

✅ Parámetros claros
   /users/123
   /users?role=admin&active=true

✅ Simplicidad
   /products (no /get-all-products)

✅ Filtrado y paginación
   /products?category=electronics&limit=20&offset=40
```

#### **Ejemplo de Endpoints**

|Método|Endpoint|Descripción|
|---|---|---|
|GET|`/posts`|Lista de posts|
|GET|`/posts/123`|Post específico|
|POST|`/posts`|Crear post|
|PUT|`/posts/123`|Actualizar post|
|PATCH|`/posts/123`|Actualizar parcialmente|
|DELETE|`/posts/123`|Eliminar post|
|GET|`/posts/123/comments`|Comentarios del post|

---

### Paso 3: Implementar Versionado

#### **En la URL (Recomendado):**

```
https://api.ejemplo.com/v1/users
https://api.ejemplo.com/v2/users
```

#### **En Headers:**

```http
Accept: application/vnd.ejemplo.v2+json
```

---

### Paso 4: Definir Códigos de Estado HTTP

#### **Códigos Comunes**

**Éxito (2xx):**

|Código|Uso|
|---|---|
|200|GET exitoso|
|201|POST exitoso (recurso creado)|
|204|DELETE exitoso (sin contenido)|

**Errores del Cliente (4xx):**

|Código|Uso|
|---|---|
|400|Petición malformada|
|401|No autenticado|
|403|Sin permisos|
|404|Recurso no encontrado|
|422|Validación fallida|
|429|Rate limit excedido|

**Errores del Servidor (5xx):**

|Código|Uso|
|---|---|
|500|Error interno del servidor|
|503|Servicio no disponible|

#### **Ejemplo de Respuestas**

**Éxito:**

```http
HTTP/1.1 201 Created
{
  "id": 123,
  "title": "Nuevo Post",
  "created_at": "2025-11-17T10:30:00Z"
}
```

**Error:**

```http
HTTP/1.1 400 Bad Request
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Datos inválidos",
    "details": [
      {
        "field": "email",
        "message": "Formato de email inválido"
      }
    ]
  }
}
```

---

### Paso 5: Documentar la API

#### **Herramientas**

**Swagger/OpenAPI:**

```yaml
openapi: 3.0.0
info:
  title: Mi API
  version: 1.0.0
paths:
  /users:
    get:
      summary: Lista de usuarios
      responses:
        '200':
          description: Éxito
```

**Postman:**

- Collections compartibles
- Ejemplos de requests
- Testing integrado

#### **Elementos Esenciales**

- Descripción general
- Autenticación requerida
- Base URL
- Lista de endpoints
- Parámetros (path, query, body)
- Ejemplos de requests y responses
- Códigos de estado posibles
- Rate limits
- Changelog de versiones

---

### Paso 6: Implementar Pruebas

#### **Tipos de Pruebas**

**Unitarias:**

```python
def test_create_user():
    response = client.post('/api/users', json={
        'name': 'Juan',
        'email': 'juan@ejemplo.com'
    })
    assert response.status_code == 201
```

**Integración:**

```python
def test_user_workflow():
    user = create_user({'name': 'Ana'})
    response = get_user(user['id'])
    assert response.status_code == 200
    delete_user(user['id'])
```

**Carga:**

- Herramientas: JMeter, Locust, k6
- Simular múltiples usuarios concurrentes

---

## Malas Prácticas a Evitar

### Verbos en URLs

```
❌ POST /api/createUser
✅ POST /api/users
```

---

### Endpoints Sobrecargados

```
❌ GET /api/getUserWithPostsAndComments/123
✅ GET /api/users/123
✅ GET /api/users/123/posts
```

---

### Ignorar Códigos de Estado

```
❌ Siempre retornar 200
{
  "status": 200,
  "error": true,
  "message": "User not found"
}

✅ HTTP 404 Not Found
{
  "error": "User not found"
}
```

---

### Diseño Inconsistente

```
❌ 
GET /api/users
GET /api/getProducts
POST /api/order/create

✅ 
GET /api/users
GET /api/products
POST /api/orders
```

---

### Sin Versionado

```
❌ GET /api/users
✅ GET /api/v1/users
```

---

### Exponer Datos Sensibles

```
❌ 
{
  "id": 123,
  "password": "$2b$10$encrypted...",
  "ssn": "123-45-6789"
}

✅ 
{
  "id": 123,
  "name": "Juan Pérez",
  "avatar": "https://cdn.ejemplo.com/123.jpg"
}
```

---

### Sin Rate Limiting

```
✅ Implementar límites:
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1735689600
```

---

### Errores Genéricos

```
❌ HTTP 500: "Error"

✅ HTTP 400:
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Datos inválidos",
    "details": [...]
  }
}
```