## Ventana Principal de Wireshark

Cuando abres Wireshark, la interfaz se divide en varias secciones principales.

---

## Componentes de la Interfaz

### 1. Barra de Menú

**Menús principales:**

**File:**

- Abrir capturas existentes
- Guardar capturas
- Exportar datos
- Cerrar archivos

**Edit:**

- Copiar información
- Buscar paquetes
- Configurar preferencias

**View:**

- Opciones de visualización
- Configurar columnas
- Reglas de coloreo

**Go:**

- Navegación entre paquetes
- Ir a paquete específico

**Capture:**

- Iniciar/detener captura
- Configurar opciones de captura
- Gestionar interfaces

**Analyze:**

- Herramientas de análisis
- Follow Stream
- Expert Information

**Statistics:**

- Estadísticas del tráfico
- Gráficos y reportes
- Protocol Hierarchy

**Tools:**

- Herramientas adicionales
- Firewall ACL Rules
- Lua scripts

**Help:**

- Ayuda y documentación
- About Wireshark

---

### 2. Barra de Herramientas

**Botones de captura:**

- **Start** (aleta de tiburón azul) - Iniciar captura
- **Stop** (cuadrado rojo) - Detener captura
- **Restart** - Reiniciar captura

**Botones de navegación:**

- Primer paquete
- Anterior paquete
- Siguiente paquete
- Último paquete

**Botones de visualización:**

- Zoom in/out
- Auto scroll
- Colorear paquetes

**Otros:**

- Aplicar filtros
- Recargar archivo

---

### 3. Barra de Filtros

**Componentes:**

- **Campo de filtro** - Escribir expresiones de filtro
- **Botón Apply** - Aplicar filtro escrito
- **Botón Clear** - Limpiar filtro actual
- **Menú desplegable** - Historial de filtros recientes
- **Marcador** (+) - Guardar filtro como favorito

**Indicadores de color:**

- **Verde** - Filtro válido
- **Rojo** - Filtro inválido (error de sintaxis)
- **Amarillo** - Filtro válido pero con advertencia

---

### 4. Panel de Lista de Paquetes

Muestra **todos los paquetes capturados** en forma de tabla.

**Columnas por defecto:**

**No.:**

- Número secuencial del paquete

**Time:**

- Marca de tiempo (configurable: absoluta, relativa, delta)

**Source:**

- Dirección IP origen

**Destination:**

- Dirección IP destino

**Protocol:**

- Protocolo utilizado (TCP, UDP, HTTP, etc.)

**Length:**

- Longitud del paquete en bytes

**Info:**

- Información resumida del paquete

**Personalización:**

- Clic derecho → **Column Preferences**
- Agregar, eliminar, reordenar columnas
- Crear columnas personalizadas

---

### 5. Panel de Detalles del Paquete

Muestra la **estructura jerárquica** del paquete seleccionado.

**Organización por capas:**

- **Frame** - Información del frame
- **Ethernet II** - Capa 2
- **Internet Protocol** - Capa 3 (IP)
- **Transmission Control Protocol** - Capa 4 (TCP/UDP)
- **Application Data** - Capa 7 (HTTP, DNS, etc.)

**Características:**

- **Expandible** por secciones (click en triángulo)
- Sincronizado con panel de bytes
- Clic derecho para opciones adicionales

---

### 6. Panel de Bytes

Muestra el **contenido hexadecimal y ASCII** del paquete.

**Vista:**

- Columna izquierda: **Offset** (desplazamiento)
- Columnas centrales: **Hexadecimal**
- Columna derecha: **ASCII** (caracteres legibles)

**Características:**

- **Sincronizado** con selección en panel de detalles
- Resaltado de bytes seleccionados
- Permite análisis a nivel de bits

---

## Tipos de Paquetes que se Pueden Capturar

### Protocolos de Capa 2 (Enlace de Datos)

**Estándares comunes:**

- **Ethernet** (802.3)
- **Wi-Fi** (802.11 a/b/g/n/ac/ax)
- **PPP** (Point-to-Point Protocol)
- **VLAN** (802.1Q)
- **ARP** (Address Resolution Protocol)

---

### Protocolos de Capa 3 (Red)

**Protocolos de enrutamiento:**

- **IPv4** / **IPv6**
- **ICMP** (ping, traceroute)
- **IGMP** (multicast)

**Protocolos de routing:**

- **OSPF** (Open Shortest Path First)
- **BGP** (Border Gateway Protocol)
- **RIP** (Routing Information Protocol)

---

### Protocolos de Capa 4 (Transporte)

**Protocolos principales:**

- **TCP** (Transmission Control Protocol)
- **UDP** (User Datagram Protocol)
- **SCTP** (Stream Control Transmission Protocol)

---

### Protocolos de Capa 7 (Aplicación)

**Web:**

- **HTTP** / **HTTPS**
- **WebSocket**

**Email:**

- **SMTP** (envío)
- **POP3** / **IMAP** (recepción)

**Transferencia de archivos:**

- **FTP** / **SFTP**
- **TFTP**
- **SMB** / **CIFS**

**DNS:**

- **DNS** (resolución de nombres)

**Acceso remoto:**

