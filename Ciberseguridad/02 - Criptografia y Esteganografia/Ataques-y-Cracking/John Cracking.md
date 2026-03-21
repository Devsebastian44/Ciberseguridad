## Introducción a John the Ripper

**John the Ripper** es una herramienta de código abierto diseñada para detectar contraseñas débiles en sistemas Unix.

Es altamente configurable y soporta múltiples formatos de hash.

---

## Instalación

### Kali Linux

```bash
john --version
sudo apt update
sudo apt install john-jumbo
```

---

### Ubuntu/Debian

```bash
sudo apt update
sudo apt install john
```

---

## Uso Básico

### Sintaxis Básica

```bash
john [opciones] [archivo_hashes]
```

---

### Primer Ejemplo

```bash
echo "usuario1:\$6\$salt\$hashedpassword" > hashes.txt
john hashes.txt
```

---

### Mostrar Contraseñas Crackeadas

```bash
john --show hashes.txt
john --show --format=crypt hashes.txt
```

---

## Formatos de Hash Soportados

### Listar Formatos

```bash
john --list=formats
```

---

### Formatos Comunes

```bash
john --format=Raw-MD5 hashes.txt
john --format=Raw-SHA1 hashes.txt
john --format=NT hashes.txt           # NTLM (Windows)
john --format=crypt hashes.txt        # Unix/Linux
```

---

## Tipos de Ataques

### Ataque de Diccionario

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
john --format=Raw-MD5 --wordlist=diccionario.txt hashes.txt
```

---

### Ataque de Fuerza Bruta

**Modo incremental (todos los caracteres):**

```bash
john --incremental hashes.txt
```

**Solo minúsculas:**

```bash
john --incremental=Lower hashes.txt
```

**Solo dígitos:**

```bash
john --incremental=Digits hashes.txt
```

---

### Reglas de Mutación

**Con reglas predefinidas:**

```bash
john --rules --wordlist=diccionario.txt hashes.txt
```

**Reglas específicas:**

```bash
john --rules=Wordlist --wordlist=diccionario.txt hashes.txt
```

---

## Configuración Avanzada

### Archivo de Configuración

**Ubicaciones:**

```
/etc/john/john.conf
~/.john/john.conf
```

---

### Crear Reglas Personalizadas

**Editar `john.conf`:**

```conf
[List.Rules:MiRegla]
$[0-9]$[0-9]    # Agregar 2 dígitos al final
c               # Capitalizar primera letra
$!              # Agregar ! al final
$@              # Agregar @ al final
$#              # Agregar # al final
```

**Usar reglas personalizadas:**

```bash
john --rules=MiRegla --wordlist=diccionario.txt hashes.txt
```

---

## Herramientas Auxiliares

### Unshadow

**Combinar `/etc/passwd` y `/etc/shadow`:**

```bash
unshadow /etc/passwd /etc/shadow > unshadowed.txt
john unshadowed.txt
```

---

### Zip2john

**Extraer hash de archivo ZIP:**

```bash
zip2john archivo.zip > zip_hash.txt
john zip_hash.txt
```

---

### Rar2john

**Extraer hash de archivo RAR:**

```bash
rar2john archivo.rar > rar_hash.txt
john rar_hash.txt
```

---

### Otras Utilidades

```bash
pdf2john archivo.pdf > pdf_hash.txt
office2john documento.docx > office_hash.txt
ssh2john id_rsa > ssh_hash.txt
keepass2john database.kdbx > keepass_hash.txt
```

---

## Ejemplos Prácticos

### Crackear `/etc/shadow`

```bash
# Combinar archivos
sudo unshadow /etc/passwd /etc/shadow > unshadowed.txt

# Crackear
john unshadowed.txt

# Ver resultados
john --show unshadowed.txt
```

---

### Uso de Diccionarios

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
john --show unshadowed.txt
```

---

### Archivos ZIP Protegidos

```bash
# Extraer hash
zip2john archivo.zip > hash.txt

# Crackear
john --format=zip --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

# Ver contraseña
john --show hash.txt
```

---

## Gestión de Sesiones

### Guardar Progreso

**John guarda automáticamente en:**

```
~/.john/john.pot
```

---

### Restaurar Sesión

```bash
# John restaura automáticamente al ejecutar
john hashes.txt

# Ver estado actual
john --status
```

---

## Mejores Prácticas

### Estrategia de Ataque

**1. Diccionario básico:**

```bash
john --wordlist=rockyou.txt hashes.txt
```

**2. Diccionario + reglas:**

```bash
john --wordlist=rockyou.txt --rules hashes.txt
```

**3. Fuerza bruta incremental:**

```bash
john --incremental hashes.txt
```

---

### Optimización

- Usar **--fork** para múltiples CPUs
- Especificar **--format** para mejor rendimiento
- Usar diccionarios **optimizados** por probabilidad
- Aplicar **reglas** antes de fuerza bruta

---

## Consideraciones

- **Solo** usar en auditorías autorizadas
- **Proteger** archivo `.john/john.pot` (contiene contraseñas)
- **Documentar** permisos obtenidos
- Respetar **privacidad** de usuarios

---