## Principios Fundamentales

### Modelo de Responsabilidad Compartida (Repaso)

- **Proveedor Cloud**: Seguridad de la infraestructura física, red, hipervisor
- **Cliente**: Seguridad de datos, aplicaciones, identidades, configuraciones, SO (según modelo)
- **Crítico**: Entender exactamente qué protege el proveedor y qué debe proteger el cliente

### Defensa en Profundidad (Defense in Depth)

- Múltiples capas de seguridad
- Si una capa falla, otras siguen protegiendo
- Capas: Red, Identity, Aplicación, Datos, Infraestructura

### Principio de Mínimo Privilegio

- Otorgar solo los permisos necesarios
- Aplicar a usuarios, aplicaciones y servicios
- Revisión periódica de permisos

### Zero Trust

- **Concepto**: "Nunca confíes, siempre verifica"
- No asumir confianza por ubicación de red
- Verificar cada acceso independientemente
- Micro-segmentación

## Identity and Access Management (IAM)

### Componentes Clave

- **Identidades**: Usuarios, grupos, roles, service accounts
- **Autenticación**: Verificar identidad (MFA recomendado)
- **Autorización**: Determinar qué puede hacer la identidad
- **Políticas**: Definen permisos (JSON/YAML típicamente)

### Mejores Prácticas

- Implementar MFA obligatorio
- Usar roles en lugar de usuarios para servicios
- Rotación regular de credenciales
- Eliminar cuentas/permisos no utilizados
- Auditar accesos regularmente
- No usar cuentas root/admin para tareas diarias

### Federación de Identidades

- Integración con proveedores externos (SAML, OAuth, OpenID Connect)
- Single Sign-On (SSO)
- Gestión centralizada

## Seguridad de Red en la Nube

### Virtual Private Cloud (VPC)

- Red virtual aislada en la nube
- Control sobre rangos IP, subnets, tablas de ruteo
- **Subnets públicas vs privadas**

### Security Groups (Firewalls Stateful)

- Actúan a nivel de instancia/recurso
- Reglas de entrada y salida
- Stateful: respuestas permitidas automáticamente
- Solo reglas de permiso (deny implícito)

### Network Access Control Lists (NACLs)

- Actúan a nivel de subnet
- Stateless: requieren reglas explícitas de entrada y salida
- Reglas de permiso y denegación
- Evaluación por orden de prioridad

### Segmentación de Red

- Aislar recursos por función/sensibilidad
- Micro-segmentación con políticas granulares
- Limitar comunicación lateral (east-west traffic)

## Seguridad de Datos

### Encriptación

**En Reposo (At Rest)**

- Datos almacenados en discos, bases de datos, backups
- Usar servicios de gestión de claves (KMS)
- Encriptación a nivel de volumen, BD, objeto

**En Tránsito (In Transit)**

- TLS/SSL para comunicaciones
- VPN para conexiones privadas
- Certificados válidos y actualizados

**Gestión de Claves**

- Servicios gestionados: AWS KMS, Azure Key Vault, GCP KMS
- Rotación automática de claves
- Separación de claves por entorno/aplicación
- Hardware Security Modules (HSM) para máxima seguridad

### Data Loss Prevention (DLP)

- Prevenir fuga de información sensible
- Clasificación de datos
- Políticas de protección automatizadas
- Monitoreo de movimiento de datos

### Backup y Recuperación

- Backups automáticos y regulares
- Almacenamiento en ubicaciones geográficas diferentes
- Pruebas de restauración periódicas
- Inmutabilidad de backups (protección contra ransomware)

## Seguridad de Contenedores

### Seguridad de Imágenes

- Escaneo de vulnerabilidades en imágenes
- Usar imágenes base oficiales y actualizadas
- Firma de imágenes (image signing)
- Registros privados seguros
- No incluir secretos en imágenes

### Runtime Security

- Políticas de seguridad de pods (Pod Security Standards)
- Limitar capacidades de contenedores
- Ejecutar como usuario no-root
- Network policies para aislar pods
- Runtime threat detection

### Kubernetes Security

- RBAC (Role-Based Access Control) estricto
- Secrets management (no hardcodear credenciales)
- API Server seguro y autenticado
- Admission Controllers para políticas
- Auditoría de eventos del cluster

## Monitoreo y Logging

### Logging Centralizado

- Recopilar logs de todas las fuentes
- Retención según compliance
- Logs inmutables
- **Logs críticos**: Accesos, cambios de configuración, eventos de seguridad

### Monitoring y Alertas

- Métricas de seguridad en tiempo real
- Alertas automáticas para anomalías
- Dashboards de seguridad
- Integración con SIEM (Security Information and Event Management)

### CloudTrail / Activity Logs

- Registro de todas las acciones API
- Quién hizo qué, cuándo, desde dónde
- Esencial para auditoría y compliance
- Proteger contra modificación/eliminación

## Compliance y Gobernanza

### Frameworks Comunes

- **ISO 27001**: Gestión de seguridad de la información
- **SOC 2**: Controles de seguridad para proveedores de servicios
- **PCI DSS**: Datos de tarjetas de pago
- **HIPAA**: Datos de salud (US)
- **GDPR**: Protección de datos personales (EU)

### Cloud Security Posture Management (CSPM)

- Evaluación continua de configuraciones
- Detección de misconfigurations
- Compliance automático con benchmarks (CIS)
- Remediación automatizada o guiada

### Infrastructure as Code (IaC) Security

- Escaneo de templates (Terraform, CloudFormation, ARM)
- Políticas de seguridad en código
- Prevención de despliegues inseguros
- Versionado y auditoría de cambios

## Threat Detection y Response

### Cloud-Native Detection

- Análisis de comportamiento
- Machine Learning para anomalías
- Threat intelligence integrada
- Detección de compromiso de identidades

### Incident Response

- Playbooks automatizados
- Aislamiento rápido de recursos comprometidos
- Snapshots para análisis forense
- Comunicación y escalamiento

### Security Automation

- Respuesta automática a eventos
- Orquestación de seguridad (SOAR)
- Reducción de tiempo de respuesta
- Consistencia en acciones