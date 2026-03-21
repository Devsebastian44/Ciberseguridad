## Tres Pilares de Control NGFW

**1. App-ID (Application Identification)**

- Identifica aplicaciones independiente del puerto
- Clasifica 3,000+ aplicaciones
- Granularidad: Control de funciones específicas (ej: Facebook-posting vs Facebook-chat)

**2. User-ID (User Identification)**

- Políticas basadas en usuario/grupo, no IP
- Integración: Active Directory, LDAP, Captive Portal
- Logs incluyen username

**3. Content-ID (Content Identification)**

- Inspección profunda de contenido
- Incluye: IPS, Antivirus, Anti-spyware, URL Filtering, File Blocking, DLP

## Security Policy (Reglas de Firewall)

### Componentes de una Regla

1. Source Zone → Destination Zone
2. Source/Destination Address
3. User/Group
4. Application
5. Service (usar **application-default**)
6. Action (Allow/Deny/Drop)
7. Security Profile Group

**Evaluación**: Top-down, primera coincidencia gana **Regla implícita**: Interzone = Deny

## Security Profiles (Protecciones)

|Profile|Función|
|---|---|
|**Antivirus**|Bloquea malware conocido, integra WildFire (sandboxing)|
|**Anti-Spyware**|Detecta C2 communication, previene exfiltración|
|**IPS (Vulnerability Protection)**|Previene exploits (SQL injection, buffer overflow, etc.)|
|**URL Filtering**|Bloquea por categoría web (80+ categorías: malware, phishing, social media)|
|**File Blocking**|Bloquea tipos de archivos (.exe, .bat, scripts)|
|**Data Filtering (DLP)**|Previene fuga de datos sensibles (tarjetas, SSN, etc.)|

**Best Practice**: Habilitar TODOS los profiles en políticas críticas

## Zonas de Seguridad

**Zonas Típicas**

- **Untrust**: Internet (confianza cero)
- **Trust**: Red interna corporativa
- **DMZ**: Servidores públicos
- **Guest**: WiFi invitados (solo Internet)
- **IoT**: Dispositivos IoT segregados

**Tráfico Inter-Zone**: Requiere política explícita, default = Deny

## NAT (Network Address Translation)

**Source NAT**

- Usuarios internos → Internet
- Oculta IPs internas

**Destination NAT**

- Publicar servidores internos
- Port forwarding

**Importante**: NAT policy + Security policy (ambas necesarias)

## SSL/TLS Decryption

### Por qué es Crítico

- 80%+ tráfico es HTTPS
- Malware se oculta en cifrado

### Métodos

- **Forward Proxy**: Tráfico saliente (usuarios → Internet)
- **Inbound Inspection**: Tráfico entrante (Internet → servidores)

### Qué NO Descifrar

- Sitios financieros (banking)
- Sitios de salud (HIPAA)
- Gobierno sensible
- **Descifrar**: General browsing, descargas, sitios riesgosos

**Consideración**: Balance seguridad vs privacidad + requisitos legales

## Logs Críticos

|Tipo|Uso|
|---|---|
|**Traffic Logs**|Sesiones permitidas/bloqueadas, análisis de uso|
|**Threat Logs**|Amenazas detectadas (IPS, AV, etc.) - CRÍTICO|
|**URL Filtering**|Sitios visitados por categoría|
|**Data Filtering**|Intentos de exfiltración - COMPLIANCE|
|**WildFire**|Archivos analizados en sandbox|

**Integración**: Enviar logs a SIEM para correlación

## High Availability (HA)

**Active/Passive**

- Un firewall activo, otro standby
- Failover automático
- Más común

**Active/Active**

- Ambos procesando tráfico
- Load balancing
- Mayor throughput

## Panorama (Gestión Centralizada)

**Funciones**

- Configurar múltiples firewalls desde consola única
- Templates de configuración
- Log collection centralizado
- Reportes y dashboards unificados
- Device Groups para agrupar firewalls

## Best Practices Esenciales

### Políticas

1. **Positive Security Model**: Deny all, allow solo lo necesario
2. **Application-Default**: Usar puertos dinámicos según aplicación
3. **Específico primero**: Reglas específicas arriba, generales abajo
4. **Documentar**: Describir propósito de cada regla

### Seguridad

- Habilitar **todos** los security profiles
- **SSL decryption** por default (con excepciones apropiadas)
- Segmentación: Múltiples zonas, no solo Trust/Untrust
- **Zero Trust**: Verificar todo, incluso tráfico interno

### Operaciones

- **Updates automáticos**: AV/AS (diario), Apps/Threats (semanal)
- **Backup** configuración regularmente
- **Monitoreo**: Review threat logs diariamente
- **Testing**: Probar cambios en lab antes de producción
- **Logs a SIEM**: Para correlación y análisis avanzado

### Alertas Configurar

- Amenazas Critical/High severity
- Authentication failures (brute force)
- Policy violations
- Certificate errors SSL