## Amenazas a Endpoints

### Tipos de Amenazas

**Malware**

- **Virus**: Se adjunta a archivos, requiere ejecución por usuario
- **Worm**: Se auto-replica y propaga sin intervención
- **Trojan**: Se disfraza como software legítimo
- **Ransomware**: Cifra archivos, exige pago para descifrar
- **Spyware**: Recopila información sin consentimiento
- **Adware**: Muestra publicidad no deseada
- **Rootkit**: Oculta presencia de malware, acceso nivel root/admin
- **Botnet**: Red de dispositivos infectados controlados remotamente

**Ataques de Ingeniería Social**

- **Phishing**: Emails fraudulentos para robar credenciales
- **Spear Phishing**: Phishing dirigido a persona/organización específica
- **Whaling**: Phishing a ejecutivos de alto nivel
- **Vishing**: Phishing por voz/teléfono
- **Smishing**: Phishing por SMS
- **Pretexting**: Crear escenario falso para obtener información
- **Baiting**: Ofrecer algo para infectar (USB, descarga gratuita)

**Otros Ataques**

- **Zero-Day**: Explota vulnerabilidad desconocida
- **Drive-by Download**: Descarga automática al visitar sitio web
- **Fileless Malware**: Opera en memoria, sin archivos en disco
- **Cryptojacking**: Usa recursos para minar criptomonedas

## Protección de Endpoints

### Antivirus/Anti-Malware

**Métodos de Detección**

- **Basado en firmas**: Compara contra base de datos de malware conocido
- **Heurístico**: Analiza comportamiento sospechoso
- **Sandboxing**: Ejecuta archivos en ambiente aislado
- **Machine Learning**: Detecta patrones anómalos

**Limitaciones**

- No detecta amenazas nuevas (zero-day) con firmas
- Requiere actualizaciones constantes
- Puede generar falsos positivos

### EDR (Endpoint Detection and Response)

**Funciones**

- Monitoreo continuo de endpoints
- Detección de comportamientos anómalos
- Respuesta automatizada a amenazas
- Análisis forense post-incidente
- Threat hunting proactivo

**Ventajas sobre Antivirus Tradicional**

- Detecta amenazas avanzadas
- Visibilidad completa de actividad
- Respuesta rápida y automatizada

### XDR (Extended Detection and Response)

**Concepto**: Integra datos de múltiples fuentes (endpoints, red, cloud, aplicaciones)

- Correlación de eventos entre capas
- Visión holística de amenazas
- Respuesta coordinada

### Hardening de Endpoints

**Configuración Segura**

- Deshabilitar servicios innecesarios
- Cerrar puertos no utilizados
- Remover software no necesario
- Configurar firewall local

**Control de Acceso**

- Principio de mínimo privilegio
- Usuarios estándar (no admin) para tareas diarias
- Cuentas de admin solo cuando necesario
- Deshabilitar cuentas no utilizadas

**Actualizaciones**

- Parches de seguridad automáticos
- Actualización regular de SO y aplicaciones
- Firmware actualizado

**Cifrado**

- Disco completo (BitLocker, FileVault)
- Protege datos si dispositivo se pierde/roba

**Otros Controles**

- Deshabilitar autorun/autoplay
- Filtrado de macros en Office
- AppLocker/whitelisting de aplicaciones
- Screen lock automático

## Amenazas a la Red

### Tipos de Ataques

**Reconnaissance (Reconocimiento)**

- **Escaneo de puertos**: Identificar servicios abiertos (nmap)
- **Escaneo de vulnerabilidades**: Buscar debilidades
- **Sniffing**: Captura de tráfico de red
- **OSINT**: Información pública sobre organización

**DoS/DDoS (Denial of Service)**

- **Objetivo**: Saturar recursos, hacer servicio no disponible
- **Tipos**:
    - Volumétrico (floods de tráfico)
    - Protocolo (agotar recursos de conexión)
    - Aplicación (ataques a capa 7)
- **DDoS**: Ataque desde múltiples fuentes (botnet)

**Man-in-the-Middle (MitM)**

- Interceptar comunicación entre dos partes
- ARP Spoofing, DNS Spoofing
- Captura/modificación de datos

**Spoofing**

- **IP Spoofing**: Falsificar dirección IP origen
- **MAC Spoofing**: Falsificar dirección MAC
- **DNS Spoofing**: Redirigir a sitio falso

**Session Hijacking**

- Robar sesión activa de usuario
- Captura de cookies/tokens de sesión

**Ataques a Contraseñas**

- **Brute Force**: Probar todas las combinaciones
- **Dictionary Attack**: Usar lista de contraseñas comunes
- **Credential Stuffing**: Usar credenciales filtradas
- **Password Spraying**: Probar contraseñas comunes en muchas cuentas

**Inyección**

- **SQL Injection**: Manipular queries de base de datos
- **Command Injection**: Ejecutar comandos en servidor
- **XSS (Cross-Site Scripting)**: Inyectar scripts en páginas web

## Seguridad de Red

### Firewall

**Tipos**

- **Packet Filtering**: Filtra por IP/puerto/protocolo (stateless)
- **Stateful**: Rastrea estado de conexiones
- **Next-Gen (NGFW)**: Inspección profunda, filtrado aplicación, IPS integrado
- **WAF (Web Application Firewall)**: Protege aplicaciones web (capa 7)

