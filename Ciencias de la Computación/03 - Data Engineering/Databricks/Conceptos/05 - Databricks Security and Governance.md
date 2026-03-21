## Introducción

La seguridad en **Databricks** se basa en múltiples capas de protección y gobernanza centralizada.

---

## Modelo de Seguridad

### Principios Fundamentales

**Pilares de seguridad:**

1. **Defense in Depth:** múltiples capas de seguridad
2. **Least Privilege:** acceso mínimo necesario
3. **Zero Trust:** verificación continua
4. **Compliance:** cumplimiento regulatorio

---

## Autenticación y Autorización

### Métodos de Autenticación

**Opciones disponibles:**

- **Single Sign-On (SSO):** SAML, OAuth
- **Personal Access Tokens:** para APIs
- **Service Principals:** para aplicaciones
- **Multi-Factor Authentication (MFA):** seguridad adicional

---

### Modelo de Autorización

**Jerarquía de acceso:**

```
User/Service Principal
    ↓
Workspace Access
    ↓
Resource Permissions
    ↓
Data Access Controls
```

---

## Unity Catalog

### Características

**Funcionalidades principales:**

- **Gobernanza** centralizada
- Control de acceso **granular** (nivel de columna)
- **Data lineage** end-to-end
- **Audit logging** completo

---

### Jerarquía de Objetos

```
Metastore
├── Catalog
│   ├── Schema
│   │   ├── Table
│   │   ├── View
│   │   └── Function
│   └── Volume
└── External Location
```

---

## Encriptación

### Datos en Reposo

**Opciones de cifrado:**

- Encriptación **nativa** del proveedor cloud
- **BYOK** (Bring Your Own Key)
- Integración con **HSMs**

---

### Datos en Tránsito

**Protección de comunicaciones:**

- **TLS 1.2+** en todas las comunicaciones
- **Certificate Pinning**
- **VPN/Private Link** para conectividad privada

---

## Compliance y Auditoría

### Certificaciones

**Estándares cumplidos:**

- **SOC 2 Type II**
- **ISO 27001**
- **GDPR**
- **HIPAA**
- **FedRAMP**

---

### Auditoría

**Capacidades de monitoreo:**

- **Audit logs** detallados
- **Data lineage** de transformaciones
- **Monitoreo** de accesos
- **Reportes** automatizados de compliance

---

## Seguridad en Redes

### Aislamiento de Red

**Componentes de red:**

- **VPC/VNet**
- **Private Endpoints**
- **Firewall rules**
- **NAT Gateways**

---

### Monitoreo de Seguridad

**Capacidades de detección:**

- Integración con **SIEM**
- **Detección** de amenazas
- **Respuesta** a incidentes
- Gestión de **vulnerabilidades**

---