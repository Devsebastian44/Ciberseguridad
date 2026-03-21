## Introducción al Sistema de Contraseñas de Windows

Windows utiliza un sistema complejo de gestión de contraseñas que incluye:

- **SAM Database:** Security Account Manager
- **Active Directory:** para entornos de dominio
- **NTLM:** NT LAN Manager hashes
- **Kerberos:** protocolo de autenticación moderno

---

## Arquitectura del Sistema

### Security Account Manager (SAM)

**Ubicación de la base de datos SAM:**

```
C:\Windows\System32\config\SAM
```

**Características:**

- Almacena cuentas de usuario locales
- Protegida por el sistema operativo
- Solo accesible con privilegios de SYSTEM

---

## Estructura de Hashes

### LM Hash (Legacy)

**Características:**

- Algoritmo: **DES** (débil)
- Longitud máxima: **14 caracteres**
- Formato: dividido en dos bloques de 7 caracteres
- Estado: **Obsoleto** desde Windows Vista

**Vulnerabilidades:**

- No case-sensitive
- Sin salt
- Fácilmente crackeable

---

### NTLM Hash

**Características:**

- Algoritmo: **MD4**
- Entrada: contraseña en Unicode
- Formato: **32 caracteres hexadecimales**
- Uso: actual en sistemas Windows

**Ejemplo:**

```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:5835048ce94ad0564e29a924a03510ef:::
```

**Formato:**

```
usuario:RID:LM_hash:NTLM_hash:::
```

---

## Proceso de Autenticación

### Autenticación Local

**Flujo:**

```
1. Usuario ingresa contraseña
2. Conversión a Unicode
3. Aplicación de MD4
4. Comparación con hash almacenado en SAM
5. Decisión de acceso
```

---

### Autenticación de Dominio (Kerberos)

**Flujo:**

```
1. Cliente solicita TGT (Ticket Granting Ticket)
2. KDC valida credenciales
3. Emisión de TGT
4. Cliente solicita TGS (Ticket Granting Service)
5. Acceso a recursos
```

**Componentes:**

- **KDC:** Key Distribution Center
- **TGT:** válido por defecto 10 horas
- **TGS:** para acceso a servicios específicos

---

## Almacenamiento de Credenciales

### Registro de Windows

**Ubicación:**

```
HKEY_LOCAL_MACHINE\SAM\SAM\Domains\Account\Users
```

**Nota:** Protegida, requiere SYSTEM para acceso

---

### Credential Manager

**Acceso:**

```
Control Panel → Credential Manager
```

**Tipos de credenciales:**

- **Windows Credentials** - credenciales de red
- **Generic Credentials** - aplicaciones
- **Certificate-Based Credentials** - certificados

**Comando:**

```cmd
cmdkey /list
```

---

## Herramientas de Análisis

### Mimikatz

**Comandos principales:**

```powershell
# Iniciar Mimikatz
mimikatz.exe

# Obtener privilegios debug
privilege::debug

# Extraer contraseñas en texto claro (si están en memoria)
sekurlsa::logonpasswords

# Dumpar SAM database
lsadump::sam

# Dumpar credenciales de dominio
lsadump::lsa /patch
```

---

### PwDump

**Uso:**

```cmd
# Extraer hashes locales
pwdump7.exe

# Guardar en archivo
pwdump7.exe > hashes.txt
```

---

## Configuración de Políticas

### Política de Contraseñas Local

**Acceso:**

```
secpol.msc → Account Policies → Password Policy
```

**Parámetros:**

- **Enforce password history** - recordar N contraseñas anteriores
- **Maximum password age** - días máximos de validez
- **Minimum password age** - días mínimos entre cambios
- **Minimum password length** - caracteres mínimos
- **Password must meet complexity requirements** - complejidad activada

---

### Política de Grupo (GPO)

**Acceso:**

```
gpmc.msc → Computer Configuration → Windows Settings → Security Settings
```

**Secciones:**

- **Account Policies** - políticas de cuenta
- **Local Policies** - políticas locales
- **Windows Firewall** - configuración de firewall

---

## Comandos Útiles

### Gestión de Usuarios

**Listar usuarios:**

```cmd
net user
```

**Ver información de usuario:**

```cmd
net user username
```

**Cambiar contraseña:**

```cmd
net user username newpassword
```

---

### Políticas de Contraseñas

**Ver política actual:**

```cmd
net accounts
```

**Exportar políticas de seguridad:**

```cmd
secedit /export /cfg security_config.inf
```

---

## Mejores Prácticas

### Configuración Segura

**Políticas recomendadas:**

- Deshabilitar **LM hash** completamente
- Longitud mínima: **12+ caracteres**
- Complejidad: **activada**
- Historial: **24 contraseñas**
- Expiración: **90 días máximo**
- Bloqueo: **5 intentos fallidos**

---

### Protección del Sistema

**Medidas de seguridad:**

- Usar **Credential Guard** (Windows 10+)
- Implementar **LAPS** (Local Administrator Password Solution)
- Activar **BitLocker** para proteger SAM
- Deshabilitar **almacenamiento de credenciales en texto claro**
- Monitorear **intentos de extracción** (Mimikatz, etc.)

---

### Defensa contra Ataques

**Pass-the-Hash mitigation:**

- Limitar cuentas con privilegios locales
- Usar **Protected Users** group
- Implementar **Remote Credential Guard**

**Credential Dumping detection:**

- Monitorear acceso a **LSASS.exe**
- Alertar en uso de **Mimikatz** signatures
- Revisar **Event ID 4688** (proceso creado)

---

## Consideraciones de Seguridad

- **Nunca** usar LM hash (deshabilitar completamente)
- **Proteger** acceso físico al servidor
- **Monitorear** extracción de credenciales
- Implementar **MFA** (Multi-Factor Authentication)
- Usar **Privileged Access Workstations** para administradores
- **Auditar** cambios en políticas de contraseñas

---