## Concepto

El **cifrado simétrico** utiliza la misma clave para cifrar y descifrar información.

Es más rápido que el asimétrico, pero requiere el intercambio seguro de claves.

---

## Características

### Ventajas

- Alta velocidad de procesamiento
- Menor consumo de recursos computacionales
- Ideal para grandes volúmenes de datos

---

### Desventajas

- Problema de distribución de claves
- Escalabilidad limitada
- Gestión compleja de claves en redes grandes

---

## Tipos de Cifrado Simétrico

### Cifrado de Bloque

**Definición:** Procesa datos en bloques de tamaño fijo (64, 128, 256 bits)

---

#### Modos de Operación

**ECB (Electronic Codebook):**

- Cada bloque se cifra independientemente
- **No recomendado** (patrones visibles)

**CBC (Cipher Block Chaining):**

- Cada bloque se XOR con el anterior
- Requiere IV (Initialization Vector)
- Modo más común

**CFB (Cipher Feedback):**

- Convierte cifrado de bloque en flujo
- No requiere padding

**OFB (Output Feedback):**

- Genera flujo de claves independiente
- Errores no se propagan

**CTR (Counter):**

- Utiliza un contador para generar el flujo
- Paralelizable
- Moderno y eficiente

---

### Cifrado de Flujo

**Definición:** Procesa datos bit a bit o byte a byte

**Características:**

- Más rápido para datos en tiempo real
- Menor latencia
- Sensible a errores de sincronización

**Ejemplos:**

- RC4 (obsoleto)
- ChaCha20 (moderno)

---

## Algoritmos Principales

### DES (Data Encryption Standard)

**Especificaciones:**

- Tamaño de bloque: **64 bits**
- Tamaño de clave: **56 bits** efectivos
- Número de rondas: **16**
- Estado: **Obsoleto** por seguridad insuficiente

---

### 3DES (Triple DES)

**Proceso:**

```text
1. Cifrar con clave K1
2. Descifrar con clave K2
3. Cifrar con clave K3
```

**Características:**

- Tamaño efectivo: **112 bits**
- Estado: En desuso, reemplazar por AES

---

### AES (Advanced Encryption Standard)

**Especificaciones:**

- Sucesor de DES
- Tamaños de clave: **128, 192, 256 bits**
- Tamaño de bloque: **128 bits**
- Número de rondas: 10, 12, 14 (según clave)

**Características:**

- **Altamente seguro** y eficiente
- Estándar actual para cifrado simétrico
- Ampliamente implementado

---

## Gestión de Claves

### Generación de Claves

**Mejores prácticas:**

- Utilizar generadores de números **aleatorios criptográficamente seguros** (CSPRNG)
- **Entropía suficiente** para evitar predictibilidad
- Longitud adecuada según el nivel de seguridad requerido

**Herramientas:**

```bash
# Generar clave aleatoria de 256 bits
openssl rand -hex 32

# Generar clave base64
openssl rand -base64 32
```

---

### Distribución de Claves

**Métodos seguros:**

- **Intercambio fuera de banda** (físico, llamada telefónica)
- **Cifrado asimétrico** (RSA, Diffie-Hellman)
- **Protocolos de intercambio** (TLS, IKE)
- Key Derivation Functions (KDF)

---

### Almacenamiento de Claves

**Opciones seguras:**

- **HSM** (Hardware Security Module) para entornos críticos
- **Almacenamiento cifrado** (vault, keychain)
- **Separación** de claves y datos
- **Control de acceso** estricto

---

## Comparación de Algoritmos

|Algoritmo|Tamaño Clave|Tamaño Bloque|Estado|Uso|
|---|---|---|---|---|
|**DES**|56 bits|64 bits|Obsoleto|No usar|
|**3DES**|168 bits|64 bits|En desuso|Migrar a AES|
|**AES-128**|128 bits|128 bits|Seguro|Recomendado|
|**AES-256**|256 bits|128 bits|Muy seguro|Datos sensibles|

---

## Mejores Prácticas

### Selección de Algoritmo

- Usar **AES** como estándar
- Evitar **DES** y **3DES**
- Considerar **ChaCha20** para móviles
- Tamaño mínimo de clave: **128 bits**

---

### Implementación Segura

- **Nunca** reutilizar claves
- Usar **IV aleatorio** único para cada operación
- Implementar **padding** correctamente (PKCS#7)
- Usar **modos autenticados** (GCM, CCM)
- **Proteger** contra ataques de canal lateral

---

### Rotación de Claves

- Establecer **política de rotación** periódica
- Rotar al **detectar compromiso**
- **Documentar** procedimientos de rotación
- Mantener **registro** de claves antiguas (solo para descifrado)

---

## Consideraciones de Seguridad

- **No** inventar algoritmos propios
- Usar **bibliotecas criptográficas** bien establecidas (OpenSSL, libsodium)
- **Actualizar** regularmente las bibliotecas
- Implementar **gestión de claves** robusta
- **Auditar** uso de criptografía regularmente

---