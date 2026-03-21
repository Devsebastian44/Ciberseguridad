## Pasos para Capturar Tráfico

### Paso 1: Preparación

**Acciones previas:**

1. Ejecutar Wireshark como **administrador** (Windows) o con permisos apropiados (Linux/macOS)
2. Identificar la **interfaz de red** correcta
3. Cerrar aplicaciones innecesarias para **reducir ruido**

**Verificar interfaz activa:**

```bash
# Linux
ip a
ifconfig

# Windows
ipconfig
```

---

### Paso 2: Configuración de Captura

**Seleccionar interfaz:**

```
Capture → Interfaces → Seleccionar interfaz activa
```

**Opciones de configuración:**

**Promiscuous mode:**

- Activar si se desea capturar **todo el tráfico** de la red
- Desactivar para capturar solo tráfico propio

**Buffer size:**

- Ajustar según memoria disponible
- Mayor buffer = menos pérdida de paquetes

**File options:**

- Configurar guardado automático
- Ring buffer para capturas continuas
- Múltiples archivos con límite de tamaño

---

### Paso 3: Aplicar Filtros de Captura (Opcional)

Los filtros de captura se aplican **durante la captura** y utilizan sintaxis **BPF (Berkeley Packet Filter)**.

**Ventaja:** Reducen el tamaño del archivo de captura

---

#### Filtros BPF Básicos

**Por puerto:**

```bash
# Solo tráfico HTTP
port 80

# HTTPS
port 443

# Múltiples puertos
port 80 or port 443 or port 22
```

**Por host:**

```bash
# Tráfico de/hacia una IP específica
host 192.168.1.100

# Tráfico desde una IP
src host 192.168.1.100

# Tráfico hacia una IP
dst host 192.168.1.100
```

**Por protocolo:**

```bash
# Solo TCP
tcp

# Solo UDP
udp

# Solo ICMP
icmp
```

**Por red:**

```bash
# Subred específica
net 192.168.1.0/24

# Combinado con protocolo
net 192.168.1.0/24 and tcp
```

---

#### Filtros BPF Combinados

**Ejemplos avanzados:**

```bash
# HTTP y HTTPS
port 80 or port 443

# TCP hacia puerto 80 desde subred específica
tcp and port 80 and src net 192.168.1.0/24

# Todo excepto SSH
not port 22

# Solo paquetes grandes
greater 1000
```

---

### Paso 4: Iniciar Captura

**Métodos:**

1. Hacer clic en el botón **Start** (aleta de tiburón azul)
2. Presionar `Ctrl+E`
3. Doble clic en la interfaz

**Durante la captura:**

- Generar tráfico de red (navegar, enviar emails, etc.)
- Observar paquetes en tiempo real
- Monitorear contador de paquetes

---

### Paso 5: Detener Captura

**Métodos:**

1. Hacer clic en el botón **Stop** (cuadrado rojo)
2. Presionar `Ctrl+E`

**Después de detener:**

- Guardar la captura: `File → Save As`
- Formato recomendado: `.pcapng` (incluye más información)

---

## Filtros de Visualización

Los filtros de visualización se aplican **después de la captura** y permiten mostrar solo paquetes específicos.

**Diferencia clave:** No reducen el archivo, solo la visualización

---

### Filtros Básicos

**Por protocolo:**

```bash
http              # Tráfico HTTP
tls               # Tráfico HTTPS (TLS)
dns               # Tráfico DNS
tcp               # Tráfico TCP
udp               # Tráfico UDP
icmp              # Paquetes ICMP
arp               # Protocolo ARP
ssh               # Tráfico SSH
```

**Por puerto:**

```bash
tcp.port == 80    # Puerto TCP 80
udp.port == 53    # Puerto UDP 53
tcp.port == 443   # HTTPS
```

---

### Filtros por Dirección IP

**IP específica:**

```bash
# Tráfico de/hacia IP
ip.addr == 192.168.1.100

# Solo tráfico desde IP (origen)
ip.src == 192.168.1.100

# Solo tráfico hacia IP (destino)
ip.dst == 192.168.1.100
```

**Subredes:**

```bash
# Tráfico de una subred
ip.addr == 192.168.1.0/24

# Tráfico entre dos subredes
ip.src == 192.168.1.0/24 and ip.dst == 10.0.0.0/8
```

**Excluir tráfico:**

```bash
# Excluir una IP
!(ip.addr == 192.168.1.100)

# Excluir subred
!(ip.addr == 192.168.1.0/24)
```

---

### Filtros por Puerto

**Puerto específico:**

```bash
# Puerto TCP o UDP
tcp.port == 80 or udp.port == 80

# Puerto de origen
tcp.srcport == 80
udp.srcport == 53

# Puerto de destino
tcp.dstport == 443
udp.dstport == 67
```

**Rango de puertos:**

