## Introducción

El **Aprendizaje Automático (Machine Learning)** es una rama de la inteligencia artificial que permite a las máquinas aprender **patrones** a partir de datos sin ser explícitamente programadas.

---

## Tipos de Aprendizaje

### Aprendizaje Supervisado

**Definición:**

- Entrenamiento con datos **etiquetados**
- Relación **input-output** conocida
- **Objetivo:** predecir resultados para nuevos datos

---

**Tipos de problemas:**

- **Clasificación:** predecir categorías (spam/no spam, diagnóstico médico)
- **Regresión:** predecir valores numéricos (precios, ventas, temperatura)

---

**Algoritmos principales:**

- **Regresión Lineal**
- **Regresión Logística**
- **Árboles de Decisión**
- **Random Forest**
- **Support Vector Machines (SVM)**
- **Redes Neuronales**
- **K-Nearest Neighbors (KNN)**

---

### Aprendizaje No Supervisado

**Definición:**

- Trabaja con datos **sin etiquetas**
- Busca **patrones** ocultos
- **Objetivo:** descubrir estructuras en los datos

---

**Tipos de problemas:**

- **Clustering:** agrupar datos similares
- **Reducción de dimensionalidad:** simplificar datos manteniendo información
- **Detección de anomalías:** identificar datos atípicos
- **Reglas de asociación:** encontrar relaciones entre elementos

---

**Algoritmos principales:**

- **K-Means**
- **DBSCAN**
- **Clustering Jerárquico**
- **PCA** (Principal Component Analysis)
- **t-SNE**
- **Isolation Forest**
- **Apriori**

---

### Aprendizaje por Refuerzo

**Definición:**

- Aprende mediante **interacción** con entorno
- Basado en **recompensas** y castigos
- **Objetivo:** maximizar recompensas acumuladas

---

**Componentes:**

- **Agente:** toma decisiones
- **Entorno:** proporciona estados
- **Acciones:** decisiones posibles
- **Recompensas:** retroalimentación

---

**Algoritmos principales:**

- **Q-Learning**
- **Deep Q-Networks (DQN)**
- **Policy Gradient**
- **Actor-Critic**
- **Proximal Policy Optimization (PPO)**

---

## Proceso de Aprendizaje Automático

### Fase 1: Recolección de Datos

**Actividades:**

- Identificar **fuentes** de datos
- **Recopilar** datos relevantes
- Asegurar **calidad** y cantidad suficiente

---

### Fase 2: Preparación de Datos

**Actividades:**

- **Limpieza:** eliminar duplicados, corregir errores
- **Normalización:** escalar valores
- **Feature Engineering:** crear características relevantes
- **Manejo** de valores faltantes

---

### Fase 3: División de Datos

**Conjuntos típicos:**

- **Entrenamiento:** 70-80% de datos
- **Validación:** 10-15% de datos
- **Prueba:** 10-15% de datos

---

### Fase 4: Selección del Modelo

**Consideraciones:**

- Tipo de **problema** (clasificación, regresión)
- Tamaño del **dataset**
- Necesidad de **interpretabilidad**
- Recursos **computacionales**

---

### Fase 5: Entrenamiento

**Proceso:**

- **Alimentar** datos al modelo
- **Ajustar** parámetros internos
- **Minimizar** función de pérdida
- **Iteraciones** múltiples (epochs)

---

### Fase 6: Evaluación

**Métricas comunes:**

**Para clasificación:**

- **Accuracy** (Exactitud)
- **Precision** (Precisión)
- **Recall** (Sensibilidad)
- **F1-Score**
- **Matriz de confusión**
- **ROC-AUC**

---

**Para regresión:**

- **MSE** (Mean Squared Error)
- **RMSE** (Root Mean Squared Error)
- **MAE** (Mean Absolute Error)
- **R² Score**

---

### Fase 7: Ajuste de Hiperparámetros

**Técnicas:**

- **Grid Search**
- **Random Search**
- **Bayesian Optimization**
- **Cross-Validation**

---

### Fase 8: Despliegue

**Consideraciones:**

