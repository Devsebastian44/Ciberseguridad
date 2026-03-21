## Firewalls Tradicionales (Legacy)

### Características

**Packet Filtering Firewall (Primera Generación)**

- Filtra basado en: IP origen/destino, puerto, protocolo
- Stateless: Cada paquete evaluado independientemente
- No entiende aplicaciones
- Rápido pero limitado

**Stateful Firewall (Segunda Generación)**

- Rastrea estado de conexiones (session table)
- Permite tráfico de retorno automáticamente
- Previene algunos ataques (SYN flood)
- Basado en 5-tuple: IP origen, IP destino, puerto origen, puerto destino, protocolo

### Limitaciones de Firewalls Legacy

**Basado en Puertos**

- Problema: Múltiples aplicaciones usan mismo puerto
- Ejemplo: Puerto 443 (HTTPS) usado por: web legítimo, malware, tunneling, P2P
- No puede diferenciar entre aplicaciones en mismo puerto
- **Regla común**: Permitir puerto 80/443 = permitir TODO sobre HTTP/HTTPS

**Sin Inspección de Contenido**

- No examina payload del paquete
- Malware puede pasar si usa puertos permitidos
- No detecta amenazas encriptadas (HTTPS)

**No Identifica Usuarios**

- Solo ve direcciones IP
- IP cambia (DHCP, móviles)
- Dificulta políticas por usuario/grupo

**Evasión Fácil**

- Tunneling de aplicaciones (usar puertos permitidos)
- Encriptación elude inspección básica
- Port hopping

**Gestión Compleja**

- Miles de reglas por puerto
- Difícil auditar y mantener
- Errores de configuración comunes

**No Protege Contra Amenazas Modernas**

- No detecta exploits de día cero
- No identifica malware avanzado
- No previene exfiltración de datos
- No analiza tráfico cifrado

## Next-Generation Firewalls (NGFW)

### Definición (Gartner)

Firewall tradicional + funcionalidades adicionales:

1. **Application awareness**: Identificación de aplicaciones
2. **Integrated IPS**: Prevención de intrusiones
3. **User/Group identification**: Control por identidad
4. **Threat intelligence**: Información de amenazas en tiempo real

### Capacidades Clave

**1. Application Control (Control de Aplicaciones)**

- **App-ID**: Identifica aplicaciones independiente del puerto
- Clasifica tráfico por aplicación real, no puerto
- Permite/bloquea aplicaciones específicas
- Granularidad: Permitir Facebook pero bloquear Facebook Games

**Ejemplo**:

- Legacy: "Permitir puerto 443"
- NGFW: "Permitir Office 365, Salesforce; Bloquear Tor, BitTorrent"

**2. User/Group Identification**

- Políticas basadas en usuario, no IP
- Integración con:
    - Active Directory
    - LDAP
    - RADIUS
    - SAML
- Usuario identificado independiente de dispositivo/ubicación
- Logs con nombre de usuario (auditoría mejorada)

**Ejemplo**:

- "Departamento de Finanzas puede acceder a ERP"
- "Usuarios invitados solo Internet, no recursos internos"

**3. Deep Packet Inspection (DPI)**

- Inspecciona contenido completo del paquete
- Detecta amenazas ocultas en payload
- Analiza tráfico encriptado (SSL/TLS inspection)
- Busca patrones de malware, exploits, command & control

**4. Integrated IPS (Intrusion Prevention System)**

- Detecta y bloquea exploits, vulnerabilidades
- Base de datos de firmas actualizada
- Prevención de:
    - Buffer overflows
    - SQL injection
    - Command injection
    - Exploits conocidos

**5. Advanced Threat Prevention**

- **Sandboxing**: Ejecuta archivos sospechosos en ambiente aislado
- **Malware analysis**: Detecta comportamientos maliciosos
- **Zero-day protection**: Protege contra amenazas desconocidas
- **C2 detection**: Identifica comunicación con servidores de atacantes

**6. URL Filtering**

- Categorización de sitios web (malware, phishing, adulto, redes sociales)
- Políticas por categoría
- Base de datos actualizada en tiempo real
- Previene acceso a sitios maliciosos

**7. SSL/TLS Decryption**

- **Problema**: 80%+ tráfico encriptado, oculta amenazas
- **Solución**: Descifra, inspecciona, re-cifra
- Detecta malware en HTTPS
- Respeta privacidad (excluir sitios financieros, salud)

**8. Threat Intelligence Integration**

- Feeds de amenazas globales en tiempo real
- Bloquea IPs/dominios maliciosos conocidos
- Actualización automática de protecciones
- Contextualización de alertas

**9. Data Loss Prevention (DLP)**

- Previene exfiltración de datos sensibles
- Detecta patrones: números de tarjeta, SSN, datos médicos
- Bloquea transferencias no autorizadas
- Visibilidad de movimiento de datos

**10. Logging y Reporting Avanzado**

- Visibilidad granular de tráfico
- Reportes por aplicación, usuario, amenaza
- Análisis forense detallado
- Compliance reporting

## Arquitectura NGFW

### Procesamiento de Paquetes

**Flujo de Inspección**

1. **Packet arrives** → Stateful inspection
2. **App-ID** → Identifica aplicación real
3. **User-ID** → Identifica usuario/grupo
4. **Content-ID** → Inspecciona payload (IPS, antivirus, URL filtering)
5. **Policy match** → Aplica regla de seguridad
6. **Forward o Drop** → Permite/bloquea según política

