## Introducción

**SSL (Secure Socket Layer)** es un protocolo criptográfico diseñado para proporcionar comunicaciones seguras a través de redes.  
Su sucesor, **TLS (Transport Layer Security)**, es ampliamente utilizado en la actualidad.

---

## Arquitectura SSL/TLS

### Componentes Principales

**1. Protocolo de Registro (Record Protocol)**

- Fragmenta, comprime y cifra los datos
- Proporciona integridad y autenticación
- Gestiona la secuencia de mensajes

**2. Protocolo de Handshake**

- Establece la conexión segura
- Negocia algoritmos criptográficos
- Intercambia claves y certificados

**3. Protocolo de Cambio de Especificaciones**

- Señaliza cambios en los parámetros de cifrado
- Coordina la transición entre estados

**4. Protocolo de Alerta**

- Maneja errores y avisos
- Proporciona información sobre el estado de la conexión

---

## Proceso de Handshake SSL/TLS

```text
Cliente → Servidor: Client Hello
Servidor → Cliente: Server Hello
Servidor → Cliente: Certificate
Servidor → Cliente: Server Hello Done
Cliente → Servidor: Client Key Exchange
Cliente → Servidor: Change Cipher Spec
Cliente → Servidor: Finished
Servidor → Cliente: Change Cipher Spec
Servidor → Cliente: Finished
```

**Detalles clave:**

- Se negocian versiones y algoritmos de cifrado
- Se intercambian certificados digitales
- Se establece la clave de sesión
- Se activa la configuración segura

---

## Versiones y Evolución

### SSL 1.0

- Nunca fue liberado públicamente
- Tenía serios problemas de seguridad

### SSL 2.0

- Primera versión pública (1995)
- Vulnerabilidades conocidas
- Obsoleto desde 2011

### SSL 3.0

- Mejoró significativamente la seguridad
- Base para TLS 1.0
- Vulnerable a ataques POODLE

### TLS 1.0

- Sucesor de SSL 3.0 (1999)
- Mejoras en seguridad
- Compatible con SSL 3.0

### TLS 1.1

- Protección contra ataques CBC
- Mejoras en vectores de inicialización

### TLS 1.2

- Soporte para SHA-256
- Mejores algoritmos de cifrado
- Ampliamente utilizado

### TLS 1.3

- Eliminación de algoritmos débiles
- Handshake más eficiente
- Mejor rendimiento y seguridad

---

## Implementación y Configuración

### Certificados Digitales

- Identificación del servidor
- Validación por autoridades certificadoras
- Tipos: DV, OV, EV

### Configuración Segura

```text
Mejores prácticas:
- Usar TLS 1.2 o superior
- Deshabilitar SSL 2.0 y 3.0
- Configurar cifrados fuertes
- Implementar HSTS
- Usar certificados válidos
```

---

## Vulnerabilidades Comunes

### Ataques a SSL/TLS

- **BEAST**: Ataque a TLS 1.0
- **POODLE**: Vulnerabilidad en SSL 3.0
- **Heartbleed**: Fallo en OpenSSL
- **FREAK**: Ataque a cifrados de exportación
- **Man-in-the-middle**: Intercepción de comunicaciones

---
