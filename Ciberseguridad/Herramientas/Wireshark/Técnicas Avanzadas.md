## Análisis de Patrones de Tráfico

### Identificación de Comportamiento Anómalo

#### Volumen de Tráfico Inusual

**Detección de paquetes grandes:**

```bash
# Paquetes mayores a 1500 bytes
frame.len > 1500

# Paquetes muy grandes (posible exfiltración)
frame.len > 8000
```

**Tráfico TCP excesivo:**

```bash
# Bytes en vuelo anormalmente altos
tcp.analysis.bytes_in_flight > 65535

# Ventana TCP anormalmente grande
tcp.window_size > 100000
```

---

#### Patrones de Temporización

**Comunicación muy rápida (posible automatización):**

```bash
# Delta de tiempo menor a 1ms
tcp.time_delta < 0.001

# Comunicación en ráfaga
frame.time_delta < 0.0001
```

**Beaconing (comunicación periódica C&C):**

```bash
# Intervalos regulares (~60 segundos)
frame.time_delta > 60 and frame.time_delta < 65

# Beaconing cada 5 minutos
frame.time_delta > 295 and frame.time_delta < 305
```

---

#### Conexiones Sospechosas

**Múltiples conexiones desde un solo host:**

```bash
# Muchas conexiones SYN desde una IP
tcp.flags.syn == 1 and ip.src == 192.168.1.100
```

**Escaneo de puertos:**

```bash
# Muchos SYN sin respuesta
tcp.flags.syn == 1 and !tcp.flags.ack

# SYN hacia múltiples puertos
tcp.flags.syn == 1 and ip.dst == 192.168.1.1
```

---

## Correlación de Eventos

### Análisis Temporal

**Rastrear flujo de ataque:**

```bash
# 1. Query DNS sospechosa
dns.qry.name == "malicious.com"

# 2. Conexión HTTP subsecuente
http.host == "malicious.com"

# 3. Tráfico posterior desde misma IP
ip.dst == [IP_del_servidor_malicioso]
```

---

### Análisis de Actividad por Usuario/Host

**Toda actividad de un host:**

```bash
# Todo tráfico web de un usuario
ip.src == 192.168.1.100 and (http or https or ftp)

# Actividad en rango de tiempo
ip.src == 192.168.1.100 and frame.time >= "2024-01-01 10:00:00"
```

---

### Análisis de Cadenas de Infección

**Metodología:**

**1. Identificar punto de entrada inicial:**

- Email con adjunto malicioso
- Descarga desde sitio comprometido
- Exploit de vulnerabilidad

**2. Seguir comunicaciones subsecuentes:**

- Conexiones a C&C
- Descarga de payloads adicionales
- Exfiltración de datos

**3. Mapear propagación lateral:**

- SMB/RDP a otros hosts internos
- Pass-the-Hash
- Movimiento entre subredes

**4. Documentar Indicadores de Compromiso (IoCs):**

- IPs maliciosas
- Dominios
- Hashes de archivos
- User-Agents sospechosos

---

## Automatización con Scripts

### Uso de tshark (CLI)

#### Extracción de Información Específica

**Extraer hosts HTTP:**

```bash
# Listar todos los hosts HTTP visitados
tshark -r capture.pcap -Y "http.request" -T fields -e http.host -e http.request.uri

# Únicos hosts HTTP
tshark -r capture.pcap -Y "http.request" -T fields -e http.host | sort | uniq
```

**Extraer IPs origen y destino:**

```bash
# Todas las conversaciones IP
tshark -r capture.pcap -T fields -e ip.src -e ip.dst | sort | uniq

# Con puertos
tshark -r capture.pcap -T fields -e ip.src -e tcp.srcport -e ip.dst -e tcp.dstport
```

---

#### Exportación de Objetos

**Extraer archivos HTTP:**

```bash
# Exportar todos los objetos HTTP
tshark -r capture.pcap --export-objects http,./extracted_files/

# Exportar objetos SMB
tshark -r capture.pcap --export-objects smb,./smb_files/
```

---

#### Estadísticas y Análisis

**Jerarquía de protocolos:**

```bash
# Ver distribución de protocolos
tshark -r capture.pcap -q -z io,phs
```

**Conversaciones:**

```bash
# Top 10 conversaciones TCP
tshark -r capture.pcap -q -z conv,tcp

# Top endpoints IP
tshark -r capture.pcap -q -z endpoints,ip
```

**Estadísticas HTTP:**

```bash
# Códigos de respuesta HTTP
tshark -r capture.pcap -q -z http,stat

# Métodos HTTP usados
tshark -r capture.pcap -q -z http_req,tree
```

---

#### Filtrado Avanzado

**Guardar paquetes filtrados:**

```bash
# Solo paquetes HTTP
tshark -r capture.pcap -Y "http" -w http_only.pcap

# Solo tráfico de IP específica
tshark -r capture.pcap -Y "ip.addr == 192.168.1.100" -w host_traffic.pcap
```

**Análisis en tiempo real:**

