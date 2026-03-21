## ¿Qué es REST?

> **REST (Representational State Transfer)** es un estilo de arquitectura de software para realizar una comunicación cliente-servidor. Los clientes y los servidores intercambian datos mediante HTTP.

### Características principales

- Estilo arquitectónico, no un protocolo
- Basado en HTTP
- Comunicación cliente-servidor
- Diseñado por Roy Fielding en 2000

---

## Conceptos Fundamentales

### **Recurso**

Todo es un recurso que puede ser identificado con una URI.

```
Ejemplos de recursos:
- Usuario: /users/123
- Producto: /products/456
- Pedido: /orders/789
```

### **Representación**

Los recursos pueden tener múltiples representaciones (JSON, XML, HTML).

```json
{
  "id": 123,
  "name": "Juan Pérez",
  "email": "juan@ejemplo.com"
}
```

### **Estado**

El servidor no guarda el estado del cliente entre peticiones.

---

## Principios de REST

### 1. Interfaz Uniforme (Uniform Interface)

#### **Identificación de Recursos**

Cada recurso tiene una URI única.

```
✅ Bien identificado:
GET /users/123
GET /products/456

❌ Mal identificado:
GET /getUserById?id=123
```

#### **HATEOAS**

Las respuestas incluyen links a acciones relacionadas.

```json
{
  "id": 123,
  "name": "Juan Pérez",
  "_links": {
    "self": { "href": "/users/123" },
    "orders": { "href": "/users/123/orders" }
  }
}
```

---

### 2. Sin Estado (Stateless)

> Cada petición del cliente al servidor debe contener toda la información necesaria para entender y procesar la solicitud.

**El servidor NO guarda:**

- Sesiones de usuario
- Estado de conversación
- Información entre peticiones

#### **Ejemplo Stateless**

```http
❌ Mal (Stateful):
POST /login
GET /profile  // Servidor recupera sesión

✅ Bien (Stateless):
POST /login
Response: { "token": "eyJhbGc..." }

GET /profile
Authorization: Bearer eyJhbGc...
```

#### **Ventajas**

|Ventaja|Descripción|
|---|---|
|**Escalabilidad**|Cualquier servidor puede manejar cualquier petición|
|**Confiabilidad**|Fácil recuperación de fallos|
|**Simplicidad**|No hay gestión de estado en servidor|

---

### 3. Cacheable

> Las respuestas deben definir si pueden ser cacheadas y por cuánto tiempo.

```http
// Respuesta cacheable
Cache-Control: max-age=3600, public
ETag: "33a64df551425fcc55e4d42a148795d9f25f89d4"

// Respuesta no cacheable
Cache-Control: no-cache, no-store, must-revalidate
```

---

### 4. Sistema de Capas (Layered System)

> La arquitectura debe estar compuesta por capas jerárquicas.

**Beneficios:**

- Encapsulación
- Flexibilidad
- Seguridad
- Escalabilidad

---

## ¿Qué es RESTful?

> **RESTful** es la implementación práctica de la arquitectura REST.

```
REST      → Estilo arquitectónico (teoría)
RESTful   → Implementación del estilo (práctica)
```

### **Ejemplo Comparativo**

#### ❌ No es RESTful

```http
POST /getUserById
POST /createNewUser
POST /updateUserInfo
POST /deleteUserFromSystem
```

#### ✅ Es RESTful

```http
GET /users/123
POST /users
PUT /users/123
DELETE /users/123
```

---

## Métodos HTTP

### **GET - Leer/Obtener**

**Características:**

- Seguro (no modifica datos)
- Idempotente
- Cacheable

```http
GET /users/123
GET /users?role=admin&active=true
```

**Respuestas:** `200 OK`, `404 Not Found`, `401 Unauthorized`

---

### **POST - Crear**

**Características:**

- No seguro
- No idempotente
- No cacheable

```http
POST /users
{
  "name": "Juan Pérez",
  "email": "juan@ejemplo.com"
}
```

**Respuestas:** `201 Created`, `400 Bad Request`, `409 Conflict`

---

### **PUT - Actualizar Completamente**

**Características:**

- No seguro
- Idempotente
- No cacheable

```http
PUT /users/123
{
  "name": "Juan Pérez",
  "email": "juan@ejemplo.com",
  "role": "admin"
}
```

**Nota:** PUT reemplaza **todo** el recurso.

**Respuestas:** `200 OK`, `204 No Content`, `404 Not Found`

---

### **PATCH - Actualizar Parcialmente**

```http
PATCH /users/123
{
  "email": "juan.nuevo@ejemplo.com"
}
```

**Diferencia con PUT:** PATCH solo modifica los campos enviados.

---

### **DELETE - Eliminar**

**Características:**

- No seguro
- Idempotente
- No cacheable

```http
DELETE /users/123
```

**Respuestas:** `204 No Content`, `404 Not Found`, `409 Conflict`

---

## Tabla Resumen de Métodos HTTP

|Método|Acción|Seguro|Idempotente|Cacheable|
|---|---|---|---|---|
|**GET**|Leer|✅|✅|✅|
|**POST**|Crear|❌|❌|❌|
|**PUT**|Actualizar todo|❌|✅|❌|
|**PATCH**|Actualizar parcial|❌|✅|❌|
|**DELETE**|Eliminar|❌|✅|❌|

### **Conceptos Clave**

- **Seguro:** No modifica datos en el servidor
- **Idempotente:** Múltiples peticiones idénticas producen el mismo resultado
- **Cacheable:** La respuesta puede ser almacenada para uso futuro

---

## Headers HTTP Importantes

### **Headers de Request**

```http
Content-Type: application/json
Accept: application/json
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### **Headers de Response**

```http
Content-Type: application/json; charset=utf-8
Cache-Control: max-age=3600, public
Location: /users/124
ETag: "33a64df551425fcc55e4d42a148795d9f25f89d4"
```

---

## Ventajas de REST

### **Escalabilidad**

- Stateless facilita load balancing
- Agregar servidores sin coordinación

### **Simplicidad**

- Usa estándares web existentes (HTTP)
- Curva de aprendizaje baja

### **Flexibilidad**

- Versionado (`/api/v1/users`)
- Múltiples representaciones (JSON, XML)

### **Cacheable**

- Reduce latencia
- Disminuye carga del servidor

---

## Desventajas de REST

### **Over-fetching y Under-fetching**

**Over-fetching:**

```http
// Cliente solo necesita name y email
// pero recibe todo el objeto con datos innecesarios
GET /users/123
```

**Under-fetching:**

```http
// Necesito usuario y sus posts
GET /users/123
GET /users/123/posts
// 2 requests cuando podría ser 1
```

### **Limitaciones con Operaciones Complejas**

```
Operaciones que no mapean bien a CRUD:
- Búsquedas complejas
- Operaciones en lote
- Transacciones
- Workflows
```

### **Seguridad**

Requiere implementar:

- HTTPS obligatorio
- Autenticación robusta
- CORS configurado
- Rate limiting