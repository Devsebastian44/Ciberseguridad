## Introducción a Certificados Digitales

### Definición

Un **certificado digital** es un documento electrónico que utiliza criptografía de clave pública para verificar la identidad de una entidad y establecer comunicaciones seguras.

---

### Propósito Principal

- **Autenticación** - Verificar identidad
- **Integridad** - Garantizar que los datos no fueron alterados
- **No repudio** - Probar autoría de acciones
- **Confidencialidad** - Cifrar comunicaciones

---

## Estructura de un Certificado X.509

### Componentes Principales

**Ejemplo de certificado:**

```
Version: 3
Serial Number: 12345678
Signature Algorithm: sha256WithRSAEncryption
Issuer: DigiCert SHA2 Secure Server CA
Validity: Not Before 2024, Not After 2025
Subject: Example Corp, CN=www.example.com
Public Key: RSA 2048 bits
Extensions: Subject Alternative Name (SAN)
```

---

## Campos Importantes

### Issuer (Emisor)

Identifica la **Autoridad de Certificación (CA)** que emitió el certificado.

---

### Subject (Sujeto)

Identifica al **propietario del certificado**.

**Campos comunes:**

- CN (Common Name)
- O (Organization)
- OU (Organizational Unit)
- C (Country)

---

### Validity (Validez)

**Fechas de inicio y expiración** del certificado.

---

### Public Key (Clave Pública)

**Algoritmos comunes:**

- **RSA** (2048, 3072, 4096 bits)
- **ECDSA** (256, 384 bits)
- DSA (obsoleto)

---

## Autoridades de Certificación (CA)

### Root CA

- **Autofirmada**
- Almacenada en trust stores de sistemas operativos
- Máxima confianza

---

### Intermediate CA

- **Firmada por Root CA**
- Mayor seguridad (Root CA offline)
- Usada para operaciones diarias

---

### Issuing CA

- Emite **certificados de usuario final**
- Puede ser Intermediate CA o específica

---

### Cadena de Certificación

```
Root CA
 └── Intermediate CA
      └── End Entity Certificate
```

---

## Tipos de Certificados

### Por Validación

**DV (Domain Validated):**

- Validación básica de dominio
- Emisión rápida (minutos)
- Menor costo

**OV (Organization Validated):**

- Validación de dominio + organización
- Verificación de entidad legal
- Mayor confianza

**EV (Extended Validation):**

- Validación exhaustiva
- Barra verde en navegadores (antiguos)
- Máxima confianza

---

### Por Cobertura

**Single Domain:**

- Un solo dominio específico
- Ejemplo: www.example.com

**Wildcard:**

- Dominio principal + subdominios
- Ejemplo: *.example.com

**Multi-Domain (SAN):**

- Múltiples dominios diferentes
- Subject Alternative Names

---

## Proceso de Emisión

### Generación de Claves

**RSA:**

```bash
openssl genrsa -out private.key 2048
```

**ECDSA:**

```bash
openssl ecparam -genkey -name secp256r1 -out private.key
```

---

### CSR (Certificate Signing Request)

**Generar CSR:**

```bash
openssl req -new -key private.key -out request.csr
```

**Ver contenido del CSR:**

```bash
openssl req -in request.csr -text -noout
```

---

## Revocación de Certificados

### CRL (Certificate Revocation List)

**Características:**

- Lista de certificados revocados
- Actualización periódica
- Descarga completa

---

### OCSP (Online Certificate Status Protocol)

**Características:**

- Verificación en tiempo real
- Consulta específica por certificado
- Más eficiente que CRL

---

### OCSP Stapling

**Características:**

- Respuesta OCSP adjunta por el servidor
- Reduce latencia
- Mayor privacidad

---

## Gestión de Certificados

### Almacenamiento Seguro

**Mejores prácticas:**

- Claves privadas **nunca compartidas**
- **Permisos restringidos** (chmod 600)
- **Backups encriptados**
- Usar HSM para entornos críticos

---

### Monitoreo

**Aspectos a monitorear:**

- **Alertas de expiración** (30-60 días antes)
- **Verificación de revocación**
- **Renovación automatizada**
- Auditorías de uso

---

### Herramientas de Gestión

**Ver certificado:**

```bash
openssl x509 -in certificate.crt -text -noout
```

**Verificar cadena:**

```bash
openssl verify -CAfile ca-bundle.crt certificate.crt
```

**Probar conexión SSL/TLS:**

```bash
openssl s_client -connect example.com:443 -servername example.com
```

**Ver fechas de expiración:**

```bash
openssl x509 -in certificate.crt -noout -dates
```

---

## Aplicaciones Prácticas

### SSL/TLS

**Uso:** Cifrado de comunicaciones web (HTTPS)

**Puertos comunes:** 443 (HTTPS), 993 (IMAPS), 995 (POP3S)

---

### Code Signing

**Uso:** Firmar software para verificar integridad y autoría

**Plataformas:** Windows, macOS, Android, iOS

---

### Email Security

**Protocolos:**

- **S/MIME** (Secure/Multipurpose Internet Mail Extensions)
- **PGP** (Pretty Good Privacy)

---

## Seguridad y Mejores Prácticas

### Protección de Claves Privadas

- Usar **HSM** (Hardware Security Module) para claves críticas
- **Nunca** almacenar en repositorios de código
- Aplicar **permisos estrictos** en archivos

---

### Configuración Segura

- Usar **algoritmos fuertes** (RSA ≥ 2048 bits, ECDSA ≥ 256 bits)
- **TLS 1.2+** únicamente (deshabilitar TLS 1.0/1.1)
- Implementar **Perfect Forward Secrecy** (PFS)
- Configurar **HSTS** (HTTP Strict Transport Security)

---

### Auditoría y Monitoreo

- **Certificate Transparency** logs
- Auditorías **periódicas** de certificados
- **Rotación regular** de certificados
- Monitoreo de **emisiones no autorizadas**

---

## Comandos Útiles

### Conversión de Formatos

**PEM a DER:**

```bash
openssl x509 -in cert.pem -outform der -out cert.der
```

**PFX/P12 a PEM:**

```bash
openssl pkcs12 -in cert.pfx -out cert.pem -nodes
```

---

### Validación

**Verificar clave privada y certificado coinciden:**

```bash
openssl x509 -noout -modulus -in certificate.crt | openssl md5
openssl rsa -noout -modulus -in private.key | openssl md5
```

---

## Consideraciones

- **Renovar** certificados antes de expiración
- **Proteger** claves privadas rigurosamente
- Usar **CA confiables** reconocidas
- Implementar **monitoreo automatizado**
- **Documentar** procedimientos de gestión

---