Editar el siguiente archivo

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

Copiar el siguiente código:

```bash
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      addresses: [192.168.1.16/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
```

Luego aplicamos cambios

```bash
sudo netplan apply

sudo netplan generate
```


