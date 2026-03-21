## Introducción

Un **servidor DHCP (Dynamic Host Configuration Protocol)** es un servicio que **asigna automáticamente direcciones IP** y otros parámetros de red a dispositivos dentro de una red. Esto evita la necesidad de configurar manualmente cada dispositivo.

Primero debemos instalar el paquete en el Router Linux

Instalamos el paquete:

```bash
sudo apt-get install isc-dhcp-server
```

## Configuración

sudo nano /etc/dhcp/dhcpd.conf   y copiamos el siguiente código

```bash
#DHCP PARA EL ROUTER LINUX
group router{
subnet 10.10.10.0 netmask 255.255.255.0 {
  range 10.10.10.1 10.10.10.20;
  option domain-name-servers 10.10.10.1;
  option domain-name "router.local";
  option subnet-mask 255.255.255.0;
  option routers 10.10.10.1;
  option broadcast-address 10.10.10.255;
   }
host router{
          hardware ethernet 08:00:27:0B:E4:AB;
          fixed-address 10.10.10.4;
   }
}
```

## Configuramos el siguiente archivo

sudo nano /etc/default/isc-dhcp-server en la carpeta DHCP

```bash
INTERFACESv4="enp0s8" (El segundo adaptador de red)
```

## Aplicamos los cambios y reiniciamos el servicio

```bash
sudo dhcpd -t -cf /etc/dhcp/dhcpd.conf

sudo service isc-dhcp-server restart

sudo service isc-dhcp-server status
```