- **Integración** con sistemas existentes
- **Monitoreo** continuo
- **Actualización** periódica
- **Escalabilidad**

---

## Conceptos Fundamentales

### Overfitting (Sobreajuste)

**Definición:**

- Modelo aprende **demasiado** del entrenamiento
- **Buen rendimiento** en entrenamiento
- **Mal rendimiento** en datos nuevos

---

**Soluciones:**

- **Regularización** (L1, L2)
- **Dropout**
- **Early stopping**
- **Más datos** de entrenamiento
- **Cross-validation**

---

### Underfitting (Subajuste)

**Definición:**

- Modelo **demasiado simple**
- **Mal rendimiento** en entrenamiento y prueba
- No captura **patrones** importantes

---

**Soluciones:**

- Aumentar **complejidad** del modelo
- Más **features** relevantes
- Reducir **regularización**
- Entrenar por **más tiempo**

---

### Sesgo vs Varianza

**Sesgo (Bias):**

- Error por **simplificaciones** del modelo
- **Alto sesgo** → underfitting

---

**Varianza:**

- Error por **sensibilidad** a fluctuaciones
- **Alta varianza** → overfitting

---

**Balance:**

- Buscar **equilibrio** óptimo
- **Trade-off** inherente

---

## Algoritmos Clave

### Regresión Lineal

**Características:**

- Predice valores **continuos**
- Asume relación **lineal**
- **Fácil** de interpretar

---

**Aplicaciones:**

- Predicción de **precios**
- **Pronósticos** de ventas
- Análisis de **tendencias**

---

### Regresión Logística

**Características:**

- **Clasificación** binaria
- Salida **probabilística** (0-1)
- Usa función **sigmoide**

---

**Aplicaciones:**

- **Detección** de spam
- **Diagnóstico** médico
- **Predicción** de churn

---

### Árboles de Decisión

**Características:**

- Estructura **jerárquica**
- **Interpretables**
- Maneja datos **categóricos** y numéricos

---

**Aplicaciones:**

- Sistemas de **soporte**
- **Aprobación** de créditos
- **Diagnóstico** médico

---

### Random Forest

**Características:**

- **Ensemble** de árboles
- Reduce **overfitting**
- **Robusto** ante ruido

---

**Aplicaciones:**

- **Clasificación** de imágenes
- **Predicción** de riesgo crediticio
- Detección de **fraude**

---

### Support Vector Machines (SVM)

**Características:**

- Encuentra **hiperplano** óptimo
- Efectivo en **alta dimensionalidad**
- Usa **kernel tricks**

---

**Aplicaciones:**

- **Clasificación** de texto
- Reconocimiento de **imágenes**
- **Bioinformática**

---

### K-Nearest Neighbors (KNN)

**Características:**

- Basado en **proximidad**
- **No paramétrico**
- **Lazy learning**

---

**Aplicaciones:**

- Sistemas de **recomendación**
- **Clasificación** de patrones
- **Imputación** de valores

---

### K-Means Clustering

**Características:**

- **Agrupa** datos similares
- **No supervisado**
- Requiere definir **K** (número de clusters)

---

**Aplicaciones:**

- **Segmentación** de clientes
- Compresión de **imágenes**
- **Análisis** de mercado

---

## Mejores Prácticas

### Preparación de Datos

**Recomendaciones:**

- **Explorar** datos antes de modelar
- **Visualizar** distribuciones
- **Documentar** transformaciones
- **Validar** calidad de datos

---

### Selección de Modelos

**Consideraciones:**

- Comenzar con modelos **simples**
- **Comparar** múltiples algoritmos
- Considerar **interpretabilidad**
- Evaluar **costo** computacional

---

### Evaluación

**Prácticas:**

- Usar **múltiples** métricas
- **Cross-validation** obligatoria
- Probar en datos **reales**
- **Monitorear** en producción

---

### Ética y Responsabilidad

**Consideraciones:**

- Evaluar **sesgos** en datos
- **Transparencia** en decisiones
- **Privacidad** de datos
- **Impacto** social

---