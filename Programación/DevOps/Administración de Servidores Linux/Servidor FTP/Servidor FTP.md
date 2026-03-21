## Introducción

Un **servidor FTP (File Transfer Protocol)** es un sistema que permite la **transferencia de archivos** entre un cliente y un servidor a través del protocolo FTP. Se usa para **subir, descargar y gestionar archivos de manera remota** en una red local o en internet.

## Instalamos FTP Server

```bash
sudo apt-get install vsftpd -y
```

## Configuración

```bash
sudo nano /etc/vsftpd.conf
```

Editamos la siguiente línea de código

![[Programación/DevOps/Administración de Servidores Linux/Servidor FTP/Img/Imagen1.png]]

## Reiniciamos

```bash
sudo service vsftpd restart

sudo service vftpd status
```

Luego para acceder a nuestro servidor podemos usar FileZilla, para acceder usamos el usuario y contraseña de nuestra máquina.