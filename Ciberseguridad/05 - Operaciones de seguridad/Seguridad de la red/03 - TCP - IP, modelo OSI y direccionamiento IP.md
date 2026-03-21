## Modelos de Red

### Modelo OSI (7 Capas)

|Capa|Nombre|Función|Ejemplos|Dispositivos|
|---|---|---|---|---|
|**7**|Aplicación|Interfaz con usuario|HTTP, FTP, SMTP, DNS|-|
|**6**|Presentación|Formato, cifrado, compresión|SSL/TLS, JPEG, ASCII|-|
|**5**|Sesión|Establecer/mantener sesiones|NetBIOS, RPC|-|
|**4**|Transporte|Entrega confiable extremo a extremo|TCP, UDP|-|
|**3**|Red|Direccionamiento lógico y ruteo|IP, ICMP, OSPF|Router|
|**2**|Enlace de Datos|Direccionamiento físico, detección errores|Ethernet, WiFi, PPP|Switch, Bridge|
|**1**|Física|Transmisión de bits|Cables, señales|Hub, cables|

**Mnemotecnia (de arriba a abajo)**: **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing

### Modelo TCP/IP (4 Capas)

|TCP/IP|OSI Equivalente|Función|
|---|---|---|
|**Aplicación**|7-5|Protocolos de usuario|
|**Transporte**|4|TCP/UDP|
|**Internet**|3|IP, ruteo|
|**Acceso a Red**|2-1|Ethernet, hardware|

## Capa de Transporte (Capa 4)

### TCP (Transmission Control Protocol)

**Características**

- **Orientado a conexión**: Establece sesión (3-way handshake)
- **Confiable**: Garantiza entrega ordenada
- **Control de flujo**: Evita saturar receptor
- **Control de congestión**: Ajusta velocidad según red
- **Full-duplex**: Transmisión bidireccional simultánea

**3-Way Handshake**

1. **SYN**: Cliente solicita conexión
2. **SYN-ACK**: Servidor acepta
3. **ACK**: Cliente confirma, conexión establecida

**Flags TCP Importantes**

- **SYN**: Sincronizar, iniciar conexión
- **ACK**: Acknowledgment
- **FIN**: Finalizar conexión
- **RST**: Reset, cerrar inmediatamente
- **PSH**: Push, enviar datos inmediatamente
- **URG**: Urgente

**Usos**: HTTP/HTTPS, FTP, SSH, email (SMTP, POP3, IMAP)

### UDP (User Datagram Protocol)

**Características**

- **Sin conexión**: No establece sesión
- **No confiable**: No garantiza entrega ni orden
- **Rápido**: Menor overhead
- **Sin control de flujo/congestión**

**Usos**: DNS, DHCP, streaming (video/audio), VoIP, gaming, SNMP

### Comparación

|Característica|TCP|UDP|
|---|---|---|
|Confiabilidad|Sí|No|
|Velocidad|Más lento|Más rápido|
|Overhead|Alto|Bajo|
|Orden|Garantizado|No garantizado|
|Uso|Datos críticos|Tiempo real|

### Puertos

**Concepto**: Identifican aplicaciones en un host

**Rangos**

- **0-1023**: Well-known (privilegiados)
- **1024-49151**: Registered
- **49152-65535**: Dinámicos/efímeros

**Puertos Comunes**

- 20/21: FTP
- 22: SSH
- 23: Telnet
- 25: SMTP
- 53: DNS
- 80: HTTP
- 110: POP3
- 143: IMAP
- 443: HTTPS
- 3389: RDP

## Direccionamiento

### Direcciones MAC (Capa 2)

**Características**

- 48 bits (6 bytes): XX:XX:XX:XX:XX:XX formato hexadecimal
- **OUI** (primeros 3 bytes): Fabricante
- **NIC** (últimos 3 bytes): Identificador único
- **Ámbito**: Solo en red local (LAN)
- Grabada en NIC (hardcoded), pero puede cambiarse por software

**Tipos**

- **Unicast**: Una dirección específica
- **Broadcast**: FF:FF:FF:FF:FF:FF (todos en LAN)
- **Multicast**: Grupo específico (01:00:5E:xx:xx:xx)

### ARP (Address Resolution Protocol)

**Función**: Resuelve IP → MAC en red local

**Proceso**

1. Host necesita MAC de una IP
2. **ARP Request** (broadcast): "¿Quién tiene IP X.X.X.X?"
3. **ARP Reply** (unicast): "Yo, mi MAC es XX:XX:XX:XX:XX:XX"
4. Se guarda en **caché ARP** (temporal)

**Comandos**

- `arp -a`: Ver caché ARP
- `arp -d`: Limpiar caché

## Direccionamiento IPv4

### Estructura

- **32 bits** divididos en 4 octetos
- Formato: 192.168.1.1
- Cada octeto: 0-255 (8 bits)

### Clases (Classful - obsoleto pero útil conocer)

|Clase|Primer Octeto|Máscara Default|Uso|
|---|---|---|---|
|A|1-126|/8 (255.0.0.0)|Redes muy grandes|
|B|128-191|/16 (255.255.0.0)|Redes medianas|
|C|192-223|/24 (255.255.255.0)|Redes pequeñas|
|D|224-239|-|Multicast|
|E|240-255|-|Experimental|

