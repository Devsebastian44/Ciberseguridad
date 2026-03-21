## Capacidades Multimodales

Los modelos multimodales pueden procesar y generar **diferentes tipos de contenido**:

- **Texto**
- **Imágenes**
- **Audio**
- **Video**
- **Código**

---

## Ventajas de la Multimodalidad

- **Comprensión** de contexto visual y textual
- **Mejora** en la interacción con IA
- **Aplicaciones** en generación de imágenes
- **Búsqueda** por imagen
- **Mejoras** en accesibilidad

---

## Prompting con Imágenes

### Ejemplo de Prompt Multimodal

```
Actúa como un tutor de inglés para principiantes. 
Aquí tienes una imagen. Describe la escena en la imagen 
usando palabras sencillas para que un estudiante de inglés 
pueda entenderla. Usa oraciones cortas y simples.
```

---

### Implementación con API

```python
from google import genai
from PIL import Image

# Cliente
client = genai.Client(api_key=GEMINI_API_KEY)

# Cargar imagen
image = Image.open("/path/to/imagen.png")

# Generar contenido multimodal
response = client.models.generate_content(
    model='gemini-2.0-flash', 
    contents=[image, "Describe la escena en la imagen usando palabras sencillas"]
)

print(response.text)
```

---

## Prompting con Audio

### Ejemplo

```
Actúa como un tutor de inglés para principiantes. 
Escucha el siguiente archivo de audio en inglés y transcribe 
lo que se dice. Luego, analiza el sentimiento de la conversación 
y explica si es positivo, negativo o neutral.
```

---

## Configuración de Parámetros

```python
response = client.models.generate_content(
    model='gemini-2.0-flash', 
    contents=["Explica el pasado simple"],
    config=types.GenerateContentConfig(
        max_output_tokens=500,
        temperature=0.1  # Controla la creatividad
    )
)
```

---

## Parámetros Importantes

### **Temperature**

- Controla la **aleatoriedad**
- **0.0** = Determinista
- **1.0** = Creativo

### **Max Tokens**

- **Límite** de longitud de respuesta

### **Top-p**

- **Sampling núcleo** para diversidad

### **Tools**

- **Funciones adicionales** disponibles

---