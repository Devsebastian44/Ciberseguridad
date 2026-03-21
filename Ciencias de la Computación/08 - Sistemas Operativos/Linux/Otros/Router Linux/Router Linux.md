## Configuración de las tarjetas de red  

Configurar dos tarjetas de red en la máquina virtual: 

- **Adaptador Puente**  
- **Red Interna** 

![[Programación/Sistemas Operativos/Linux/Otros/Router Linux/Img/Imagen1.png]]

Luego, editamos el siguiente archivo:

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

Y copiamos el siguiente código:

```bash
network:
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
       addresses: [10.10.10.1/24]
       #gateway4: 192.168.1.1
       nameservers:
         addresses: [8.8.8.8, 8.8.4.4]
  version: 2
```

![[Programación/Sistemas Operativos/Linux/Otros/Router Linux/Img/Imagen2.png]]

Aplicamos los cambios:

```bash
sudo netplan apply
ip rou
```

## Habilitar IP Forwarding

```bash
sudo cat /proc/sys/net/ipv4/ip_forward
sudo nano /etc/sysctl.conf #
```

descomentamos la siguiente línea de código

![[Programación/Sistemas Operativos/Linux/Otros/Router Linux/Img/Imagen3.png]]

aplicamos los cambios:

```bash
sudo sysctl -p /etc/sysctl.conf
sudo cat /proc/sys/net/ipv4/ip_forward
```

## Configuración de Iptables

```bash
sudo iptables -L
sudo iptables -L -nv -t nat
sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
sudo apt-get install iptables-persistent
sudo netfilter-persistent save
```

Luego de esto configurar otra máquina virtual con red interna y poner la puerta de enlace la IP de la red interna del router Linux.

```bash
auto eth2
iface eth2 inet static
    address 10.10.10.2
    netmask 255.255.255.0
    gateway 10.10.10.1
```