```bash
# Captura en vivo con filtro
tshark -i eth0 -Y "dns"

# Mostrar solo campos específicos
tshark -i eth0 -Y "http.request" -T fields -e http.host -e http.request.uri
```

---

### Scripts de Automatización

#### Script Bash - Análisis de DNS

**Ejemplo:**

```bash
#!/bin/bash

# Extraer queries DNS únicas
tshark -r capture.pcap -Y "dns.flags.response == 0" \
  -T fields -e dns.qry.name | sort | uniq > dns_queries.txt

# Contar queries por dominio
echo "Top 10 dominios consultados:"
cat dns_queries.txt | rev | cut -d'.' -f1-2 | rev | sort | uniq -c | sort -rn | head -10
```

---

#### Script Bash - Detección de Exfiltración

**Ejemplo:**

```bash
#!/bin/bash

# Buscar conexiones con volumen alto de salida
echo "Hosts con más de 10MB de tráfico saliente:"
tshark -r capture.pcap -q -z conv,tcp | \
  awk '$1 !~ /^[A-Z]/ && $8 > 10000000 {print $1, $8}' | \
  sort -k2 -rn
```

---

#### Script Python - Análisis Avanzado

**Ejemplo con pyshark:**

```python
import pyshark

# Abrir captura
cap = pyshark.FileCapture('capture.pcap', display_filter='http')

# Analizar paquetes HTTP
http_hosts = {}
for packet in cap:
    try:
        host = packet.http.host
        http_hosts[host] = http_hosts.get(host, 0) + 1
    except AttributeError:
        pass

# Mostrar resultados
for host, count in sorted(http_hosts.items(), key=lambda x: x[1], reverse=True):
    print(f"{host}: {count} requests")
```

---

## Análisis de Malware

### Identificación de Comunicaciones C&C

**Patrones comunes:**

```bash
# User-Agents sospechosos
http.user_agent contains "Bot" or http.user_agent contains "Scanner"

# Conexiones a IPs en lugar de dominios
http.host matches "^[0-9]+\\.[0-9]+\\.[0-9]+\\.[0-9]+$"

# Puertos no estándar para HTTP
tcp.port != 80 and tcp.port != 443 and http
```

---

### Análisis de Payloads

**Buscar strings sospechosos:**

```bash
# Buscar comandos shell
frame contains "cmd.exe" or frame contains "/bin/sh"

# Buscar scripts PowerShell
frame contains "powershell" or frame contains "Invoke-"

# Buscar herramientas de hacking
frame contains "mimikatz" or frame contains "metasploit"
```

---

## Detección de Ataques

### SQL Injection

**Patrones de ataque:**

```bash
# Buscar SQL en URLs
http.request.uri contains "union" or http.request.uri contains "select"

# OR 1=1
http.request.uri contains "or 1=1"

# Comentarios SQL
http.request.uri contains "--" or http.request.uri contains "/*"
```

---

### XSS (Cross-Site Scripting)

**Patrones de ataque:**

```bash
# Tags script
http.request.uri contains "<script"

# Eventos JavaScript
http.request.uri contains "onerror=" or http.request.uri contains "onload="

# JavaScript codificado
http.request.uri contains "javascript:"
```

---

### Fuerza Bruta

**Detección:**

```bash
# Múltiples intentos de login
http.request.method == "POST" and http.request.uri contains "login"

# Múltiples conexiones SSH fallidas
tcp.port == 22 and tcp.flags.reset == 1

# Múltiples códigos 401/403
http.response.code == 401 or http.response.code == 403
```

---

## Análisis de Rendimiento

### Identificar Cuellos de Botella

**Latencia alta:**

```bash
# RTT alto en TCP
tcp.analysis.ack_rtt > 0.5

# Time to first byte alto
http.time > 2
```

**Retransmisiones:**

```bash
# Contar retransmisiones
tcp.analysis.retransmission

# Por host origen
ip.src == 192.168.1.100 and tcp.analysis.retransmission
```

---

### Análisis de Bandwidth

**Tráfico por protocolo:**

```bash
# Usar Statistics → Protocol Hierarchy

# O con tshark
tshark -r capture.pcap -q -z io,phs
```

---

## Mejores Prácticas

### Análisis Forense

**Documentación:**

- Registrar **timestamp** de eventos clave
- **Capturar pantallas** de evidencias
- Mantener **cadena de custodia**
- **Hash** de archivos de captura

**Metodología:**

1. **Overview** general (Statistics)
2. **Filtrado** progresivo
3. **Correlación** de eventos
4. **Documentación** de hallazgos
5. **Validación** de hipótesis

---

### Automatización

**Scripts reusables:**

- Crear **biblioteca** de scripts comunes
- **Parametrizar** filtros y opciones
- **Documentar** uso y ejemplos
- **Versionar** scripts (Git)

---

## Consideraciones

- Análisis avanzado requiere **conocimiento profundo** de protocolos
- **Combinar** múltiples técnicas para mejor efectividad
- **Automatizar** tareas repetitivas con scripts
- Mantener **actualizado** conocimiento de nuevas amenazas
- **Practicar** regularmente con capturas reales

---