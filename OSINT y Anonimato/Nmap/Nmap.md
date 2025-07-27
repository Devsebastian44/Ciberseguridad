# Escaneo de puertos con Nmap


Nmap es una herramienta de código abierto para exploración de redes y auditoría de seguridad. Permite analizar rápidamente redes grandes o equipos individuales, utilizando paquetes IP "crudos" para identificar dispositivos activos, servicios que ofrecen (con nombre y versión), sistemas operativos que usan, y tipos de cortafuegos o filtros presentes, entre otras características.

## Instalación

```
sudo apt-get install nmap
```

## USO

### Escaneo de red

Supongamos que el número IP de tu máquina virtual es 192.168.172.136. Entonces, para escanear la red de dicha dirección, habrá que hacer un análisis de todo el rango de direcciones IP que irá desde 192.168.172.0 hasta 192.168.172.255. Para hacer esto en Nmap, ejecuta el siguiente comando en la consola de Kali:

```
nmap -sn 192.168.172.0/24
```

### Escaneo de Puertos

Con nmap tenemos una herramienta especializada en analizar los puertos de los sistemas informáticos, obteniendo información sobre si están abiertos, cerrados o protegidos con cortafuegos. Esto se puede hacer con multitud de finalidades, como saber que servicios se están ofreciendo desde un equipo por los administradores o por seguridad, buscando solventar algún problema que pueda llegar en forma de vulnerabilidad.

**Estado de los puertos con Nmap**

* **Open:** una aplicación está activamente aceptando conexiones TCP o UDP. El puerto está abierto y se puede utilizar, los pentesters podrán utilizar este puerto abierto para explotar el sistema. Es el estado por defecto si no tenemos ningún firewall bloqueando accesos.

* **Closed:** un puerto que está cerrado es accesible porque responde a Nmap, sin embargo, no hay ninguna aplicación funcionando en dicho puerto. Es útil para descubrir que un host está levantado, o como parte de la detección de un sistema operativo. De cara al administrador del sistema, es recomendable filtrar estos puertos con el firewall para que no sean accesibles. De cara al pentester, es recomendable dejar estos puertos “cerrados” para analizar más tarde, por si ponen algún servicio nuevo.

* **Filtered:** en este estado Nmap no puede determinar si el puerto está abierto, porque hay un firewall filtrando los paquetes de Nmap en dicho puerto. Estos puertos filtrados son los que aparecerán cuando tengamos un firewall activado. Nmap intentará en varias ocasiones intentar conectar, lo que hace que el escaneo de puertos sea bastante lento.

* **Open| Filtered:** Nmap no sabe si el puerto está abierto o filtrado. Esto ocurre porque el puerto abierto no envía ninguna respuesta, y dicha falta de respuesta podría ser por el firewall. Este estado aparece cuando usamos UDP y IP, y utilizamos escaneos FIN, NULL y Xmas.

* **Closed | Filtered:** en este estado no se sabe si el puerto está cerrado o filtrado. Solo se usa este estado en el IP Idle Scan.


**Escaneo rápido de puertos**

```
nmap 192.168.1.3
```

El programa nos devolverá los puertos que se encuentran abiertos en el equipo objetivo.


**Realizar escaneo de un rango de puertos**

En lugar de realizar un escaneo de todos los puertos, podemos establecer un rango de puertos a comprobar. Para eso ejecutaremos:

Si queremos realizar un escaneo de puertos desde el puerto 20 TCP hasta el puerto 500 TCP en la dirección IP 192.168.1.3, basta con ejecutar la siguiente orden:

```
nmap -p 20-500 192.168.1.3
```

**Detectar el sistema operativo**

Podemos indicar a Nmap que detecte el sistema operativo. Esto lo realiza enviando paquetes y analizando la forma en que los devuelve, siendo en cada sistema totalmente diferente.

```
nmap -A 192.168.1.3
```

**Listado de todos los comandos**

Esta herrmienta es realmente completa, hasta el momento hemos utilizado los comandos básicos para descubrir hosts y también para ver si tiene los puertos abiertos, sin embargo, esto no se queda así, y tenemos un gran listado de comandos para exprimir al máximo esta herramienta.

* **Descubrir sistemas**

  * -PS n tcp syn ping
  * -PA n ping TCP ACK
  * -PU n ping UDP
  * -PM Netmask Req
  * -PP Timestamp Req
  * -PE Echo Req
  * -sL análisis de listado
  * -PO ping por protocolo
  * -PN No hacer ping
  * -n no hacer DNS
  * -R Resolver DNS en todos los sistemas objetivo
  * -traceroute: trazar ruta al sistema (para topologías de red)
  * -sP realizar ping

* **Tipos de Escaneo:**
  * TCP SYN (-sS) 
  * UDP ( -sU ) 
  * TCP ACK ( -sA ) 
  * TCP NULL ( -sN ) 
  * TCP XMAS ( -sX ) 
  * TCP FIN ( -sF ) 
  * TCP IDLE ( -sI )
  * -O Información del sistema operativo 
  * -v Verbosity 
  * -sV Información de las versiones 
  * -A Activa la detección de sistema operativo, de versiones y traceroute 
  * -Pn No ping 
  * -p- escaneo de todos los puertos
  * -p número de puerto

* **Modos y Tiempos**
-T 0,1,2,3,4,5 : Tiempo y envio de paquetes 
paranoid 0 
  * sneaky 1 
  * polite 2 
  * normal 3 
  * aggressive 4 
  * insane 5 
 
Los modos 1 y 2 se utilizan para evadir IDS 

* **-sS** análiza utilizando TCP SYN: Este tipo de escaneo, está basado en la velocidad de escaneo, de ahí la versatilidad que mencionamos anteriormente, ya que permite escanear miles de puertos por segundo en una red que se encuentre desprotegida o carezca de un firewall.

* **-sT** análisis utilizando TCP CONNECT: Este tipo de exploración, podríamos decir que es la que se utiliza principalmente, sobre todo cuando no podemos ejecutar un escaneo tipo SYN

* **-sU** análisis utilizando UDP: Este tipo de escaneo es bastante simple, suele utilizarse sobre todo cuando queremos realizar un seguimiento de puertos como los DNS, SNMP y DHCP en nuestra red.

* **Duración y ejecución:**
  * -T0 paranoico
  * -T1 sigiloso
  * -T2 sofisticado
  * -T3 normal
  * -T4 agresivo
  * -T5 locura
  * –min-hostgroup
  * –max-hostgroup
  * –min-rate
  * –max-rate
  * –min-parallelism
  * –max-parallelism
  * –min-rtt-timeout
  * –max-rtt-timeout
  * –initial-rtt-timeout
  * –max-retries
  * –host-timeout –scan-delay

* **Detección de servicios y versiones**
  * -sV: detección de la versión de servicios
  * –all-ports no excluir puertos
  * –version-all probar cada exploración
  * –version-trace rastrear la actividad del análisis de versión
  * -O detección del Sistema. Operativo
  * –fuzzy detección del SO

* **Evasión de Firewalls/IDS**
  * -f fragmentar paquetes
  * -D d1,d2 encubrir análisis con señuelos
  * -S ip falsear dirección origen
  * –g source falsear puerto origen
  * –randomize-hosts orden
  * –spoof-mac mac cambiar MAC de origen
  
* **Formatos de salida**
  * -oN guardar en formato normal
  * -oX guardar en formato XML
  * -oG guardar en formato para posteriormente usar Grep
  * -oA guardar en todos los formatos anteriores

Nmap es una herramienta útil, que nos puede dar muchas facilidades a la hora de escanear redes.