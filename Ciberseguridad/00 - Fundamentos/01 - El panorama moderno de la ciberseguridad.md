## Tendencias Modernas de Ciberseguridad

### Amenazas Principales

**Ransomware:**

- Ataques dirigidos a organizaciones críticas
- Ransomware-as-a-Service (RaaS)
- Doble extorsión (cifrado + amenaza de publicación)

**Trabajo Remoto:**

- Expansión del perímetro de seguridad
- Mayor superficie de ataque
- Necesidad de Zero Trust

**Supply Chain Attacks:**

- Compromiso de proveedores terceros
- Ejemplos: SolarWinds, Log4j

**Shortage de Talento:**

- Escasez global de profesionales
- Brecha de habilidades

---

## Cloud Computing

### Modelos de Servicio

**IaaS (Infrastructure as a Service):**

- Infraestructura virtualizada (compute, storage, network)
- Ejemplos: AWS EC2, Azure VMs
- Cliente gestiona: OS, aplicaciones, datos

**PaaS (Platform as a Service):**

- Plataforma de desarrollo
- Ejemplos: Azure App Service, Google App Engine
- Cliente gestiona: Aplicaciones y datos

**SaaS (Software as a Service):**

- Aplicaciones completas vía web
- Ejemplos: Office 365, Salesforce, Gmail
- Cliente gestiona: Solo datos y accesos

### Modelos de Deployment

- **Public Cloud:** Recursos compartidos multi-tenant
- **Private Cloud:** Infraestructura dedicada
- **Hybrid Cloud:** Combinación public + private
- **Multi-Cloud:** Múltiples proveedores (AWS + Azure + GCP)

---

## Desafíos de Seguridad en SaaS

### Shared Responsibility Model

**Proveedor Cloud:** Seguridad DE la nube (infraestructura)  
**Cliente:** Seguridad EN la nube (datos, configuración, IAM)

**Problema:** Clientes asumen que el proveedor protege TODO

### Amenazas Principales

**Misconfiguraciones:**

- Buckets S3 públicos
- Bases de datos expuestas
- MFA no habilitado

**Account Compromise:**

- Credenciales débiles
- Phishing de credenciales cloud
- Falta de MFA

**Data Breaches:**

- Acceso no autorizado
- Insider threats
- Exfiltración de datos

**Insecure APIs:**

- APIs sin autenticación
- Exposición de datos sensibles

**Shadow IT:**

- Aplicaciones SaaS no autorizadas
- Falta de visibilidad
- Riesgos de compliance

**Insufficient Access Controls:**

- Privilegios excesivos
- Falta de least privilege

---

## Regulaciones de Seguridad

### Principales Regulaciones

**GDPR (General Data Protection Regulation):**

- Región: Unión Europea
- Protección de datos personales
- Notificación de brechas en 72 horas
- Multas: Hasta €20M o 4% ingresos globales

**HIPAA:**

- Región: Estados Unidos
- Protección de información de salud (PHI)
- Cifrado, access controls, audit trails

**PCI DSS:**

- Protección de datos de tarjetas de pago
- 12 requisitos (firewall, cifrado, access control, logging, etc.)

**SOX:**

- Protección de datos financieros (empresas públicas USA)

**CCPA:**

- Derechos de privacidad (California)
- Derecho a saber, eliminar, opt-out

### Frameworks y Estándares

**ISO/IEC 27001:**

- Gestión de seguridad de información (ISMS)
- Certificación internacional

**NIST Cybersecurity Framework:**

- 5 Funciones: Identify, Protect, Detect, Respond, Recover

**CIS Controls:**

- 18 controles críticos de seguridad

---

## Soluciones de Seguridad Moderna

**Zero Trust:**

- "Never trust, always verify"
- Verificación continua
- Least privilege

**CSPM (Cloud Security Posture Management):**

- Monitoreo de configuraciones cloud
- Detección de misconfiguraciones

**CASB (Cloud Access Security Broker):**

- Visibilidad de cloud apps
- DLP, threat protection
- Compliance enforcement

**SASE (Secure Access Service Edge):**

- Convergencia red + seguridad
- Protección para usuarios remotos