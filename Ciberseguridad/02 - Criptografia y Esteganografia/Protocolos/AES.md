## Introducción

**AES (Advanced Encryption Standard)** es un algoritmo de cifrado simétrico adoptado por el gobierno de Estados Unidos como estándar de cifrado.

Reemplazó al DES y es ampliamente utilizado en todo el mundo.

---

## Características Técnicas

### Especificaciones

**Información básica:**

- Algoritmo: **Rijndael**
- Tipo: Cifrado de bloque simétrico
- Tamaño de bloque: **128 bits**
- Tamaños de clave: **128, 192, 256 bits**
- Número de rondas: **10, 12, 14** (según tamaño de clave)

---

### Operaciones Fundamentales

#### **1. SubBytes**

**Función:** Sustitución no lineal

**Características:**

- Utiliza la S-box (Substitution box)
- Proporciona **confusión**
- Operación byte a byte

---

#### **2. ShiftRows**

**Función:** Desplazamiento cíclico de filas

**Características:**

- Proporciona **difusión**
- Cada fila se desplaza diferente cantidad

---

#### **3. MixColumns**

**Función:** Transformación lineal de columnas

**Características:**

- Usa aritmética en campos finitos GF(2^8)
- Aumenta la **difusión**
- No se aplica en la ronda final

---

#### **4. AddRoundKey**

**Función:** XOR con la clave de ronda

**Características:**

- Incorpora la clave secreta
- Operación reversible
- Único paso que usa la clave

---

## Proceso de Cifrado AES

### AES-128 (10 rondas)

**Pasos:**

```text
1. Expansión de clave (Key Schedule)

2. Ronda inicial:
   - AddRoundKey

3. 9 rondas principales:
   - SubBytes
   - ShiftRows
   - MixColumns
   - AddRoundKey

4. Ronda final:
   - SubBytes
   - ShiftRows
   - AddRoundKey (sin MixColumns)
```

---

### Variantes según Longitud de Clave

|Clave|Rondas|Nivel de Seguridad|
|---|---|---|
|**AES-128**|10|Alto|
|**AES-192**|12|Muy alto|
|**AES-256**|14|Máximo|

---

## Modos de Operación AES

### ECB (Electronic Codebook)

**Características:**

- Cada bloque se cifra independientemente
- Patrones visibles en datos similares
- **No recomendado** para uso general

**Uso:** Solo para datos aleatorios pequeños

---

### CBC (Cipher Block Chaining)

**Características:**

- Cada bloque se XOR con el anterior
- Requiere **IV** (Initialization Vector)
- Propaga errores
- **Modo más común**

**Ventajas:** Oculta patrones

**Desventajas:** No paralelizable para cifrado

---

### CFB (Cipher Feedback)

**Características:**

- Convierte cifrado de bloque en flujo
- Permite cifrar datos menores al bloque
- Propaga errores

---

### OFB (Output Feedback)

**Características:**

- Genera flujo de claves independiente
- No propaga errores
- Requiere IV único

---

### CTR (Counter)

**Características:**

- Utiliza contador para generar flujo
- **Paralelizable** (cifrado y descifrado)
- Acceso aleatorio a datos
- No propaga errores

**Ventajas:** Alto rendimiento

---

### GCM (Galois/Counter Mode)

**Características:**

- **Cifrado autenticado** (AEAD)
- Proporciona integridad y autenticación
- Altamente eficiente
- **Recomendado** para uso moderno

**Ventajas:** Seguridad + rendimiento

---

## Implementación

### Estructura Básica (C)

```c
typedef struct {
    uint8_t state[4][4];      // Estado interno
    uint8_t key[16];          // Clave original
    uint8_t round_keys[176];  // Claves de ronda
} AES_ctx;

void AES_init(AES_ctx* ctx, const uint8_t* key);
void AES_encrypt(AES_ctx* ctx, uint8_t* data);
void AES_decrypt(AES_ctx* ctx, uint8_t* data);
```

---

### Optimización por Hardware

**AES-NI (Intel/AMD):**

- Instrucciones dedicadas de CPU
- Aceleración de 5-10x
- Resistente a ataques de timing

**Otras implementaciones:**

- FPGA para alto throughput
- ASIC para dispositivos dedicados

---

### Implementación Segura

**Consideraciones:**

- **Tiempo constante** (prevenir timing attacks)
- **Protección** contra ataques de canal lateral
- **Gestión segura** de claves en memoria
- **Limpiar** claves después de uso

---

## Seguridad AES

### Resistencia a Ataques

**Ataques conocidos:**

- **Criptoanálisis diferencial:** resistente
- **Criptoanálisis lineal:** resistente
- **Fuerza bruta:** inviable (AES-128 = 2^128 combinaciones)
- **Ataques de canal lateral:** requieren mitigación

---

### Consideraciones de Seguridad

**Mejores prácticas:**

- Usar claves de **longitud adecuada** (mínimo 128 bits)
- **IV único y aleatorio** para cada operación
- **Proteger claves** en memoria (no en disco sin cifrar)
- **Validar entrada** antes de procesar
- Usar **modos autenticados** (GCM) cuando sea posible

---

## Aplicaciones AES

### Estándares y Protocolos

**Seguridad de redes:**

- **WPA2/WPA3** - WiFi
- **IPSec** - VPN
- **SSL/TLS** - HTTPS
- **SSH** - acceso remoto

---

### Aplicaciones Comerciales

**Uso común:**

- **Cifrado de disco** (BitLocker, FileVault)
- **Comunicaciones móviles** (4G, 5G)
- **Servicios cloud** (AWS, Azure, GCP)
- **Aplicaciones bancarias** y financieras
- **Mensajería** (Signal, WhatsApp)

---

## Comparación con Otros Algoritmos

|Algoritmo|Tamaño Bloque|Tamaño Clave|Estado|
|---|---|---|---|
|**DES**|64 bits|56 bits|Obsoleto|
|**3DES**|64 bits|168 bits|En desuso|
|**AES**|128 bits|128/192/256 bits|**Actual**|
|**ChaCha20**|- (flujo)|256 bits|Moderno|

---

## Mejores Prácticas

### Selección de Parámetros

**Longitud de clave:**

- **AES-128:** suficiente para mayoría de casos
- **AES-256:** datos muy sensibles o largo plazo

**Modo de operación:**

- **GCM:** primera opción (autenticado)
- **CBC:** alternativa si GCM no disponible
- **Evitar ECB:** siempre

---

### Gestión de Claves

**Generación:**

- Usar **CSPRNG** (generador criptográfico)
- **Nunca** derivar de contraseñas sin KDF

**Almacenamiento:**

- **HSM** para claves críticas
- **Cifrar** claves en reposo
- **No** hardcodear en código fuente

**Rotación:**

- **Política** de rotación periódica
- **Revocar** claves comprometidas inmediatamente

---

## Consideraciones

- AES es el **estándar de facto** para cifrado simétrico
- Usar **implementaciones probadas** (OpenSSL, libsodium)
- **No** implementar AES manualmente sin experiencia
- Usar **modos autenticados** para prevenir manipulación
- **Actualizar** bibliotecas criptográficas regularmente

---