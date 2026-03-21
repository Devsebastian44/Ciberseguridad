## ¿Qué es SASE?

**Definición**: Convergencia de **Red (SD-WAN) + Seguridad** entregada desde la **nube** como servicio unificado

**SASE = Networking + Security as a Service**

## Por Qué SASE (Problemas que Resuelve)

### Modelo Tradicional (Problemas)

- **Backhauling**: Tráfico cloud hace rodeo innecesario (Sucursal → Datacenter → Internet → SaaS)
- **Latencia alta**: Mala experiencia usuario
- **Costos altos**: MPLS caro, appliances en cada sitio
- **Complejidad**: Múltiples vendors, gestión fragmentada
- **No escala**: Para usuarios remotos y cloud

### Drivers para SASE

1. **Adopción Cloud/SaaS** (Office 365, Salesforce, etc.)
2. **Trabajo remoto/distribuido** (usuarios en cualquier parte)
3. **Transformación digital** (migración a cloud)
4. **Amenazas avanzadas** (ransomware, phishing)

## Componentes SASE

### Seguridad (SSE)

|Componente|Función|
|---|---|
|**SWG** (Secure Web Gateway)|URL filtering, malware detection, SSL inspection|
|**CASB** (Cloud Access Security Broker)|Visibilidad/control de apps cloud (shadow IT), DLP en SaaS|
|**ZTNA** (Zero Trust Network Access)|Reemplazo VPN, acceso granular solo a apps específicas|
|**FWaaS** (Firewall as a Service)|NGFW en la nube (IPS, App-ID, threat prevention)|
|**DLP**|Previene fuga de datos sensibles|

### Networking

**SD-WAN**

- Múltiples transportes (MPLS, Internet, LTE)
- Ruteo inteligente por aplicación
- QoS, failover automático
- Reduce costos (menos MPLS)

**DNS Security**

- Bloquea queries maliciosas
- Previene C2, phishing

## ZTNA vs VPN Tradicional

|VPN|ZTNA|
|---|---|
|Acceso a red completa|Acceso solo a apps específicas|
|Basado en ubicación|Basado en identidad + contexto|
|Trust implícito|Never trust, always verify|
|Mayor superficie de ataque|Menor superficie de ataque|

## Beneficios Clave SASE

### 1. Rendimiento

- Usuarios conectan a PoP cercano (baja latencia)
- No backhauling (directo a cloud)
- Mejor experiencia usuario

### 2. Seguridad Consistente

- Mismas políticas para todos (oficina, remoto, sucursales)
- Protección sigue al usuario, no ubicación

### 3. Simplicidad

- Gestión centralizada (single pane of glass)
- No appliances en cada sitio
- Despliegue rápido (días vs meses)

### 4. Costos Reducidos

- Menos/elimina MPLS
- No hardware en sucursales
- Modelo OpEx (pago por uso)

### 5. Escalabilidad

- Agregar usuarios/sitios sin hardware
- Escala elástica

## Arquitectura SASE

```
Usuario/Sucursal → PoP SASE más cercano → Inspección Security + SD-WAN → Destino
```

**PoPs Globales**: Distribuidos geográficamente para baja latencia **Single-Pass**: Inspección + ruteo en una pasada (alto rendimiento)

## Casos de Uso

**1. Trabajo Remoto**

- ZTNA para acceso a apps corporativas (sin VPN)
- SWG protege navegación web
- DLP previene fuga de datos

**2. Transformación Cloud**

- SD-WAN optimiza tráfico a SaaS/IaaS
- CASB protege apps cloud
- FWaaS protege workloads

**3. Sucursales sin IT**

- Seguridad cloud-delivered (no firewall local)
- Gestión centralizada
- Bajo costo por sitio

## SASE vs Tradicional

|Aspecto|Tradicional|SASE|
|---|---|---|
|Entrega|Appliances on-prem|Cloud service|
|Tráfico cloud|Backhauling|Directo|
|Acceso remoto|VPN|ZTNA|
|Gestión|Múltiples consolas|Unificada|
|Escalabilidad|Hardware|Elástica|
|Despliegue|Semanas/meses|Días|

## Implementación (Enfoque Recomendado)

### Migración por Fases

1. **Fase 1**: Remote users (ZTNA)
2. **Fase 2**: SaaS security (CASB, SWG)
3. **Fase 3**: Sucursales (SD-WAN)
4. **Fase 4**: Datacenter migration

### Consideraciones

- **Conectividad**: Ancho de banda Internet suficiente, redundancia
- **Integración**: SSO, AD, SIEM
- **Políticas**: Mapear existentes a SASE
- **Capacitación**: Usuarios y staff IT

## Proveedores Principales

- **Palo Alto Networks** (Prisma SASE)
- **Zscaler**
- **Netskope**
- **Cisco**

## Best Practices

### Seguridad

- Zero Trust por default
- MFA obligatorio
- Inspección SSL/TLS
- DLP habilitado

### Operaciones

- Monitoreo continuo
- Logs a SIEM
- Documentar políticas
- Testing regular

### Rendimiento

- Usuarios al PoP más cercano
- QoS para apps críticas
- Dimensionar ancho de banda adecuadamente