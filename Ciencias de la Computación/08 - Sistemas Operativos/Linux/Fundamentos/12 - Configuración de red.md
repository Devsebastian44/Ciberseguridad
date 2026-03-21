# Conceptos básicos de red

## Protocolos de red

- **TCP/IP**: Protocolo de comunicación principal
- **IPv4**: Direcciones de 32 bits (192.168.1.1)
- **IPv6**: Direcciones de 128 bits (2001:db8::1)
- **DHCP**: Asignación automática de direcciones IP
- **DNS**: Sistema de nombres de dominio

## Tipos de direcciones IP

- **IP pública**: Accesible desde Internet
- **IP privada**: Uso interno en redes locales
    - Clase A: 10.0.0.0/8
    - Clase B: 172.16.0.0/12
    - Clase C: 192.168.0.0/16


# Configuración de interfaces de red

## Comandos básicos de red

```bash
# Mostrar interfaces de red
ip addr show
ifconfig

# Mostrar tabla de ruteo
ip route show
route -n

# Estadísticas de red
netstat -i
ss -i

# Configurar IP estática temporal
ip addr add 192.168.1.100/24 dev eth0
ifconfig eth0 192.168.1.100 netmask 255.255.255.0

# Activar/desactivar interfaz
ip link set eth0 up
ip link set eth0 down
```

## Configuración permanente

Debian/Ubuntu (/etc/network/interfaces):

```bash
# Configuración DHCP
auto eth0
iface eth0 inet dhcp

# Configuración estática
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
```

Red Hat/CentOS (/etc/sysconfig/network-scripts/ifcfg-eth0):

```bash
# Configuración estática
DEVICE=eth0
BOOTPROTO=static
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=8.8.4.4
ONBOOT=yes
```

## NetworkManager

```bash
# Estado de NetworkManager
nmcli general status

# Listar conexiones
nmcli connection show

# Crear conexión
nmcli connection add type ethernet con-name "mi-conexion" ifname eth0

# Modificar conexión
nmcli connection modify "mi-conexion" ipv4.addresses 192.168.1.100/24

# Activar conexión
nmcli connection up "mi-conexion"

# Configurar DNS
nmcli connection modify "mi-conexion" ipv4.dns "8.8.8.8 8.8.4.4"
```


# Configuración de DNS

## Archivo /etc/resolv.conf

```bash
# Configurar servidores DNS
nameserver 8.8.8.8
nameserver 8.8.4.4
search example.com
```

## Archivo /etc/hosts

```bash
# Resolución local de nombres
127.0.0.1   localhost
192.168.1.10   servidor.local servidor
```


# Herramientas de diagnóstico

## Conectividad básica

```bash
# Probar conectividad
ping google.com

# Probar conectividad IPv6
ping6 google.com

# Trazar ruta
traceroute google.com
tracepath google.com

# Resolución DNS
nslookup google.com
dig google.com

# Información de dominio
whois google.com
```

## Puertos y servicios

```bash
# Puertos abiertos
netstat -tuln
ss -tuln

# Conexiones activas
netstat -tun
ss -tun

# Procesos usando puertos
netstat -tulpn
ss -tulpn

# Probar puerto específico
telnet servidor.com 80
nc -zv servidor.com 80
```


# Cortafuegos (Firewall)

## iptables

```bash
# Ver reglas actuales
iptables -L

# Permitir puerto específico
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Bloquear IP específica
iptables -A INPUT -s 192.168.1.100 -j DROP

# Guardar reglas
iptables-save > /etc/iptables/rules.v4

# Restaurar reglas
iptables-restore < /etc/iptables/rules.v4
```

## ufw (Ubuntu)

```bash
# Habilitar firewall
ufw enable

# Estado del firewall
ufw status

# Permitir puerto
ufw allow 22
ufw allow ssh

# Denegar puerto
ufw deny 80

# Eliminar regla
ufw delete allow 22
```

## firewalld (Red Hat/CentOS)

```bash
# Estado del firewall
firewall-cmd --state

# Zonas disponibles
firewall-cmd --get-zones

# Zona por defecto
firewall-cmd --get-default-zone

# Permitir servicio
firewall-cmd --add-service=ssh --permanent

# Permitir puerto
firewall-cmd --add-port=80/tcp --permanent

# Recargar configuración
firewall-cmd --reload
```