**Nota**: 127.x.x.x reservado para loopback (localhost)

### Direcciones Privadas (RFC 1918)

**No enrutables en Internet**

- **Clase A**: 10.0.0.0/8 (10.0.0.0 - 10.255.255.255)
- **Clase B**: 172.16.0.0/12 (172.16.0.0 - 172.31.255.255)
- **Clase C**: 192.168.0.0/16 (192.168.0.0 - 192.168.255.255)

**Otros rangos especiales**

- **Loopback**: 127.0.0.0/8
- **APIPA**: 169.254.0.0/16 (autoconfiguración sin DHCP)
- **Link-local**: 169.254.0.0/16

### Máscara de Subred

**Función**: Separa porción de red de porción de host

**Notación CIDR**: /XX (número de bits en 1)

- /24 = 255.255.255.0
- /16 = 255.255.0.0
- /8 = 255.0.0.0

**Ejemplo**

- IP: 192.168.1.10/24
- Red: 192.168.1.0
- Hosts: .1 a .254
- Broadcast: 192.168.1.255

## Subnetting

### Concepto

Dividir una red en subredes más pequeñas para:

- Organización lógica
- Seguridad
- Eficiencia en uso de IPs
- Reducir dominio de broadcast

### Cálculos Básicos

**Fórmula de Hosts**

- Hosts disponibles = 2^(bits de host) - 2
- -2 porque: dirección de red + broadcast no utilizables

**Ejemplo /24**

- 32 - 24 = 8 bits para hosts
- 2^8 - 2 = 254 hosts utilizables

### Tabla de Referencia Rápida

|CIDR|Máscara|Hosts|Uso Típico|
|---|---|---|---|
|/30|255.255.255.252|2|Punto a punto|
|/29|255.255.255.248|6|Muy pequeña|
|/28|255.255.255.240|14|Pequeña|
|/27|255.255.255.224|30|-|
|/26|255.255.255.192|62|-|
|/25|255.255.255.128|126|-|
|/24|255.255.255.0|254|Red clase C|
|/16|255.255.0.0|65,534|Red clase B|
|/8|255.0.0.0|16,777,214|Red clase A|

### Proceso de Subnetting

**Ejemplo**: Dividir 192.168.1.0/24 en 4 subredes

1. **Determinar bits necesarios**: 2^n ≥ subredes → 2^2 = 4 → necesito 2 bits
2. **Nueva máscara**: /24 + 2 = /26 (255.255.255.192)
3. **Incremento**: 256 - 192 = 64
4. **Subredes resultantes**:
    - 192.168.1.0/26 (hosts: .1-.62, broadcast: .63)
    - 192.168.1.64/26 (hosts: .65-.126, broadcast: .127)
    - 192.168.1.128/26 (hosts: .129-.190, broadcast: .191)
    - 192.168.1.192/26 (hosts: .193-.254, broadcast: .255)

### VLSM (Variable Length Subnet Mask)

**Concepto**: Usar diferentes tamaños de subred según necesidades

**Ejemplo**: Red 192.168.1.0/24, necesito:

- Subred A: 100 hosts → /25 (126 hosts)
- Subred B: 50 hosts → /26 (62 hosts)
- Subred C: 25 hosts → /27 (30 hosts)
- Enlaces punto a punto: /30 (2 hosts)

**Regla**: Asignar desde la subred más grande a la más pequeña

## IPv6 (Introducción)

### Características

- **128 bits** (vs 32 de IPv4)
- Formato: 2001:0db8:85a3:0000:0000:8a2e:0370:7334
- Notación abreviada: 2001:db8:85a3::8a2e:370:7334

**Ventajas sobre IPv4**

- Espacio de direcciones enorme
- No necesita NAT
- IPsec obligatorio
- Autoconfiguración (SLAAC)
- No fragmentación en routers

**Tipos de Direcciones**

- **Unicast**: Una interfaz
    - Global: Enrutable en Internet (2000::/3)
    - Link-local: Solo red local (fe80::/10)
- **Multicast**: Grupo de interfaces (ff00::/8)
- **Anycast**: La más cercana de un grupo
- **No existe broadcast**: Reemplazado por multicast

## NAT (Network Address Translation)

### Función

Traduce IPs privadas ↔ IPs públicas

### Tipos

**Static NAT**

- 1 IP privada → 1 IP pública fija
- Bidireccional
- Servidores internos accesibles desde Internet

**Dynamic NAT**

- Pool de IPs públicas
- Asignación temporal bajo demanda
- Limitado por tamaño del pool

**PAT (Port Address Translation) / NAT Overload**

- Múltiples IPs privadas → 1 IP pública
- Diferencia por puerto origen
- Más común en hogares/SMB

**Ventajas**

- Conserva IPs públicas
- Seguridad por obscuridad
- Flexibilidad en redes internas

**Desventajas**

- Rompe conectividad end-to-end
- Problemas con algunos protocolos (IPsec, FTP)
- No es seguridad real (no reemplaza firewall)