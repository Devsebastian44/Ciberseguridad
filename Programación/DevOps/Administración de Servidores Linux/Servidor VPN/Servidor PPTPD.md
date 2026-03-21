## Introducción

PPTPD (**Point-to-Point Tunneling Protocol Daemon**) es un servidor que implementa el protocolo **PPTP (Point-to-Point Tunneling Protocol)** en sistemas Linux y Unix. PPTP es un protocolo de red que permite establecer **redes privadas virtuales (VPN)** mediante el encapsulamiento del tráfico de red en túneles seguros.

## Instalar el paquete

```bash
sudo apt-get install pptpd -y
```

## Configuración

```bash
sudo systemctl enable pptpd
```

sudo nano /etc/pptpd.conf  y luego configuramos la siguiente línea de código

![[Programación/DevOps/Administración de Servidores Linux/Servidor VPN/Img/Imagen1.png]]

sudo nano /etc/ppp/pptpd-options  para cambiar el nombre y DNS del servidor

![[Programación/DevOps/Administración de Servidores Linux/Servidor VPN/Img/Imagen3.png]]

![[Programación/DevOps/Administración de Servidores Linux/Servidor VPN/Img/Imagen3.png]]

sudo nano /etc/ppp/chap-secrets   para cambiar usuario y contraseña

![[Programación/DevOps/Administración de Servidores Linux/Servidor VPN/Img/Imagen4.png]]

sudo nano /etc/sysctl.conf  y descomentamos la siguiente línea de comandos

![[Programación/DevOps/Administración de Servidores Linux/Servidor VPN/Img/Imagen5.png]]

sudo nano /etc/systemd/system/rc-local.service   y copíamos el siguiente código

```bash
[Unit]
Description=/etc/rc.local Compatibility
ConditionPathExists=/etc/rc.local

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=multi-user.target[Unit]
Description=/etc/rc.local Compatibility
ConditionPathExists=/etc/rc.local

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=multi-user.target
```

sudo nano /etc/rc.local   y copiamos el siguiente código

```bash
#!/bin/bash

iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o enp0s3 -j MASQUERADE
```

```bash
sudo service pptpd status

sudo service pptpd start
```

Por último si al conectarte al tu servidor VPN se cae el internet te recomiendo ver el video

![https://www.youtube.com/watch?v=NU5-wX4z5lQ](https://www.youtube.com/watch?v=NU5-wX4z5lQ)





