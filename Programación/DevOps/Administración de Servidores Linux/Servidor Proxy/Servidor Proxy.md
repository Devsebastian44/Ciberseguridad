## Introducción

Un **servidor Proxy** es un intermediario entre un cliente (usuario) e internet. Actúa como un **puente entre el usuario y los servidores a los que accede**, gestionando y filtrando las solicitudes de conexión.

## Instalacion

```bash
sudo apt-get install squid
```

## Configuración

```bash
sudo systemctl start squid

sudo systemctl enable squid
```

sudo nano /etc/squid/squid.conf  y pulsamos CTRL + W y buscamos http_access deny all y modificamos la siguiente parte

![[Programación/DevOps/Administración de Servidores Linux/Servidor Proxy/Img/Imagen1.png]]

```bash
sudo systemctl restart squid
```

# Configuración de Sitios

## Creamos un archivo con los sitios que vamos a bloquear

sudo nano /etc/squid/blocked.acl  y escribimos los sitos que vamos a bloquear

```
.facebook.com

.youtube.com
```

## Luego configuramos el archivo de squid

sudo nano /etc/squid/squid.conf  y pulsamos CTRL + W y buscamos acl localnet y copiamos el siguiente código

```bash
acl blocked_websites dstdomain "/etc/squid/blocked.acl"

http_access deny blocked_websites
```

![[Programación/DevOps/Administración de Servidores Linux/Servidor Proxy/Img/Imagen2.png]]

```bash
sudo systemctl restart squid
```

Luego configuramos el la maquina cliente el proxy y ponemos como puerto 3128


