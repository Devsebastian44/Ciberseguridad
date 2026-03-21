## Introducción

Un **servidor MySQL** es un sistema de gestión de bases de datos **relacional y de código abierto**, utilizado para almacenar, organizar y gestionar grandes volúmenes de datos. MySQL permite **crear, modificar, eliminar y consultar bases de datos** de manera eficiente.

## Instalamos el paquete

```bash
sudo apt update

sudo apt-get install mysql-server

sudo mysql
```

Luego cambiar la autenticación y los privilegios usuario

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'Password444@';

exit
```

```bash
sudo mysql -u root -p   (Y ponemos las contraseña)
```

Para acceder a una base de datos remota

```mysql
CREATE USER 'usuario'@'%' IDENTIFIED BY 'Password444@';

GRANT ALL PRIVILEGES ON *.* TO 'usuario'@'%' WITH GRANT OPTION;

DROP USER 'root'@'localhost';

CREATE USER 'root'@'localhost' IDENTIFIED BY 'python 444';
```

sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf   y editamos la siguiente línea de código

![[Programación/DevOps/Administración de Servidores Linux/Servidor MySQL/Img/Imagen1.png]]

```bash
sudo service mysql restart
```

Ahora desde nuestra PC accedemos al servidor remoto

```bash
sudo mysql -h 192.168.1.16 -u root -p
```

![https://www.youtube.com/watch?v=uxocMv-AtaU&t=572s](https://www.youtube.com/watch?v=uxocMv-AtaU&t=572s)
