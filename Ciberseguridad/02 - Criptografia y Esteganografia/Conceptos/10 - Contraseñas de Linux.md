## Introducción a las Contraseñas en Linux

Linux utiliza un sistema sofisticado de gestión de contraseñas que incluye:

- **Archivos de contraseñas:** `/etc/passwd`, `/etc/shadow`
- **Algoritmos de hash:** SHA-256, SHA-512, bcrypt, scrypt
- **Sistemas de autenticación:** PAM (Pluggable Authentication Modules)

---

## Estructura del Sistema de Contraseñas

### Archivo `/etc/passwd`

**Formato:**

```
usuario:x:UID:GID:GECOS:directorio_home:shell
```

**Ejemplo:**

```
root:x:0:0:root:/root:/bin/bash
john:x:1000:1000:John Doe,,,:/home/john:/bin/bash
```

**Campos:**

- `x` = contraseña en `/etc/shadow`
- `UID` = User ID
- `GID` = Group ID
- `GECOS` = información del usuario

---

### Archivo `/etc/shadow`

**Formato:**

```
usuario:contraseña_hash:último_cambio:min_días:max_días:aviso:inactivo:expiración:reservado
```

**Ejemplo:**

```
root:$6$rounds=5000$salt$hash:18000:0:99999:7:::
john:$6$xyz$abcdef...:18000:0:99999:7:::
```

**Campos importantes:**

- `contraseña_hash` = hash de la contraseña
- `último_cambio` = días desde época (1970-01-01)
- `min_días` = días mínimos entre cambios
- `max_días` = días máximos de validez
- `aviso` = días de advertencia antes de expirar

---

## Algoritmos de Hash

### Identificadores de Algoritmos

```
$1$  = MD5 (obsoleto)
$2a$ = Blowfish (bcrypt)
$5$  = SHA-256
$6$  = SHA-512
$7$  = scrypt
$y$  = yescrypt
```

---

### Estructura del Hash SHA-512

```
$6$rounds=5000$salt$hash
│  │            │    └─ Hash resultante
│  │            └─ Salt (semilla aleatoria)
│  └─ Número de rounds (iteraciones)
└─ Identificador del algoritmo
```

**Características:**

- **Salt:** único por usuario, previene rainbow tables
- **Rounds:** más iteraciones = más seguro (y más lento)
- **Hash:** resultado final de aplicar el algoritmo

---

## Proceso de Autenticación

### Flujo de Verificación

**Paso a paso:**

1. **Entrada de usuario:** credenciales ingresadas
2. **Búsqueda en `/etc/passwd`:** localiza el usuario
3. **Recuperación del hash:** lee desde `/etc/shadow`
4. **Generación del hash:** aplica el mismo algoritmo a la contraseña ingresada
5. **Comparación:** se contrastan ambos hashes
6. **Decisión:** acceso permitido o denegado

---

### Código Simplificado

```c
int verify_password(const char *username, const char *password) {
    struct spwd *shadow_entry;
    char *encrypted;
    
    // Obtener entrada de shadow
    shadow_entry = getspnam(username);
    if (!shadow_entry) return 0;
    
    // Generar hash con la contraseña ingresada
    encrypted = crypt(password, shadow_entry->sp_pwdp);
    
    // Comparar hashes
    return strcmp(encrypted, shadow_entry->sp_pwdp) == 0;
}
```

---

## Configuración de Políticas

### `/etc/login.defs`

**Parámetros de contraseñas:**

```bash
PASS_MAX_DAYS   90    # Días máximos de validez
PASS_MIN_DAYS   1     # Días mínimos entre cambios
PASS_WARN_AGE   7     # Días de advertencia
PASS_MIN_LEN    8     # Longitud mínima
```

**Ver configuración actual:**

```bash
grep -E "PASS_" /etc/login.defs
```

---

### PAM Configuration

**Archivo:** `/etc/pam.d/common-password`

**Ejemplo de configuración:**

```bash
# Requisitos de calidad
password required pam_pwquality.so retry=3 minlen=8 difok=3

# Algoritmo de hash
password required pam_unix.so sha512 shadow nullok try_first_pass
```

**Parámetros importantes:**

- `minlen=8` = longitud mínima
- `difok=3` = caracteres diferentes de la anterior
- `retry=3` = intentos permitidos
- `sha512` = algoritmo de hash

---

## Comandos de Gestión

### Ver información de usuario

```bash
# Ver entrada en passwd
getent passwd username

# Ver entrada en shadow (requiere root)
sudo getent shadow username

# Ver política de expiración
sudo chage -l username
```

---

### Modificar políticas

```bash
# Establecer expiración de contraseña
sudo chage -M 90 username    # Máximo 90 días
sudo chage -m 7 username     # Mínimo 7 días entre cambios
sudo chage -W 14 username    # Advertir 14 días antes

# Forzar cambio en próximo login
sudo chage -d 0 username
```

---

### Cambiar contraseñas

```bash
# Cambiar propia contraseña
passwd

# Cambiar contraseña de otro usuario (root)
sudo passwd username

# Bloquear cuenta
sudo passwd -l username

# Desbloquear cuenta
sudo passwd -u username
```

---

## Mejores Prácticas

### Políticas Recomendadas

**Configuración segura:**

- Usar **SHA-512** o superior
- Establecer **expiración** (90 días máximo)
- Requerir **longitud mínima** (12+ caracteres)
- Implementar **complejidad** (mayúsculas, minúsculas, números, símbolos)
- Configurar **intentos fallidos** limitados

---

### Seguridad del Sistema

**Permisos correctos:**

```bash
# /etc/passwd debe ser legible por todos
chmod 644 /etc/passwd

# /etc/shadow solo para root
chmod 640 /etc/shadow
chown root:shadow /etc/shadow
```

**Verificar permisos:**

```bash
ls -l /etc/passwd /etc/shadow
```

---

## Consideraciones de Seguridad

- **Nunca** almacenar contraseñas en texto plano
- Usar **algoritmos modernos** (SHA-512, bcrypt, Argon2)
- Implementar **salt único** por usuario
- Configurar **políticas de expiración**
- Auditar **intentos fallidos** regularmente
- **Proteger** acceso a `/etc/shadow`

---