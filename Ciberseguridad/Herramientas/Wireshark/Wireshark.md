## ¿Qué es el Modelo OSI?

El **Modelo OSI (Open Systems Interconnection)** es un marco conceptual que describe cómo diferentes sistemas de comunicación pueden interactuar entre sí.

Fue desarrollado por la **Organización Internacional de Normalización (ISO)** en 1984 y divide la comunicación de red en **7 capas distintas**.

**Propósito:** Estandarizar las funciones de red para facilitar la interoperabilidad entre diferentes sistemas.

---

## Las 7 Capas del Modelo OSI

### Capa 7 - Aplicación (Application Layer)

**Función:** Proporciona servicios de red directamente a las aplicaciones del usuario

**Protocolos comunes:**

- **HTTP/HTTPS** - Navegación web
- **FTP/SFTP** - Transferencia de archivos
- **SMTP/POP3/IMAP** - Correo electrónico
- **DNS** - Resolución de nombres
- **SSH** - Acceso remoto seguro
- **Telnet** - Acceso remoto (inseguro)

**Características:**

- Interfaz entre el usuario y la red
- Manejo de la presentación de datos al usuario
- Servicios como transferencia de archivos, correo electrónico, navegación web

**En Wireshark:** Datos de aplicación visibles (HTTP headers, DNS queries, etc.)

---

### Capa 6 - Presentación (Presentation Layer)

**Función:** Traducción, cifrado y compresión de datos

**Ejemplos:**

- **SSL/TLS** - Cifrado de comunicaciones
- **JPEG, PNG, GIF** - Formatos de imagen
- **MPEG, MP4** - Formatos de video
- **ASCII, Unicode** - Codificación de texto

**Características:**

- Conversión de formatos de datos
- Cifrado y descifrado
- Compresión y descompresión
- Traducción entre diferentes representaciones

**En Wireshark:** Visible en negociación TLS/SSL

---

### Capa 5 - Sesión (Session Layer)

**Función:** Establece, mantiene y termina sesiones entre aplicaciones

**Protocolos:**

- **NetBIOS** - Servicios de red Windows
- **RPC** - Remote Procedure Call
- **SQL sessions** - Sesiones de base de datos
- **PAP** - Password Authentication Protocol

**Características:**

- Control de diálogos (half-duplex, full-duplex)
- Sincronización de sesiones
- Recuperación de sesiones interrumpidas
- Checkpointing

**En Wireshark:** Difícil de ver directamente, integrada en protocolos superiores

---

### Capa 4 - Transporte (Transport Layer)

**Función:** Entrega confiable de datos extremo a extremo

**Protocolos:**

- **TCP** (Transmission Control Protocol) - Confiable, orientado a conexión
- **UDP** (User Datagram Protocol) - No confiable, sin conexión
- **SCTP** (Stream Control Transmission Protocol)

**Características:**

- Control de flujo
- Detección y corrección de errores
- Segmentación y reensamblaje
- Multiplexación mediante puertos

**En Wireshark:** Headers TCP/UDP claramente visibles

---

### Capa 3 - Red (Network Layer)

**Función:** Enrutamiento de paquetes entre diferentes redes

**Protocolos:**

- **IP** (IPv4/IPv6) - Direccionamiento y enrutamiento
- **ICMP** - Mensajes de error y diagnóstico
- **ARP** - Resolución de direcciones (IP a MAC)
- **OSPF, BGP, RIP** - Protocolos de enrutamiento

**Características:**

- Direccionamiento lógico (direcciones IP)
- Enrutamiento de paquetes
- Fragmentación y reensamblaje de paquetes
- Control de congestión

**En Wireshark:** Header IP con direcciones origen/destino

---

### Capa 2 - Enlace de Datos (Data Link Layer)

**Función:** Transmisión confiable de datos dentro de una red local

**Protocolos y tecnologías:**

- **Ethernet** (802.3) - Redes cableadas
- **Wi-Fi** (802.11) - Redes inalámbricas
- **PPP** - Point-to-Point Protocol
- **Frame Relay** - WAN
- **VLAN** (802.1Q) - Segmentación lógica

**Características:**

- Direccionamiento físico (direcciones MAC)
- Detección de errores (CRC)
- Control de acceso al medio (MAC)
- Framing (encapsulación en frames)

**Subcapas:**

- **LLC** (Logical Link Control)
- **MAC** (Media Access Control)

**En Wireshark:** Header Ethernet con direcciones MAC

---

### Capa 1 - Física (Physical Layer)

**Función:** Transmisión de bits a través del medio físico

**Medios de transmisión:**

- **Cables de cobre** (UTP, STP, coaxial)
- **Fibra óptica** (monomodo, multimodo)
- **Ondas de radio** (Wi-Fi, Bluetooth, celular)
- **Infrarrojos**

**Características:**

- Especificaciones eléctricas y físicas
- Topología de red (bus, estrella, anillo)
- Sincronización de bits
- Voltajes y señales
- Conectores y pinouts

**En Wireshark:** No directamente visible (Wireshark captura desde Capa 2)

---