**Single-Pass Architecture**

- Todo el análisis en una pasada
- Procesamiento paralelo
- Alto rendimiento con inspección profunda

### Security Zones

**Concepto**: Agrupar interfaces por nivel de confianza

**Zonas Típicas**

- **Untrust**: Internet (confianza cero)
- **Trust**: Red interna corporativa
- **DMZ**: Servidores públicos (web, mail)
- **Guest**: WiFi invitados
- **IoT**: Dispositivos IoT segregados

**Políticas Inter-Zone**

- Tráfico controlado entre zonas
- Default deny entre zonas
- Permite segmentación lógica

## Casos de Uso NGFW

### 1. Permitir Aplicaciones Críticas, Bloquear Riesgosas

- **Permitir**: Office 365, Salesforce, Webex
- **Bloquear**: P2P, Tor, proxy anónimos
- **Limitar**: YouTube (solo en horarios), redes sociales

### 2. Proteger Contra Amenazas Avanzadas

- Bloquear exploits conocidos (IPS)
- Detectar malware en descargas
- Prevenir C2 communication
- Sandboxing de archivos ejecutables

### 3. Prevenir Exfiltración de Datos

- DLP detecta datos sensibles saliendo
- Bloquea uploads no autorizados
- Alerta sobre transferencias sospechosas

### 4. Segmentación de Red

- Separar usuarios, servidores, IoT, invitados
- Zero Trust: verificar todo tráfico inter-segmento
- Limitar movimiento lateral de atacantes

### 5. Acceso Remoto Seguro

- VPN SSL integrada
- Políticas por usuario remoto
- Inspección de tráfico VPN

### 6. Visibilidad y Compliance

- Reportes detallados de aplicaciones usadas
- Auditoría de accesos por usuario
- Evidencia para compliance (PCI-DSS, HIPAA)

## Legacy vs NGFW: Comparación

|Capacidad|Legacy Firewall|NGFW|
|---|---|---|
|**Filtrado**|Puerto/IP/Protocolo|Aplicación + Usuario + Contenido|
|**Inspección**|Header únicamente|Deep Packet Inspection|
|**Usuario**|Solo IP (no identifica)|User-ID integrado|
|**Aplicaciones**|Basado en puerto (limitado)|App-ID (granular)|
|**Amenazas**|No detecta|IPS, Antivirus, Sandboxing|
|**Tráfico cifrado**|No inspecciona|SSL/TLS decryption|
|**Políticas**|Miles de reglas por puerto|Políticas simples por aplicación|
|**Visibilidad**|Básica (IPs, puertos)|Completa (apps, usuarios, amenazas)|
|**Protección**|Perimetro básico|Multi-capa avanzada|

## Desafíos Modernos que NGFW Resuelve

### 1. Proliferación de Aplicaciones

- Miles de aplicaciones cloud (SaaS)
- Aplicaciones usan puertos estándar (80/443)
- **Solución NGFW**: App-ID identifica y controla

### 2. Movilidad y BYOD

- Usuarios acceden desde múltiples dispositivos
- IP cambia constantemente
- **Solución NGFW**: User-ID sigue al usuario

### 3. Tráfico Encriptado

- 80%+ tráfico es HTTPS
- Malware se oculta en cifrado
- **Solución NGFW**: SSL inspection

### 4. Amenazas Avanzadas

- Zero-days, APTs, ransomware
- Firewalls legacy no detectan
- **Solución NGFW**: Sandboxing, threat intelligence

### 5. Cloud y Virtualización

- Workloads migran a cloud
- Tráfico east-west (servidor a servidor)
- **Solución NGFW**: VM-series, micro-segmentación

### 6. Compliance

- Regulaciones requieren visibilidad y control
- Auditorías demandan logs detallados
- **Solución NGFW**: Logging granular, reportes compliance

## Consideraciones de Implementación

### Rendimiento

- SSL inspection consume recursos
- Sizing adecuado para throughput requerido
- Considerar: usuarios, aplicaciones, inspección habilitada

### Políticas

- Comenzar con políticas amplias, refinar gradualmente
- Usar logs para entender tráfico antes de bloquear
- Documentar excepciones

### SSL Decryption

- Definir qué descifrar (no todo es necesario)
- Excluir: financiero, salud, sitios personales sensibles
- Considerar privacidad y legal

### High Availability

- Configuración Active/Passive o Active/Active
- Sincronización de sesiones
- Failover automático

### Integración

- Conectar con AD/LDAP para User-ID
- Integrar con SIEM para correlación
- APIs para automatización

### Capacitación

- Equipo debe entender capacidades NGFW
- Políticas basadas en aplicación, no puerto
- Interpretación de logs avanzados

## Mejores Prácticas

1. **Positive Security Model**: Permitir solo lo necesario, bloquear todo lo demás
2. **Segmentación**: Dividir red en zonas de seguridad
3. **User-based policies**: Políticas por rol/grupo, no por IP
4. **Enable all security features**: IPS, antivirus, URL filtering, sandboxing
5. **SSL inspection**: Inspeccionar tráfico cifrado (con excepciones apropiadas)
6. **Regular updates**: Mantener firmas y threat intelligence actualizadas
7. **Monitoring**: Revisar logs y alertas regularmente
8. **Documentation**: Documentar políticas y cambios
9. **Testing**: Probar cambios en ambiente de prueba primero
10. **Least privilege**: Solo permisos necesarios