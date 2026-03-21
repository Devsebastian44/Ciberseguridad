## Contraseñas de Linux y Ataques

### Fundamentos de Contraseñas en Linux

**Archivos principales:**

- `/etc/passwd` - Información de usuarios
- `/etc/shadow` - Hashes de contraseñas (solo root)

**Algoritmos de hash comunes:**

- **SHA-512** (más seguro)
- **SHA-256**
- MD5 (obsoleto)

---

## Herramientas de Análisis

### John the Ripper

**Preparación de archivos:**

```bash
sudo unshadow /etc/passwd /etc/shadow > hashes.txt
```

**Ataque de diccionario:**

```bash
john --wordlist=passwords.txt --format=sha512crypt hashes.txt
```

**Ataque de fuerza bruta:**

```bash
john --format=sha512crypt hashes.txt
```

**Ver contraseñas crackeadas:**

```bash
john --show hashes.txt
```

---

### Hashcat

**Identificar modos de hash:**

```bash
hashcat --help | grep -i linux
```

**Modo 1800** = sha512crypt (Linux)

**Ataque de diccionario:**

```bash
hashcat -m 1800 -a 0 hashes.txt diccionario.txt
```

**Ataque de fuerza bruta (máscaras):**

```bash
# ?l = lowercase, ?u = uppercase, ?d = digit, ?s = special
hashcat -m 1800 -a 3 hashes.txt ?l?l?l?l?d?d?d?d
```

**Ver resultados:**

```bash
hashcat -m 1800 hashes.txt --show
```

---

## Extracción de Contraseñas

### Método Manual

**Copiar archivos del sistema:**

```bash
sudo cp /etc/passwd passwd_copy
sudo cp /etc/shadow shadow_copy
```

**Combinar archivos:**

```bash
unshadow passwd_copy shadow_copy > combined.txt
```

**Formato resultante:**

```
username:$6$salt$hash:UID:GID:GECOS:home:shell
```

---

### Script de Extracción Automatizado

```python
#!/usr/bin/env python3
import crypt

def extract_hashes():
    """
    Extrae hashes de contraseñas del archivo /etc/shadow
    Requiere permisos de root
    """
    try:
        with open('/etc/shadow', 'r') as f:
            for line in f:
                if line.strip() and not line.startswith('#'):
                    fields = line.split(':')
                    username = fields[0]
                    password_hash = fields[1]
                    
                    # Filtrar usuarios sin contraseña o bloqueados
                    if password_hash and password_hash not in ['!', '*', '!!']:
                        print(f"{username}:{password_hash}")
                        
    except PermissionError:
        print("Error: Se requieren permisos de root")
        print("Ejecutar con: sudo python3 script.py")
    except FileNotFoundError:
        print("Error: Archivo /etc/shadow no encontrado")

if __name__ == "__main__":
    extract_hashes()
```

**Uso:**

```bash
sudo python3 extract_hashes.py > hashes.txt
```

---

## Creación de Contraseñas Seguras

### Generación de Hashes con Python

```python
#!/usr/bin/env python3
import crypt
import secrets
import string

def generate_password_hash(password, algorithm='sha512'):
    """
    Genera un hash de contraseña compatible con Linux
    
    Args:
        password (str): Contraseña en texto plano
        algorithm (str): 'sha512' o 'sha256'
    
    Returns:
        str: Hash de contraseña
    """
    # Generar salt aleatorio
    salt_chars = string.ascii_letters + string.digits + './'
    salt = ''.join(secrets.choice(salt_chars) for _ in range(16))
    
    # Seleccionar método de hash
    if algorithm == 'sha512':
        method = crypt.METHOD_SHA512
    elif algorithm == 'sha256':
        method = crypt.METHOD_SHA256
    else:
        method = crypt.METHOD_SHA512
    
    # Generar hash
    return crypt.crypt(password, method)

# Ejemplo de uso
password = "MiContraseñaSegura123!"
hash_result = generate_password_hash(password)
print(f"Contraseña: {password}")
print(f"Hash generado: {hash_result}")
```

**Uso del hash generado:**

```bash
sudo usermod -p 'HASH_GENERADO' username
```

---

### Generador de Contraseñas Aleatorias

```python
#!/usr/bin/env python3
import secrets
import string

def generate_secure_password(length=16, use_special=True):
    """
    Genera una contraseña aleatoria segura
    
    Args:
        length (int): Longitud de la contraseña
        use_special (bool): Incluir caracteres especiales
    
    Returns:
        str: Contraseña generada
    """
    characters = string.ascii_letters + string.digits
    if use_special:
        characters += string.punctuation
    
    password = ''.join(secrets.choice(characters) for _ in range(length))
    return password

# Generar varias contraseñas
print("Contraseñas generadas:")
for i in range(5):
    pwd = generate_secure_password(16, use_special=True)
    print(f"{i+1}. {pwd}")
```

---

## Auditoría de Contraseñas

### Script de Auditoría Completo

