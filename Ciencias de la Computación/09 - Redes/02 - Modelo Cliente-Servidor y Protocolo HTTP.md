## Modelo cliente-servidor

El modelo **cliente-servidor** es la base de las aplicaciones web modernas.  
- **Cliente:** Dispositivo o aplicación que solicita recursos (ejemplo: navegador web).  
- **Servidor:** Equipo que hospeda la aplicación y responde a las solicitudes del cliente.  
Este modelo permite estructurar aplicaciones de forma escalable y accesible globalmente.

## Hospedaje de aplicaciones web

Para que una aplicación sea accesible en la web, debe estar hospedada en un **servidor**.  
El servidor recibe las solicitudes de los clientes y devuelve los recursos solicitados (páginas, datos, archivos).

## Visualización local

Herramientas como **Visual Studio Code** junto con la extensión **Live Preview** permiten visualizar aplicaciones web de manera local antes de publicarlas en un servidor.  
Esto facilita la depuración y el desarrollo.

## Puertos HTTP y HTTPS

- **HTTP (puerto 80):** Comunicación sin cifrado.  
- **HTTPS (puerto 443):** Comunicación cifrada mediante TLS/SSL, garantizando seguridad y autenticación.  
La diferencia principal radica en la protección de los datos transmitidos.

## Evolución del protocolo HTTP

- **HTTP/1.0:** Primer estándar, limitado en eficiencia.  
- **HTTP/1.1:** Introdujo conexiones persistentes y mejoras en rendimiento.  
- **HTTP/2:** Optimización con multiplexación y compresión de encabezados.  
- **HTTP/3:** Basado en el protocolo QUIC, mejora la velocidad y seguridad en conexiones modernas.

## Inspección de solicitudes HTTP

- **CURL:** Herramienta de línea de comandos para realizar solicitudes HTTP y analizar respuestas.  
- **DevTools (navegadores):** Permiten inspeccionar solicitudes, respuestas, encabezados y tiempos de carga.

## Estructura de una solicitud HTTP

Una solicitud HTTP incluye:
- **Método:** Define la acción a realizar.  
  - **GET:** Obtener recursos.  
  - **POST:** Enviar datos al servidor.  
  - **PUT:** Actualizar recursos existentes.  
  - **DELETE:** Eliminar recursos.  
- **URL:** Dirección del recurso solicitado.  
- **Encabezados:** Información adicional sobre la solicitud (ejemplo: tipo de contenido, autenticación).  
- **Cuerpo (body):** Datos enviados en la solicitud (principalmente en POST y PUT).

## Encabezados HTTP y content-type

Los **encabezados HTTP** transmiten metadatos sobre la solicitud y la respuesta.  
El **Content-Type** especifica el formato de los datos enviados o recibidos:  
- `text/html` → páginas web.  
- `application/json` → datos estructurados en JSON.  
- `multipart/form-data` → envío de archivos.  

Estos elementos garantizan que cliente y servidor interpreten correctamente la información.
