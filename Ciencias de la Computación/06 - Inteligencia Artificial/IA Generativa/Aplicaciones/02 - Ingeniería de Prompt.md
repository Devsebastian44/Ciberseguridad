## Fundamentos de los Modelos de Lenguaje

### Tokenización

Los **tokens** son las unidades básicas que procesa el modelo:

- **Palabras completas**
- **Subpalabras**
- **Caracteres especiales**

---

### Parámetro de Temperatura

La **temperatura** controla la **aleatoriedad** en la selección de tokens:

- **Temp = 0** → Determinista (siempre la misma respuesta)
- **Temp < 1** → Conservador (predecible)
- **Temp = 1** → Natural (balanceado)
- **Temp > 1** → Creativo (aleatorio)

---

#### Configuraciones Recomendadas

1. **Análisis factual:** 0.1–0.3
2. **Conversación natural:** 0.7–0.9
3. **Escritura creativa:** 1.0–1.5

---

## ¿Qué es la Ingeniería de Prompts?

Diseñar, optimizar y refinar **instrucciones** para obtener respuestas **precisas y útiles** de modelos de lenguaje.

---

## Principales Recomendaciones

### Claridad y Especificidad

**❌ Prompt vago:**

```
Háblame sobre marketing
```

**✅ Prompt específico:**

```
Explica 3 estrategias de marketing digital para pequeñas empresas en 2024
```

---

### Estructura Clara

**Plantilla recomendada:**

```
CONTEXTO: [Situación o antecedentes]
TAREA: [Qué debe hacer el modelo]
FORMATO: [Cómo debe responder]
RESTRICCIONES: [Qué evitar o límites]
```

---

### Proporcionar Ejemplos

**Ejemplo de clasificación de sentimientos:**

```
Clasifica el sentimiento de estas reseñas:

Reseña: "Excelente producto, superó mis expectativas"
Sentimiento: Positivo

Reseña: "No funciona como esperaba, decepcionante"
Sentimiento: Negativo

Reseña: "El producto llegó tarde y roto"
Sentimiento: [respuesta del modelo]
```

---

### Definir el Rol

**Ejemplo:**

```
Actúa como analista financiero senior con 10 años de experiencia.
Analiza el siguiente estado financiero...
```

---

### Pedir Razonamiento Explícito

**Ejemplo:**

```
Explica tu razonamiento paso a paso antes de dar la respuesta final.
```

---

### Usar Instrucciones Negativas

**Ejemplo:**

```
NO incluyas información especulativa.
NO uses jerga técnica.
NO superes 200 palabras.
```

---

## Técnicas Zero-shot y Few-shot

### Zero-shot Prompting

**Definición:** Tarea **sin ejemplos previos**.

**Ejemplo:**

```
Traduce al francés: "Buenos días"
```

---

### Few-shot Prompting

**Definición:** Proporcionar **1–5 ejemplos** antes de la tarea.

**Ejemplo:**

```
Traduce al francés:
"Buenos días" → "Bonjour"
"Gracias" → "Merci"
"Adiós" → [respuesta del modelo]
```

---

### Chain of Thought (CoT)

Solicitar al modelo que **muestre su razonamiento** paso a paso.

#### **Zero-shot CoT**

Añadir: **"Piensa paso a paso"**

```
Resuelve: 23 × 47
Piensa paso a paso.
```

#### **Few-shot CoT**

Proporcionar ejemplos con **razonamiento explícito**:

```
Problema: 15 × 12
Razonamiento: 
15 × 10 = 150
15 × 2 = 30
150 + 30 = 180

Problema: 23 × 47
Razonamiento: [respuesta del modelo]
```

---

## Técnicas Avanzadas

### Least-to-Most Prompting

**Definición:** Descomponer problemas complejos en **pasos simples**.

**Ejemplo:**

```
Problema complejo: Calcular el ROI de una campaña de marketing

Paso 1: ¿Cuál es la inversión total?
Paso 2: ¿Cuáles son los ingresos generados?
Paso 3: Calcula el ROI usando la fórmula
```

---

### Self-Consistency

**Definición:** Generar **múltiples razonamientos** y elegir el más frecuente.

**Proceso:**

1. Generar 5 respuestas diferentes
2. Analizar razonamientos
3. Seleccionar la respuesta más común

---

### Chain of Verification (CoVe)

**Proceso de verificación en pasos:**

1. **Respuesta inicial** - Generar respuesta
2. **Preguntas de verificación** - ¿Es correcta? ¿Tiene sentido?
3. **Corrección final** - Ajustar si es necesario

---

## Mejores Prácticas Generales

### Checklist para Prompts Efectivos

✅ **Objetivo claro** - ¿Qué quiero lograr? ✅ **Contexto suficiente** - ¿Tiene toda la información? ✅ **Formato especificado** - ¿Cómo debe responder? ✅ **Ejemplos incluidos** - ¿Necesita ejemplos? ✅ **Casos extremos considerados** - ¿Qué puede salir mal?

---

### Principios Fundamentales

1. **Claridad sobre creatividad** - Ser específico es mejor que ser vago
2. **Iteración constante** - Probar y mejorar
3. **Contexto es clave** - Más contexto = mejores respuestas
4. **Validación sistemática** - Verificar resultados

---

### Cuándo Usar Cada Técnica

|Técnica|Cuándo Usar|
|---|---|
|**Zero-shot**|Tareas simples y generales|
|**Few-shot**|Tareas complejas o especializadas|
|**Chain of Thought**|Problemas matemáticos o lógicos|
|**Técnicas Avanzadas**|Problemas muy complejos, alta precisión requerida|

---