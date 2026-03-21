## Introducción

**Tor (The Onion Router)** es una red de anonimato que requiere configuración y uso adecuados para maximizar la privacidad y seguridad.

---

## Mejores Prácticas

### Configuración Inicial

**Requisitos básicos:**

- Descargar **únicamente** de fuentes oficiales (`torproject.org`)
- **Verificar** firmas digitales antes de instalar
- **Actualizar** regularmente a la última versión
- Usar en sistema **limpio** (sin malware preexistente)

---

### Durante la Navegación

**Configuración recomendada:**

- Mantener **JavaScript desactivado** (nivel de seguridad alto)
- Usar **siempre HTTPS** (nunca HTTP)
- **Evitar plugins** (Flash, Java, ActiveX)
- **Cerrar Tor** completamente al terminar sesiones

---

### Seguridad Adicional

**Capas de protección:**

- Usar **VPN + Tor** para anonimato adicional
- Activar **cortafuegos** (firewall)
- Usar sistemas operativos seguros (**Tails, Whonix**)
- **Verificar** circuitos y cambiar identidad regularmente

---

## Prácticas Prohibidas

### Configuración Incorrecta

**NO hacer:**

- **NO modificar** configuraciones predeterminadas sin conocimiento
- **NO instalar** extensiones adicionales del navegador
- **NO usar** versiones no oficiales
- **NO compartir** perfil de Tor entre usuarios

---

### Errores de Navegación

**NO hacer:**

- **NO iniciar sesión** en cuentas personales (Gmail, Facebook, etc.)
- **NO descargar** archivos ejecutables (riesgo de malware)
- **NO usar torrents** a través de Tor
- **NO habilitar** JavaScript sin necesidad

---

### Errores de Seguridad

**NO hacer:**

- **NO usar** Tor para actividades ilegales
- **NO confiar** ciegamente en la red
- **NO usar HTTP** (solo HTTPS con candado verde)
- **NO reutilizar** contraseñas de otras cuentas

---

## Amenazas Comunes

### Ataques de Correlación

**Características:**

- **Análisis de tráfico** (monitoreo entrada/salida)
- **Timing attacks** (patrones temporales de actividad)
- **Mitigación:** usar múltiples identidades, cambiar circuitos

---

### Compromiso de Nodos

**Tipos de amenazas:**

- **Nodos maliciosos** controlados por atacantes
- **Nodos gubernamentales** con monitoreo estatal
- **Nodos de salida** pueden ver tráfico no cifrado
- **Mitigación:** cambiar circuitos regularmente, usar HTTPS siempre

---

### Vulnerabilidades del Navegador

**Riesgos:**

- **JavaScript** puede revelar identidad real
- **Plugins** pueden filtrar información
- **Cookies** pueden rastrear sesiones
- **Mitigación:** nivel de seguridad "Safest" en Tor Browser

---

## Configuración Recomendada

### Nivel de Seguridad

**Configuración por nivel:**

- **Standard:** JavaScript habilitado (menos seguro)
- **Safer:** JavaScript en sitios HTTPS (recomendado)
- **Safest:** JavaScript deshabilitado (máxima seguridad)

---

### Sistemas Operativos Especializados

**Opciones recomendadas:**

- **Tails:** sistema operativo amnésico y portable
- **Whonix:** aislamiento completo mediante virtualización
- **Qubes OS + Whonix:** máxima seguridad con compartimentación

---

## Combinación VPN + Tor

### Configuraciones Posibles

**VPN → Tor:**

- VPN oculta uso de Tor a ISP
- Protege contra compromiso de nodos de entrada
- Requiere **confiar en el proveedor VPN**

**Tor → VPN:**

- Útil para acceder a servicios que bloquean Tor
- Menor protección de anonimato
- **No recomendado** generalmente

---

## Mejores Prácticas Generales

**Recomendaciones esenciales:**

- **Nunca** revelar información personal mientras usas Tor
- **Cambiar** identidad regularmente (botón "New Identity")
- **Verificar** que el circuito pase por múltiples países
- Usar **contraseñas únicas** para servicios en Tor
- **No mezclar** actividades anónimas con identificables
- Mantener el navegador **actualizado**
- Usar **HTTPS Everywhere** (incluido en Tor Browser)
- **Desconfiar** de archivos descargados desde sitios .onion
- **No maximizar** la ventana del navegador (fingerprinting)
- Usar **modo privado** siempre (incluido por defecto)

---