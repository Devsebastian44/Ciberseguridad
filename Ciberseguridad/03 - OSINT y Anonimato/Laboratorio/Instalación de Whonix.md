## ¿Qué es Whonix?

**Whonix** es un sistema operativo orientado a la privacidad que consta de **dos máquinas virtuales** que trabajan en conjunto para garantizar el anonimato completo.

### Componentes Principales

#### **Whonix-Gateway**

- Ejecuta **Tor** como puerta de enlace
- Maneja toda la conectividad de red
- Proporciona aislamiento de red

#### **Whonix-Workstation**

- Estación de trabajo **completamente aislada**
- Todo el tráfico pasa por Gateway
- No tiene acceso directo a internet

---

### Ventajas de Whonix

- **Aislamiento completo** entre red y aplicaciones
- **Prevención de leaks** - Imposible filtrar la IP real
- **Configuración automática** de Tor
- **Actualizaciones seguras** y anónimas

---

## Requisitos del Sistema

### Hardware Mínimo

- **RAM** - 2GB mínimo (recomendado **4GB+**)
- **Almacenamiento** - 20GB libres
- **Procesador** - Con soporte de virtualización
- **Virtualización** - VT-x (Intel) o AMD-V habilitado en BIOS

---

### Software Necesario

- **Hipervisor** - VirtualBox, VMware Workstation o KVM
- **Sistema operativo host** - Windows, macOS o Linux
- **Conexión a internet** - Para descargas y actualizaciones

---

## Instalación Paso a Paso

### Paso 1: Preparación del Entorno

#### Instalar VirtualBox

- Descargar desde el **sitio oficial**
- Instalar y **reiniciar** si es necesario
- Verificar instalación correcta

#### Habilitar Virtualización

- Acceder a **BIOS/UEFI**
- Habilitar **VT-x** (Intel) o **AMD-V** (AMD)
- Guardar y reiniciar

---

### Paso 2: Obtener Whonix

#### Descarga

- Visitar `https://www.whonix.org/download/`
- Descargar **Whonix-Gateway** y **Whonix-Workstation**
- Seleccionar versión para VirtualBox

#### Verificación

- Verificar integridad con **checksums SHA256**
- Confirmar autenticidad de los archivos

---

### Paso 3: Importar en VirtualBox

#### Proceso de Importación

1. Abrir VirtualBox
2. **Archivo → Importar servicio virtualizado**
3. Importar primero **Gateway**, luego **Workstation**
4. Revisar configuración antes de confirmar

---

### Paso 4: Configuración de Red

Esta configuración es **crítica** para el funcionamiento y seguridad de Whonix.

#### **Whonix-Gateway**

- **Adaptador 1:** NAT (conexión a internet)
- **Adaptador 2:** Red interna **"Whonix"**

#### **Whonix-Workstation**

- **Adaptador 1:** Red interna **"Whonix"** (sin acceso directo a internet)
- No configurar más adaptadores

---

### Paso 5: Primera Ejecución

#### Iniciar Gateway

1. Arrancar **Whonix-Gateway** primero
2. Esperar **configuración automática** de Tor
3. Verificar **conexión Tor** establecida
4. Confirmar que el estado es "Connected"

#### Iniciar Workstation

1. Iniciar **Whonix-Workstation**
2. Comprobar **comunicación interna** con Gateway
3. Verificar que todo el tráfico pasa por Tor

---

## Configuración Avanzada

### Whonix-Gateway

#### Tor Control Panel

- Acceder al **"Tor Control Panel"**
- Configurar opciones avanzadas:
    - **Puertos personalizados**
    - **Bridges** (para evasión de censura)
    - **Proxy intermedio** adicional

---

### Whonix-Workstation

#### Actualización del Sistema

- Actualizar desde **terminal** o gestor gráfico
- Todas las descargas pasan por Tor automáticamente

#### Instalación de Software

- Usar **gestor de paquetes** (APT)
- Todo el software se descarga por Tor
- Mantener sistema actualizado

---

## Integración con Kali Linux

### Método 1: Kali como Workstation Personalizada

Usar Kali Linux en lugar de Whonix-Workstation para herramientas de pentesting.

#### Configuración

1. Crear VM con **Kali Linux**
2. Configurar red interna **"Whonix"**
3. Configurar **proxy manual:**
    - HTTP/HTTPS → `10.152.152.10:8118`
    - SOCKS → `10.152.152.10:9050`

---

### Método 2: Uso de Proxychains

Forzar aplicaciones de Kali a usar Tor mediante Proxychains.

#### Configuración

**Instalar Proxychains:**

```bash
apt install proxychains4
```

**Configurar archivo `/etc/proxychains4.conf`:**

```
socks5 10.152.152.10 9050
```

**Uso:**

```bash
proxychains4 nmap -sT ejemplo.com
proxychains4 firefox
```

---

### Método 3: Configuración Global

Configurar todo el sistema Kali para usar Whonix Gateway.

#### Proceso

- Configurar **proxy del sistema** para usar Gateway
- Aplicar configuración a **todas las aplicaciones**
- Verificar que todo el tráfico pasa por Tor

---

## Verificación y Pruebas

### Pruebas de Funcionamiento

#### **Verificar IP**

- Comprobar que sea **distinta a la IP real**
- Usar sitios como whatismyipaddress.com

#### **DNS**

- Confirmar que consultas pasan por **Tor**
- No debe haber leaks de DNS

#### **Aplicaciones**

- Verificar que **todo el tráfico** use Tor
- Probar múltiples aplicaciones

#### **Aislamiento**

- Workstation **no debe acceder** directo a internet
- Todo debe pasar por Gateway

---

### Herramientas de Verificación

#### Navegador Web

- Visitar `https://check.torproject.org/`
- Confirmar conexión Tor activa

#### Herramientas de Red

- `curl --socks5 10.152.152.10:9050 https://check.torproject.org/`
- Verificar IP anónima

#### Logs del Sistema

- Revisar logs de Tor en Gateway
- Monitorear conexiones en Workstation

---