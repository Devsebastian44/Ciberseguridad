## Introducción

TCPdump es una herramienta de captura de paquetes de red que se ejecuta en la línea de comandos de sistemas Unix y Linux. Utiliza la biblioteca **libpcap** para capturar paquetes de datos que pasan a través de una interfaz de red específica.

Es muy flexible y permite a los usuarios especificar filtros para capturar solo el tráfico de interés.

---

## Instalación

```bash
sudo apt-get install tcpdump
```

---

## Uso

### Ejecución básica

Para capturar tráfico en una interfaz de red específica:

```bash
sudo tcpdump -i interfaz
```

Para capturar tráfico en todas las interfaces:

```bash
sudo tcpdump -i any
```

Para capturar solo un número específico de paquetes:

```bash
sudo tcpdump -c NUMERO_PAQUETES
```

---

### Capturar tráfico por IP o subred

```bash
sudo tcpdump -i NOMBRE_INTERFAZ host IP
```

---

### Capturar tráfico por puerto y rangos

Por un puerto específico:

```bash
sudo tcpdump -i NOMBRE_INTERFAZ port NUMERO_PUERTO
```

Por un rango de puertos:

```bash
sudo tcpdump -i NOMBRE_INTERFAZ portrange PUERTO_INICIO PUERTO_FIN
```

---

### Filtrado de paquetes

Para capturar solo paquetes ICMP (ping):

```bash
sudo tcpdump -i interfaz icmp
```

---

### Guardar la captura en un archivo

```bash
sudo tcpdump -i interfaz -w archivo.pcap
```

---

### Lectura de archivos de captura

Para analizar un archivo previamente guardado:

```bash
sudo tcpdump -r archivo.pcap
```

---
