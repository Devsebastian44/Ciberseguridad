## Introducción

Un **servidor Samba** es un software que permite compartir archivos e impresoras entre sistemas **Windows y Linux** dentro de una red. Implementa el protocolo **SMB (Server Message Block)**, utilizado por Windows para compartir recursos.

## Instalamos el paquete

```bash
sudo apt-get install samba -y
```
## Configuración

sudo nano /etc/samba/smb.conf    y copiaremos el siguiente código en la última línea de comando

```bash
[servidor]
path = /home/usuario/servidor
browseable = yes
create mask = 0777
directory mask = 0777
writable = yes
hosts allow = 10.10.10.14  esto es opcional ya que sirve para seleccionar las IP que quiero que se conecte
```

![[Programación/DevOps/Administración de Servidores Linux/Servidor Samba/Img/Imagen1.png]]

## Configuración de red en SAMBA

En caso de tener dos adaptadores de red y queremos configurar para que SAMBA escuche a uno solo debemos configurar lo siguiente

sudo nano /etc/samba/smb.conf    y configuramos el nombre del adaptador y descomentamos

![[Programación/DevOps/Administración de Servidores Linux/Servidor Samba/Img/Imagen2.png]]

## Creamos el directorio donde se va alojar los archivos

```bash
sudo mkdir servidor

sudo chmod 777 servidor
```

## Configuramos usuarios para acceder al servidor

```bash
sudo useradd Usuario

sudo smbpasswd -a Usuario
```

## Reiniciamos el servicio Samba

```bash
sudo service smbd restart
```
