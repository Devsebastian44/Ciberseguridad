## Introducción

Windows utiliza diversos mecanismos para gestionar y almacenar contraseñas de manera segura. Estos sistemas han evolucionado considerablemente desde las primeras versiones del sistema operativo para hacer frente a amenazas modernas.

---

## Componentes Principales

### Security Accounts Manager (SAM)

El **SAM** es la base de datos principal que almacena las cuentas de usuario locales y sus hashes de contraseñas.

#### Características

- **Ubicación:** `C:\Windows\System32\config\SAM`
- **Función:** Base de datos de cuentas de usuario locales
- **Protección:** Encriptado con clave almacenada en archivo **SYSTEM**

---

### Local Security Authority (LSA)

La **LSA** gestiona las políticas de seguridad locales y los procesos de autenticación del sistema.

#### Componentes Clave

**LSASS.exe**

- Proceso responsable de la **autenticación**
- Ejecuta verificación de credenciales
- Gestiona sesiones de usuario

**LSA Secrets**

- Almacena **credenciales de servicios**
- Guarda cuentas de sistema
- Protege información sensible

---

### Active Directory (AD)

**Active Directory** proporciona gestión centralizada de credenciales en entornos empresariales.

#### Características

- **Base de datos:** `NTDS.dit` contiene todos los objetos del directorio
- **Replicación:** Sincronización automática entre controladores de dominio
- **Gestión centralizada** de usuarios, grupos y políticas

---

## Tipos de Hashes en Windows

### NTLM (NT LAN Manager)

**NTLM** es el sistema de hash actual utilizado por Windows para almacenar contraseñas.

#### Características Técnicas

- **Algoritmo:** MD4
- **Formato:** 32 caracteres hexadecimales
- **Ejemplo:** `aad3b435b51404eeaad3b435b51404ee:5835048ce94ad0564e29a924a03510ef`

#### Vulnerabilidades

- **No utiliza salt** - Vulnerable a tablas precalculadas
- **Vulnerable a rainbow tables** - Ataques con tablas precomputadas
- **Aún utilizado** por compatibilidad legacy

---

### LM Hash (LAN Manager)

**LM Hash** es un sistema obsoleto considerado extremadamente inseguro.

#### Estado y Debilidades

- **Estado:** Deprecado desde **Windows Vista**
- **Debilidades críticas:**
    - Convierte contraseñas a **mayúsculas**
    - Divide contraseñas en bloques de **7 caracteres**
    - **Extremadamente vulnerable** a ataques

---

## Almacenamiento de Credenciales

### Credential Manager

El **Credential Manager** almacena credenciales guardadas por el usuario de forma encriptada.

#### Características

- **Ubicación:** Panel de Control → Credential Manager
- **Tipos de credenciales:**
    - **Windows Credentials** - Credenciales de dominio/red
    - **Generic Credentials** - Credenciales de aplicaciones
- **Protección:** Encriptado con **DPAPI**

---

### Data Protection API (DPAPI)

**DPAPI** es el sistema de Windows para proteger datos sensibles del usuario mediante encriptación.

#### Funcionamiento

**Master Key:**

- Derivada de la **contraseña del usuario**
- Única por usuario

**Backup Key:**

- Para recuperación por **administradores**
- Almacenada en el dominio

**Ubicación:** `%APPDATA%\Microsoft\Protect\`

---

## Políticas de Contraseñas

### Configuración Local

Gestión de políticas de contraseñas a nivel de sistema local.

```powershell
# Ver políticas actuales
net accounts

# Aplicar configuración de seguridad
secedit /configure /cfg C:\path\to\security.inf
```

---

### Group Policy Objects (GPO)

Configuración centralizada de políticas de contraseñas en entornos de dominio.

#### Ruta de Configuración

**Computer Configuration → Windows Settings → Security Settings → Account Policies**

#### Opciones Principales

- **Longitud mínima de contraseña** - Caracteres mínimos requeridos
- **Complejidad requerida** - Mayúsculas, minúsculas, números, símbolos
- **Historial de contraseñas** - Prevenir reutilización
- **Tiempo de vida máximo** - Expiración de contraseñas

---

## Herramientas de Extracción

### Mimikatz

**Mimikatz** es la herramienta más conocida para extracción de credenciales desde la memoria de Windows.

#### Comandos Principales

```
# Extraer credenciales de memoria
sekurlsa::logonpasswords

# Extraer WDigest
sekurlsa::wdigest

# Extraer tickets Kerberos
sekurlsa::kerberos
```

---

### Secretsdump (Impacket)

Herramienta para **extracción remota** de hashes desde sistemas Windows.

#### Sintaxis de Uso

```bash
# Extracción remota básica
secretsdump.py domain/user:password@target

# Extracción con hash
secretsdump.py -hashes LM:NT domain/user@target
```

---

## Medidas de Protección

### Windows Defender Credential Guard

**Credential Guard** protege credenciales utilizando **virtualización basada en seguridad**.

#### Características

- **Función:** Protege credenciales usando **virtualizaciónCONCRETE**
- **Requisitos:** Hardware compatible con **HVCI**
- **Configuración:** Group Policy o Registry
- **Protección:** Aísla secretos en entorno virtualizado

---

### LAPS (Local Administrator Password Solution)

**LAPS** proporciona gestión automatizada de contraseñas de administrador local en entornos empresariales.

#### Características Principales

- **Contraseñas únicas** por equipo
- **Rotación automática** programada
- **Almacenamiento seguro** en Active Directory
- **Prevención de lateral movement** con cuentas locales

---