## Perfiles de Atacantes

### 1. Script Kiddies

- Baja habilidad técnica
- Usan herramientas pre-hechas
- Motivación: Diversión, ego
- **Peligrosidad:** Baja

### 2. Hacktivists

- Motivación: Ideología política/social
- Ataques: DDoS, defacement, data leaks
- Ejemplos: Anonymous, LulzSec
- **Peligrosidad:** Media

### 3. Cybercriminals

- **Motivación: Ganancia financiera**
- Ransomware, fraude, robo de datos
- Ransomware-as-a-Service (RaaS)
- **Peligrosidad:** Alta

### 4. Insider Threats

- **Malicious:** Intención maliciosa (robo IP, sabotaje)
- **Negligent:** Errores, descuidos
- Acceso legítimo a sistemas
- **Peligrosidad:** Muy Alta

### 5. Nation-State Actors (APTs)

- Motivación: Espionaje, sabotaje
- Recursos ilimitados, altamente sofisticados
- Ejemplos: APT28 (Rusia), Lazarus (Corea del Norte)
- Técnicas: Zero-days, custom malware
- **Peligrosidad:** Extremadamente Alta

### 6. Terrorist Groups

- Motivación: Terror, ideología extremista
- Objetivos: Infraestructura crítica
- **Peligrosidad:** Muy Alta

### 7. Competitors

- Espionaje industrial/corporativo
- Robo de propiedad intelectual
- Secretos comerciales

---

## Cyberattack Lifecycle (Kill Chain)

### 1. Reconnaissance (Reconocimiento)

**Objetivo:** Recopilar información del objetivo

**Actividades:**

- OSINT (Open Source Intelligence)
- Identificar empleados (LinkedIn)
- Tecnologías usadas
- IPs, dominios

**Tipos:**

- **Passive:** Sin interacción (OSINT)
- **Active:** Scanning (detectable)

### 2. Weaponization (Armado)

**Objetivo:** Crear exploit/payload

**Actividades:**

- Desarrollar malware
- Crear documento malicioso (PDF, Office)
- Combinar exploit + payload
- Ofuscar código

### 3. Delivery (Entrega)

**Objetivo:** Transmitir el arma al objetivo

**Métodos:**

- **Email phishing** (más común)
- Spear phishing
- Watering hole
- USB drops
- Drive-by downloads

### 4. Exploitation (Explotación)

**Objetivo:** Ejecutar código en sistema víctima

**Técnicas:**

- Vulnerabilidades (CVEs)
- Zero-days
- SQL injection
- Privilege escalation

### 5. Installation (Instalación)

**Objetivo:** Establecer persistencia

**Mecanismos:**

- Registry keys (Windows)
- Scheduled tasks
- Services/Daemons
- Rootkits

### 6. Command & Control (C2)

**Objetivo:** Comunicación con servidor del atacante

**Canales:**

- HTTP/HTTPS (puerto 80/443)
- DNS tunneling
- Social media (Twitter, Telegram)
- Domain Generation Algorithm (DGA)

### 7. Actions on Objectives

**Objetivo:** Cumplir misión del atacante

**Acciones:**

- **Data Exfiltration:** Robo de datos
- **Lateral Movement:** Moverse a otros sistemas
- **Privilege Escalation:** Obtener admin/root
- **Destruction:** Ransomware, borrar datos

---

## MITRE ATT&CK Framework

### Definición

**ATT&CK** = Adversarial Tactics, Techniques, and Common Knowledge

- Knowledge base de tácticas y técnicas de atacantes
- Basado en observaciones del mundo real

### 14 Tácticas (Enterprise)

**1. Reconnaissance** - Gathering information  
**2. Resource Development** - Acquire infrastructure  
**3. Initial Access** - Phishing, exploit public apps  
**4. Execution** - Ejecutar código malicioso  
**5. Persistence** - Mantener acceso  
**6. Privilege Escalation** - Obtener permisos mayores  
**7. Defense Evasion** - Evitar detección  
**8. Credential Access** - Robar credenciales (Mimikatz)  
**9. Discovery** - Explorar el entorno  
**10. Lateral Movement** - Moverse entre sistemas (RDP, SSH)  
**11. Collection** - Recolectar datos objetivo  
**12. Command and Control** - Comunicación C2  
**13. Exfiltration** - Extraer datos  
**14. Impact** - Ransomware, destrucción

### Uso de ATT&CK

- Mapear controles de seguridad a técnicas
- Identificar gaps de cobertura
- Threat hunting basado en TTPs
- Crear detecciones en SIEM/EDR

---

## Seguridad Wireless

### Vulnerabilidades

**Protocolos:**

- **WEP:** Completamente roto - NUNCA USAR
- **WPA:** Vulnerable
- **WPA2:** Vulnerable a KRACK
- **WPA3:** Más seguro (recomendado)

### Ataques Comunes

**1. Eavesdropping:**

- Capturar tráfico wireless
- Herramienta: Wireshark

**2. Deauthentication Attack:**

- Desconectar clientes
- Capturar WPA handshake
- Brute force offline

**3. Evil Twin:**

- AP falso con mismo SSID
- MITM attacks
- Interceptar todo el tráfico

**4. WPS Attack:**

- PIN de 8 dígitos
- Brute force en horas
- **Mitigación:** Deshabilitar WPS

**5. Rogue Access Points:**

- AP no autorizado en red corporativa
- Bypass de controles

### Mejores Prácticas

✅ **WPA3** con contraseñas fuertes  
✅ **802.1X** (Enterprise authentication)  
✅ **Network segmentation** (VLANs)  
✅ **WIPS** (Wireless Intrusion Prevention)  
✅ **Deshabilitar WPS**  
✅ **Guest network isolation**  
✅ **Monitoreo de rogue APs**
