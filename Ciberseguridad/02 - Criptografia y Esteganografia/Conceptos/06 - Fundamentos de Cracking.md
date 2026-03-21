## ¿Qué es el Password Cracking?

El **password cracking** es el proceso de recuperar contraseñas desde datos almacenados o transmitidos por un sistema informático.

### Usos Legítimos

- Administradores que han olvidado contraseñas
- **Auditorías de seguridad autorizadas**
- Recuperación de datos propios

### Usos Maliciosos

- Atacantes que buscan **acceso no autorizado**
- Robo de credenciales

---

## Tipos de Ataques de Contraseñas

### Ataque de Diccionario

Utiliza una **lista predefinida de contraseñas comunes** para probar accesos de forma rápida y eficiente.

#### Características

- **Rápido** para contraseñas débiles
- Limitado a contraseñas en el diccionario
- Efectivo contra contraseñas comunes

#### Diccionarios Comunes

- **rockyou.txt** - 14+ millones de contraseñas
- **password.lst** - Lista estándar
- **darkweb2017-top10000.txt** - Top passwords filtradas

---

### Ataque de Fuerza Bruta

Prueba **todas las combinaciones posibles** de caracteres hasta encontrar la contraseña correcta.

#### Características

- **Garantiza** encontrar la contraseña eventualmente
- **Extremadamente lento** para contraseñas largas
- Consumo intensivo de recursos

#### Ejemplo de Complejidad

- 8 caracteres alfanuméricos = **62^8 = 218 billones** de combinaciones

---

### Ataque Híbrido

Combina **diccionario con mutaciones** para probar variaciones de palabras comunes.

#### Características

- Más efectivo que diccionario puro
- Prueba variaciones predecibles
- Balance entre velocidad y cobertura

#### Ejemplos de Mutaciones

```
password → password123
password → Password!
password → p@ssw0rd
password → Password2024!
```

---

### Ataque de Máscara

Utiliza **patrones conocidos** de contraseñas para definir la estructura esperada.

#### Sintaxis de Máscara

- `?l` = minúscula
- `?u` = mayúscula
- `?d` = dígito
- `?s` = símbolo

#### Ejemplo de Uso

```
Máscara: ?u?l?l?l?l?d?d?d
Resultado: Password123
(1 mayúscula, 4 minúsculas, 3 dígitos)
```

---

## Tipos de Hashes Comunes

### Hashes de Sistema

#### **MD5**

- Velocidad: **Muy rápido**
- Seguridad: **Inseguro** (colisiones conocidas)
- Uso: **No recomendado** para contraseñas

#### **SHA-1**

- Velocidad: Rápido
- Seguridad: **Comprometido** (colisiones demostradas)
- Uso: **No recomendado**

#### **SHA-256/SHA-512**

- Velocidad: Rápido
- Seguridad: Más seguros
- Limitación: Sin salt, **vulnerable a rainbow tables**

---

### Hashes de Contraseñas (Diseñados para ser Lentos)

#### **bcrypt**

- Tipo: Adaptativo
- Seguridad: **Muy seguro**
- Característica: Ajustable con **"cost factor"**

#### **scrypt**

- Tipo: **Memory-hard**
- Seguridad: **Muy seguro**
- Característica: Resistente a hardware especializado

#### **PBKDF2**

- Tipo: Estándar **NIST**
- Seguridad: **Seguro**
- Característica: Configurable (iteraciones)

#### **Argon2**

- Tipo: Ganador **PHC 2015**
- Seguridad: **Muy seguro**
- Característica: **Memory-hard** y configurable

---

### Hashes de Sistemas Operativos

#### **NTLM (Windows)**

- Algoritmo: MD4
- Seguridad: **Vulnerable**
- Estado: Actual en Windows

#### **LM (Windows Legacy)**

- Algoritmo: DES
- Seguridad: **Muy vulnerable**
- Estado: Obsoleto desde Vista

#### **Unix DES**

- Algoritmo: DES modificado
- Seguridad: **Vulnerable**
- Estado: Sistemas Unix antiguos

#### **Unix SHA-512**

- Algoritmo: SHA-512 crypt
- Formato: `$6$salt$hash`
- Seguridad: **Seguro**
- Estado: Actual en Linux moderno

---

## Factores que Afectan el Cracking

### Longitud de Contraseña

El impacto de la longitud es **exponencial** en la dificultad de cracking.

#### Tiempo Estimado

- **6 caracteres** - Minutos
- **8 caracteres** - Horas/días
- **10 caracteres** - Meses/años
- **12+ caracteres** - Inviable con fuerza bruta

---

### Complejidad de Caracteres

#### Conjuntos de Caracteres

- **Solo minúsculas (26)** - Débil
- **Alfanumérico (62)** - Medio
- **Con símbolos (95)** - Fuerte

---

### Algoritmo de Hash

La velocidad de cracking varía dramáticamente según el algoritmo.

#### Velocidad de Cracking (GPU)

- **MD5** - 100+ GH/s
- **NTLM** - 100+ GH/s
- **bcrypt** - 50 KH/s (**2000x más lento**)

---

## Herramientas Principales

### Hashcat

**Características:**

- Usa **GPU** para máxima velocidad
- Soporta **300+ tipos de hash**
- Múltiples modos de ataque
- Optimización avanzada

---

### John the Ripper

**Características:**

- **Multiplataforma** (Windows, Linux, macOS)
- Detección automática de formato
- Reglas de mutación flexibles
- Amplia comunidad

---

### Hydra

**Características:**

- Ataques **online** (SSH, FTP, HTTP)
- Múltiples protocolos soportados
- **Paralelización** de conexiones
- Ideal para servicios de red

---

## Mejores Prácticas para Defensa

### Políticas de Contraseñas

- Longitud mínima: **12+ caracteres**
- Usar **algoritmos lentos** (bcrypt, Argon2)
- Implementar **salt único** por contraseña
- Forzar **complejidad** (mayúsculas, números, símbolos)

---

### Protecciones Adicionales

- Implementar **rate limiting**
- Bloquear tras **múltiples intentos fallidos**
- Usar **MFA** (autenticación multi-factor)
- Monitorear **intentos de acceso sospechosos**

---

## Metodología para Auditoría

### Proceso Recomendado

1. Obtener **autorización por escrito**
2. Comenzar con ataque de **diccionario**
3. Aplicar **reglas de mutación**
4. Usar **máscaras** para patrones comunes
5. **Documentar** todos los hallazgos
6. **Recomendar** mejoras específicas

---

## Consideraciones Éticas y Legales

### Principios Fundamentales

- **Solo** realizar cracking con **autorización explícita**
- **Proteger** todos los datos obtenidos
- **No distribuir** contraseñas crackeadas
- **Cumplir** con leyes locales e internacionales
- **Documentar** permisos y metodología
- **Disclosure responsable** de vulnerabilidades encontradas

---