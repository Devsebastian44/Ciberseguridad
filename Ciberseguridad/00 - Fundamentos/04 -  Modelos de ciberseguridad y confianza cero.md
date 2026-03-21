## Limitaciones del Modelo Perimeter-Based

### Modelo Tradicional (Castle-and-Moat)

**Concepto:**

- Perímetro de red = "muralla del castillo"
- Dentro = confiado
- Fuera = no confiado
- Firewall como barrera principal

**Asunciones:**

```
Internet (no confiado) → Firewall → Red interna (confiada)
```

### Limitaciones Críticas

**1. Perímetro Difuso/Inexistente**

- **Trabajo remoto:** Usuarios fuera de la red corporativa
- **Cloud/SaaS:** Aplicaciones fuera del perímetro
- **BYOD:** Dispositivos no controlados
- **Partners/Proveedores:** Acceso externo necesario

**2. Insider Threats**

- **Asunción fallida:** "Dentro = confiado"
- Empleados maliciosos o comprometidos
- Movimiento lateral sin restricciones

**3. Lateral Movement**

- Una vez dentro, acceso amplio
- Atacante puede moverse libremente
- Difícil contener brechas

**4. Falta de Visibilidad**

- Tráfico Este-Oeste (interno) no inspeccionado
- No monitoreo de usuarios/dispositivos internos

**5. Inadecuado para Cloud**

- SaaS apps fuera del perímetro
- Datos distribuidos globalmente
- Multi-cloud environments

---

## Zero Trust Model

### Principio Fundamental

**"Never Trust, Always Verify"**

- **No confiar en nada** por default (ni interno ni externo)
- **Verificar explícitamente** cada acceso
- **Asumir breach:** Actuar como si ya estuvieras comprometido

### Filosofía Core

```
Modelo Tradicional: Trust but Verify
Zero Trust:         Never Trust, Always Verify
```

**Cambio de paradigma:**

- **Antes:** Ubicación determina confianza (dentro/fuera)
- **Ahora:** Identidad + contexto determina acceso

---

## Principios de Zero Trust

### 1. Verify Explicitly

**Siempre autenticar y autorizar** basado en todos los datos disponibles:

- Identidad del usuario
- Ubicación (geolocalización)
- Device health (postura del dispositivo)
- Servicio/aplicación
- Clasificación de datos
- Anomalías comportamentales

**Decisión de acceso en tiempo real**

### 2. Least Privilege Access

- **Mínimo acceso necesario** para realizar la tarea
- Just-In-Time (JIT) access
- Just-Enough-Access (JEA)
- Limitar blast radius (radio de impacto)

**Ejemplo:**

```
Usuario necesita acceder solo a archivo X
→ Acceso SOLO a archivo X (no carpeta completa)
→ Solo por tiempo necesario
→ Solo lectura (si no necesita editar)
```

### 3. Assume Breach

- **Operar como si ya estuvieras comprometido**
- Minimizar blast radius
- **Micro-segmentación**
- Cifrado end-to-end
- Analytics para detectar amenazas
- Logging y monitoreo exhaustivo

---

## Arquitectura Zero Trust

### Componentes Clave

#### **1. Identity and Access Management (IAM)**

**Strong Authentication:**

- **Multi-Factor Authentication (MFA)** obligatorio
- Passwordless (FIDO2, biometrics)
- Conditional Access (basado en riesgo)

**Identity Provider (IdP):**

- Azure AD, Okta, Ping Identity
- Single Sign-On (SSO)
- Centralización de identidades

#### **2. Device Security**

**Endpoint Protection:**

- EDR (Endpoint Detection and Response)
- Device compliance checks
- Patch status verification
- Encryption verification

**Device Trust:**

- Managed devices vs BYOD
- Health attestation
- Continuous monitoring

#### **3. Micro-Segmentation**

**Definición:** Dividir red en segmentos muy pequeños

**Beneficios:**

- Limitar lateral movement
- Contener brechas
- Granular security policies

**Implementación:**

```
Tradicional: VLAN grande (todos los servidores web juntos)
Zero Trust: Cada aplicación/workload en segmento separado
```

**Software-Defined Perimeters (SDP)**

#### **4. Policy Engine**

**Decision Point centralizado:**

```
Usuario + Dispositivo + Contexto → Policy Engine → Permitir/Denegar
```

**Factores evaluados:**

- Identidad autenticada
- Device compliance
- Location
- Time of day
- Risk score
- Data sensitivity

**Adaptativo:** Políticas ajustan en tiempo real

#### **5. Data Protection**

