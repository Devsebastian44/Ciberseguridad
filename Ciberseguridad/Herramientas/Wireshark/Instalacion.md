## ¿Qué es Wireshark?

**Wireshark** es un analizador de protocolos de red gratuito y de código abierto que permite:

- Capturar tráfico de red en tiempo real
- Analizar paquetes de datos detalladamente
- Detectar problemas de red y seguridad
- Realizar ingeniería inversa de protocolos
- Auditar la seguridad de la red

**Historia:** Originalmente llamado Ethereal, renombrado a Wireshark en 2006.

---

## Características Principales

### Multiplataforma

**Sistemas operativos soportados:**

- **Windows** (7, 8, 10, 11)
- **macOS** (10.13+)
- **Linux** (diversas distribuciones)
- **BSD** (FreeBSD, OpenBSD, NetBSD)

**Interfaces:**

- Interfaz gráfica intuitiva (GUI)
- Versión de línea de comandos (**tshark**)
- Dumpcap (motor de captura)

---

### Soporte Extensivo de Protocolos

**Capacidades:**

- Más de **3000 protocolos** soportados
- Decodificación **automática** de protocolos
- Análisis de **múltiples capas** OSI
- Disección profunda de paquetes

**Protocolos comunes:**

- HTTP, HTTPS, DNS, FTP, SSH
- TCP, UDP, ICMP
- SMB, NFS, DHCP
- Y muchos más...

---

### Capacidades Avanzadas

**Análisis:**

- Filtrado en **tiempo real**
- Análisis **estadístico** completo
- Coloreo de paquetes
- Expert Information System

**Exportación:**

- Múltiples formatos (CSV, XML, JSON)
- Exportación de objetos (HTTP, SMB)
- Captura de pantalla

**Flujos:**

- Seguimiento de flujos **TCP/UDP/HTTP**
- Reconstrucción de conversaciones
- Exportación de streams

---

## Instalación de Wireshark

### En Windows

**Paso 1: Descarga**

**Sitio oficial:**

```
https://www.wireshark.org/download.html
```

**Versiones disponibles:**

- 64-bit (recomendado)
- 32-bit
- Portable (no requiere instalación)

---

**Paso 2: Instalación**

**Proceso:**

1. Ejecutar el archivo `.exe` descargado
2. Aceptar términos de licencia (GPL)
3. Seleccionar componentes:
    - **Wireshark** (obligatorio)
    - **TShark** (recomendado)
    - **Plugins/Extensions** (opcional)
4. **Importante:** Instalar **Npcap** cuando se solicite
    - Driver de captura de paquetes
    - Sucesor de WinPcap
    - Necesario para capturar tráfico

**Notas:**

- **WinPcap** está obsoleto, usar **Npcap**
- Npcap requiere reinicio en algunos casos

---

**Paso 3: Configuración Inicial**

**Primera ejecución:**

1. Ejecutar como **administrador** (clic derecho → Run as administrator)
2. Seleccionar interfaz de red apropiada
3. Iniciar captura de prueba

**Verificar instalación:**

- Ver interfaces disponibles
- Capturar tráfico de prueba (ping, navegación web)

---

### En Linux (Ubuntu/Debian)

**Instalación desde repositorios:**

```bash
# Actualizar repositorios
sudo apt update

# Instalar Wireshark
sudo apt install wireshark

# Durante instalación, elegir:
# "Should non-superusers be able to capture packets?" → Yes
```

---

**Configurar permisos (método recomendado):**

```bash
# Agregar usuario al grupo wireshark
sudo usermod -aG wireshark $USER

# Verificar pertenencia al grupo
groups $USER

# Reiniciar sesión para aplicar cambios
# (logout y login nuevamente)
```

**Alternativa (no recomendada por seguridad):**

```bash
# Ejecutar siempre con sudo
sudo wireshark
```

---

**Instalación de versión más reciente (PPA):**

```bash
# Agregar PPA oficial
sudo add-apt-repository ppa:wireshark-dev/stable
sudo apt update
sudo apt install wireshark
```

---

### En Linux (CentOS/RHEL/Fedora)

**Instalación:**

```bash
# CentOS/RHEL 8+
sudo dnf install wireshark

# CentOS/RHEL 7
sudo yum install wireshark

# Fedora
sudo dnf install wireshark-qt
```

**Configurar permisos:**

```bash
sudo usermod -aG wireshark $USER
```

---

### En macOS

#### **Método 1: Homebrew (recomendado)**

**Requisitos previos:**

