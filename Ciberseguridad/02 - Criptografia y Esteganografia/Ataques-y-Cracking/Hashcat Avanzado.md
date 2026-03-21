## Introducción a Hashcat

**Hashcat** es considerado el **"cracker de contraseñas más rápido del mundo"**.

Utiliza la potencia de **GPU** y **CPU** para crackear hashes de manera extremadamente eficiente.

---

## Instalación

### Kali Linux

```bash
hashcat --version
sudo apt install hashcat
```

---

### Drivers GPU

```bash
# NVIDIA
sudo apt install nvidia-driver

# AMD
sudo apt install mesa-opencl-icd
```

---

## Arquitectura de Hashcat

### Componentes Principales

- **Motor de Hash** - Algoritmos optimizados
- **Motor de Ataque** - Generación de candidatos
- **Motor de Reglas** - Transformaciones de palabras
- **Motor de Distribución** - Multi-GPU

---

## Modos de Ataque

### Modo 0: Diccionario Directo

```bash
hashcat -m 0 -a 0 hashes.txt wordlist.txt
```

---

### Modo 1: Combinación

```bash
hashcat -m 0 -a 1 hashes.txt wordlist1.txt wordlist2.txt
```

---

### Modo 3: Fuerza Bruta

```bash
hashcat -m 0 -a 3 hashes.txt ?a?a?a?a?a?a
```

---

### Modo 6: Híbrido (Diccionario + Máscara)

```bash
hashcat -m 0 -a 6 hashes.txt wordlist.txt ?d?d?d
```

---

## Tipos de Hash Soportados

### Hashes Comunes

```bash
hashcat -m 0 hashes.txt wordlist.txt      # MD5
hashcat -m 100 hashes.txt wordlist.txt    # SHA-1
hashcat -m 1400 hashes.txt wordlist.txt   # SHA-256
hashcat -m 1000 hashes.txt wordlist.txt   # NTLM (Windows)
hashcat -m 1800 hashes.txt wordlist.txt   # SHA-512 Crypt (Linux)
```

---

### Hashes con Salt

```bash
hashcat -m 10 hashes.txt wordlist.txt     # MD5 con salt
hashcat -m 110 hashes.txt wordlist.txt    # SHA-1 con salt
```

**Formato:**

```
hash:salt
```

---

## Máscaras y Charsets

### Máscaras Predefinidas

```
?l = letras minúsculas (a-z)
?u = letras mayúsculas (A-Z)
?d = dígitos (0-9)
?s = símbolos especiales
?a = todos los anteriores
?h = hexadecimal (0-9a-f)
?b = bytes (0x00-0xff)
```

---

### Ejemplos de Máscaras

```bash
# 8 caracteres cualquiera
hashcat -m 0 -a 3 hashes.txt ?a?a?a?a?a?a?a?a

# 4 letras + 4 dígitos
hashcat -m 0 -a 3 hashes.txt ?l?l?l?l?d?d?d?d

# Charset personalizado
hashcat -m 0 -a 3 hashes.txt -1 ?l?d Password?1?1?1
```

---

## Reglas de Mutación

### Uso de Reglas

```bash
# Con archivo de reglas
hashcat -m 0 -a 0 hashes.txt wordlist.txt -r /usr/share/hashcat/rules/best64.rule

# Múltiples archivos de reglas
hashcat -m 0 -a 0 hashes.txt wordlist.txt -r reglas1.rule -r reglas2.rule
```

---

### Sintaxis de Reglas Básicas

```
:      # No cambio
c      # Capitalizar primera letra
u      # TODO MAYÚSCULAS
l      # todo minúsculas
$1$2$3 # Agregar 123 al final
^Pass  # Agregar "Pass" al inicio
d      # Duplicar palabra
r      # Invertir palabra
```

**Ejemplo de archivo de reglas:**

```
:
c
u
$1$2$3
$2$0$2$4
sa@ se3 si1 so0
```

---

## Optimización de Rendimiento

### Configuración GPU

```bash
# Seleccionar GPU específica
hashcat -m 0 -a 3 -d 1 hashes.txt ?a?a?a?a?a?a

# Workload máximo
hashcat -m 0 -a 3 -w 3 hashes.txt ?a?a?a?a?a?a
```

**Niveles de workload (-w):**

- `1` = Low (PC usable)
- `2` = Default (balance)
- `3` = High (máximo rendimiento)
- `4` = Nightmare (sistema no usable)

---

### Sesiones y Checkpoint

```bash
# Crear sesión
hashcat -m 0 -a 3 --session=misesion hashes.txt ?a?a?a?a?a?a

# Restaurar sesión
hashcat --restore --session=misesion

# Auto-guardar cada 60 segundos
hashcat -m 0 -a 3 --restore-timer=60 hashes.txt ?a?a?a?a?a?a
```

---

## Utilidades de Hashcat

### Generar Candidatos

```bash
# Desde máscara
hashcat --stdout -a 3 ?l?l?l?l > candidates.txt

# Con reglas
hashcat -a 0 wordlist.txt -r best64.rule --stdout > mutaciones.txt
```

---

### Combinator

```bash
combinator wordlist1.txt wordlist2.txt > combined.txt
```

---

### Análisis de Hashes

```bash
# Identificar tipo de hash
hashcat --identify hash.txt

# Benchmark
hashcat -b
```

---

## Mejores Prácticas

### Estrategia de Ataque

**1. Diccionario básico**

```bash
hashcat -m [tipo] -a 0 hashes.txt wordlist.txt
```

**2. Diccionario + reglas**

```bash
hashcat -m [tipo] -a 0 hashes.txt wordlist.txt -r best64.rule
```

**3. Híbrido**

```bash
hashcat -m [tipo] -a 6 hashes.txt wordlist.txt ?d?d?d
```

**4. Fuerza bruta**

```bash
hashcat -m [tipo] -a 3 hashes.txt --increment --increment-min=6 --increment-max=8 ?a?a?a?a?a?a?a?a
```

---

## Consideraciones

- **Solo** usar en auditorías autorizadas
- Usar **-w 3** para máximo rendimiento
- Mantener **drivers actualizados**
- **Proteger** resultados obtenidos

---