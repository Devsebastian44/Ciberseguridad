## Spamming

**Definición:** Mensajes no solicitados enviados en masa

**Tipos:**

- Email spam (más común)
- SMS spam (smishing)
- Social media spam

**Propósitos:**

- Publicidad no solicitada
- Distribución de malware
- Phishing
- Fraude

**Volumen:** 45-85% del email global es spam

---

## Phishing

### Tipos de Phishing

#### **1. Email Phishing (Genérico)**

- Emails masivos no personalizados
- Baja tasa de éxito (alto volumen)
- Señuelos: Bancos, urgencia, verificación de cuenta

**Señales:**

- Sender address sospechoso
- Urgencia artificial
- Errores gramaticales
- Links que no coinciden
- Solicitud de credenciales

#### **2. Spear Phishing (Dirigido)**

- **Altamente personalizado**
- Investigación previa del objetivo (OSINT)
- Mayor tasa de éxito
- Usa nombres reales, proyectos, roles

#### **3. Whaling**

- Dirigido a ejecutivos (CEO, CFO, CTO)
- Alto impacto: Información crítica, autorizaciones financieras

#### **4. Smishing (SMS Phishing)**

- Mensajes de texto
- Ejemplos: "Package delivery failed", "Bank alert"
- Mayor tasa de apertura en móviles

#### **5. Vishing (Voice Phishing)**

- Llamadas telefónicas
- Caller ID spoofing
- Ejemplo: "Microsoft Tech Support scam"

#### **6. Angler Phishing**

- Via social media (Twitter, Facebook)
- Cuentas falsas de customer support
- Interceptar quejas de clientes

#### **7. Clone Phishing**

- Copiar email legítimo
- Reemplazar links/adjuntos con maliciosos
- Reenviar como "updated version"

#### **8. Pharming**

- DNS poisoning
- Usuario escribe URL correcta → redirigido a sitio falso

### Business Email Compromise (BEC)

**CEO Fraud:**

- Email spoofed del CEO → CFO
- "Wire $500K urgently. Confidential."

**Invoice Scam:**

- Suplantar proveedor legítimo
- Factura con nueva cuenta bancaria

**Account Compromise:**

- Compromiso real de cuenta de empleado
- Solicitudes de wire transfers

**Impacto:** Pérdidas $50K-$2M por incidente

### Técnicas de Phishing

**URL Obfuscation:**

```
Homograph: paypаl.com (letra cirílica)
Subdomain: www.paypal.com.evil.com
Typosquatting: paypa1.com
URL shortener: bit.ly/xxxxx
```

**Email Spoofing:**

- Display name: `"CEO" <attacker@evil.com>`
- Domain spoofing (sin SPF/DKIM/DMARC)

**Malicious Attachments:**

- Macro-enabled Office docs (.docm, .xlsm)
- JavaScript files (.js)
- Archives con ejecutables (.zip)
- PDF con exploits

**Credential Harvesting:**

```
Email phishing → Click link → Fake login page → 
Víctima ingresa credenciales → Enviadas a atacante
```

---

## Bots y Botnets

### Definiciones

**Bot:** Programa malicioso que ejecuta tareas automatizadas bajo control remoto

**Botnet:** Red de dispositivos comprometidos (zombies) controlados por botmaster

**Tamaño:** Miles a millones de bots

### Arquitecturas de Botnet

#### **1. Centralized (Cliente-Servidor)**

```
Botmaster → C2 Server → Bots
```

- Control simple y directo
- **Desventaja:** Single point of failure
- Ejemplos: Zeus, Conficker

#### **2. Peer-to-Peer (P2P)**

```
Botmaster → Algunos bots → Otros bots (sin servidor central)
```

- Muy resistente a takedowns
- Difícil de desmantelar
- Ejemplos: Gameover ZeuS, Sality

#### **3. Hybrid**

- Combinación centralizado + P2P
- C2 servers + P2P para resiliencia

### Canales C2