```bash
# Rango TCP
tcp.port >= 1000 and tcp.port <= 2000

# Puertos altos (no privilegiados)
tcp.port > 1024
```

---

### Filtros por Flags TCP

**Flags específicos:**

```bash
# Paquetes SYN
tcp.flags.syn == 1

# SYN-ACK
tcp.flags.syn == 1 and tcp.flags.ack == 1

# FIN
tcp.flags.fin == 1

# RST
tcp.flags.reset == 1

# PSH
tcp.flags.push == 1
```

---

### Filtros de Contenido

**Buscar en payload:**

```bash
# Buscar texto específico
tcp contains "password"
http contains "login"
udp contains "secret"

# Case-sensitive
frame contains "Admin"
```

**Expresiones regulares:**

```bash
# Coincide con patrón
http.request.uri matches ".*\\.php$"
http.host matches ".*\\.com$"
```

---

### Filtros por Tamaño

**Longitud de paquetes:**

```bash
# Paquetes mayores a 1000 bytes
frame.len > 1000

# Paquetes menores a 100 bytes
frame.len < 100

# Paquetes de tamaño exacto
frame.len == 1500
```

---

### Filtros Avanzados

**Combinaciones complejas:**

```bash
# HTTP desde IP específica
http and ip.src == 192.168.1.100

# TCP SYN hacia puerto 80
tcp.flags.syn == 1 and tcp.dstport == 80

# DNS queries (no responses)
dns and dns.flags.response == 0

# Retransmisiones TCP
tcp.analysis.retransmission

# HTTP POST requests
http.request.method == "POST"

# HTTPS con SNI específico
tls.handshake.extensions_server_name == "www.example.com"
```

---

## Operadores de Filtros

### Operadores de Comparación

**Símbolos:**

- `==` : Igual a
- `!=` : Diferente de
- `>` : Mayor que
- `<` : Menor que
- `>=` : Mayor o igual que
- `<=` : Menor o igual que

**Ejemplos:**

```bash
tcp.port == 80
frame.len > 1000
tcp.window_size != 0
```

---

### Operadores Lógicos

**Operadores:**

- `and` o `&&` : Y lógico
- `or` o `||` : O lógico
- `not` o `!` : Negación

**Ejemplos:**

```bash
# AND
tcp and port 80

# OR
tcp.port == 80 or tcp.port == 443

# NOT
not tcp.port == 22
!(ip.addr == 192.168.1.1)
```

---

### Operadores de Contenido

**Operadores:**

- `contains` : Contiene cadena
- `matches` : Coincide con regex

**Ejemplos:**

```bash
# Contains
http contains "admin"
frame contains "password"

# Matches
http.host matches ".*\\.com$"
dns.qry.name matches "^www\\."
```

---

## Guardado de Filtros

### Crear Filtro Favorito

**Pasos:**

1. Escribir filtro en barra de filtros
2. Click en el **+** a la derecha
3. Asignar **nombre** descriptivo
4. Click **OK**

**Acceso rápido:**

- Menú desplegable junto a la barra de filtros
- Click en el nombre del filtro

---

### Botones de Filtro Rápido

**Crear botones:**

1. Click derecho en barra de filtros
2. **Display Filter Expression**
3. Seleccionar filtro
4. Asignar a botón

---

## Mejores Prácticas

### Durante la Captura

**Captura eficiente:**

- Usar **filtros de captura** para reducir datos
- Capturar solo el **tráfico necesario**
- **Rotar archivos** en capturas largas
- Usar **ring buffer** para capturas continuas

---

### Filtros de Visualización

**Análisis efectivo:**

- Comenzar con filtros **simples**
- Ir **refinando** progresivamente
- **Guardar** filtros útiles
- **Documentar** filtros complejos

---

### Seguridad

**Protección de datos:**

- **No** capturar en redes sin autorización
- **Cifrar** archivos de captura sensibles
- **Eliminar** capturas después de análisis
- Respetar **privacidad** y leyes locales

---

## Comandos Útiles

### Captura desde Línea de Comandos

**tshark (CLI de Wireshark):**

```bash
# Captura básica
tshark -i eth0 -w captura.pcap

# Con filtro de captura
tshark -i eth0 -f "port 80" -w http.pcap

# Con filtro de visualización
tshark -i eth0 -Y "http" -w http_display.pcap

# Captura por tiempo
tshark -i eth0 -a duration:60 -w 1min.pcap

# Captura con ring buffer
tshark -i eth0 -b filesize:100000 -b files:10 -w capture.pcap
```

---

## Consideraciones

- **Filtros de captura** (BPF) se aplican durante la captura
- **Filtros de visualización** se aplican después
- Sintaxis **diferente** entre ambos tipos
- **Privilegios** de administrador necesarios para captura
- **Impacto** en rendimiento con capturas grandes
- Usar **ring buffer** para capturas continuas

---