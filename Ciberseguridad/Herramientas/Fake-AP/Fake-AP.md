## Introducción

Fake AP permite crear puntos de acceso Wi-Fi falsos para simular redes legítimas, con el fin de analizar el comportamiento de los usuarios, evaluar la seguridad y realizar pruebas de suplantación o recolección de datos.

---

## Requisitos

- Kali Linux
- Adaptador TP-Link TL-WN722N

---

## Configuración

### Instalación de servicios

Primero instalamos los servicios **hostapd** y **dnsmasq**:

```bash
sudo apt-get install hostapd dnsmasq -y
```

---

### Configuración de archivos

#### hostapd.conf

```conf
interface=wlan0
driver=nl80211
ssid=Wiifi-nombre # Nombre de la red
hw_mode=g
channel=7
macaddr_acl=0
ignore_broadcast_ssid=0
ignore_broadcast_ssid=Wifiwpa=2
wpa_passphrase=contraseña # Contraseña de la red
wpa_key_mgmt=WPA-PSK
wpa_pairwise=CCMP
wpa_group_rekey=86400
ieee80211n=1
wme_enabled=1
```

#### dnsmasq.conf

```conf
interface=wlan0
dhcp-range=192.168.1.2,192.168.1.30,255.255.255.0,12h
dhcp-option=3,192.168.1.1
dhcp-option=6,192.168.1.1
server=8.8.8.8
log-facility=/home/usuario/dnsmasq.log
log-queries
log-dhcp
listen-address=127.0.0.1
```

---

### Configuración para obtener credenciales

```bash
airmon-ng start wlan0
ifconfig wlan0 up 192.168.1.1 netmask 255.255.255.0
route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.1.1
iptables --table nat --append POSTROUTING --out-interface eth0 -j MASQUERADE
iptables --append FORWARD --in-interface wlan0 -j ACCEPT
```

---

### Ejecución de servicios

En una terminal:

```bash
sudo su
hostapd hostapd.conf
```

En otra terminal:

```bash
sudo su
dnsmasq -C dnsmasq.conf -d
```

---
