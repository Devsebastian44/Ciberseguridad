## Concepto

El **cifrado asimétrico**, también conocido como criptografía de clave pública, utiliza un par de claves matemáticamente relacionadas:

- **Clave pública:** disponible para todos, se usa para cifrar
- **Clave privada:** secreta, solo conocida por el propietario, se usa para descifrar

---

## Características Principales

### Ventajas

- No requiere intercambio previo de claves secretas
- Permite autenticación digital
- Facilita el no repudio
- Escalable para grandes redes

---

### Desventajas

- Computacionalmente más lento que el cifrado simétrico
- Requiere mayor procesamiento
- Vulnerable a ataques de fuerza bruta si las claves son cortas

---

## Algoritmos Principales

### RSA (Rivest-Shamir-Adleman)

**Proceso de generación de claves:**

```text
1. Seleccionar dos números primos grandes p y q
2. Calcular n = p × q
3. Calcular φ(n) = (p-1) × (q-1)
4. Elegir e tal que 1 < e < φ(n) y gcd(e, φ(n)) = 1
5. Calcular d tal que d × e ≡ 1 (mod φ(n))
6. Clave pública: (e, n)
7. Clave privada: (d, n)
```

**Características:**

- Longitud de clave recomendada: **≥ 2048 bits**
- Uso común: cifrado y firma digital
- Base: factorización de números primos

---

### Diffie-Hellman

**Función:** Permite el intercambio seguro de claves a través de un canal inseguro

**Características:**

- Base para muchos protocolos de intercambio de claves
- Vulnerable al ataque **man-in-the-middle** sin autenticación
- Usado en TLS, IPsec, SSH

---

### Curvas Elípticas (ECC)

**Características:**

- Basado en la matemática de curvas elípticas
- Ofrece la misma seguridad que RSA con claves más cortas
- Más eficiente en términos de procesamiento y ancho de banda

**Comparación:**

- ECC 256 bits ≈ RSA 3072 bits
- ECC 384 bits ≈ RSA 7680 bits

---

## Aplicaciones Prácticas

### Firma Digital

**Proceso:**

```text
1. Crear hash del documento
2. Cifrar el hash con la clave privada
3. Adjuntar la firma al documento
4. Verificar descifrando con la clave pública
```

**Garantiza:**

- Autenticidad del origen
- Integridad del mensaje
- No repudio

---

### Intercambio de Claves

**Usos:**

- Establecimiento de claves de sesión seguras
- Autenticación mutua entre partes
- Prevención de ataques de intercepción

---

## Comparación con Cifrado Simétrico

|Aspecto|Asimétrico|Simétrico|
|---|---|---|
|**Claves**|Par (pública/privada)|Una clave compartida|
|**Velocidad**|Lento|Rápido|
|**Uso típico**|Intercambio de claves, firmas|Cifrado de datos|
|**Longitud de clave**|2048-4096 bits (RSA)|128-256 bits (AES)|

---

## Mejores Prácticas

### Gestión de Claves

- Usar longitudes de clave **≥ 2048 bits** (RSA)
- **Proteger** la clave privada rigurosamente
- **Rotar** claves periódicamente
- Usar **HSM** para claves críticas

---

### Uso Híbrido

**Práctica común:**

1. Usar cifrado **asimétrico** para intercambiar clave de sesión
2. Usar cifrado **simétrico** para datos (más rápido)
3. Ejemplo: **TLS/SSL**

---

## Consideraciones de Seguridad

- **Nunca** compartir la clave privada
- Usar **algoritmos modernos** (RSA ≥ 2048, ECC ≥ 256)
- Implementar **padding** adecuado (OAEP para RSA)
- **Proteger** contra ataques de canal lateral
- Mantener **claves actualizadas**

---