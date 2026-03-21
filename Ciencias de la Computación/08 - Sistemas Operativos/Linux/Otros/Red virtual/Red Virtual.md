# Configurar dos tarjetas de red en una máquina virtual

## Configuramos el siguiente archivo

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

Y copiamos el siguiente código:

```bash
network:
  ethernets:
    enp0s3:
     addresses: [192.168.1.18/24]
     gateway4: 192.168.1.1
     nameservers:
      addresses: [8.8.8.8, 8.8.4.4]
    enp0s8:
     addresses: [10.0.2.15/24]
     gateway4: 10.0.2.1
     nameservers:
      addresses: [8.8.8.8, 8.8.4.4]
  version: 2
```

## Configuración en Debian

```bash
auto eth0
iface eth0 inet static
    address 192.168.1.20
    netmask 255.255.255.0
    gateway 192.168.1.1

auto eth1
iface eth1 inet static
    address 10.0.2.17
    netmask 255.255.255.0
```


