## Verificación con testssl.sh

**testssl.sh** es una herramienta de línea de comandos gratuita que verifica el servicio de un servidor en cualquier puerto para admitir cifrados TLS/SSL, protocolos, fallas criptográficas recientes y más.

---

## Instalación

```bash
sudo apt-get install testssl.sh
```

---

## Uso

### Comando básico

```bash
testssl [options] <URL>
```

### Ejemplo

```bash
testssl https://www.facebook.com
```

### Verificar protocolos activados por STARTTLS

Servicios soportados: ftp, smtp, pop3, imap, xmpp, telnet, ldap, postgres, mysql.

```bash
testssl.sh -t smtp https://www.facebook.com/
```

<p align="center"> <img src="./Img/Ejemplo 1.png"> </p>

<p align="center"> <img src="./Img/Ejemplo 2.png"> </p>

---
