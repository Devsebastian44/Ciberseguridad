## Introducción

El **aprendizaje automático (ML)** es una subdisciplina de la inteligencia artificial que permite a las máquinas aprender **patrones** a partir de datos sin ser explícitamente programadas.

---

## Los Tres Paradigmas Fundamentales

### Aprendizaje Supervisado

**Características:**

- Usa datos **etiquetados** (input-output conocidos)
- **Objetivo:** predecir resultados para nuevos datos

---

### Aprendizaje No Supervisado

**Características:**

- Encuentra **patrones ocultos** en datos sin etiquetas
- **Objetivo:** descubrir estructuras o agrupaciones

---

### Aprendizaje de Refuerzo

**Características:**

- Aprende mediante **interacciones** y retroalimentación (recompensas/castigos)
- **Objetivo:** maximizar recompensas en decisiones secuenciales

---

## Aprendizaje Supervisado

### Concepto

Entrenamiento con datos que contienen **features** y **labels** correctas.

---

### Tipos de Problemas

**Clasificación:**

- Predecir **categorías**
- Ejemplos: spam/no spam, diagnóstico médico, reconocimiento de imágenes

---

**Regresión:**

- Predecir valores **numéricos continuos**
- Ejemplos: precios, ventas, temperatura

---

### Algoritmos Comunes

**Clasificación:**

- Regresión Logística
- Árboles de Decisión
- SVM
- Random Forest
- Redes Neuronales

---

**Regresión:**

- Regresión Lineal
- Regresión Polinomial
- Random Forest Regressor
- Redes Neuronales

---

### Proceso Típico

**Flujo de trabajo:**

1. **Recolección** de datos
2. **División** en entrenamiento/validación/prueba
3. **Entrenamiento** del modelo
4. **Evaluación** y validación
5. **Ajuste** de hiperparámetros
6. **Despliegue**

---

## Aprendizaje No Supervisado

### Concepto

Trabaja con datos **sin etiquetas**, buscando patrones o estructuras ocultas.

---

### Tipos Principales

**Clustering:**

- Agrupar datos similares
- Algoritmos: K-means, DBSCAN, jerárquico

---

**Reducción de Dimensionalidad:**

- Simplificar datos
- Algoritmos: PCA, t-SNE, UMAP

---

**Detección de Anomalías:**

- Identificar datos atípicos
- Algoritmos: Isolation Forest, One-Class SVM

---

**Reglas de Asociación:**

- Encontrar relaciones entre elementos
- Algoritmos: Apriori, FP-Growth

---

### Ventajas y Desafíos

**Ventajas:**

- **No requiere** datos etiquetados
- Descubre **patrones no evidentes**
- Útil para **exploración** inicial

---

**Desafíos:**

- **Difícil** evaluar resultados
- Interpretación **subjetiva**
- Selección de algoritmos **compleja**

---

## Aprendizaje de Refuerzo

### Concepto

Basado en **acción-recompensa**. El agente aprende interactuando con un entorno y recibiendo retroalimentación.

---

### Componentes

**Elementos principales:**

- **Agente:** toma decisiones
- **Entorno:** proporciona estados y recompensas
- **Estados:** situaciones específicas
- **Acciones:** decisiones posibles
- **Recompensas:** retroalimentación positiva o negativa

---

### Aplicaciones

**Casos de uso:**

- **Juegos:** AlphaGo, poker
- **Robótica:** control, navegación
- **Finanzas:** trading algorítmico
- **Recomendaciones** adaptativas
- **Vehículos** autónomos

---

### Algoritmos Populares

**Métodos principales:**

- Q-Learning
- Policy Gradient
- Actor-Critic
- Deep Q-Networks (DQN)
- Proximal Policy Optimization (PPO)

---

## Cómo Aprenden las Máquinas

### Proceso de Aprendizaje

**Pasos fundamentales:**

1. **Representación de datos:** vectores, matrices, tensores, feature engineering
2. **Función objetivo:** define qué optimizar (error, coherencia, recompensas)
3. **Algoritmo de optimización:** gradiente descendente, algoritmos evolutivos
4. **Generalización:** aplicar lo aprendido a datos nuevos, evitando overfitting

---

### Factores Clave

**Elementos críticos:**

- **Calidad de los datos:** representativos, limpios, balanceados
- **Selección del algoritmo:** depende del problema (No Free Lunch theorem)
- **Evaluación rigurosa:** métricas adecuadas, validación cruzada, conjuntos de prueba independientes

---