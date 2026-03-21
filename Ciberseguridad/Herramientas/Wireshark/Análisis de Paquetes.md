## Estructura de un Paquete

Cada paquete capturado en Wireshark contiene información organizada por capas del modelo OSI.

---

## Información de Frame (Capa 1)

**Campos principales:**

- **Arrival Time:** Momento de captura
- **Frame Length:** Longitud total del frame
- **Capture Length:** Longitud capturada
- **Protocols in frame:** Protocolos presentes

---

## Información de Ethernet (Capa 2)

**Campos principales:**

- **Destination MAC:** Dirección MAC destino
- **Source MAC:** Dirección MAC origen
- **EtherType:** Tipo de protocolo de capa superior (0x0800 = IPv4, 0x86DD = IPv6)

---

## Información de IP (Capa 3)

### Campos del Header IPv4

**Identificación:**

- **Version:** IPv4 o IPv6
- **Header Length:** Longitud del header IP
- **Total Length:** Longitud total del paquete

**QoS y Fragmentación:**

- **Type of Service:** Calidad de servicio
- **Identification:** Identificador del paquete
- **Flags:** Control de fragmentación (DF, MF)
- **Fragment Offset:** Offset de fragmento

**Routing y Control:**

- **Time to Live (TTL):** Límite de saltos
- **Protocol:** Protocolo de capa superior (6=TCP, 17=UDP)
- **Header Checksum:** Verificación de integridad

**Direcciones:**

- **Source Address:** Dirección IP origen
- **Destination Address:** Dirección IP destino

---

## Información de TCP/UDP (Capa 4)

### TCP (Transmission Control Protocol)

**Puertos:**

- **Source Port** / **Destination Port**

**Control de Secuencia:**

- **Sequence Number:** Número de secuencia
- **Acknowledgment Number:** Número de confirmación

**Header y Flags:**

- **Header Length:** Tamaño del header TCP
- **Flags:** SYN, ACK, FIN, RST, PSH, URG

**Control de Flujo:**

- **Window Size:** Tamaño de ventana
- **Checksum:** Verificación de integridad
- **Urgent Pointer:** Puntero de urgencia

---

### UDP (User Datagram Protocol)

**Campos (header simple):**

- **Source Port** / **Destination Port**
- **Length:** Longitud total
- **Checksum:** Verificación opcional

---

## Análisis de Protocolos Específicos

### HTTP

**Filtros comunes:**

```bash
# Todas las peticiones HTTP
http.request

# Todas las respuestas HTTP
http.response

# Métodos específicos
http.request.method == "GET"
http.request.method == "POST"

# Códigos de respuesta
http.response.code == 200
http.response.code == 404

# Por host
http.host == "www.example.com"

# Por URI
http.request.uri contains "/admin"
http.request.uri matches ".*\\.php$"
```

**Campos importantes:**

- Request Method (GET, POST, PUT, DELETE)
- Request URI
- HTTP Version
- Status Code
- Headers (User-Agent, Cookie, etc.)

---

### DNS

**Filtros comunes:**

```bash
# Consultas DNS
dns.flags.response == 0

# Respuestas DNS
dns.flags.response == 1

# Tipos de registro
dns.qry.type == 1         # A record
dns.qry.type == 28        # AAAA record
dns.qry.type == 5         # CNAME

# Por nombre de dominio
dns.qry.name contains "google.com"
dns.qry.name == "www.example.com"
```

**Campos importantes:**

- Transaction ID
- Flags (query/response)
- Question (consulta)
- Answer (respuesta)
- Authority
- Additional

---

### TCP

**Filtros de flags:**

```bash
# SYN packets
tcp.flags.syn == 1

# FIN packets
tcp.flags.fin == 1

# RST packets
tcp.flags.reset == 1

# SYN-ACK
tcp.flags.syn == 1 and tcp.flags.ack == 1
```

**Filtros de análisis:**

```bash
# Retransmisiones
tcp.analysis.retransmission

# Window zero
tcp.window_size == 0

# Duplicados
tcp.analysis.duplicate_ack
```

---

## Filtros de Visualización Avanzados

### Filtros por Contenido

**Buscar texto en payload:**

