## Cortex XSOAR

Plataforma SOAR de Palo Alto Networks con +600 integraciones y capacidades de Threat Intelligence Management integradas.

---

## Tipos de Threat Intelligence

### 1. Strategic

- Audiencia: Ejecutivos
- Contenido: Tendencias, riesgos de negocio

### 2. Tactical

- Audiencia: SOC managers
- Contenido: TTPs, campañas

### 3. Operational

- Audiencia: Analysts
- Contenido: Detalles de ataques específicos

### 4. Technical

- Audiencia: SOC analysts
- Contenido: IoCs (IPs, dominios, hashes)

---

## Indicators of Compromise (IoCs)

**Network-based:** IPs, dominios, URLs  
**Host-based:** File hashes, nombres de archivos  
**Email-based:** Senders maliciosos, patrones phishing  
**Behavioral:** Patrones de ataque, C2 communications

---

## Threat Intelligence Lifecycle

1. **Planning** - Definir requisitos
2. **Collection** - Feeds comerciales/open-source
3. **Processing** - Normalización, deduplicación
4. **Analysis** - Correlación, priorización
5. **Dissemination** - Distribución a sistemas
6. **Feedback** - Evaluación y mejora

---

## TIM en XSOAR

### Funcionalidades

- Agregación de múltiples feeds (comerciales + open-source)
- Normalización automática de formatos
- Enriquecimiento de IoCs (VirusTotal, etc.)
- Scoring y priorización inteligente
- Distribución automática a Firewalls, SIEM, EDR
- Lifecycle management (expiración automática)

### Fuentes Comunes

**Comerciales:** Recorded Future, CrowdStrike, AutoFocus  
**Open Source:** AlienVault OTX, MISP, VirusTotal, Abuse.ch

---

## Workflows Clave

### 1. Process Indicators

```
Nuevo IoC → Validar → Normalizar → Enriquecer → 
Calcular score → Distribuir a sistemas
```

### 2. Enrich Alerts

```
Alerta con IP → Query TIM → Agregar contexto 
(APT, campañas) → Elevar prioridad
```

### 3. Retro-Hunt

```
Nuevo IoC crítico → Buscar en logs históricos → 
Buscar en endpoints → SI encontrado: Crear incidente
```

---

## External Dynamic Lists (EDL)

XSOAR genera listas de IoCs que firewalls Palo Alto consumen automáticamente para bloqueos dinámicos.

```
XSOAR TIM → Genera EDL → Firewall consulta cada X min → 
Actualiza bloqueos
```

---

## AutoFocus Integration

Threat Intelligence service de Palo Alto que enriquece IoCs con:

- Verdict (malicious/benign)
- Campañas asociadas
- Análisis behavioral
- Samples relacionados

---

## MISP Integration

Sharing bidireccional de threat intelligence con comunidades (ISACs, ISAOs).

---

## Best Practices

1. **Seleccionar fuentes relevantes** a tu industria
2. **Scoring y priorización** para manejar volumen
3. **Automatizar distribución** a sistemas
4. **Agregar contexto**, no solo IoCs
5. **Expiración automática** de indicadores obsoletos
6. **Medir efectividad** (detecciones, bloqueos, MTTD)

---

## Métricas Clave

- Detecciones generadas por TI
- Bloqueos preventivos
- Reducción de MTTD
- False positive rate
- ROI de feeds

---

## Desafíos

- **Overload** de información (miles de IoCs diarios)
- **Calidad variable** y falsos positivos
- **Relevancia** - filtrar lo que importa
- **Operacionalización** - usar efectivamente la inteligencia