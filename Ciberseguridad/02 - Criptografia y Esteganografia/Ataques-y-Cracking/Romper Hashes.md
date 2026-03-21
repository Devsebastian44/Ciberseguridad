## Introducción al Ataque de Hashes

El proceso de **"romper" un hash** consiste en encontrar el valor original (plaintext) que produce un hash específico.

Este proceso es fundamental en la auditoría de seguridad y el análisis forense.

---

## Tipos de Ataques de Hash

### Ataques de Fuerza Bruta

**Concepto:** Probar todas las combinaciones posibles

**Ventaja:** Garantía de éxito eventual

**Desventaja:** Tiempo computacional extremo

**Ejemplo en Python:**

```python
import hashlib, itertools, string

def brute_force_hash(target_hash, max_length=4):
    charset = string.ascii_lowercase + string.digits
    for length in range(1, max_length + 1):
        for attempt in itertools.product(charset, repeat=length):
            password = ''.join(attempt)
            if hashlib.md5(password.encode()).hexdigest() == target_hash:
                return password
    return None
```

---

### Ataques de Diccionario

**Concepto:** Usar listas de contraseñas comunes

**Ventaja:** Más rápido que fuerza bruta

**Limitación:** Solo funciona con contraseñas conocidas

**Ejemplo en Python:**

```python
def dictionary_attack(target_hash, dictionary_file):
    with open(dictionary_file, 'r') as f:
        for password in f:
            password = password.strip()
            if hashlib.sha256(password.encode()).hexdigest() == target_hash:
                return password
    return None
```

---

### Ataques Rainbow Tables

**Concepto:** Tablas precomputadas hash-valor

**Ventaja:** Intercambio espacio-tiempo

**Desventaja:** Requiere almacenamiento masivo

---

## Herramientas de Cracking

### Hashcat

**Ataque de diccionario:**

```bash
hashcat -m 0 -a 0 hash.txt rockyou.txt
```

**Fuerza bruta con máscara:**

```bash
hashcat -m 0 -a 3 hash.txt ?l?l?l?l?d?d?d?d
```

**Híbrido (diccionario + números):**

```bash
hashcat -m 0 -a 6 hash.txt rockyou.txt ?d?d?d?d
```

---

### John the Ripper

**Diccionario:**

```bash
john --wordlist=rockyou.txt hash.txt
```

**Con reglas:**

```bash
john --wordlist=rockyou.txt --rules hash.txt
```

**Ver resultados:**

```bash
john --show hash.txt
```

---

### CrackStation

**Características:**

- Servicio online
- Base de datos con millones de hashes precomputados
- Limitación: dependiente de su base de datos

**URL:** https://crackstation.net/

---

## Algoritmos de Hash Vulnerables

### MD5

**Estado:** Criptográficamente roto

**Vulnerabilidad:** Colisiones conocidas

**Velocidad de cracking:** Muy rápido

**Recomendación:** No usar para seguridad

---

### SHA-1

**Estado:** Criptográficamente roto

**Vulnerabilidad:** Colisiones demostradas en 2017

**Uso actual:** Siendo eliminado gradualmente

---

### SHA-256

**Estado:** Actualmente seguro

**Resistencia:** No se conocen ataques prácticos

**Uso:** Ampliamente recomendado

---

## Defensas contra Ataques de Hash

### Salting

**Concepto:** Agregar valor aleatorio único a cada contraseña

**Ejemplo en Python:**

```python
import hashlib, os

def hash_with_salt(password):
    salt = os.urandom(32)
    password_hash = hashlib.pbkdf2_hmac(
        'sha256',
        password.encode('utf-8'),
        salt,
        100000
    )
    return salt + password_hash
```

**Beneficio:** Previene rainbow tables y ataques precomputados

---

### Key Stretching

**Concepto:** Aumentar el tiempo de cómputo

**Implementación:** Múltiples iteraciones del hash

**Algoritmos recomendados:**

- **PBKDF2** (Password-Based Key Derivation Function 2)
- **bcrypt** (basado en Blowfish)
- **scrypt** (memory-hard)
- **Argon2** (ganador de Password Hashing Competition)

---

### Pepper

**Concepto:** Clave secreta adicional

**Almacenamiento:** Separado de la base de datos

**Beneficio:** Protección adicional contra dumps de BD

---

## Mejores Prácticas

### Para Cracking (Auditoría)

- Usar **hashcat** para GPU (más rápido)
- Comenzar con **diccionarios comunes**
- Aplicar **reglas** antes de fuerza bruta
- Identificar **tipo de hash** correctamente

---

### Para Defensa

- **Nunca** usar MD5 o SHA-1 para contraseñas
- Usar **algoritmos modernos** (Argon2, bcrypt)
- Implementar **salt único** por contraseña
- Aplicar **key stretching** (mínimo 100,000 iteraciones)
- Considerar **pepper** para protección adicional

---

## Consideraciones

- **Solo** usar en auditorías autorizadas
- **Proteger** hashes obtenidos
- **No distribuir** contraseñas crackeadas
- **Documentar** metodología y resultados

---