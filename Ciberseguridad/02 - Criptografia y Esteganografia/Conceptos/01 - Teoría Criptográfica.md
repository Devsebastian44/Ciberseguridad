## ¿Qué es la Criptografía?

La **criptografía** es la ciencia que se encarga de proteger la información mediante técnicas de cifrado, asegurando que solo las personas autorizadas puedan acceder a ella.

---

## Objetivos Principales de la Criptografía

### Confidencialidad

Proteger la información de **accesos no autorizados** y mantener el contenido privado.

### Integridad

Garantizar que la información **no ha sido alterada** durante su almacenamiento o transmisión.

### Autenticación

Verificar la **identidad del emisor** y confirmar el origen legítimo de la información.

### No Repudio

Evitar que el emisor pueda **negar haber enviado** la información o realizar una acción.

---

## Conceptos Fundamentales

### Terminología Básica

#### **Texto plano (Plaintext)**

- Información original **sin cifrar**
- Legible y comprensible

#### **Texto cifrado (Ciphertext)**

- Información **después del proceso de cifrado**
- Ilegible sin la clave correcta

#### **Clave (Key)**

- Valor utilizado para **cifrar y descifrar** información
- Debe mantenerse secreta

#### **Algoritmo**

- Método matemático utilizado para el cifrado
- Puede ser público

#### **Cifrado**

- Proceso de convertir **texto plano en texto cifrado**
- También llamado encriptación

#### **Descifrado**

- Proceso inverso de convertir **texto cifrado en texto plano**
- También llamado desencriptación

---

## Principios de Kerckhoffs

Los **Principios de Kerckhoffs** establecen los fundamentos de la seguridad criptográfica moderna, enfatizando que la seguridad debe residir en la clave, no en el secreto del algoritmo.

### Los Seis Principios

1. El sistema debe ser **prácticamente indescifrable**, si no matemáticamente
    
2. **No debe requerir secreto** y puede caer en manos del enemigo sin inconvenientes
    
3. La clave debe ser **comunicable y retenible** sin ayuda escrita
    
4. Debe ser aplicable a las **comunicaciones telegráficas** (o modernas)
    
5. Debe ser **portátil** y su uso no debe requerir varias personas
    
6. Debe ser **fácil de usar** sin gran esfuerzo mental
    

---

## Tipos de Criptografía

### Criptografía Clásica

Métodos históricos de cifrado utilizados antes de la era computacional.

#### **Cifrado por Sustitución**

- Reemplaza caracteres por otros
- Ejemplo: A→D, B→E, C→F

#### **Cifrado por Transposición**

- Cambia el **orden de los caracteres**
- Mantiene los caracteres originales

#### **Cifrado César**

- Desplaza letras del alfabeto un **número fijo de posiciones**
- Ejemplo: desplazamiento de 3 posiciones

---

### Criptografía Moderna

Sistemas criptográficos basados en computación y matemáticas avanzadas.

#### **Cifrado de Bloque**

- Procesa datos en **bloques de tamaño fijo**
- Ejemplos: AES, DES

#### **Cifrado de Flujo**

- Procesa datos **bit a bit** o byte a byte
- Más rápido para datos en streaming

#### **Criptografía Cuántica**

- Utiliza principios de la **mecánica cuántica**
- Promete seguridad absoluta
- Tecnología emergente

---