## Infraestructura web y HTTP

La infraestructura web permite compartir aplicaciones de manera global.  
El protocolo **HTTP (Hypertext Transfer Protocol)** es el mecanismo principal para la comunicación entre clientes y servidores, garantizando que las aplicaciones puedan ser accedidas desde cualquier parte del mundo.

## Tipos de redes

- **LAN (Local Area Network):** Redes de alcance limitado, como oficinas o hogares.  
- **WAN (Wide Area Network):** Redes de gran extensión, que conectan múltiples LAN a través de grandes distancias.  
- **Internet:** La red global que interconecta millones de dispositivos y utiliza protocolos estandarizados para la comunicación.

## Protocolos de comunicación

El modelo **TCP/IP** organiza la comunicación en capas:
- **Capa de aplicación:** Donde operan protocolos como HTTP, FTP, SMTP.  
- **Capa de transporte:** Encargada de la transmisión confiable o rápida de datos (TCP y UDP).  
- **Capa de red:** Responsable del direccionamiento y enrutamiento (IP).  
- **Capa de enlace:** Maneja la transmisión física de datos en la red.

## TCP vs UDP

- **TCP (Transmission Control Protocol):**  
  - Orientado a la conexión.  
  - Garantiza entrega confiable y ordenada de los datos.  
  - Usado en aplicaciones como navegación web, correos electrónicos y transferencia de archivos.  

- **UDP (User Datagram Protocol):**  
  - No orientado a la conexión.  
  - Más rápido, pero sin garantía de entrega.  
  - Usado en aplicaciones que requieren velocidad, como streaming de video, llamadas VoIP y juegos en línea.

## Direccionamiento IP

Cada dispositivo en una red se identifica mediante una **dirección IP**.  
Existen dos versiones principales:  
- **IPv4:** Direcciones de 32 bits, formato decimal (ejemplo: 192.168.1.1).  
- **IPv6:** Direcciones de 128 bits, formato hexadecimal, creadas para suplir la escasez de IPv4.

## Sistema de Nombres de Dominio (DNS)

El **DNS (Domain Name System)** traduce nombres de dominio legibles (ejemplo: `www.ejemplo.com`) en direcciones IP.  
Esto facilita el acceso a sitios web sin necesidad de recordar números.

### Proceso de resolución DNS

1. El usuario ingresa una URL en el navegador.  
2. El navegador consulta el servidor DNS configurado.  
3. El servidor DNS devuelve la dirección IP correspondiente.  
4. El navegador establece conexión con el servidor web usando esa IP.

## Estructura de una URL

Una **URL (Uniform Resource Locator)** define la ubicación de un recurso en la web.  
Ejemplo: `https://www.ejemplo.com:443/ruta/recurso?param=valor`

Componentes principales:
- **Esquema:** Protocolo usado (http, https, ftp).  
- **Dominio:** Nombre del servidor (`www.ejemplo.com`).  
- **Puerto:** Número que identifica el servicio (443 para HTTPS).  
- **Ruta:** Ubicación del recurso (`/ruta/recurso`).  
- **Parámetros:** Información adicional (`?param=valor`).

## Seguridad y autenticación

Los dominios y certificados digitales permiten verificar la autenticidad de los sitios web.  
El uso de **HTTPS** asegura la comunicación mediante cifrado, protegiendo la información transmitida entre cliente y servidor.
