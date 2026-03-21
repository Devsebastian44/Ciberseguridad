## Visión General de Cortex

### Plataforma Cortex

- **Definición**: Suite de seguridad nativa de nube de Palo Alto Networks
- **Enfoque**: Seguridad integral y automatizada para entornos cloud
- **Integración**: Conecta prevención, detección y respuesta
- **Cloud-Native**: Diseñado específicamente para arquitecturas modernas

### Componentes Principales

- **Prisma Cloud**: CSPM y protección de workloads
- **Cortex XDR**: Extended Detection and Response
- **Cortex XSOAR**: Security Orchestration, Automation and Response
- **Cortex Xpanse**: Attack Surface Management

## Prisma Cloud

### Funcionalidades Core

**Cloud Security Posture Management (CSPM)**

- Evaluación continua de configuraciones multi-cloud
- Detección de misconfigurations en tiempo real
- Compliance con frameworks (CIS, PCI-DSS, GDPR, HIPAA, etc.)
- Visibilidad completa del inventario cloud
- Remediación guiada y automatizada

**Cloud Workload Protection Platform (CWPP)**

- Protección de hosts, contenedores y serverless
- Vulnerability scanning
- Runtime defense
- Compliance checking de workloads

**Cloud Network Security (CNS)**

- Micro-segmentación
- Visibilidad de tráfico este-oeste
- Políticas de red granulares
- Protección de APIs

**Cloud Infrastructure Entitlement Management (CIEM)**

- Análisis de permisos IAM
- Detección de exceso de privilegios
- Identificación de identidades no utilizadas
- Least privilege enforcement

### Capacidades de Seguridad

**Shift-Left Security**

- Integración en CI/CD pipelines
- Escaneo de IaC (Terraform, CloudFormation, ARM, Kubernetes YAML)
- Detección de problemas antes del despliegue
- Developer-friendly feedback

**Runtime Protection**

- Protección de contenedores en ejecución
- Behavioral analysis
- Threat intelligence integrada
- Automated incident response

**Data Security**

- Clasificación de datos sensibles
- Detección de exposición pública
- DLP policies
- Compliance de almacenamiento

### Soporte Multi-Cloud

- **AWS, Azure, GCP, Oracle Cloud**
- **Alibaba Cloud**
- Gestión unificada desde consola única
- Políticas consistentes entre clouds

## Cortex XDR (Extended Detection and Response)

### Concepto XDR

- **Evolución de EDR**: Más allá de endpoints
- **Correlación**: Datos de red, endpoints, cloud, aplicaciones
- **Analytics**: Machine learning y behavioral analysis
- **Automated Response**: Respuesta coordinada entre vectores

### Capacidades

**Detección Avanzada**

- Behavioral threat detection
- Analytics basados en IA/ML
- Correlation de eventos multi-fuente
- Threat intelligence de Unit 42 (equipo de investigación de Palo Alto)

**Investigación**

- Timeline visual de incidentes
- Root cause analysis automatizado
- Contexto completo del ataque
- Reducción de alertas (menos false positives)

**Respuesta Automatizada**

- Playbooks pre-construidos
- Aislamiento de endpoints
- Bloqueo de procesos maliciosos
- Integración con firewall/network

**Hunting Proactivo**

- Queries personalizadas (XQL language)
- Búsqueda de IoCs
- Threat hunting guided
- Historical analysis

## Cortex XSOAR (Security Orchestration, Automation and Response)

### Funcionalidad SOAR

**Orquestación**

- Integración con 500+ herramientas de seguridad
- Workflows automatizados
- Coordinación entre equipos y herramientas

**Automatización**

- Playbooks personalizables
- Respuesta automática a incidentes
- Reducción de tareas manuales
- Consistencia en procesos

**Case Management**

- Gestión centralizada de incidentes
- Colaboración de equipo SOC
- Métricas y reporting
- SLA tracking

**Threat Intelligence Management**

- Agregación de feeds de TI
- Enriquecimiento automático de alertas
- Scoring de amenazas
- Compartir IoCs

### Beneficios

- Reducción de MTTR (Mean Time To Respond)
- Aumento de eficiencia del SOC
- Escalabilidad de operaciones
- Menor fatiga de analistas

## Cortex Xpanse (Attack Surface Management)

### Descubrimiento de Activos

- Escaneo continuo de internet
- Identificación de activos expuestos desconocidos (shadow IT)
- Inventario automático
- Detección de subsidiarias y adquisiciones

### Evaluación de Riesgos

- Priorización basada en exposición real
- Identificación de vulnerabilidades externas
- Certificados expirados/débiles
- Servicios mal configurados

### Gestión de Superficie de Ataque

- Visibilidad de lo que ven los atacantes
- Atribución de activos a organizaciones
- Alertas de nuevos activos expuestos
- Remediación guiada

## Arquitectura de Protección Cloud

### Visibilidad Unificada

- Dashboard único para multi-cloud
- Inventario completo de recursos
- Flujo de tráfico visualizado
- Estado de compliance en tiempo real

### Políticas Centralizadas

- Definir una vez, aplicar en todos lados
- Consistencia entre entornos
- Policy as Code
- Version control de políticas

### Automated Remediation

- Respuesta inmediata a violaciones
- Scripts de remediación personalizables
- Integración con ticketing systems
- Audit trail completo

## Mejores Prácticas con Cortex

### Implementación

1. **Assessment inicial**: Inventario y baseline de seguridad
2. **Quick wins**: Resolver misconfigurations críticas
3. **Policy tuning**: Ajustar para reducir false positives
4. **Automation**: Implementar respuestas automáticas gradualmente
5. **Integration**: Conectar con herramientas existentes

### Operación Continua

- Revisión semanal de alertas críticas
- Actualización mensual de políticas
- Tuning trimestral de detecciones
- Training continuo del equipo
- Métricas de seguridad (KPIs)

### Integración DevSecOps

- Shift-left en pipeline CI/CD
- Gates de seguridad automatizados
- Feedback a desarrolladores
- Security champions program

## Prisma Cloud vs Herramientas Nativas

### Ventajas sobre Herramientas Cloud-Native

- **Multi-cloud unificado** vs herramientas por proveedor
- **Consistencia de políticas** entre clouds
- **Visibilidad completa** de entornos híbridos
- **Expertise integrado** (CIS benchmarks, compliance)
- **Detección avanzada** con ML/AI
- **Ecosistema integrado** (XDR, XSOAR)

### Cuándo Usar Prisma Cloud

- Entornos multi-cloud
- Necesidad de compliance riguroso
- Equipos de seguridad pequeños
- Requerimientos de automatización
- Protección de contenedores/Kubernetes a escala

## Casos de Uso Comunes

### Compliance Automation

- Mapeo automático a frameworks regulatorios
- Reportes de auditoría automáticos
- Evidencia continua de compliance
- Alertas de drift de compliance

### Container Security

- Scanning de registros
- Admission control en Kubernetes
- Runtime protection de contenedores
- Secrets scanning

### DevSecOps Enablement

- Feedback en PR/commits
- Breaking builds por vulnerabilidades críticas
- Security as code validation
- Developer portal para auto-servicio

### Cloud Migration Security

- Security assessment pre-migración
- Monitoreo durante migración
- Validation post-migración
- Continuous security posture