## Introducción

**PGP (Pretty Good Privacy)** es un programa de criptografía que proporciona privacidad y autenticación para comunicaciones de datos.

Utiliza una combinación de cifrado simétrico y asimétrico.

---

## Arquitectura PGP

### Componentes Principales

#### **1. Cifrado Híbrido**

**Características:**

- Cifrado simétrico para los datos (rápido)
- Cifrado asimétrico para la clave de sesión (seguro)
- Combina eficiencia y seguridad

---

#### **2. Firmas Digitales**

**Funciones:**

- **Autenticación** del remitente
- **Verificación** de integridad
- **No repudio** (prueba de autoría)

---

#### **3. Compresión**

**Beneficios:**

- Reduce el tamaño de los datos
- Mejora la seguridad al eliminar redundancias
- Aplicada antes del cifrado

---

#### **4. Codificación Base64**

**Función:**

- Conversión a texto ASCII
- Compatible con sistemas de correo electrónico
- Facilita transmisión

---

## Procesos de Cifrado y Descifrado

### Proceso de Cifrado PGP

**Pasos:**

```text
1. Comprimir mensaje (opcional)
2. Generar clave de sesión aleatoria
3. Cifrar el mensaje con clave de sesión (AES, por ejemplo)
4. Cifrar clave de sesión con clave pública del destinatario (RSA)
5. Combinar mensaje cifrado + clave de sesión cifrada
6. Codificar en Base64 si es necesario
```

---

### Proceso de Descifrado PGP

**Pasos:**

```text
1. Decodificar Base64 (si aplica)
2. Extraer clave de sesión cifrada
3. Descifrar clave de sesión con clave privada (RSA)
4. Descifrar mensaje usando clave de sesión (AES)
5. Descomprimir mensaje
6. Verificar integridad y autenticidad
```

---

## Gestión de Claves PGP

### Generación de Claves

**Algoritmos soportados:**

- **RSA** (más común)
- DSA (firma)
- Elípticas (ECC)

**Recomendaciones:**

- Longitud: **≥ 2048 bits** (RSA)
- Generación con **entropía suficiente**
- Fecha de expiración configurada

---

### Anillo de Claves (Keyring)

**Tipos de claves almacenadas:**

- **Claves públicas:** de otros usuarios
- **Claves privadas:** propias (protegidas con contraseña)

**Ubicación típica:**

```
~/.gnupg/pubring.kbx   (claves públicas)
~/.gnupg/secring.gpg   (claves privadas)
```

---

### Red de Confianza (Web of Trust)

**Características:**

- Modelo **descentralizado** de confianza
- Validación mediante **firmas cruzadas**
- Niveles de confianza configurables

**Niveles:**

- **Unknown:** sin información
- **None:** no confiable
- **Marginal:** algo confiable
- **Full:** completamente confiable
- **Ultimate:** clave propia

---

## Implementaciones

### OpenPGP

**Características:**

- Estándar abierto (**RFC 4880**)
- Múltiples implementaciones
- Interoperabilidad garantizada

---

### GnuPG (GPG)

**Características:**

- Implementación **libre** de OpenPGP
- **Multiplataforma** (Linux, Windows, macOS)
- Ampliamente utilizada

**Instalación:**

```bash
# Debian/Ubuntu
sudo apt install gnupg

# macOS
brew install gnupg

# Windows
# Descargar desde https://gnupg.org
```

---

## Comandos Básicos GPG

### Generación y Gestión de Claves

**Generar par de claves:**

```bash
gpg --gen-key
gpg --full-gen-key  # Opciones avanzadas
```

**Listar claves:**

```bash
gpg --list-keys              # Claves públicas
gpg --list-secret-keys       # Claves privadas
```

**Exportar clave pública:**

```bash
gpg --export -a "Usuario" > clave_publica.asc
gpg --export --armor "email@example.com" > clave.asc
```

**Importar clave pública:**

```bash
gpg --import clave_publica.asc
```

**Eliminar claves:**

```bash
gpg --delete-key "Usuario"        # Pública
gpg --delete-secret-key "Usuario" # Privada
```

---

### Cifrado y Descifrado

**Cifrar archivo:**

```bash
gpg --encrypt -r "Destinatario" archivo.txt
gpg -e -r "email@example.com" archivo.txt
```

**Cifrar con múltiples destinatarios:**

```bash
gpg -e -r "persona1@example.com" -r "persona2@example.com" archivo.txt
```

**Descifrar archivo:**

```bash
gpg --decrypt archivo.txt.gpg
gpg -d archivo.txt.gpg > archivo_descifrado.txt
```

---

### Firmas Digitales

**Firmar archivo:**

```bash
gpg --sign archivo.txt              # Firma binaria
gpg --clearsign archivo.txt         # Firma legible
gpg --detach-sign archivo.txt       # Firma separada
```

**Verificar firma:**

```bash
gpg --verify archivo.txt.gpg
gpg --verify archivo.txt.sig archivo.txt  # Firma separada
```

---

### Cifrado Simétrico

**Sin claves públicas:**

```bash
gpg --symmetric archivo.txt  # Usa contraseña
gpg -c archivo.txt
```

---

## Aplicaciones Prácticas

### Correo Electrónico Seguro

**Usos:**

- **Cifrado** de mensajes sensibles
- **Firma digital** de correos
- **Verificación** de autenticidad del remitente

**Clientes compatibles:**

- Thunderbird + Enigmail
- Apple Mail + GPGTools
- Outlook + Gpg4win

---

### Almacenamiento Seguro

**Aplicaciones:**

- Cifrado de **archivos sensibles**
- **Backup seguro** de datos
- Protección de **documentos confidenciales**

---

### Comunicaciones Seguras

**Usos:**

- Mensajería instantánea cifrada
- Transferencia segura de archivos
- Comunicaciones empresariales

---

## Mejores Prácticas

### Gestión de Claves

**Generación:**

- Usar **≥ 2048 bits** para RSA
- Establecer **fecha de expiración**
- Proteger clave privada con **contraseña fuerte**

**Backup:**

- **Exportar** y guardar clave privada en lugar seguro
- **Múltiples copias** en ubicaciones diferentes
- Considerar **paper key** para recuperación

**Revocación:**

- Generar **certificado de revocación** al crear claves
- Guardar en lugar seguro
- Publicar si la clave es comprometida

---

### Uso Seguro

**Protección:**

- **Nunca** compartir clave privada
- Usar **passphrase fuerte** (12+ caracteres)
- **Verificar huellas** (fingerprints) antes de confiar
- **Firmar** claves de contactos conocidos

**Verificación:**

```bash
# Ver fingerprint de una clave
gpg --fingerprint "email@example.com"
```

---

### Publicación de Claves

**Servidores de claves:**

```bash
# Enviar clave a servidor
gpg --send-keys KEYID

# Buscar clave en servidor
gpg --search-keys "email@example.com"

# Recibir clave de servidor
gpg --recv-keys KEYID
```

**Servidores comunes:**

- keys.openpgp.org
- keyserver.ubuntu.com
- pgp.mit.edu

---

## Consideraciones

- PGP es **estándar** para cifrado de correo electrónico
- **Verificar siempre** identidad antes de confiar en claves
- **Proteger** clave privada con contraseña fuerte
- **Renovar** claves antes de expiración
- Usar **GPG moderno** (versión 2.x+)
- **Documentar** procedimientos de recuperación

---