- **SSH** (seguro)
- **Telnet** (inseguro)
- **RDP** (Remote Desktop)

**Otros:**

- **DHCP**
- **SNMP**
- **NTP**
- **LDAP**

---

## Configuración de Interfaces

### Selección de Interfaz

**Pasos:**

1. Ir a **Capture → Interfaces** (o presionar `Ctrl+I`)
2. Ver lista de interfaces disponibles
3. Seleccionar la interfaz apropiada

**Tipos de interfaces:**

**Ethernet:**

- Tráfico cableado
- eth0, eth1 (Linux)
- Local Area Connection (Windows)

**Wi-Fi:**

- Tráfico inalámbrico
- wlan0, wlan1 (Linux)
- Wireless Network Connection (Windows)

**Loopback:**

- Tráfico local (127.0.0.1)
- lo (Linux)
- Loopback (Windows)

**Otras:**

- USB
- Bluetooth
- Interfaces virtuales (VPN, VM)

---

### Información de Interfaces

**Datos mostrados:**

- **Nombre** de la interfaz
- **Dirección IP** asignada
- **Tráfico** actual (packets/sec)
- **Gráfico** de actividad en tiempo real

**Selección múltiple:**

- Posible capturar en varias interfaces simultáneamente
- Útil para monitoreo completo

---

## Opciones de Captura

### Promiscuous Mode

**Función:**

- Capturar **todo el tráfico** en el segmento de red
- No solo el tráfico destinado a la interfaz

**Cuándo usar:**

- Análisis de red completo
- Troubleshooting de red
- Monitoreo de seguridad

**Cuándo NO usar:**

- Solo interesa tráfico propio
- Reducir volumen de captura

---

### Monitor Mode (Wi-Fi)

**Función:**

- Capturar **todo el tráfico 802.11** (incluyendo management frames)
- Ver redes no asociadas
- Capturar handshakes WPA/WPA2

**Requisitos:**

- **Adaptador Wi-Fi compatible**
- Drivers apropiados
- Permisos de administrador

**Nota:** No todas las tarjetas Wi-Fi soportan monitor mode

---

### Buffer Size

**Función:**

- Tamaño del **buffer de captura** en memoria

**Consideraciones:**

- **Mayor buffer** = menos pérdida de paquetes
- **Menor buffer** = menos uso de RAM

**Recomendación:**

- Tráfico ligero: 1-2 MB
- Tráfico pesado: 10-50 MB

---

### Capture Filter

**Función:**

- Filtrar **durante la captura** (reduce tamaño de archivo)

**Sintaxis:** BPF (Berkeley Packet Filter)

**Ejemplos:**

```bash
port 80              # Solo HTTP
host 192.168.1.100   # Solo esta IP
tcp                  # Solo TCP
```

**Diferencia vs Display Filter:**

- **Capture filter** - Se aplica durante captura (BPF)
- **Display filter** - Se aplica después de captura (Wireshark)

---

### File Options

**Configuración de guardado:**

**Auto-save:**

- Guardar automáticamente cada X tiempo
- Guardar cada X MB
- Ring buffer (sobrescribir archivos antiguos)

**Formato:**

- `.pcapng` (recomendado, más información)
- `.pcap` (compatibilidad legacy)

---

## Preferencias Comunes

### Configurar Wireshark

**Acceso:**

```
Edit → Preferences
```

**Opciones útiles:**

**Appearance:**

- Layout (disposición de paneles)
- Font (tamaño de fuente)
- Colors (esquema de colores)

**Protocols:**

- Configuración por protocolo
- HTTP, TCP, DNS, etc.

**Name Resolution:**

- Resolver nombres DNS
- Resolver direcciones MAC
- Resolver puertos

---

## Atajos de Teclado Útiles

**Captura:**

- `Ctrl+E` - Iniciar/detener captura
- `Ctrl+R` - Reiniciar captura

**Navegación:**

- `Ctrl+G` - Ir a paquete específico
- `Ctrl+N` - Siguiente paquete
- `Ctrl+B` - Anterior paquete

**Filtros:**

- `Ctrl+/` - Enfocar barra de filtros
- `Alt+Enter` - Aplicar filtro

**Búsqueda:**

- `Ctrl+F` - Buscar paquete

**Otros:**

- `Ctrl+W` - Cerrar archivo
- `Ctrl+Q` - Salir de Wireshark

---

## Mejores Prácticas

### Antes de Capturar

**Preparación:**

- Cerrar **aplicaciones innecesarias**
- Identificar **interfaz correcta**
- Configurar **filtros de captura** si es necesario
- Tener **espacio en disco** suficiente

---

### Durante la Captura

**Monitoreo:**

- Observar **contador de paquetes**
- Verificar que se capture tráfico esperado
- Detener cuando sea suficiente

---

### Después de Capturar

**Análisis:**

- **Guardar** captura inmediatamente
- Aplicar **filtros de visualización**
- Usar **Statistics** para overview
- **Documentar** hallazgos importantes

---

## Consideraciones

- Wireshark requiere **privilegios de administrador** para capturar
- **No** capturar en redes sin autorización
- Capturas pueden contener **información sensible**
- **Proteger** archivos de captura apropiadamente
- Conocer las **leyes locales** sobre captura de tráfico

---