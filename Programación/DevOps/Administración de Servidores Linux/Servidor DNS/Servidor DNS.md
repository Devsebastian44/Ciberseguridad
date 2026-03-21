## Introducción

Un **servidor DNS (Domain Name System)** es un sistema que traduce los nombres de dominio (como `google.com`) en direcciones IP (como `142.250.217.78`). Esto es necesario porque los dispositivos en la red se comunican a través de direcciones IP, pero los nombres de dominio son más fáciles de recordar para los humanos.
## Instalamos el paquete

```bash
sudo apt install bind9 bind9-utils -y
```

## Configuración

```bash
sudo ufw status

sudo ufw allow bind9

sudo systemctl status bind9
```

sudo nano /etc/bind/named.conf.options y copiamos el siguiente código

```bash
listen-on { any; };
allow-query { localhost; 10.10.10.0/24; };   aquí ponemos la IP de la subred
```

![[Programación/DevOps/Administración de Servidores Linux/Servidor DNS/Img/Imagen1.png]]

sudo nano /etc/default/named

![[Programación/DevOps/Administración de Servidores Linux/Servidor DNS/Img/Imagen2.png]]

```bash
sudo named-checkconf

sudo systemctl restart bind9
```

sudo nano /etc/bind/named.conf.local   y copiamos el siguiente código

```bash
zone "router.local" IN {
        type master;
        file "/etc/bind/zonas/db.router.local";

};

zone "10.10.10.in-addr-.arpa" {  aquí debe ir la dirección IP inversa
       type master;
       file "/etc/bind/zonas/db.10.10.10";  aquí debe ir la dirección IP inversa

};
```

![[Programación/DevOps/Administración de Servidores Linux/Servidor DNS/Img/Imagen3.png]]

Guardamos y escribimos los siguientes comandos

```bash
sudo mkdir /etc/bind/zonas

sudo cp /etc/bind/db.local /etc/bind/zonas/db.router.local
```

sudo nano /etc/bind/zonas/db.router.local   y nos debe quedar así

![[Programación/DevOps/Administración de Servidores Linux/Servidor DNS/Img/Imagen4.png]]

```bash
sudo cp /etc/bind/zonas/db.router.local /etc/bind/zonas/db.10.10.10

sudo nano /etc/bind/zonas/db.10.10.10
```

![[Programación/DevOps/Administración de Servidores Linux/Servidor DNS/Img/Imagen5.png]]

```bash
sudo named-checkzone router.local /etc/bind/zonas/db.router.local

sudo named-checkzone 10.10.10.in-addr.arpa /etc/bind/zonas/db.10.10.10   aquí debe ir la dirección IP inversa

sudo systemctl restart bind9
```

sudo nano /etc/resolv.conf   y nos debe quedar así

![[Imagen6.png]]

## Creamos el backup y hacemos permanente los cambios

```bash
sudo cp /etc/resolv.conf /etc/resolv.conf.bak

sudo chattr +i /etc/resolv.conf.bak

sudo rm /etc/resolv.conf

sudo cp /etc/resolv.conf.bak /etc/resolv.conf
```

![https://www.youtube.com/watch?v=jq5potgQ7_k](https://www.youtube.com/watch?v=jq5potgQ7_k)