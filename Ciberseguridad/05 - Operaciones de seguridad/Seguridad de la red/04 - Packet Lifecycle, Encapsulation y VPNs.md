## Circuit vs Packet Switching

**Circuit Switching**

- Conexión dedicada durante toda la comunicación
- Ancho de banda reservado
- Ejemplo: Teléfono tradicional

**Packet Switching**

- Datos en paquetes independientes
- Recursos compartidos dinámicamente
- Ejemplo: Internet

## Encapsulación de Datos

### Proceso (de arriba hacia abajo)

|Capa|PDU|Agrega|
|---|---|---|
|Aplicación|Data|Datos usuario|
|Transporte|Segment|Header TCP/UDP (puertos)|
|Red|Packet|Header IP (IPs origen/destino)|
|Enlace|Frame|Header/Trailer (MACs, FCS)|
|Física|Bits|Señales eléctricas/ópticas|

**Desencapsulación**: Proceso inverso al recibir

## Ciclo de Vida del Paquete

1. **Generación**: Aplicación crea datos, se encapsulan
2. **Ruteo local**: ¿Mismo segmento? → Directo. ¿Diferente? → Default gateway
3. **ARP**: Resuelve IP a MAC si es necesario
4. **Transmisión**: Frame enviado por medio físico
5. **En cada router**:
    - Verifica integridad (FCS)
    - Consulta tabla de ruteo
    - Decrementa TTL (previene loops)
    - Reencapsula con nuevo frame
6. **Entrega final**: Host destino desencapsula y entrega a aplicación

**TTL (Time To Live)**

- Previene loops infinitos
- Cada router decrementa en 1
- Si llega a 0, paquete descartado

## VPN (Virtual Private Network)

### Concepto

Conexión segura y cifrada sobre red pública (Internet)

### Tipos

**Site-to-Site**

- Conecta redes completas (oficinas)
- Router a router, permanente

**Remote Access**

- Usuario individual a red corporativa
- Cliente VPN, bajo demanda

### Protocolos Principales

**IPsec**

- Capa 3 (Red)
- Muy seguro, standard industria
- Complejo de configurar
- Modos: Tunnel (site-to-site), Transport (host-to-host)

**SSL/TLS VPN**

- Capa 4-7 (Aplicación)
- Fácil de usar (navegador web)
- Atraviesa firewalls fácilmente
- Ejemplos: Cisco AnyConnect, GlobalProtect

**OpenVPN**

- Open source, muy configurable
- Usa SSL/TLS
- Requiere cliente

**WireGuard**

- Moderno, ligero, rápido
- Criptografía moderna
- Creciente adopción

### Seguridad VPN

**Cifrado**

- AES-256 (más usado)
- Protege confidencialidad

**Autenticación**

- Pre-Shared Key (PSK): Simple
- Certificados digitales: Más seguro
- Usuario/contraseña + MFA: Recomendado

**Integridad**

- SHA-256 (verifica datos no alterados)

### Split Tunneling

- **Split**: Solo tráfico corporativo por VPN, resto directo a Internet
- **Full Tunnel**: Todo el tráfico por VPN (más seguro)

### Mejores Prácticas

- Usar protocolos modernos (IPsec/IKEv2, OpenVPN, WireGuard)
- Cifrado fuerte (AES-256)
- Implementar MFA
- Preferir Full Tunnel
- Mantener actualizado