```bash
# En cualquier protocolo TCP
tcp contains "password"

# En HTTP
http contains "login"

# En UDP
udp contains "secret"

# Expresiones regulares
http.request.uri matches ".*\\.php$"
```

---

### Filtros por Tiempo

**Rango de tiempo absoluto:**

```bash
frame.time >= "2023-01-01 00:00:00" and frame.time <= "2023-01-01 23:59:59"
```

**Tiempo relativo:**

```bash
# Primeros 10 segundos de captura
frame.time_relative >= 0 and frame.time_relative <= 10
```

---

### Filtros por Análisis TCP

**Problemas de red:**

```bash
# ACK duplicados
tcp.analysis.duplicate_ack

# Paquetes fuera de orden
tcp.analysis.out_of_order

# Ventana zero
tcp.analysis.zero_window

# Retransmisión rápida
tcp.analysis.fast_retransmission
```

---

### Filtros Combinados

**Ejemplos prácticos:**

```bash
# HTTP POST con credenciales
http.request.method == "POST" and http contains "password"

# DNS queries desde IP específica
dns.flags.response == 0 and ip.src == 192.168.1.100

# TCP SYN flood detection
tcp.flags.syn == 1 and tcp.flags.ack == 0

# Paquetes grandes
frame.len > 1500
```

---

## Coloreo de Paquetes

Wireshark utiliza colores para identificar diferentes tipos de tráfico.

---

### Colores Predeterminados

**Por protocolo:**

- **Verde claro:** TCP
- **Azul claro:** UDP
- **Amarillo:** HTTP
- **Púrpura:** ICMP
- **Gris:** ARP

**Por estado:**

- **Negro:** Paquetes con errores
- **Rojo:** Problemas (retransmisiones, RST)

---

### Personalizar Colores

**Pasos:**

1. Ir a **View → Coloring Rules**
2. Click en **New** para crear nueva regla
3. Ingresar **nombre** de la regla
4. Definir **filtro** (ej: `http.request.method == "POST"`)
5. Seleccionar **colores** (foreground y background)
6. Click **OK**

**Ejemplos de reglas personalizadas:**

- Resaltar tráfico SSH: `tcp.port == 22`
- Resaltar IPs sospechosas: `ip.addr == 10.0.0.100`
- Resaltar errores HTTP: `http.response.code >= 400`

---

## Estadísticas de Captura

### Statistics Menu

**Protocol Hierarchy:**

```
Statistics → Protocol Hierarchy
```

- Muestra distribución de protocolos
- Porcentaje de cada protocolo

**Conversations:**

```
Statistics → Conversations
```

- Conversaciones Ethernet, IP, TCP, UDP
- Volumen de datos por conversación

**Endpoints:**

```
Statistics → Endpoints
```

- Lista de endpoints por protocolo
- Tráfico de cada endpoint

**I/O Graphs:**

```
Statistics → I/O Graphs
```

- Gráficos de tráfico en el tiempo
- Filtros personalizados

---

## Exportación de Datos

### Exportar Objetos

**HTTP Objects:**

```
File → Export Objects → HTTP
```

- Exportar archivos descargados vía HTTP

**Otros protocolos:**

- SMB
- TFTP
- DICOM

---

### Exportar Paquetes

**Como archivo de captura:**

```
File → Export Specified Packets
```

**Como texto:**

```
File → Export Packet Dissections
```

---

## Mejores Prácticas

### Captura Eficiente

- Usar **filtros de captura** para reducir tamaño
- Capturar solo lo **necesario**
- **Rotar archivos** en capturas largas
- Usar **ring buffer** para capturas continuas

---

### Análisis

- Comenzar con **Statistics** para overview
- Usar **Follow Stream** para ver conversaciones completas
- Aplicar **filtros de visualización** progresivamente
- **Colorear** tráfico importante
- **Documentar** hallazgos con comentarios de paquetes

---

## Consideraciones

- Capturar tráfico puede contener **información sensible**
- **Respetar** privacidad y leyes locales
- Usar solo en **redes autorizadas**
- **Cifrar** archivos de captura si contienen datos sensibles
- **Eliminar** capturas después de análisis

---