## Topologías de Red

### Topologías Físicas Básicas

**Bus**

- Todos los dispositivos conectados a un cable central (backbone)
- Señal viaja en ambas direcciones
- Fallo en el cable principal afecta toda la red
- Obsoleta en redes modernas

**Star (Estrella)**

- Todos los dispositivos conectan a un punto central (switch/hub)
- Topología más común en LANs modernas
- Fallo de dispositivo no afecta a otros
- Fallo del nodo central tumba toda la red
- Fácil troubleshooting y escalabilidad

**Ring (Anillo)**

- Dispositivos conectados en círculo cerrado
- Datos viajan en una dirección (o ambas en dual-ring)
- Fallo de un nodo puede afectar la red (sin redundancia)
- Usado en MANs y algunas tecnologías (FDDI, Token Ring)

**Mesh (Malla)**

- **Full Mesh**: Cada dispositivo conectado a todos los demás
- **Partial Mesh**: Algunos dispositivos con múltiples conexiones
- Alta redundancia y confiabilidad
- Costosa de implementar
- Común en backbones de ISP y WANs

**Hybrid (Híbrida)**

- Combinación de topologías
- Ejemplo: Star-Bus, Star-Ring
- Flexibilidad según necesidades
- Más común en redes empresariales grandes

### Topologías Lógicas

- Describe cómo fluyen los datos, no cómo están conectados físicamente
- Ejemplo: Ethernet es lógicamente bus aunque físicamente sea estrella

## Dispositivos de Conectividad

### Hub

- Dispositivo Capa 1 (Física)
- Repite señal a todos los puertos (broadcasting)
- No inteligente, no filtra tráfico
- Crea dominio de colisión único
- **Obsoleto**: Reemplazado por switches

### Switch

- Dispositivo Capa 2 (Enlace de Datos)
- Aprende direcciones MAC y reenvía selectivamente
- **MAC Address Table**: Mapea puertos a direcciones MAC
- Crea dominios de colisión separados por puerto
- **Full-duplex**: Transmisión y recepción simultánea
- Tipos: Unmanaged (básico) y Managed (configurable)

### Router

- Dispositivo Capa 3 (Red)
- Enruta paquetes entre redes diferentes
- Usa direcciones IP para tomar decisiones
- **Tabla de ruteo**: Determina mejor path
- Separa dominios de broadcast
- Funciones: NAT, firewall básico, DHCP, QoS

### Access Point (AP)

- Extiende red cableada a wireless
- Conecta dispositivos WiFi a LAN
- Standards: 802.11a/b/g/n/ac/ax (WiFi 6)
- Puede ser standalone o controlado centralmente

### Modem

- **Modulator-Demodulator**
- Convierte señales digitales a analógicas y viceversa
- Tipos: DSL, Cable, Fiber
- Proporciona conectividad WAN/Internet

### Firewall

- Filtra tráfico basado en políticas de seguridad
- Puede operar en Capas 3-7
- **Stateful**: Rastrea estado de conexiones
- **Next-Gen Firewalls**: Inspección profunda, IPS, filtrado de aplicaciones

## Modelo OSI y TCP/IP

### Capas del Modelo OSI

**Capa 7 - Aplicación**

- Interacción con aplicaciones de usuario
- Protocolos: HTTP, HTTPS, FTP, SMTP, DNS, SSH

**Capa 6 - Presentación**

- Formato y cifrado de datos
- Traducción, compresión, encriptación

**Capa 5 - Sesión**

- Establece, mantiene y termina sesiones
- Control de diálogo

**Capa 4 - Transporte**

- Entrega confiable de datos extremo a extremo
- Protocolos: TCP (confiable), UDP (no confiable)
- Segmentación y reensamblado
- Control de flujo y errores

**Capa 3 - Red**

- Direccionamiento lógico (IP) y ruteo
- Determinación de mejor ruta
- Protocolo principal: IP (IPv4, IPv6)

**Capa 2 - Enlace de Datos**

- Direccionamiento físico (MAC)
- Frame formatting
- Detección de errores (CRC)
- Control de acceso al medio

**Capa 1 - Física**

- Transmisión de bits en el medio
- Cables, conectores, señales eléctricas/ópticas
- Standards físicos

### Modelo TCP/IP (4 Capas)

- **Aplicación**: Combina OSI 5-7
- **Transporte**: TCP/UDP (igual OSI 4)
- **Internet**: IP routing (igual OSI 3)
- **Acceso a Red**: Combina OSI 1-2

## Tecnologías y Protocolos de Ruteo

### Conceptos Básicos de Ruteo

**Tabla de Ruteo**

- Lista de rutas conocidas hacia redes destino
- Información: Red destino, next-hop, interfaz, métrica
- Fuentes: Directamente conectadas, estáticas, dinámicas

**Métricas de Ruteo**

- **Hop count**: Número de routers hasta destino
- **Bandwidth**: Ancho de banda del enlace
- **Delay**: Latencia del path
- **Cost**: Valor calculado (OSPF usa bandwidth)

**Administrative Distance (AD)**

- Confiabilidad de la fuente de ruta (0-255)
- Menor AD = más confiable
- Ejemplos: Conectada=0, Estática=1, OSPF=110, RIP=120

### Tipos de Rutas

**Rutas Directamente Conectadas**

- Redes en interfaces activas del router
- AD = 0, más confiables

**Rutas Estáticas**

- Configuradas manualmente por administrador
- Control preciso, no consume recursos
- No se adapta automáticamente a cambios
- Útil para rutas default y redes pequeñas

**Rutas Dinámicas**

- Aprendidas automáticamente por protocolos de ruteo
- Se adaptan a cambios de topología
- Mayor overhead de procesamiento

### Protocolos de Ruteo Dinámico

**Clasificación por Alcance**

