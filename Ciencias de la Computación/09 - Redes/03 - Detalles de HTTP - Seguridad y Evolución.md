## Códigos de estado HTTP

El protocolo HTTP utiliza **códigos de estado** para indicar el resultado de una solicitud.  
Se dividen en cinco categorías principales:

- **1xx (Informativos):** Indican que la solicitud fue recibida y el proceso continúa.  
- **2xx (Éxito):** La solicitud fue procesada correctamente (ejemplo: 200 OK).  
- **3xx (Redirección):** El recurso solicitado se encuentra en otra ubicación (ejemplo: 301 Moved Permanently).  
- **4xx (Errores del cliente):** Problemas en la solicitud del cliente (ejemplo: 404 Not Found).  
- **5xx (Errores del servidor):** Fallos en el servidor al procesar la solicitud (ejemplo: 500 Internal Server Error).

## Encabezados HTTP

Los **encabezados** transmiten información adicional en las solicitudes y respuestas.  
Ejemplos importantes:
- **Content-Type:** Define el formato de los datos (ejemplo: `application/json`, `text/html`).  
- **Authorization:** Permite enviar credenciales para autenticar al cliente.  
Estos encabezados son esenciales para la correcta interpretación y seguridad de la comunicación.

## Herramientas de inspección

- **Postman:** Plataforma que permite construir, enviar y analizar solicitudes HTTP de manera gráfica.  
- **DevTools y CURL:** Complementan el análisis mostrando encabezados, cuerpos y tiempos de respuesta.

## HTTP, HTTPS y HTTP/3

- **HTTP:** Comunicación sin cifrado, más vulnerable a ataques.  
- **HTTPS:** Añade seguridad mediante **TLS/SSL**, protegiendo la confidencialidad e integridad de los datos.  
- **HTTP/3:** Evolución moderna basada en el protocolo **QUIC**, que mejora la velocidad y la seguridad en conexiones actuales.

## Cookies y sesiones

El almacenamiento de información en el cliente mediante **cookies** y **sesiones** permite:  
- Recordar preferencias del usuario.  
- Mantener sesiones activas en aplicaciones web.  
- Mejorar la experiencia personalizada.  
Sin embargo, requieren medidas de seguridad para evitar robo de información.

## Seguridad en operaciones web

La seguridad es fundamental en aplicaciones modernas para proteger contra ataques como:  
- **Phishing**  
- **Man-in-the-Middle (MITM)**  
- **Inyección de código (SQL Injection, XSS)**  

## Protocolo TLS

El **TLS (Transport Layer Security)** es la base de la seguridad en HTTPS.  
Proporciona:
- **Cifrado:** Protege la información transmitida.  
- **Integridad:** Garantiza que los datos no sean alterados.  
- **Autenticación:** Verifica la identidad del servidor.

## Certificados digitales

Los **certificados digitales** validan la autenticidad de un sitio web.  
- Emitidos por **Autoridades Certificadoras (CA)**.  
- Permiten establecer conexiones seguras mediante HTTPS.  
- Son esenciales para la confianza del usuario y la protección contra sitios falsos.