- **HTTP/HTTPS:** Tráfico parece legítimo (puerto 80/443)
- **DNS:** DNS tunneling
- **Social Media:** Twitter, Telegram, Pastebin
- **DGA (Domain Generation Algorithms):** Bot genera miles de dominios diarios

---

## Tipos de Botnets por Función

### 1. Spam Botnets

- Envío masivo de spam
- Millones de emails diarios
- Ejemplos: Cutwail, Grum
- **Impacto:** 85%+ spam global

### 2. DDoS Botnets

**Tipos de Ataques:**

- **Volumétricos:** UDP flood, DNS amplification
- **Protocol:** SYN flood, ACK flood
- **Application layer:** HTTP flood, Slowloris

**Ejemplos:**

- **Mirai:** IoT devices, credenciales default, ataques 1+ Tbps

### 3. Banking Trojans

- Robo de credenciales financieras
- Keylogging, form grabbing, web injects
- Ejemplos: Zeus, Emotet, TrickBot, Dridex

### 4. Click Fraud Botnets

- Fraude publicitario (clicks en ads)
- Miles de millones en fraude anualmente

### 5. Cryptocurrency Mining

- Cryptojacking (minería de criptomonedas)
- Uso de CPU/GPU de víctimas
- Ejemplos: Smominru, Adylkuzz

### 6. Ransomware Distribution

- Distribución de ransomware
- Ejemplo: Emotet → loader de Ryuk, Conti

---

## Ciclo de Vida del Bot

**1. Infection:** Email phishing, exploit kits, credenciales débiles  
**2. Installation:** Persistencia, deshabilitar AV  
**3. Registration:** Beacon al C2, asignar ID  
**4. Idle State:** Espera comandos, heartbeat periódico  
**5. Command Execution:** DDoS, spam, steal, update  
**6. Update/Removal:** Actualización o auto-destrucción

---

## Medidas de Seguridad

### Prevención

**Email Security:**

- Anti-spam/anti-phishing filters
- Sandboxing de adjuntos
- **DMARC/SPF/DKIM** (validar sender)
- User awareness training

**Endpoint Protection:**

- Next-gen Antivirus
- **EDR** (behavioral detection)
- Application whitelisting
- Disable macros

**Patch Management:**

- Actualizar OS y aplicaciones
- Priorizar CVEs críticos
- Automated patching

**Network Segmentation:**

- Segmentar red (IoT separado)
- VLANs por función
- Limitar lateral movement

**Access Controls:**

- **Least privilege**
- **MFA** (Multi-Factor Authentication)
- **Cambiar credenciales default** (crítico IoT)

### Detección

**Network Monitoring:**

- **Beaconing** (comunicación periódica al C2)
- Tráfico a IPs maliciosas
- DNS queries sospechosas (DGA patterns)
- IDS/IPS, NTA (Network Traffic Analysis)

**Endpoint Monitoring:**

- Procesos desconocidos
- Uso elevado CPU/GPU (cryptomining)
- Network connections inesperadas
- EDR, SIEM

**Threat Intelligence:**

- Feeds de C2 IPs/dominios conocidos
- IoCs de botnets
- Bloqueo proactivo

### Respuesta

**Containment:**

- **Aislar endpoints infectados**
- **Bloquear C2 communication**
- Prevenir lateral movement

**Eradication:**

- Eliminar malware
- Remover persistencia
- Clean or reimage sistemas
- Cambiar credenciales

**Bloqueo C2:**

- **Sinkholing:** Redirigir tráfico C2
- **DNS blackholing**
- **Firewall rules**
- Takedown collaboration

---

## Defensas Específicas

### DDoS Botnets

- DDoS mitigation services (Cloudflare, Akamai)
- Rate limiting
- Traffic scrubbing

### Spam Botnets

- Email authentication (SPF/DKIM/DMARC)
- Reputation-based filtering

### Banking Trojans

- Out-of-band verification
- Transaction monitoring
- Virtual keyboards (anti-keylogging)

### IoT Botnets

- **Cambiar default credentials** (crítico)
- Firmware updates
- Network isolation (VLAN separada)
