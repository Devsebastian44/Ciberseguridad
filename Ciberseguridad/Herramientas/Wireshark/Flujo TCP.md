## ¿Qué es el Seguimiento de Flujo TCP?

El seguimiento de flujo TCP permite reconstruir una **conversación completa** entre dos hosts, mostrando todos los datos intercambiados en orden cronológico.

**Utilidad:** Ver toda la comunicación como una conversación continua en lugar de paquetes individuales.

---

## Cómo Seguir un Flujo TCP

### Método 1: Menú Contextual

**Pasos:**

1. Seleccionar cualquier paquete del flujo TCP
2. Clic derecho
3. **Follow → TCP Stream**

---

### Método 2: Menú Principal

**Pasos:**

1. Seleccionar un paquete TCP
2. Ir a **Analyze → Follow → TCP Stream**

---

### Método 3: Atajo de Teclado

**Atajos:**

- **Ctrl+Alt+Shift+T** (Windows/Linux)
- **Cmd+Option+Shift+T** (macOS)

---

## Ventana de Seguimiento TCP

### Opciones de Visualización

**Formatos disponibles:**

**ASCII:**

- Texto legible
- Ideal para HTTP, SMTP, FTP, Telnet

**EBCDIC:**

- Codificación de mainframes IBM
- Poco común actualmente

**Hex Dump:**

- Datos en hexadecimal + ASCII
- Útil para análisis técnico

**C Arrays:**

- Datos como arrays de C
- Útil para desarrollo/debugging

**Raw:**

- Datos binarios sin procesar
- **Necesario para extracción de archivos**

---

### Controles de Dirección

**Opciones de filtrado:**

- **Entire conversation** - Toda la comunicación
- **Client → Server** - Solo datos enviados por el cliente
- **Server → Client** - Solo datos enviados por el servidor

**Colores:**

- **Rojo** - Datos del cliente
- **Azul** - Datos del servidor

---

### Opciones Adicionales

**Filtros:**

- **Find** - Buscar texto en la conversación
- **Save As** - Guardar conversación
- **Print** - Imprimir conversación

**Información visible:**

- Número de stream
- Filtro aplicado automáticamente

---

## Análisis de Conversaciones Específicas

### Sesión HTTP

**Ejemplo de flujo:**

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0...
Cookie: session=abc123

HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<html>...</html>
```

**Información visible:**

- Headers completos
- Contenido web (HTML, CSS, JS)
- Cookies y sesiones
- Parámetros POST con datos de formularios

---

### Sesión FTP

**Ejemplo de flujo:**

```ftp
USER anonymous
331 Password required
PASS guest@example.com
230 Login successful
PWD
257 "/" is current directory
LIST
150 Opening data connection
226 Transfer complete
```

**Información visible:**

- **Credenciales** en texto plano
- Comandos FTP
- Listados de directorios
- Control de transferencia de archivos

---

### Sesión SMTP

**Ejemplo de flujo:**

```smtp
EHLO client.example.com
250-PIPELINING
250-SIZE 10240000
250 STARTTLS
MAIL FROM:<sender@example.com>
250 OK
RCPT TO:<receiver@example.com>
250 OK
DATA
354 End data with <CR><LF>.<CR><LF>
Subject: Test Email
...
.
250 OK: queued
```

**Información visible:**

- Comandos de autenticación
- Capacidades del servidor
- Contenido del email (si no usa STARTTLS)

---

### Sesión SSH

**Limitación:**

```
SSH-2.0-OpenSSH_8.2
SSH-2.0-OpenSSH_7.9
[Datos cifrados]
```

**Nota:** Solo se puede ver el handshake inicial, el resto está **cifrado** y no es legible.

---

## Seguimiento de Flujos UDP

Aunque UDP **no es orientado a conexión**, Wireshark puede seguir flujos UDP.

**Acceso:**

- Clic derecho → **Follow → UDP Stream**

---

### Casos de Uso UDP

**DNS:**

```bash
# Query
example.com. IN A

# Response
example.com. 300 IN A 93.184.216.34
```

**Streaming de video/audio:**

- RTP (Real-time Transport Protocol)
- RTSP

**Juegos en línea:**

- Comunicación de estado del juego
- Sincronización de jugadores

**Protocolos IoT:**

- MQTT
- CoAP

---

## Análisis Avanzado de Flujos

### Estadísticas de Flujo

**Acceso:**

```
Statistics → Conversations
```

**Información por flujo:**

- **Address A/B** - Direcciones IP
- **Port A/B** - Puertos origen/destino
- **Packets** - Cantidad de paquetes
- **Bytes** - Volumen de datos
- **Duration** - Duración de la conversación

**Pestañas disponibles:**

- Ethernet
- IPv4 / IPv6
- TCP / UDP

---

### Gráficos de Flujo

**Acceso:**

```
Statistics → Flow Graph
```

**Visualización:**

- Secuencia temporal de paquetes
- Direcciones y puertos
- Tiempos de respuesta
- Handshakes TCP
- Identificación de problemas

**Filtros:**

- Aplicar filtros de visualización
- Limitar a flujos específicos

---

## Filtros Relacionados con Flujos

### Filtrar por Flujo Específico

**Por número de stream:**

```bash
# Stream TCP número 0
tcp.stream eq 0

# Stream UDP número 0
udp.stream eq 0

