## Introducción

Un **servidor web** es un software o hardware que procesa y responde a las solicitudes de los clientes (navegadores web) a través del protocolo **HTTP (Hypertext Transfer Protocol)** o **HTTPS (HTTP seguro)**. Su función principal es **almacenar, procesar y entregar** páginas web a los usuarios cuando estos ingresan una URL en su navegador. Puede referirse tanto al **software** que gestiona las peticiones web (como Apache o Nginx) como al **hardware** en el que se ejecuta dicho software.

## Instalar el paquete

```bash
sudo apt-get install apache2 -y

sudo apt-get install apache2-doc
```

## Modificar la página web por defecto

```bash
sudo su

mv /var/www/html/index.html  /var/www/html/prede-index.html
```

nano /var/www/html/index.html  y copiamos el siguiente código

```html
<!DOCTYPE html>
<html>
   <head>
    <title>Programig</title>
  </head>
   <body>
       <h1>WEB por defecto</h1>
       <h2>Programing</h2>
        <p>Funcionando Correctamente</p>
   </body>
</html>
```

## Servidores Virtuales por nombre

```bash
cd /var/www

mkdir 1programing

mkdir 2programing

mkdir 3programing

nano 1programing/index.html

nano 2programing/index.html
```

esto ira primero en 1programing y ponemos los mismo, pero editando y poniendo en 2programing

```html
<!DOCTYPE html>
<html>
   <head>
    <title>1 Programig</title>
  </head>
   <body>
       <h1>1Programing</h1>
        <p>Dominio www.1programing.es</p>
   </body>
</html>
```

```bash
cp /etc/apache2/sites-available/000-default.conf  /etc/apache2/sites-available/1programing.conf
```

nano /etc/apache2/sites-available/1programing.conf   borramos todo y copiamos el siguiente código  y así en los demás archivos pero cambiando por 2programing

```bash
<VirtualHost *:80>
        ServerName 1programing.es
        ServerAdmin root@1programing.es
        ServerAlias www.1programing.es
        DocumentRoot /var/www/1programing
        DirectoryIndex index.html
</VirtualHost>
```

```bash
a2ensite 1programing.conf

a2ensite 2programing.conf

a2dissite 000-default.conf

systemctl reload apache2
```

nano /etc/hosts  y copiamos el siguiente código

```bash
10.10.10.6 www.1programing.es

10.10.10.6 www.2programing.es
```

![[Programación/DevOps/Administración de Servidores Linux/Servidor Web/Img/Imagen1.png]]

```bash
cd /var/www/3programing/
```

nano index.html   y copiamos el siguiente código

```html
<!DOCTYPE html>
<html>
   <head>
    <title>3 Programig</title>
  </head>
   <body>
       <h1>3Programing 8081</h1>
        <p>Solo por el puerto 8081</p>
   </body>
</html>
```

nano /etc/apache2/sites-available/3programing.conf  y copiamos el siguiente código

```bash
<VirtualHost *:8081>
        ServerName 3programing.es
        ServerAdmin root@3programing.es
        ServerAlias www.3programing.es
        DocumentRoot /var/www/3programing
        DirectoryIndex index.html
</VirtualHost>
```

nano /etc/apache2/ports.conf   para abrir el puerto 8081 escribimos lo siguiente
```bash
Listen 8081
```

```bash
cd ..

a2dissite *

systemctl reload apache2

a2ensite 1programing.conf

a2ensite 3programing.conf
```


