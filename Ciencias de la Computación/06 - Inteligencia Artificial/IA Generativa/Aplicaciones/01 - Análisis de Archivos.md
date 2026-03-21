## Análisis de Tablas Excel/CSV

### Herramientas

- **Pandas + OpenAI/LLMs** - Interpretación de DataFrames
- **LangChain** - Framework de análisis
- **ChatGPT Code Interpreter** - Análisis interactivo
- **Jupyter/Google Colab** - Notebooks con IA

---

### Ejemplo de Uso

```python
import pandas as pd

# Cargar datos
df = pd.read_csv("ventas.csv")
print(df.describe())

# Consultar a la IA:
# "¿Cuál fue el producto más vendido en 2023?"
```

---

## Análisis de PDFs

### Herramientas

- **PDFReader + LLM** (ChatGPT, Claude)
- **PyMuPDF, pdfplumber** - Bibliotecas Python
- **LangChain + PDFLoader** - Procesamiento de documentos
- **ChatGPT** - Carga directa de PDFs

---

### Ejemplo de Uso

```python
from langchain.document_loaders import PyPDFLoader

# Cargar PDF
loader = PyPDFLoader("contrato.pdf")
pages = loader.load_and_split()

# Consultas:
# "Resume los puntos clave del contrato"
# "¿Cuáles son las cláusulas de pago?"
```

---

## Análisis de Imágenes

### Herramientas

- **GPT-4 con visión** - Modelo multimodal
- **CLIP** (Contrastive Language-Image Pretraining)
- **DALL·E, Stable Diffusion** - Generación y análisis
- **ChatGPT** - Entrada de imágenes

---

### Ejemplo de Uso

**Consultas típicas:**

- "¿Qué está ocurriendo en esta imagen?"
- "Describe los objetos y posibles acciones"
- "Identifica elementos en la fotografía"

---

## Análisis de Audios

### Herramientas

- **Whisper (OpenAI)** - Transcripción de audio
- **Speech-to-Text APIs** - Google, Azure, AssemblyAI
- **Integración con LLMs** - Resumir transcripciones

---

### Ejemplo de Uso

```bash
# Transcripción con Whisper
whisper archivo.mp3 --model medium --language Spanish
```

**Consultas sobre la transcripción:**

- "Resume el audio en 3 frases"
- "¿Qué temas se mencionan en la reunión?"
- "Extrae las conclusiones principales"

---