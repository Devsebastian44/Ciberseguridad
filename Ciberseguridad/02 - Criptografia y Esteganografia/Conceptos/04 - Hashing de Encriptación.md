## Fundamentos del Hashing

### Propiedades de las Funciones Hash

Las funciones hash criptográficas deben cumplir con propiedades específicas para garantizar su seguridad.

#### Propiedades Esenciales

1. **Determinística** - Mismo input produce mismo output siempre
2. **Rápida** - Computación eficiente del hash
3. **Avalanche Effect** - Pequeños cambios causan grandes diferencias en el output
4. **Irreversible** - No se puede obtener el input del output
5. **Resistente a colisiones** - Difícil encontrar dos inputs con mismo hash

---

### Ejemplo Práctico de Análisis

```python
import hashlib

def analyze_hash_properties(text):
    algorithms = ['md5', 'sha1', 'sha256', 'sha512']
    results = {}
    
    for algo in algorithms:
        hash_func = getattr(hashlib, algo)
        hash_value = hash_func(text.encode()).hexdigest()
        results[algo] = {
            'hash': hash_value,
            'length': len(hash_value),
            'bits': len(hash_value) * 4
        }
    
    return results
```

---

## Análisis de Entropía

La **entropía** mide el grado de aleatoriedad o desorden en los datos, siendo un indicador clave para detectar encriptación.

### Medición de Entropía

```python
import math
from collections import Counter

def calculate_entropy(data):
    if not data:
        return 0
    
    counter = Counter(data)
    length = len(data)
    entropy = 0
    
    for count in counter.values():
        probability = count / length
        entropy -= probability * math.log2(probability)
    
    return entropy
```

**Interpretación:**

- **Entropía baja (< 3)** - Datos estructurados o texto plano
- **Entropía media (3-6)** - Datos comprimidos
- **Entropía alta (> 7)** - Datos encriptados o aleatorios

---

## Algoritmos de Encriptación Simétrica

### AES (Advanced Encryption Standard)

**AES** es el estándar de encriptación simétrica más utilizado actualmente, considerado **altamente seguro** y eficiente.

#### Implementación en Python

```python
from cryptography.fernet import Fernet

def aes_encrypt_decrypt_example():
    # Generar clave
    key = Fernet.generate_key()
    cipher = Fernet(key)
    
    # Encriptar
    plaintext = b"Mensaje secreto"
    ciphertext = cipher.encrypt(plaintext)
    
    # Desencriptar
    decrypted = cipher.decrypt(ciphertext)
    
    print(f"Texto original: {plaintext}")
    print(f"Texto encriptado: {ciphertext}")
    print(f"Texto desencriptado: {decrypted}")
```

---

### DES y Triple DES

**DES (Data Encryption Standard)** es considerado **obsoleto** debido a su tamaño de clave pequeño. **Triple DES** aplica DES tres veces para mayor seguridad.

#### Implementación de Triple DES

```python
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
from cryptography.hazmat.backends import default_backend
import os

def des_encryption_example():
    # Generar clave e IV
    key = os.urandom(8)
    iv = os.urandom(8)
    
    # Crear cipher
    cipher = Cipher(
        algorithms.TripleDES(key), 
        modes.CBC(iv), 
        backend=default_backend()
    )
    encryptor = cipher.encryptor()
    
    # Preparar texto con padding
    plaintext = b"Texto de ejemplo para DES"
    pad_length = 8 - (len(plaintext) % 8)
    padded = plaintext + bytes([pad_length] * pad_length)
    
    # Encriptar
    ciphertext = encryptor.update(padded) + encryptor.finalize()
    
    return key, iv, ciphertext
```

---

## Modos de Operación

Los **modos de operación** definen cómo se aplica el algoritmo de encriptación a bloques de datos.

### ECB (Electronic Codebook)

- Cada bloque se encripta **independientemente**
- **Patrones visibles** en datos estructurados
- **No recomendado** para datos confidenciales

---

### CBC (Cipher Block Chaining)

- Cada bloque depende del **bloque anterior**
- Requiere **vector de inicialización (IV)**
- Mejor que ECB, pero vulnerable a ciertos ataques

---

### GCM (Galois/Counter Mode)

- **Encriptación autenticada**
- Proporciona **confidencialidad e integridad**
- **Recomendado** para aplicaciones modernas

---

## Análisis de Debilidades

### Identificación de Patrones

La detección de **bloques repetidos** puede indicar uso de modos de encriptación débiles como ECB.

```python
def detect_encryption_patterns(ciphertext):
    block_size = 16
    blocks = [ciphertext[i:i+block_size] 
              for i in range(0, len(ciphertext), block_size)]
    
    unique_blocks = set(blocks)
    
    return {
        'repeated_blocks': len(blocks) - len(unique_blocks),
        'total_blocks': len(blocks),
        'uniqueness_ratio': len(unique_blocks) / len(blocks)
    }
```

**Interpretación:**

- **Ratio bajo** - Posible uso de ECB o datos estructurados
- **Ratio alto** - Encriptación fuerte o datos aleatorios

---

### Análisis de Frecuencia

El **análisis de frecuencia** ayuda a determinar si los datos están encriptados o comprimidos.

```python
def frequency_analysis(data):
    frequency = {}
    
    # Contar frecuencia de cada byte
    for byte in data:
        frequency[byte] = frequency.get(byte, 0) + 1
    
    # Calcular chi-cuadrado
    expected = len(data) / 256
    chi_squared = sum((count - expected) ** 2 / expected 
                      for count in frequency.values())
    
    return {
        'frequency': frequency,
        'chi_squared': chi_squared,
        'randomness_score': chi_squared / len(data)
    }
```

**Interpretación:**

- **Chi-squared bajo** - Distribución uniforme (encriptación fuerte)
- **Chi-squared alto** - Distribución no uniforme (texto plano o débil)

---

## Herramientas de Análisis

### CyberChef

**CyberChef** es una herramienta web para análisis y transformación de datos con interfaz visual intuitiva.

#### Funcionalidades Principales

- **Decodificación** - Base64, Hex, URL encoding
- **Hashing** - MD5, SHA, BLAKE2
- **Encriptación** - AES, DES, RSA
- **Análisis** - Entropía, frecuencia, XOR

---

### Hashid

Herramienta para **identificación automática** de tipos de hash.

```bash
# Identificar hash desde archivo
hashid -m hash.txt

# Identificar hash específico
hashid -m 5d41402abc4b2a76b9719d911017c592
```

**Salida:** Muestra posibles tipos de hash y modos de Hashcat

---

### Hash-identifier

Herramienta interactiva para **identificar tipos de hash**.

```bash
# Iniciar herramienta interactiva
hash-identifier
```

**Uso:** Pegar el hash y obtener identificación automática del tipo

---