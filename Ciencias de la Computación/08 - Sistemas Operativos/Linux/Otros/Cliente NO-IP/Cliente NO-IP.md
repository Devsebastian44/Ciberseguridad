**NO-IP** es un servicio de **DNS dinámico (Dynamic DNS o DDNS)** que permite asignar un **nombre de dominio fijo** a una dirección IP que cambia constantemente, como las que asignan la mayoría de los proveedores de Internet residencial.
# Requisitos previos  

**NOTA**: Primero debemos crear un host en NO-IP.  
Si queremos configurar otro cliente en otra máquina, debemos desactivar el puerto 80.  

# Instalación  

### Iniciar sesión como root  

```bash
sudo -i
```

## Descargar el Cliente

```bash
cd /usr/local/src
wget https://www.noip.com/client/linux/noip-duc-linux.tar.gz
tar xzf noip-duc-linux.tar.gz
cd noip-2.1.9-1/
```

## Instalar el Cliente

```bash
sudo apt-get install build-essential -y 
sudo apt-get install make
make
make install
```

Ingresamos el usuario y contraseña de nuestra cuenta NO-IP y ponemos `30` y `N` en las preguntas.

## Activar el cliente

```bash
noip2 -S
```

## Configuración en Nextcloud

```bash
cd /var/www/html/nextcloud/nextcloud/
nano config/config.php
```

Agregar:

```bash
1 => 'nubeprivada.hopto.org',  // Dirección del cliente NO-IP
'overwrite.cli.url' => 'http://192.168.1.15/nextcloud',  // IP del servidor
'overwrite.cli.url' => 'nubeprivada.hopto.org/nextcloud',  // Cliente NO-IP
'overwrite.cli.url' => 'http://186.71.81.5/nextcloud',  // Acceso desde Internet
```

![[Programación/Sistemas Operativos/Linux/Otros/Cliente NO-IP/Img/Imagen1.png]]

## Reiniciar Apache

```bash
sudo service apache2 restart
```