**Clasificación de datos:**

- Public, Internal, Confidential, Restricted
- Políticas basadas en clasificación

**Encryption:**

- At rest
- In transit
- End-to-end

**DLP (Data Loss Prevention):**

- Prevenir exfiltración
- Control de sharing

#### **6. Network Security**

**ZTNA (Zero Trust Network Access):**

- Reemplazo de VPN tradicional
- Acceso granular (app-level, no network-level)
- Identity-based, no IP-based

**SWG (Secure Web Gateway):**

- Inspección de tráfico web
- Protection contra amenazas web

**CASB (Cloud Access Security Broker):**

- Visibilidad y control de SaaS apps
- Shadow IT detection

#### **7. Visibility and Analytics**

**SIEM/SOAR:**

- Logging centralizado
- Correlation de eventos
- Automated response

**UEBA (User and Entity Behavior Analytics):**

- Behavioral baselines
- Anomaly detection
- Insider threat detection

**Continuous Monitoring:**

- Tiempo real
- Todas las interacciones
- User, device, application, data

---

## Implementación Zero Trust

### Enfoque por Fases

#### **Fase 1: Visualizar**

- Identificar todos los assets (usuarios, dispositivos, aplicaciones, datos)
- Mapear flujos de tráfico
- Identificar datos sensibles

#### **Fase 2: Mitigar**

- Implementar MFA
- Detectar amenazas
- Remediar vulnerabilidades

#### **Fase 3: Optimizar**

- Aplicar least privilege
- Micro-segmentación
- Automatización

### Modelo de Madurez

**Nivel 1 - Traditional:**

- Perímetro-based
- Static policies

**Nivel 2 - Advanced:**

- MFA implementado
- Alguna segmentación
- Cloud-aware

**Nivel 3 - Optimal (Zero Trust):**

- Fully automated
- Dynamic policies
- Micro-segmentation
- Continuous verification

---

## Tecnologías Enablers

### SASE (Secure Access Service Edge)

**Definición:** Convergencia de red + seguridad en cloud-native service

**Componentes:**

- **SD-WAN** (Software-Defined WAN)
- **ZTNA** (Zero Trust Network Access)
- **SWG** (Secure Web Gateway)
- **CASB** (Cloud Access Security Broker)
- **FWaaS** (Firewall as a Service)

**Beneficio:** Security follows user (no importa ubicación)

### ZTNA (Zero Trust Network Access)

**vs VPN Tradicional:**

|**VPN**|**ZTNA**|
|---|---|
|Network-level access|Application-level access|
|IP-based trust|Identity-based trust|
|Acceso amplio una vez dentro|Granular, least privilege|
|Lateral movement fácil|Lateral movement bloqueado|

**Funcionamiento ZTNA:**

```
Usuario autenticado → Solicita app → Policy check → 
Micro-tunnel a app específica (no network access)
```

### Software-Defined Perimeter (SDP)

- Infraestructura "dark" (invisible hasta autenticación)
- Conexiones 1-to-1
- Oculta recursos de atacantes

---

## Beneficios de Zero Trust

✅ **Reducción de superficie de ataque**  
✅ **Protección contra lateral movement**  
✅ **Mejor protección de datos sensibles**  
✅ **Compliance mejorado** (logging detallado)  
✅ **Soporte para trabajo remoto/hybrid**  
✅ **Cloud-native compatible**  
✅ **Visibilidad mejorada** (todas las interacciones)  
✅ **Detección de amenazas más rápida**

---

## Desafíos de Implementación

**Complejidad:**

- Requiere transformación cultural y técnica
- Múltiples tecnologías a integrar

**Costo inicial:**

- Inversión significativa
- Tiempo de implementación

**Legacy systems:**

- Aplicaciones antiguas no compatibles
- Migración gradual necesaria

**User experience:**

- Balance entre seguridad y usabilidad
- MFA puede frustrar usuarios (si mal implementado)

**Skills gap:**

- Requiere nuevas habilidades del equipo

---

## Mejores Prácticas

**1. Start Small:**

- Piloto con aplicación crítica
- Expandir gradualmente

**2. Priorizar:**

- Crown jewels primero (datos más sensibles)
- Usuarios de alto riesgo primero (privilegiados)

**3. User Experience:**

- SSO para reducir friction
- Passwordless donde posible
- Context-aware (menos MFA si low-risk)

**4. Automation:**

- Policy enforcement automatizado
- Orchestration de respuesta

**5. Continuous Improvement:**

- Revisar políticas regularmente
- Adaptar a nuevas amenazas
- Feedback de usuarios
