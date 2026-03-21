## Escaneo de Puertos con Nmap

**Nmap** es una herramienta de código abierto para exploración de redes y auditoría de seguridad.  
Permite identificar dispositivos activos, servicios, sistemas operativos y tipos de cortafuegos presentes.

---

## Instalación

```bash
sudo apt-get install nmap
```

---

## Uso

### Escaneo de red

```bash
nmap -sn 192.168.172.0/24
```

Analiza todo el rango de direcciones IP desde `192.168.172.0` hasta `192.168.172.255`.

---

### Escaneo de puertos

Nmap analiza puertos abiertos, cerrados o filtrados.

**Estados de puertos:**

- **Open**: aplicación acepta conexiones
- **Closed**: puerto accesible pero sin aplicación activa
- **Filtered**: firewall bloquea paquetes
- **Open|Filtered**: indeterminado (UDP, FIN, NULL, Xmas)
- **Closed|Filtered**: indeterminado (Idle Scan)

**Ejemplos:**

```bash
nmap 192.168.1.3                # Escaneo rápido
nmap -p 20-500 192.168.1.3      # Escaneo de rango
nmap -A 192.168.1.3             # Detectar sistema operativo
```

---

## Listado de Comandos

### Descubrir sistemas

- `-PS` TCP SYN ping
- `-PA` TCP ACK ping
- `-PU` UDP ping
- `-PM` Netmask Req
- `-PP` Timestamp Req
- `-PE` Echo Req
- `-sL` listado
- `-PO` ping por protocolo
- `-PN` sin ping
- `-n` sin DNS
- `-R` resolver DNS
- `--traceroute` trazar ruta
- `-sP` ping scan

---

### Tipos de escaneo

- `-sS` TCP SYN
- `-sU` UDP
- `-sA` TCP ACK
- `-sN` TCP NULL
- `-sX` TCP Xmas
- `-sF` TCP FIN
- `-sI` TCP Idle
- `-O` detección de OS
- `-sV` detección de versiones
- `-A` escaneo agresivo

---

### Timing y modos

- `-T0` paranoico
- `-T1` sigiloso
- `-T2` educado
- `-T3` normal
- `-T4` agresivo
- `-T5` insano

Opciones avanzadas:  
`--min-hostgroup`, `--max-hostgroup`, `--min-rate`, `--max-rate`, `--min-parallelism`, `--max-parallelism`, `--max-retries`, `--host-timeout`, `--scan-delay`

---

### Detección de servicios y versiones

- `-sV` versión de servicios
- `--version-all` probar todas las exploraciones
- `--version-trace` rastrear actividad
- `-O` detección de OS
- `--fuzzy` detección aproximada

---

### Evasión de Firewalls/IDS

- `-f` fragmentar paquetes
- `-D` señuelos
- `-S` falsificar IP origen
- `--g` falsificar puerto origen
- `--randomize-hosts` orden aleatorio
- `--spoof-mac` cambiar MAC

---

### Formatos de salida

- `-oN` formato normal
- `-oX` XML
- `-oG` Grepable
- `-oA` todos los formatos

---

✅ Ahora tu archivo está listo para Obsidian:

- Sin título repetido al inicio.
- Con jerarquía clara y progresiva.
- Bloques de código y listas organizados para máxima legibilidad.

¿Quieres que te prepare también un **índice automático (tabla de contenidos)** al inicio de este archivo para navegar rápido entre instalación, uso, comandos, timing, evasión y salida en Obsidian?