**Nextcloud** es una plataforma de almacenamiento en la nube **autohospedada** y de código abierto que permite sincronizar, compartir y gestionar archivos de manera segura, similar a servicios como **Google Drive, Dropbox o OneDrive**, pero con control total sobre los datos.

# Instalación

```bash 
sudo apt update

sudo apt upgrade

sudo su
```

## Instalar PHP:

```bash 
sudo apt install -y php-cli php-fpm php-json php-intl php-imagick php-pdo php-mysql php-zip php-gd php-mbstring php-curl php-xml php-pear php-bcmath
```

## PHP 8.1

```bash
sudo add-apt-repository ppa:ondrej/php

sudo apt-get install php8.1

sudo apt-get update

sudo apt-get install php8.1 php8.1-common php8.1-mysql php8.1-pgsql php8.1-xml php8.1-mbstring php8.1-curl php8.1-gd php8.1-zip php8.1-intl
```

## Instalar Mysql:

```bash
sudo apt install mysql-server -y
```

## Configurar Mysql

```bash
sudo mysql
```

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'Password444@';

exit

mysql -u root -p (escribir contraseña que pusimos en el anterior comando)

CREATE USER 'nextcloud'@'localhost' IDENTIFIED BY 'Password444@';

CREATE DATABASE nextcloud;

GRANT ALL PRIVILEGES ON nextcloud.* TO ' nextcloud'@'localhost';

FLUSH PRIVILEGES;

exit
```

## Configurar:

```bash
cd /etc/apache2/sites-available/

cp 000-default.conf nextcloud.conf

a2dissite 000-default.conf

systemctl reload apache2
```

nano nextcloud.conf y agregar el siguiente código

```bash
<Directory /var/www/html/nextcloud>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
        SetEnv HOME /var/www/html/nextcloud
        SetEnv HTTP_HOME /var/www/html/nextcloud
        <IfModule mod_dav.c>
          Dav off
        </IfModule>
        </directory>
```

![[Programación/Sistemas Operativos/Linux/Otros/Nextcloud/Img/Imagen1.png]]

```bash
a2enmod rewrite dir mime env headers

service apache2 restart

cd /var/www/html

mkdir nextcloud

chmod 750 nextcloud/

chown www-data:www-data nextcloud/

cd nextcloud/

wget [https://download.nextcloud.com/server/installer/setup-nextcloud.php](https://download.nextcloud.com/server/installer/setup-nextcloud.php)

chown www-data:www-data setup-nextcloud.php

a2ensite nextcloud.conf

service apache2 restart
```

## Configurar directorios

```bash
sudo nano /etc/apache2/apache2.conf   y copiamos el siguiente código en la ultima línea

ServerSignature Off

ServerTokens Prod

service apache2 restart

a2dismod  --force autoindex

service apache2 restart
```

## Acceder desde Internet

Primero tendremos que abrir el Puerto 80 del router luego asignamos la IP de nuestro Servidor Nextcloud, luego de esto configuraremos el siguiente archivo de nuestro servidor

```bash
cd /var/www/html/nextcloud/nextcloud/

nano config/config.php   y agregamos el siguiente codigo

1 => 'TU IP PUBLICA',
```

![[Programación/Sistemas Operativos/Linux/Otros/Nextcloud/Img/Imagen2.png]]

# Onlyoffice Nextcloud

## Configuración
```bash
sudo su
```

nano /etc/php/7.4/apache2/php.ini  y CTRL + W y buscamos  memory_limit

![[Programación/Sistemas Operativos/Linux/Otros/Nextcloud/Img/Imagen3.png]]

```bash
systemctl restart apache2
```

Luego en nextcloud activamos Document Server

**Nota:** Depende la versión de PHP para editar el archivo  /etc/php/7.4/apache2/php.ini