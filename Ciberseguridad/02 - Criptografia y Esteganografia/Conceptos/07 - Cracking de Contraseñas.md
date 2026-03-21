## Conceptos Fundamentales

### Definición

El **cracking de contraseñas** es el proceso de recuperar contraseñas mediante diversos métodos computacionales, aprovechando debilidades en algoritmos de hash o mediante fuerza bruta.

---

## Tipos de Ataques

### Ataque de Diccionario

**Características:**

- Utiliza listas predefinidas de contraseñas comunes
- Rápido para contraseñas comunes
- Inefectivo contra contraseñas únicas

**Herramientas:** John the Ripper, Hashcat

---

### Ataque de Fuerza Bruta

**Características:**

- Prueba todas las combinaciones posibles
- Garantiza encontrar la contraseña eventualmente
- Tiempo exponencial según la longitud
- Computacionalmente intensivo

**Ejemplo:** Para 8 caracteres alfanuméricos = 62^8 = 218 billones de combinaciones

---

### Ataque Híbrido

**Características:**

- Combina diccionario con modificaciones
- Más efectivo que diccionario puro

**Técnicas comunes:**

- Añadir números al final (password123)
- Capitalizar primera letra (Password)
- Reemplazar caracteres l33t speak (p@ssw0rd)
- Combinar palabras (passwordadmin)

---

### Rainbow Tables

**Características:**

- Tablas precomputadas de hashes
- Intercambia espacio de almacenamiento por tiempo
- Muy rápido para hashes sin salt

**Limitaciones:**

- Inefectivo contra hashes con salt
- Requiere almacenamiento masivo
- Específico por algoritmo

---

## Factores que Afectan la Velocidad

### Algoritmo de Hash

**Algoritmos rápidos:**

- **MD5:** 50+ billion/sec (GPU)
- **SHA-1:** 30+ billion/sec
- **NTLM:** 100+ billion/sec

**Algoritmos lentos (diseñados para resistir):**

- **bcrypt:** ~50,000/sec
- **scrypt:** ~10,000/sec
- **Argon2:** ~5,000/sec

---

### Hardware

**CPU:**

- Múltiples núcleos para paralelización
- Bueno para algoritmos secuenciales

**GPU:**

- Masivamente paralelo (miles de cores)
- Ideal para MD5, SHA-1, NTLM
- Ejemplo: RTX 4090 = 100+ GH/s para MD5

**RAM:**

- Afecta el tamaño de diccionarios cargados
- Importante para reglas complejas

---

### Optimizaciones

**Técnicas:**

- **Reglas de mutación** - transformaciones automáticas
- **Máscaras de patrones** - definir estructura (Password?d?d?d)
- **Distribución en clusters** - múltiples máquinas
- **Uso de GPUs múltiples** - escalabilidad

---

## Complejidad de Contraseñas

### Entropía

**Fórmula:**

```
E = log₂(R^L)
```

Donde:

- **E** = entropía en bits
- **R** = rango de caracteres posibles
- **L** = longitud de contraseña

---

**Ejemplos:**

**8 caracteres solo minúsculas (26):**

```
E = log₂(26^8) = 37.6 bits
```

**8 caracteres alfanuméricos (62):**

```
E = log₂(62^8) = 47.6 bits
```

**12 caracteres con símbolos (95):**

```
E = log₂(95^12) = 79.2 bits
```

---

### Tiempo de Cracking Estimado

**Fórmula:**

```
Tiempo = (R^L) / (2 × velocidad_hash)
```

**Ejemplo práctico:**

```
Contraseña: 8 caracteres alfanuméricos
Combinaciones: 62^8 = 218,340,105,584,896
Velocidad GPU (MD5): 100,000,000,000 h/s
Tiempo promedio: 218T / (2 × 100G) = 1,092 segundos ≈ 18 minutos
```

---

## Técnicas de Defensa

### Password Stretching

**Propósito:** Hacer más lento el proceso de hash

**Implementaciones:**

- **PBKDF2** - Password-Based Key Derivation Function 2
- **bcrypt** - basado en Blowfish
- **scrypt** - memory-hard
- **Argon2** - ganador de Password Hashing Competition

**Beneficio:** Aumenta el tiempo de cracking exponencialmente

---

### Salt

**Función:** Prevenir ataques rainbow table

**Características:**

- Valor aleatorio único por contraseña
- Concatenado con la contraseña antes de hashear
- Almacenado junto al hash

**Implementación:**

```
salt = random_bytes(32)
hash = SHA256(password + salt)
almacenar: salt + hash
```

**Beneficio:** Cada contraseña tiene hash diferente, incluso si son iguales

---

### Pepper

**Función:** Clave secreta adicional

**Características:**

- No se almacena en la base de datos
- Mismo valor para todas las contraseñas
- Protección adicional si la BD es comprometida

---

## Mejores Prácticas

### Para Usuarios

**Crear contraseñas fuertes:**

- Mínimo **12 caracteres**
- Usar **mayúsculas, minúsculas, números, símbolos**
- **No** usar palabras del diccionario
- **No** reutilizar contraseñas
- Usar **gestor de contraseñas**

---

### Para Desarrolladores

**Implementación segura:**

- Usar **algoritmos lentos** (bcrypt, Argon2)
- Implementar **salt único** por contraseña
- **Nunca** almacenar en texto plano
- Aplicar **key stretching** (mínimo 100,000 iteraciones)
- Considerar **pepper** para protección adicional

---

### Para Auditores

**Metodología:**

- Comenzar con **diccionario común**
- Aplicar **reglas de mutación**
- Usar **máscaras** para patrones conocidos
- Intentar **fuerza bruta** solo en cortas
- **Documentar** hallazgos y recomendar mejoras

---

## Consideraciones

- **Solo** realizar cracking en auditorías autorizadas
- **Proteger** hashes obtenidos
- **No distribuir** contraseñas crackeadas
- **Documentar** metodología y resultados
- **Recomendar** mejoras de seguridad

---