# Stream específico con contexto
tcp.stream eq 5 and http
```

**Por endpoints:**

```bash
# Comunicación entre dos IPs específicas
ip.addr == 192.168.1.100 and ip.addr == 192.168.1.200 and tcp.port == 80

# Entre IP y subred
ip.src == 192.168.1.100 and ip.dst == 10.0.0.0/8
```

---

### Análisis de Múltiples Flujos

**Varios streams:**

```bash
# Dos streams específicos
tcp.stream eq 0 or tcp.stream eq 1

# Rangos de streams
tcp.stream >= 0 and tcp.stream <= 5

# Streams con condición temporal
frame.time >= "2023-01-01 10:00:00" and tcp.stream eq 0
```

**Problemas de red:**

```bash
# Retransmisiones en cualquier stream
tcp.analysis.retransmission

# ACKs duplicados
tcp.analysis.duplicate_ack

# Todos los problemas TCP
tcp.analysis.flags
```

---

## Exportación de Datos de Flujo

### Guardar Conversación Completa

**Desde Follow Stream:**

1. Abrir **Follow TCP/UDP Stream**
2. Seleccionar formato apropiado:
    - **ASCII** para texto
    - **Raw** para archivos binarios
3. Click en **Save As**
4. Elegir ubicación y nombre

---

### Exportar Múltiples Flujos

**Método 1 - Paquetes específicos:**

1. Aplicar filtro (ej: `tcp.stream eq 0`)
2. Ir a **File → Export Specified Packets**
3. Seleccionar "Displayed" packets
4. Guardar archivo PCAP

**Método 2 - Todos los streams con filtro:**

```bash
# Exportar solo HTTP
http
```

1. **File → Export Specified Packets**
2. Guardar como nuevo PCAP

---

## Casos de Uso Prácticos

### Análisis Forense

#### Reconstrucción de Actividad Web

**Objetivo:** Ver qué sitios visitó un usuario

**Pasos:**

```bash
# 1. Filtrar actividad HTTP del usuario
ip.src == 192.168.1.100 and http

# 2. Identificar streams
Statistics → Conversations → TCP

# 3. Seguir cada flujo relevante
tcp.stream eq 0, tcp.stream eq 1, etc.
```

---

#### Análisis de Transferencia de Archivos

**Objetivo:** Extraer archivos transferidos por FTP

**Pasos:**

```bash
# 1. Identificar transferencias FTP-DATA
ftp-data

# 2. Seguir flujo del archivo
tcp.stream eq 5

# 3. Guardar en formato Raw
```

---

### Análisis de Seguridad

#### Detección de Exfiltración de Datos

**Objetivo:** Identificar salida no autorizada de datos

**Pasos:**

```bash
# 1. Buscar conexiones salientes sospechosas
tcp.flags.syn == 1 and !(ip.dst == 192.168.1.0/24)

# 2. Identificar volumen alto de datos
Statistics → Conversations (ordenar por Bytes)

# 3. Analizar contenido de conexiones
tcp.stream eq 10
```

---

#### Análisis de Comunicaciones Maliciosas

**Objetivo:** Detectar C&C (Command & Control)

**Pasos:**

```bash
# 1. Buscar tráfico en puertos no estándar
tcp.port > 1024 and tcp.port < 49152

# 2. Identificar comunicación periódica (beaconing)
Statistics → Flow Graph

# 3. Examinar contenido
tcp.stream eq 15
```

---

### Troubleshooting de Red

#### Identificar Problemas de Conectividad

**Handshakes fallidos:**

```bash
# SYN sin respuesta
tcp.flags.syn == 1 and tcp.flags.ack == 0

# RST después de SYN
tcp.flags.reset == 1
```

**Análisis de latencia:**

```bash
# RTT alto
tcp.analysis.ack_rtt > 1.0

# Timeouts
tcp.analysis.retransmission
```

---

#### Diagnóstico de Rendimiento

**Retransmisiones:**

```bash
# Identificar retransmisiones TCP
tcp.analysis.retransmission

# Contar retransmisiones por stream
Statistics → TCP Stream Graphs → Round Trip Time
```

**Window zero (problemas de buffer):**

```bash
# Ventana TCP en cero
tcp.window_size == 0

# Analizar flujo específico
tcp.stream eq 3
```

---

## Mejores Prácticas

### Durante el Análisis

**Flujo de trabajo:**

1. **Filtrar** por protocolo o IP relevante
2. Revisar **Statistics → Conversations** para overview
3. **Seguir streams** individuales para detalle
4. **Documentar** hallazgos importantes
5. **Exportar** evidencias relevantes

---

### Seguridad

**Protección de datos:**

- **No** compartir capturas con datos sensibles
- **Anonimizar** IPs si es necesario
- **Cifrar** archivos de captura con información crítica
- **Eliminar** después de análisis

---

## Limitaciones

**Protocolos cifrados:**

- **HTTPS** - Contenido no visible (solo metadata)
- **SSH** - Solo handshake visible
- **SFTP** - Completamente cifrado
- **VPN** - Túnel cifrado

**Solución:** Necesario claves privadas para descifrar (TLS/SSL)

---

## Consideraciones

- Follow Stream es **esencial** para análisis forense
- **Siempre** verificar integridad de datos extraídos
- **Documentar** número de stream en reportes
- Usar **filtros** para reducir ruido
- Follow Stream aplica **filtro automático** (`tcp.stream eq X`)

---