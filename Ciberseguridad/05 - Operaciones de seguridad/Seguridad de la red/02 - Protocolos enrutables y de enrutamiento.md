## Diferencia Fundamental

**Protocolos Enrutables (Routed)**

- Transportan datos de usuario entre redes
- Ejemplos: IPv4, IPv6
- Contienen direccionamiento de Capa 3

**Protocolos de Enrutamiento (Routing)**

- Intercambian información para construir tablas de ruteo
- Ejemplos: RIP, OSPF, EIGRP, BGP
- No transportan datos de usuario

## Métricas de Enrutamiento

|Métrica|Descripción|Usado por|
|---|---|---|
|**Hop Count**|Número de routers hasta destino|RIP|
|**Bandwidth**|Capacidad del enlace|OSPF, EIGRP|
|**Delay**|Tiempo de tránsito|EIGRP|
|**Cost**|Valor calculado (100M/bandwidth)|OSPF|

**Regla**: Menor métrica = mejor ruta

## Administrative Distance (AD)

**Define confiabilidad de la fuente de ruta** (menor = más confiable):

|Fuente|AD|
|---|---|
|Conectada directamente|0|
|Estática|1|
|EIGRP|90|
|OSPF|110|
|RIP|120|

## Protocolos Principales

### RIP

- **Tipo**: Distance Vector
- **Métrica**: Solo hop count (máx 15)
- **Updates**: Cada 30 segundos
- **Ventaja**: Simple
- **Desventaja**: Convergencia lenta, no escala

### OSPF

- **Tipo**: Link State
- **Métrica**: Cost basado en bandwidth
- **Updates**: Solo cuando hay cambios
- **Ventaja**: Convergencia rápida, escala bien con áreas
- **Desventaja**: Más complejo, usa más CPU/memoria
- **Concepto clave**: Área 0 (backbone) obligatoria

### EIGRP

- **Tipo**: Híbrido/Advanced Distance Vector
- **Métrica**: Bandwidth + Delay
- **Ventaja**: Convergencia muy rápida con Feasible Successor
- **Desventaja**: Históricamente propietario Cisco
- **Concepto clave**: DUAL previene loops

### BGP

- **Tipo**: Path Vector
- **Uso**: Ruteo entre ISPs (Internet)
- **Decisión**: Basada en políticas y atributos, no solo métrica

## DNS (Domain Name System)

### Función Principal

Traduce nombres de dominio a direcciones IP

- **Ejemplo**: www.google.com → 142.250.185.46
- **Puerto**: 53 (UDP)

### Jerarquía

```
Root (.) → TLD (.com, .org) → Domain (google) → Subdomain (www)
```

### Registros Importantes

|Tipo|Función|
|---|---|
|**A**|Nombre → IPv4|
|**AAAA**|Nombre → IPv6|
|**CNAME**|Alias|
|**MX**|Servidor de correo|
|**NS**|Servidor DNS autoritativo|

### Proceso de Resolución

1. Cliente pregunta a resolver local
2. Resolver verifica caché
3. Si no está: consulta Root → TLD → Autoritativo
4. Responde al cliente y guarda en caché

### Seguridad DNS

- **DNSSEC**: Firma criptográfica (autentica, no cifra)
- **DoT/DoH**: DNS sobre TLS/HTTPS (cifra queries)
- **Amenazas**: Cache poisoning, DDoS, tunneling