**Ubicación**

- Network Firewall: Perímetro de red
- Host-based Firewall: En cada endpoint

**Zonas de Seguridad**

- **Outside/Untrusted**: Internet
- **DMZ**: Servidores públicos (web, mail)
- **Inside/Trusted**: Red interna

### IDS/IPS

**IDS (Intrusion Detection System)**

- Monitorea tráfico, detecta actividad sospechosa
- **Alerta** pero no bloquea
- Tipos:
    - **NIDS**: Network-based (analiza tráfico de red)
    - **HIDS**: Host-based (analiza logs/archivos en host)

**IPS (Intrusion Prevention System)**

- IDS + **bloqueo activo**
- Inline con el tráfico
- Puede generar falsos positivos que afecten servicios

**Métodos de Detección**

- **Basado en firmas**: Patrones de ataques conocidos
- **Basado en anomalías**: Desviación del comportamiento normal
- **Híbrido**: Combinación de ambos

### VLANs (Virtual LANs)

**Concepto**: Segmentar red lógicamente en switch

- Separar tráfico por función/departamento
- Mejora seguridad y rendimiento
- Reduce dominio de broadcast

**Segmentación Típica**

- VLAN 10: Usuarios corporativos
- VLAN 20: Invitados/WiFi público
- VLAN 30: Servidores
- VLAN 40: VoIP
- VLAN 50: IoT
- VLAN 99: Administración

### ACLs (Access Control Lists)

**Función**: Filtrar tráfico en routers/switches

- Basado en IP origen/destino, puertos, protocolos
- **Standard ACL**: Solo IP origen
- **Extended ACL**: IP origen/destino, puertos, protocolo

**Mejores Prácticas**

- Regla implícita: deny all al final
- Colocar reglas más específicas primero
- Documentar propósito de cada regla

### NAC (Network Access Control)

**Función**: Controlar qué dispositivos acceden a la red

- Verificar cumplimiento de políticas antes de acceso
- Quarantine de dispositivos no conformes
- Integración con autenticación (802.1X)

**Verificaciones**

- Antivirus actualizado
- Parches instalados
- Firewall activo
- Cifrado de disco

## Metodología de Troubleshooting

### Proceso Estructurado

**1. Identificar el Problema**

- Recopilar información
- Preguntar al usuario
- Identificar síntomas
- Determinar cambios recientes
- Duplicar el problema si es posible

**2. Establecer Teoría de Causa Probable**

- Considerar causas obvias primero
- Cuestionar lo obvio
- Desarrollar hipótesis

**3. Probar la Teoría**

- Confirmar teoría
- Si se confirma: proceder al siguiente paso
- Si no: establecer nueva teoría

**4. Establecer Plan de Acción**

- Definir pasos para resolver
- Identificar efectos potenciales
- Obtener aprobación si necesario

**5. Implementar Solución**

- Ejecutar plan
- Documentar acciones
- Hacer backup antes si aplica

**6. Verificar Funcionalidad Completa**

- Confirmar que problema está resuelto
- Verificar que no se crearon nuevos problemas
- Medidas preventivas

**7. Documentar**

- Problema encontrado
- Pasos tomados
- Solución implementada
- Lecciones aprendidas

### Herramientas de Troubleshooting

**Comandos de Red**

- `ping`: Verificar conectividad (ICMP)
- `traceroute/tracert`: Mapear ruta de paquetes
- `nslookup/dig`: Verificar resolución DNS
- `ipconfig/ifconfig`: Ver configuración IP
- `netstat`: Ver conexiones activas y puertos
- `arp -a`: Ver caché ARP
- `nmap`: Escaneo de puertos/servicios

**Analizadores de Red**

- **Wireshark**: Captura y análisis de paquetes
- **tcpdump**: Captura en línea de comandos

**Logs**

- Firewall logs
- IDS/IPS logs
- System logs (syslog, Event Viewer)
- Application logs
- Authentication logs

## Mejores Prácticas de Seguridad

### Defensa en Profundidad (Defense in Depth)

- Múltiples capas de seguridad
- Si una falla, otras protegen

**Capas Típicas**

1. Perímetro: Firewall, IPS
2. Red: Segmentación, ACLs
3. Endpoint: Antivirus, EDR, hardening
4. Aplicación: WAF, secure coding
5. Datos: Cifrado, DLP
6. Usuario: Capacitación, MFA

### Principio de Mínimo Privilegio

- Acceso solo lo necesario
- Cuando necesario
- Por tiempo necesario

### Zero Trust

- "Never trust, always verify"
- Verificar cada acceso
- No confiar por ubicación de red
- Micro-segmentación

### Capacitación de Usuarios

- Conciencia de seguridad
- Identificar phishing
- Reporte de incidentes
- Políticas de contraseñas seguras

### Gestión de Parches

- Inventario de activos
- Priorizar parches críticos
- Testing antes de producción
- Automatizar cuando posible

### Backups

- Regla 3-2-1: 3 copias, 2 medios diferentes, 1 offsite
- Probar restauración regularmente
- Proteger backups (inmutables)

### Monitoreo Continuo

- SIEM para correlación de eventos
- Alertas en tiempo real
- Threat intelligence
- Security metrics/KPIs

### Plan de Respuesta a Incidentes

- Preparación
- Detección y análisis
- Contención
- Erradicación
- Recuperación
- Lecciones aprendidas