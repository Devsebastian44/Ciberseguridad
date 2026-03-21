## Benchmarking de Modelos

### Importancia del Benchmarking

- **Evaluar** rendimiento de diferentes modelos
- **Comparar** capacidades específicas
- **Seleccionar** el modelo adecuado para cada tarea

---

### Recursos

- **LLM Arena Leaderboard**
- **HuggingFace Arena**
- **Benchmarks específicos** por dominio

---

## Fine-Tuning

### ¿Qué es Fine-Tuning?

Proceso de **adaptación** de un modelo preentrenado a necesidades específicas mediante **entrenamiento adicional** con datos curados.

---

### ¿Cuándo usar Fine-Tuning?

- Necesitas que el modelo **aprenda patrones nuevos**
- **Especialización** en un dominio específico
- **Mejora de precisión** en tareas particulares
- **Consistencia** en estilo de respuesta

---

### Datos Requeridos

- **Conjunto de datos curado**
- **Ejemplos específicos** para entrenamiento
- Datos de **calidad y relevantes**

---

### Implementación

```python
# Google AI Studio proporciona herramientas de Fine-Tuning
# https://aistudio.google.com/app/library
```

---

## RAG (Retrieval Augmented Generation)

### ¿Qué es RAG?

Técnica que combina la **generación de texto** con la **recuperación de información externa** para proporcionar respuestas más precisas y actualizadas.

---

## Arquitectura RAG

1. **Base de Conocimiento** → Vector Database
2. **Query** → Embedding del usuario
3. **Retrieval** → Búsqueda de documentos relevantes
4. **Augmentation** → Combinación con el prompt
5. **Generation** → Respuesta final del LLM

---

### ¿Cuándo usar RAG?

- Necesitas **respuestas actualizadas**
- **No quieres modificar** el modelo base
- Integrar **información externa** o privada
- Información que **cambia frecuentemente**

---

### Datos Requeridos

- **Base de datos** de documentos
- **Sistema de embeddings**
- **Índice vectorial** para búsqueda

---

## Fine-Tuning vs RAG

|Aspecto|Fine-Tuning|RAG|
|---|---|---|
|**Ventajas**|• Mejora precisión en tareas específicas <br> • Reduce dependencia de documentos externos <br> • Mejora coherencia del estilo|• No requiere modificar modelo base <br> • Información en tiempo real <br> • Más eficiente y económico|
|**Desventajas**|• Requiere tiempo y recursos computacionales <br> • Puede volverse obsoleto <br> • Necesita reentrenamiento|• Depende de calidad de documentos <br> • Respuestas menos coherentes si información inconsistente|

---

## Vector Databases

### ¿Qué son?

- Almacenan **embeddings** de documentos
- Permiten **búsqueda semántica** eficiente

---

### Ejemplos

- **Pinecone**
- **Weaviate**
- **Chroma**

---