```bash
#!/bin/bash

echo "================================================"
echo "=== Auditoría de Contraseñas del Sistema ==="
echo "================================================"
echo "Fecha: $(date)"
echo "Hostname: $(hostname)"
echo

# 1. Usuarios con contraseñas potencialmente débiles
echo "----------------------------------------"
echo "1. USUARIOS CON POSIBLES CONTRASEÑAS DÉBILES"
echo "----------------------------------------"
awk -F: '($2 != "x" && $2 != "*" && $2 != "!") {print $1}' /etc/passwd

# 2. Usuarios sin contraseña
echo -e "\n----------------------------------------"
echo "2. USUARIOS SIN CONTRASEÑA (CRÍTICO)"
echo "----------------------------------------"
sudo awk -F: '($2 == "" || $2 == "!") {print $1}' /etc/shadow

# 3. Usuarios con contraseñas próximas a expirar
echo -e "\n----------------------------------------"
echo "3. CONTRASEÑAS PRÓXIMAS A EXPIRAR"
echo "----------------------------------------"
while IFS=: read -r username password lastchange min max warn inactive expire reserved; do
    if [[ $max != "" && $max -gt 0 ]]; then
        current_days=$(( $(date +%s) / 86400 ))
        expire_days=$(( lastchange + max ))
        days_left=$(( expire_days - current_days ))
        
        if [[ $days_left -le 7 && $days_left -ge 0 ]]; then
            echo "  - $username expira en $days_left días"
        fi
    fi
done < /etc/shadow

# 4. Configuración de políticas
echo -e "\n----------------------------------------"
echo "4. CONFIGURACIÓN DE POLÍTICAS"
echo "----------------------------------------"
echo "Políticas en /etc/login.defs:"
grep -E "(PASS_MAX_DAYS|PASS_MIN_DAYS|PASS_WARN_AGE|PASS_MIN_LEN)" /etc/login.defs

# 5. Usuarios con UID 0 (privilegios de root)
echo -e "\n----------------------------------------"
echo "5. USUARIOS CON UID 0 (PRIVILEGIOS ROOT)"
echo "----------------------------------------"
awk -F: '($3 == 0) {print $1}' /etc/passwd

# 6. Algoritmos de hash utilizados
echo -e "\n----------------------------------------"
echo "6. ALGORITMOS DE HASH EN USO"
echo "----------------------------------------"
sudo awk -F: '{
    if ($2 ~ /^\$6\$/) print $1 ": SHA-512"
    else if ($2 ~ /^\$5\$/) print $1 ": SHA-256"
    else if ($2 ~ /^\$1\$/) print $1 ": MD5 (INSEGURO)"
    else if ($2 ~ /^\$2/) print $1 ": Blowfish"
}' /etc/shadow | head -10

echo -e "\n================================================"
echo "=== Auditoría Completada ==="
echo "================================================"
```

**Ejecutar auditoría:**

```bash
sudo bash audit_passwords.sh
sudo bash audit_passwords.sh > audit_report_$(date +%Y%m%d).txt
```

---

## Análisis de Políticas de Contraseñas

### Verificar PAM (Pluggable Authentication Modules)

**Archivo de configuración:**

```bash
cat /etc/pam.d/common-password
```

**Requisitos típicos:**

```
# Longitud mínima de 12 caracteres
password requisite pam_pwquality.so retry=3 minlen=12

# Requerir mayúsculas, minúsculas, dígitos
password requisite pam_pwquality.so ucredit=-1 lcredit=-1 dcredit=-1

# Prevenir reutilización de últimas 5 contraseñas
password required pam_pwhistory.so remember=5
```

---

### Verificar Configuración de Expiración

**Para usuario específico:**

```bash
sudo chage -l username
```

**Establecer política de expiración:**

```bash
# Máximo 90 días
sudo chage -M 90 username

# Mínimo 7 días entre cambios
sudo chage -m 7 username

# Advertir 14 días antes
sudo chage -W 14 username
```

---

## Mejores Prácticas

### Políticas Recomendadas

**Configuración en `/etc/login.defs`:**

```
PASS_MAX_DAYS   90
PASS_MIN_DAYS   7
PASS_WARN_AGE   14
PASS_MIN_LEN    12
```

**Requisitos de complejidad:**

- Mínimo **12 caracteres**
- Al menos **1 mayúscula**
- Al menos **1 minúscula**
- Al menos **1 dígito**
- Al menos **1 carácter especial**

---

### Protección del Sistema

**Permisos correctos:**

```bash
sudo chmod 644 /etc/passwd
sudo chmod 640 /etc/shadow
sudo chown root:shadow /etc/shadow
```

**Verificar permisos:**

```bash
ls -l /etc/passwd /etc/shadow
```

**Resultado esperado:**

```
-rw-r--r-- 1 root root   /etc/passwd
-rw-r----- 1 root shadow /etc/shadow
```

---

## Herramientas Adicionales

### CrackLib - Verificador de Contraseñas

**Instalación:**

```bash
sudo apt install cracklib-runtime
```

**Verificar contraseña:**

```bash
echo "password123" | cracklib-check
# Resultado: password123: it is too simplistic/systematic
```

---

### pwscore - Evaluación de Fortaleza

**Uso:**

```bash
echo "MyP@ssw0rd123!" | pwscore
# Resultado: Score entre 0-100
```

---

## Contramedidas y Defensa

### Prevención de Ataques

**1. Bloqueo de intentos fallidos:**

```bash
# Configurar en /etc/pam.d/common-auth
auth required pam_tally2.so deny=5 unlock_time=900
```

**2. Auditoría de intentos:**

```bash
sudo lastb | head -20
```

**3. Monitoreo de logs:**

```bash
sudo tail -f /var/log/auth.log | grep -i "failed password"
```

---

### Detección de Actividad Sospechosa

**Usuarios conectados actualmente:**

```bash
who
w
last | head -20
```

**Últimos logins fallidos:**

```bash
sudo lastb
```

**Sesiones SSH activas:**

```bash
ss -tunap | grep :22
```

---

## Recursos y Referencias

### Herramientas Mencionadas

- **John the Ripper:** https://www.openwall.com/john/
- **Hashcat:** https://hashcat.net/hashcat/
- **CrackLib:** https://github.com/cracklib/cracklib

### Documentación

- `man shadow`
- `man passwd`
- `man pam.d`
- `man chage`

---