## Encapsulación de Datos

### Proceso de Encapsulación (Envío)

**Flujo descendente:**

```
Capa 7 (Aplicación)     → Datos
Capa 6 (Presentación)   → Datos (formateados)
Capa 5 (Sesión)         → Datos (con control de sesión)
Capa 4 (Transporte)     → Segmentos (TCP) / Datagramas (UDP)
Capa 3 (Red)            → Paquetes
Capa 2 (Enlace)         → Frames
Capa 1 (Física)         → Bits
```

---

### Proceso de Desencapsulación (Recepción)

**Flujo ascendente:**

```
Capa 1 → Bits recibidos
Capa 2 → Frame validado (CRC)
Capa 3 → Paquete extraído
Capa 4 → Segmento reensamblado
Capa 5 → Sesión gestionada
Capa 6 → Datos decodificados
Capa 7 → Datos entregados a aplicación
```

---

## Importancia del Modelo OSI en el Análisis de Red

Cuando utilizamos **Wireshark** para analizar tráfico de red, es fundamental comprender el modelo OSI porque:

---

### Organización Jerárquica

**En Wireshark:**

- Cada paquete muestra información de **múltiples capas**
- Panel de detalles organizado **por capas**
- Fácil navegación entre capas

**Ejemplo de un paquete HTTP:**

```
Frame (información general)
└── Ethernet II (Capa 2)
    └── Internet Protocol (Capa 3)
        └── Transmission Control Protocol (Capa 4)
            └── Hypertext Transfer Protocol (Capa 7)
```

---

### Identificación de Problemas

**Por capa:**

- **Capa 1:** Problemas de cableado, interferencia
- **Capa 2:** Colisiones, direcciones MAC duplicadas
- **Capa 3:** Problemas de routing, TTL expirado
- **Capa 4:** Retransmisiones TCP, puertos bloqueados
- **Capa 7:** Errores de aplicación, timeouts

---

### Análisis Sistemático

**Metodología:**

1. **Verificar Capa 2** - ¿Frames llegando correctamente?
2. **Verificar Capa 3** - ¿Routing funcionando?
3. **Verificar Capa 4** - ¿Conexión TCP establecida?
4. **Verificar Capa 7** - ¿Aplicación respondiendo?

---

### Comprensión de Interacción de Protocolos

**Relaciones entre capas:**

- **DNS** (Capa 7) sobre **UDP** (Capa 4)
- **HTTP** (Capa 7) sobre **TCP** (Capa 4)
- **TCP/UDP** (Capa 4) sobre **IP** (Capa 3)
- **IP** (Capa 3) sobre **Ethernet** (Capa 2)

---

## Modelo OSI vs TCP/IP

### Comparación

|OSI (7 capas)|TCP/IP (4 capas)|Protocolos|
|---|---|---|
|7. Aplicación|4. Aplicación|HTTP, FTP, DNS|
|6. Presentación|4. Aplicación|SSL/TLS|
|5. Sesión|4. Aplicación|NetBIOS|
|4. Transporte|3. Transporte|TCP, UDP|
|3. Red|2. Internet|IP, ICMP|
|2. Enlace de Datos|1. Acceso a Red|Ethernet, Wi-Fi|
|1. Física|1. Acceso a Red|Cables, Radio|

**Nota:** El modelo TCP/IP es el usado en la práctica, OSI es más teórico/educativo.

---

## Aplicación Práctica en Wireshark

### Filtros por Capa

**Capa 2 (Enlace):**

```bash
eth.addr == 00:11:22:33:44:55
```

**Capa 3 (Red):**

```bash
ip.addr == 192.168.1.100
```

**Capa 4 (Transporte):**

```bash
tcp.port == 80
udp.port == 53
```

**Capa 7 (Aplicación):**

```bash
http
dns
ftp
```

---

### Análisis de Paquete Completo

**Ejemplo paso a paso:**

1. **Frame** - 1514 bytes capturados
2. **Ethernet** - Src MAC: aa:bb:cc:dd:ee:ff, Dst MAC: 11:22:33:44:55:66
3. **IP** - Src: 192.168.1.100, Dst: 93.184.216.34
4. **TCP** - Src Port: 54321, Dst Port: 80, Flags: PSH, ACK
5. **HTTP** - GET /index.html HTTP/1.1

---

## Mejores Prácticas

### Para Análisis

**Enfoque de capas:**

- Comenzar desde **Capa 7** (síntomas visibles)
- Descender por capas según sea necesario
- **Correlacionar** información entre capas

---

### Troubleshooting

**Metodología:**

1. **Identificar** síntoma (Capa 7)
2. **Verificar** capas inferiores progresivamente
3. **Aislar** la capa problemática
4. **Resolver** el problema específico

---

## Consideraciones

- El modelo OSI es **teórico** y educativo
- En la práctica se usa el modelo **TCP/IP**
- Wireshark muestra información de **todas las capas**
- Entender OSI facilita **troubleshooting** sistemático
- **No todas** las comunicaciones usan todas las capas
- Algunos protocolos no encajan perfectamente en el modelo

---