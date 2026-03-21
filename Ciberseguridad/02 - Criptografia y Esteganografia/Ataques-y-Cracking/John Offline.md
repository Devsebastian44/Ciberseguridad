## Introducción a John the Ripper

### Descripción

**John the Ripper** es una herramienta de cracking de contraseñas de código abierto, diseñada para detectar contraseñas débiles en sistemas Unix/Linux y Windows.

---

### Características Principales

- Detección automática de múltiples formatos de hash
- Modos de ataque: diccionario, fuerza bruta, incremental
- Reglas flexibles de modificación de contraseñas
- Multiplataforma: Linux, Windows, macOS

---

## Instalación y Configuración

### Linux (Ubuntu/Debian)

```bash
sudo apt-get install john
```

**Compilar desde fuente:**

```bash
git clone https://github.com/openwall/john
cd john/src
make
```

---

### Archivos de Configuración

**Archivos principales:**

- `john.conf` = configuración principal
- `john.pot` = contraseñas crackeadas

**Ubicación:**

- `/etc/john/`
- `~/.john/`

---

## Formatos de Hash Soportados

### Sistemas Unix/Linux

- **DES:** formato tradicional Unix
- **MD5:** `$1$salt$hash`
- **SHA-256:** `$5$salt$hash`
- **SHA-512:** `$6$salt$hash`

---

### Sistemas Windows

- **NTLM:** formato moderno
- **LM:** legacy (desaconsejado)

---

### Aplicaciones Web

- **MySQL**
- **WordPress:** `$P$salt$hash`
- **Drupal:** `$S$salt$hash`

---

## Modos de Operación

### Modo Single

```bash
john --single hashfile
```

**Descripción:** Deriva contraseñas del nombre de usuario

---

### Modo Wordlist

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashfile
```

**Diccionarios comunes:**

- `rockyou.txt`
- `password.lst`
- `darkweb2017-top10000.txt`

---

### Modo Incremental

```bash
john --incremental hashfile
```

**Descripción:** Fuerza bruta inteligente con estadísticas de caracteres

---

## Reglas de Mutación

### Sintaxis Básica

```bash
[List.Rules:Custom]
$[0-9]   # Añadir dígito al final
^[A-Z]   # Capitalizar primera letra
c        # Capitalizar
l        # Minúsculas
u        # Mayúsculas
```

---

### Reglas Avanzadas

```bash
sa4              # s -> 4
so0              # o -> 0
sa@              # s -> @
csa4$[0-9]       # Capitalizar + s->4 + dígito
```

**Usar reglas:**

```bash
john --wordlist=passwords.txt --rules=custom hashes.txt
```

---

## Ejemplos Prácticos

### Cracking de Shadow File

```bash
# Combinar archivos
sudo unshadow /etc/passwd /etc/shadow > hashes.txt

# Crackear
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt

# Ver resultados
john --show hashes.txt
```

---

### Cracking de Hashes NTLM

```bash
# Crear archivo con hash NTLM
echo "user:1001:aad3b435b51404eeaad3b435b51404ee:5835048ce94ad0564e29a924a03510ef:::" > ntlm.txt

# Crackear
john --format=nt ntlm.txt

# Ver resultado
john --show --format=nt ntlm.txt
```

---

### Uso con Reglas Personalizadas

```bash
john --wordlist=passwords.txt --rules=custom hashes.txt
john --wordlist=passwords.txt --rules=Single hashes.txt
```

---

## Optimización y Rendimiento

### Paralelización

**Múltiples CPUs:**

```bash
john --fork=4 hashfile
```

**Distribución en nodos:**

```bash
# Nodo 1 de 4
john --node=1/4 hashfile

# Nodo 2 de 4
john --node=2/4 hashfile
```

---

### Sesiones

**Crear sesión:**

```bash
john --session=mysession hashfile
```

**Restaurar sesión:**

```bash
john --restore=mysession
```

**Ver estado:**

```bash
john --status=mysession
```

---

## Herramientas Auxiliares

### Estadísticas

**Ver estado actual:**

```bash
john --status=session_name
```

**Benchmark:**

```bash
john --test
```

---

## Mejores Prácticas

### Estrategia de Ataque

**1. Modo Single primero:**

```bash
john --single hashes.txt
```

**2. Diccionario común:**

```bash
john --wordlist=rockyou.txt hashes.txt
```

**3. Diccionario + reglas:**

```bash
john --wordlist=rockyou.txt --rules hashes.txt
```

**4. Incremental:**

```bash
john --incremental hashes.txt
```

---

### Optimización

- Usar **--fork** para aprovechar múltiples CPUs
- Especificar **--format** para mejor rendimiento
- Guardar sesiones para ataques largos
- Revisar **john.pot** regularmente

---

## Consideraciones

- **Solo** usar en auditorías autorizadas
- **Proteger** archivo `john.pot` (contiene contraseñas)
- **Documentar** permisos y resultados
- Respetar **privacidad** de usuarios

---