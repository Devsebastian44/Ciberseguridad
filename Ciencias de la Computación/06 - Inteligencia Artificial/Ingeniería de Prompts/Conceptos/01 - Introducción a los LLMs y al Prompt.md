## ¿Qué son los LLMs?

Los **Large Language Models (LLMs)** son modelos de inteligencia artificial basados en la arquitectura **Transformer** que procesan y generan texto de manera similar al lenguaje humano.

---

## Conceptos Fundamentales

### Tokens

- **Unidades básicas** de procesamiento de texto
- Pueden ser **palabras, partes de palabras o caracteres**
- Determinan el **límite de contexto** del modelo

---

### Embeddings

- **Representaciones numéricas** de palabras o frases
- Capturan el **significado semántico** del texto
- Permiten al modelo entender **relaciones entre conceptos**

---

### Generación de Texto

- Proceso de **predicción** de la siguiente palabra más probable
- Se basa en **patrones aprendidos** durante el entrenamiento

---

## Técnicas de Prompting

### Zero-shot Prompting

Dar instrucciones **directas sin ejemplos previos**.

**Ejemplo:**

```
Simula una conversación en inglés con un estudiante 
que está aprendiendo a presentarse
```

---

### Few-shot Prompting

Incluir **ejemplos** para guiar la respuesta del modelo.

**Ejemplo:**

```
Actúa como un tutor de inglés para principiantes. 
Simula una conversación en inglés con un estudiante 
que está aprendiendo a presentarse. 

Aquí tienes ejemplos previos:

Estudiante: Hello! My name is Ana. What's your name?
Tutor: Hi Ana! My name is John. Nice to meet you!

Ahora continúa la conversación con otro estudiante principiante.
```

---

### Chain-of-Thought (CoT) Prompting

Estructurar el prompt con **pasos específicos** para guiar el razonamiento.

**Ejemplo:**

```
Actúa como un tutor de inglés para principiantes. 
Para ayudar a un estudiante a practicar su presentación 
en inglés, sigue estos pasos:

1️⃣ Haz que el estudiante se presente
2️⃣ Corrige cualquier error y explica por qué
3️⃣ Agrega una pregunta para continuar la conversación
4️⃣ Responde de forma natural y motivadora

Sigue estos pasos para guiar la conversación.
```

---

## Uso de APIs

### Configuración con Gemini API

```python
# Instalación
!pip install -q google-genai

# Imports
from google import genai
from getpass import getpass

# Configuración de API key
GEMINI_API_KEY = getpass('Enter API key: ')

# Cliente
client = genai.Client(api_key=GEMINI_API_KEY)

# Generar contenido
response = client.models.generate_content(
    model='gemini-2.0-flash', 
    contents="Actúa como profe de inglés y explica el pasado imperfecto con ejemplos."
)

print(response.text)
```

---

## Consideraciones Importantes

### Alucinaciones

- **No todas las respuestas** son correctas o reales
- Siempre **verificar** la información crítica
- **Evaluar** las respuestas mediante benchmarking

---

### Mejores Prácticas

- Usar **instrucciones claras** y específicas
- **Probar** diferentes enfoques y plataformas
- **Dividir** preguntas complejas en pasos
- **Evitar** ambigüedad y falta de contexto
- **Practicar** constantemente

---