## Introducción

**Tails (The Amnesic Incognito Live System)** es un sistema operativo portátil diseñado para preservar la privacidad y el anonimato.

---

## Características Principales

### Sistema Amnésico

**Características:**

- **No deja rastros** en el sistema después de su uso
- La RAM se limpia al apagar
- Sin persistencia por defecto
- Protección contra **análisis forense**

---

### Sistema Incógnito

**Características:**

- Todo el tráfico pasa **obligatoriamente por Tor**
- **Anonimato** forzado a nivel de sistema
- Bloqueo de conexiones directas
- **Cifrado** en todas las comunicaciones

---

### Sistema Portátil

**Características:**

- Funciona desde **USB o DVD**
- No requiere **instalación** permanente
- Booteable en cualquier computadora
- **Independiente** del sistema operativo host

---

## Principios de Diseño

### Seguridad por Defecto

**Características:**

- **Anonimato** configurado automáticamente
- **Cifrado fuerte** en todas las comunicaciones
- Herramientas de seguridad **preinstaladas**
- Actualizaciones de seguridad **automáticas**

---

## Casos de Uso

### Usuarios Típicos

**Perfiles comunes:**

- **Periodistas:** proteger fuentes confidenciales
- **Activistas:** evitar persecución política
- **Investigadores:** acceso seguro a información sensible
- **Usuarios comunes:** proteger privacidad personal
- **Denunciantes:** comunicación anónima segura

---

### Escenarios de Uso

**Situaciones recomendadas:**

- Países con **censura** gubernamental
- Redes **no confiables** (WiFi públicas)
- Investigación **sensible**
- Comunicación **segura** y confidencial
- Acceso a información **bloqueada**

---

## Arquitectura de Seguridad

### Capas de Protección

**Niveles de seguridad:**

1. **Hardware:** arranque desde medios extraíbles
2. **Sistema:** Debian GNU/Linux endurecido
3. **Red:** todo el tráfico por Tor obligatoriamente
4. **Aplicación:** apps preconfiguradas para privacidad

---

### Herramientas Incluidas

**Navegación y comunicación:**

- **Tor Browser:** navegación anónima
- **Thunderbird:** correo con cifrado PGP
- **OnionShare:** compartir archivos anónimamente
- **Pidgin:** mensajería con OTR

---

**Productividad y utilidades:**

- **LibreOffice:** suite ofimática
- **KeePassXC:** gestor de contraseñas
- **GIMP:** edición de imágenes
- **Audacity:** edición de audio

---

**Seguridad y cifrado:**

- **MAT (Metadata Anonymisation Toolkit):** eliminar metadatos
- **GnuPG:** cifrado de archivos
- **VeraCrypt:** volúmenes cifrados
- **Electrum:** billetera Bitcoin

---

## Almacenamiento Persistente

### Volumen Persistente

**Características:**

- **Opcional:** se puede habilitar en USB
- **Cifrado** con LUKS
- **Selectivo:** elegir qué datos guardar
- Protegido con **contraseña**

---

### Datos que se pueden Persistir

**Categorías disponibles:**

- Configuraciones personales
- Archivos del usuario
- Claves de **cifrado** (PGP, SSH)
- Configuración de red
- **Marcadores** del navegador
- Aplicaciones adicionales

---

## Seguridad y Limitaciones

### Fortalezas

**Ventajas principales:**

- **Anonimato** forzado por diseño
- **Amnesia** total del sistema
- Herramientas **preconfiguradas** correctamente
- **Actualizaciones** de seguridad regulares
- Comunidad activa y **auditorías** externas

---

### Limitaciones

**Restricciones importantes:**

- **No protege** contra keyloggers de hardware
- **No protege** si el BIOS está comprometido
- Requiere **confiar** en la red Tor
- **Rendimiento** reducido por el enrutamiento Tor
- Incompatible con algunas **aplicaciones**

---

## Instalación y Uso

### Requisitos del Sistema

**Especificaciones mínimas:**

- **CPU:** x86_64 compatible
- **RAM:** mínimo 2 GB (recomendado 4 GB)
- **USB:** mínimo 8 GB
- **Boot:** soporte de arranque USB en BIOS/UEFI

---

### Proceso de Instalación

**Pasos básicos:**

1. **Descargar** imagen ISO de `tails.net`
2. **Verificar** firma digital con GnuPG
3. **Crear** USB booteable con Etcher o similar
4. **Configurar** BIOS/UEFI para arranque USB
5. **Iniciar** sistema desde USB

---

## Mejores Prácticas

**Recomendaciones esenciales:**

- **Verificar** siempre la firma digital antes de usar
- Usar **volumen persistente** solo cuando sea necesario
- **No mezclar** actividades anónimas con identificables
- **Actualizar** Tails regularmente
- Usar en hardware **confiable** (no comprometido)
- **Apagar** completamente entre sesiones sensibles
- No usar en **máquinas virtuales** (reduce seguridad)
- Mantener **contraseña fuerte** para volumen persistente
- **Destruir** USB de forma segura cuando ya no se necesite

---