- **IGP (Interior Gateway Protocol)**: Dentro de una organización (AS)
    - RIP, OSPF, EIGRP
- **EGP (Exterior Gateway Protocol)**: Entre organizaciones
    - BGP

**Clasificación por Algoritmo**

**Distance Vector**

- Comparten tabla completa con vecinos
- Decisión basada en distancia y dirección
- Convergencia más lenta
- Ejemplo: **RIP (Routing Information Protocol)**
    - Métrica: Hop count (máx 15)
    - Actualización cada 30 segundos
    - Simple pero limitado

**Link State**

- Comparten estado de enlaces con todos
- Cada router construye mapa completo
- Convergencia rápida
- Mayor uso de CPU y memoria
- Ejemplo: **OSPF (Open Shortest Path First)**
    - Métrica: Cost basado en bandwidth
    - Áreas para escalabilidad
    - Standard abierto (no propietario)

**Híbrido/Advanced Distance Vector**

- Ejemplo: **EIGRP (Enhanced Interior Gateway Routing Protocol)**
    - Propietario de Cisco
    - Convergencia rápida
    - Menor overhead que link state
    - Métrica compuesta (bandwidth, delay, load, reliability)

**Path Vector**

- Ejemplo: **BGP (Border Gateway Protocol)**
    - Protocolo de ruteo de Internet
    - Decisiones basadas en políticas
    - Escala masiva
    - Previene loops con AS-Path

### Conceptos Avanzados

**Default Route (Ruta por Defecto)**

- 0.0.0.0/0 o ::/0 (IPv6)
- Gateway of last resort
- Hacia dónde enviar tráfico sin ruta específica

**Longest Match Rule**

- Router elige ruta más específica (mayor prefix length)
- /32 más específica que /24

**Load Balancing**

- Múltiples rutas con igual costo
- Distribuye tráfico entre paths
- Equal-cost multipath (ECMP)

## Internet of Things (IoT)

### Definición y Características

- Red de dispositivos físicos conectados a Internet
- Recopilan, comparten e intercambian datos
- Sensores, actuadores, conectividad embebida
- Mínima o nula intervención humana

### Categorías de Dispositivos IoT

**Consumer IoT**

- Smart home devices (termostatos, luces, cerraduras)
- Wearables (smartwatches, fitness trackers)
- Smart appliances (refrigeradores, lavadoras)

**Commercial IoT**

- Healthcare: Monitoreo de pacientes, equipos médicos
- Retail: Inventory tracking, beacons
- Smart buildings: HVAC, iluminación, seguridad

**Industrial IoT (IIoT)**

- Manufacturing: Sensores de producción, mantenimiento predictivo
- Agricultura: Monitoreo de cultivos, riego automatizado
- Energía: Smart grids, medidores inteligentes
- Logística: Tracking de flota, supply chain

### Tecnologías de Conectividad IoT

**Corto Alcance**

- **Bluetooth/BLE**: Bajo consumo, dispositivos personales
- **Zigbee**: Mesh network, smart home
- **Z-Wave**: Similar a Zigbee, smart home
- **NFC**: Muy corto alcance, pagos

**Largo Alcance**

- **WiFi**: Alta velocidad, mayor consumo
- **Cellular (4G/5G)**: Cobertura amplia, vehículos conectados
- **LoRaWAN**: Largo alcance, bajo consumo, sensores remotos
- **Sigfox**: Similar a LoRa, redes propietarias
- **NB-IoT**: Cellular para IoT, bajo consumo

### Arquitectura IoT

**Capa de Dispositivos**

- Sensores y actuadores
- Recopilación de datos

**Capa de Red/Conectividad**

- Gateways IoT
- Transmisión de datos

**Capa de Plataforma/Cloud**

- Procesamiento y almacenamiento
- Analytics y machine learning

**Capa de Aplicación**

- Interfaces de usuario
- Business logic

### Desafíos de Seguridad IoT

**Vulnerabilidades Comunes**

- Credenciales por defecto no cambiadas
- Firmware desactualizado sin parches
- Falta de cifrado en comunicaciones
- Autenticación débil o inexistente
- Superficie de ataque amplia

**Ataques Conocidos**

- Botnets IoT (Mirai)
- DDoS usando dispositivos comprometidos
- Eavesdropping en comunicaciones
- Ransomware en dispositivos críticos

**Mejores Prácticas de Seguridad**

- Cambiar credenciales por defecto
- Segmentación de red (VLAN para IoT)
- Actualización regular de firmware
- Cifrado de comunicaciones (TLS)
- Autenticación fuerte
- Monitoreo de tráfico IoT
- Disable servicios innecesarios
- Network access control (NAC)

### Protocolos IoT Comunes

**Mensajería**

- **MQTT**: Publish/Subscribe, bajo overhead
- **CoAP**: Similar a HTTP pero más ligero
- **AMQP**: Message queuing

**Descubrimiento**

- **mDNS/Bonjour**: Autodescubrimiento local
- **UPnP**: Plug and play universal

## Direccionamiento IP

### IPv4

- 32 bits, formato: 192.168.1.1
- ~4.3 mil millones de direcciones
- Clases: A, B, C (classful - obsoleto)
- CIDR: Notación moderna con máscaras variables
- Escasez de direcciones → NAT, IPv6

### IPv6

- 128 bits, formato: 2001:0db8:85a3::8a2e:0370:7334
- 340 undecillion direcciones
- Características: Autoconfiguración, IPsec obligatorio, no fragmentación en routers
- Adopción gradual pero en crecimiento

### NAT (Network Address Translation)

- Traduce IPs privadas a públicas
- Conserva direcciones IPv4 públicas
- Tipos: Static NAT, Dynamic NAT, PAT (Overload)
- Común en routers domésticos y empresariales