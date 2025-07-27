# Tcpdump

TCPdump es una herramienta de captura de paquetes de red que se ejecuta en la línea de comandos de sistemas Unix y Linux. Utiliza la biblioteca libpcap para capturar paquetes de datos que pasan a través de una interfaz de red específica. TCPdump es muy flexible y permite a los usuarios especificar filtros para capturar solo el tráfico de interés.

### Instalación

```
sudo apt-get install tcpdump
```

### USO:

**Ejecución básica:** Para capturar tráfico en una interfaz de red específica, ejecuta el siguiente comando (reemplaza interfaz con el nombre de tu interfaz de red, por ejemplo, eth0):

```
sudo tcpdump -i interfaz
```

Si queremos especificar todas las interfaces de red, para capturar todo el tráfico de todas ellas a la vez, entonces tienes que poner la siguiente orden:

```
sudo tcpdump -i any
```

Si quieres capturar solamente un cierto número de paquetes, entonces deberás poner la siguiente orden:

```
sudo tcpdump -c NUMERO_PAQUETES
```

**Capturar tráfico por IP o subred:** tcpdump nos permite filtrar por direcciones IP e incluso subredes, para ello, podemos poner la siguiente orden:

```
sudo tcpdump -i NOMBRE_INTERFAZ host IP
```

**Capturar tráfico por puerto y rangos:** En el caso de que quieras filtrar por puertos, ya sea un puerto únicamente o un rango de puertos, puedes hacerlo de la siguiente forma:

```
sudo tcpdump -i NOMBRE_INTERFAZ port NUMERO_PUERTO
```

```
sudo tcpdump -i NOMBRE_INTERFAZ portrange PUERTO_INICIO PUERTO_FIN
```

**Filtrado de paquetes:** Puedes aplicar filtros para capturar solo el tráfico que te interesa. Por ejemplo, para capturar solo paquetes ICMP (ping), puedes usar:

```
sudo tcpdump -i interfaz icmp
```

**Guardar la captura en un archivo:** Puedes guardar la salida de TCPdump en un archivo para su análisis posterior. Por ejemplo:

```
sudo tcpdump -i interfaz -w archivo.pcap
```

**Lectura de archivos de captura:** Para analizar un archivo de captura previamente guardado, puedes utilizar el siguiente comando:

```
sudo tcpdump -i interfaz -w archivo.pcap
```