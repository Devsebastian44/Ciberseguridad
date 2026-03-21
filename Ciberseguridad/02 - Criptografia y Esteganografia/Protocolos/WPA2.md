## Introducción

**WPA3 (Wi-Fi Protected Access 3)** es la última generación de protocolos de seguridad para redes inalámbricas, lanzado en 2018 por la Wi-Fi Alliance.

Representa una mejora significativa sobre WPA2 en términos de seguridad y funcionalidad.

---

## Características Principales

### SAE (Simultaneous Authentication of Equals)

**Características:**

- Reemplaza el **4-way handshake** de WPA2
- **Protección** contra ataques offline de diccionario
- **Autenticación mutua** entre dispositivos
- Hace inviables los ataques offline incluso con contraseñas débiles

---

### Cifrado Individualizado

**Características:**

- Cada dispositivo tiene su propia **clave de cifrado**
- Si un dispositivo es comprometido, otros permanecen **seguros**
- Uso de **claves dinámicas** por sesión

---

### Forward Secrecy

**Características:**

- Las claves pasadas **no pueden** desencriptar comunicaciones futuras
- **Generación dinámica** de claves
- Limita el impacto de compromisos de clave

---

## Modos de Operación

### WPA3-Personal

**Características:**

- Uso doméstico y pequeñas empresas
- Contraseña compartida **(PSK)**
- Cifrado de **128 bits**
- **Protección** contra ataques offline

---

### WPA3-Enterprise

**Características:**

- Organizaciones grandes
- Cifrado de **192 bits**
- **Autenticación individual** por usuario
- **Certificados digitales**
- Protección adicional para datos **sensibles**

---

## Mejoras de Seguridad

### Protección contra KRACK

**Características:**

- **Problema:** Key Reinstallation Attacks en WPA2
- **Solución:** nuevo protocolo SAE
- **Resultado:** eliminación de vulnerabilidades conocidas

---

### Cifrado Mejorado

**Especificaciones:**

- Algoritmo: **AES-256** en modo GCM
- Mayor **resistencia** a ataques criptográficos
- Mejora significativa sobre **AES-128** de WPA2

---

## Implementación

### Configuración WPA3-Personal

**Archivo hostapd.conf:**

```bash
interface=wlan0
driver=nl80211
ssid=MiRedWPA3
hw_mode=g
channel=7
wmm_enabled=1
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=MiContraseñaSegura123
wpa_key_mgmt=SAE
wpa_pairwise=CCMP
rsn_pairwise=CCMP
```

---

## Compatibilidad

### Modo Transición (WPA3/WPA2)

**Consideraciones:**

- Soporte para dispositivos **legacy**
- **Implementación gradual** recomendada
- Posible **degradación** de seguridad en modo mixto

---

### Requisitos de Hardware

**Necesidades:**

- Chips Wi-Fi que soporten **WPA3**
- **Actualización** de firmware en dispositivos existentes
- **Certificación** por Wi-Fi Alliance

---

## Comparación WPA2 vs WPA3

|Característica|WPA2|WPA3|
|---|---|---|
|**Handshake**|4-way handshake|SAE|
|**Cifrado**|AES-128|AES-128/256|
|**Protección offline**|Vulnerable|Protegido|
|**Forward Secrecy**|No|Sí|
|**Ataques KRACK**|Vulnerable|Inmune|

---

## Mejores Prácticas

**Recomendaciones:**

- Migrar a **WPA3-Personal** para uso doméstico
- Usar **WPA3-Enterprise** con cifrado de 192 bits para entornos corporativos
- Implementar **modo transición** (WPA3/WPA2) durante migración
- **Actualizar firmware** de dispositivos regularmente
- **Verificar certificación** Wi-Fi Alliance en nuevos dispositivos
- Usar **contraseñas fuertes** (mínimo 12 caracteres)
- **Deshabilitar WPA2** puro cuando todos los dispositivos soporten WPA3

---