```bash
# Instalar Homebrew si no lo tienes
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Instalación:**

```bash
# Instalar Wireshark
brew install --cask wireshark

# Verificar instalación
wireshark --version
```

---

#### **Método 2: Descarga Directa**

**Pasos:**

1. Descargar archivo `.dmg` desde sitio oficial
2. Abrir archivo `.dmg`
3. Arrastrar **Wireshark** a carpeta **Applications**
4. Instalar **ChmodBPF** (incluido, necesario para captura)

**Primera ejecución:**

- Permitir en **System Preferences → Security & Privacy**
- Aceptar instalación de extensión de kernel

---

## Verificar Instalación

### Comprobar Versión

**Comando:**

```bash
# GUI
wireshark --version

# CLI
tshark --version
```

**Información mostrada:**

- Versión de Wireshark
- Versión de Qt/GTK
- Plugins compilados
- Librerías disponibles

---

### Verificar Interfaces

**Comando:**

```bash
# Listar interfaces disponibles
tshark -D

# o desde GUI
# Capture → Interfaces
```

**Salida esperada:**

```
1. eth0 (Ethernet)
2. wlan0 (WiFi)
3. lo (Loopback)
```

---

## Requisitos del Sistema

### Mínimos

**Hardware:**

- **RAM:** 512 MB
- **Espacio en disco:** 200 MB
- **Procesador:** 1 GHz

**Nota:** Suficiente para capturas pequeñas y análisis básico

---

### Recomendados

**Hardware:**

- **RAM:** 4 GB o más (8 GB para análisis pesado)
- **Espacio en disco:** 5 GB o más
- **Procesador:** Multi-core (2+ cores)

**Para análisis intensivo:**

- RAM: 16 GB+
- SSD para almacenamiento de capturas
- CPU: 4+ cores

---

### Requisitos de Software

**Windows:**

- Windows 7 SP1 o superior
- .NET Framework 4.5+
- Npcap driver

**Linux:**

- Kernel 2.6.32 o superior
- libpcap 1.0.0+
- GTK+ 3.x o Qt 5.x

**macOS:**

- macOS 10.13 (High Sierra) o superior
- Xcode Command Line Tools (para Homebrew)

---

## Solución de Problemas Comunes

### Windows: "No interfaces found"

**Soluciones:**

1. Reinstalar **Npcap**
2. Ejecutar como **administrador**
3. Verificar servicio Npcap:

```cmd
sc query npcap
```

---

### Linux: "Permission denied"

**Soluciones:**

1. Verificar pertenencia al grupo:

```bash
groups | grep wireshark
```

2. Si no está, agregar:

```bash
sudo usermod -aG wireshark $USER
# Reiniciar sesión
```

3. Verificar permisos de dumpcap:

```bash
ls -l /usr/bin/dumpcap
```

---

### macOS: "You don't have permission to capture"

**Soluciones:**

1. Reinstalar ChmodBPF:

```bash
# Ejecutar script incluido
/Library/Application Support/Wireshark/ChmodBPF/ChmodBPF
```

2. Dar permisos manualmente:

```bash
sudo chmod 644 /dev/bpf*
```

---

## Primeros Pasos

### Captura de Prueba

**Pasos:**

1. Abrir Wireshark
2. Seleccionar interfaz de red activa
3. Click en **Start** (aleta de tiburón azul)
4. Generar tráfico (abrir navegador, hacer ping)
5. Click en **Stop** (cuadrado rojo)
6. Observar paquetes capturados

---

### Filtros Básicos

**Probar filtros simples:**

```bash
# Solo HTTP
http

# Solo DNS
dns

# Solo una IP
ip.addr == 192.168.1.1
```

---

## Recursos Adicionales

### Documentación Oficial

**Enlaces:**

- Guía de usuario: https://www.wireshark.org/docs/
- Wiki: https://wiki.wireshark.org/
- FAQs: https://www.wireshark.org/faq.html

---

### Comunidad

**Soporte:**

- Foro oficial: https://ask.wireshark.org/
- Lista de correo: wireshark-users
- Discord/Slack (comunidades no oficiales)

---

### Cursos y Tutoriales

**Recursos de aprendizaje:**

- Wireshark University (cursos oficiales)
- YouTube (canales dedicados)
- Libros recomendados: "Wireshark Network Analysis"

---

## Consideraciones

- Wireshark requiere **privilegios elevados** para capturar
- **No** capturar en redes sin autorización
- Respetar **privacidad** y **leyes locales**
- Capturas pueden contener **información sensible**
- **Actualizar** regularmente para seguridad y nuevas características

---