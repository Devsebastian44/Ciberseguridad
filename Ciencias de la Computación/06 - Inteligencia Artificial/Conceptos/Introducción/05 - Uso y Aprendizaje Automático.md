## Introducción

Los tres paradigmas del **aprendizaje automático** ofrecen diferentes enfoques para resolver problemas según la naturaleza de los datos y objetivos.

---

## Aprendizaje Supervisado

### Definición

El aprendizaje supervisado es una metodología donde el algoritmo aprende a partir de datos de **entrenamiento** que incluyen tanto las **entradas** como las **salidas** esperadas.

---

### Características Principales

**Propiedades:**

- Datos **etiquetados**
- **Objetivo** claro predefinido
- **Evaluación** objetiva con métricas
- **Generalización** a datos nuevos

---

### Tipos de Problemas

**Clasificación:**

- **Objetivo:** predecir categorías discretas
- **Ejemplos:** spam/no spam, diagnóstico médico, reconocimiento de imágenes, análisis de sentimientos

---

**Algoritmos comunes:**

- **Regresión Logística**
- **Árboles de Decisión**
- **Random Forest**
- **SVM**
- **Redes Neuronales**

---

**Regresión:**

- **Objetivo:** predecir valores numéricos continuos
- **Ejemplos:** precios de casas, temperatura, salario, ventas

---

**Algoritmos comunes:**

- **Regresión Lineal**
- Regresión **Polinómica**
- **Regularización** (Lasso, Ridge)
- **Árboles de Regresión**

---

### Proceso de Trabajo

**Flujo completo:**

1. **Recolección** de datos
2. **Preprocesamiento** (limpieza, normalización)
3. **División** de datos (train/validation/test)
4. **Entrenamiento** del modelo
5. **Validación** con datos separados
6. **Evaluación** de desempeño
7. **Despliegue** en producción

---

### Métricas de Evaluación

**Para clasificación:**

- **Accuracy** (Exactitud)
- **Precision** (Precisión)
- **Recall** (Sensibilidad)
- **F1-Score**

---

**Para regresión:**

- **MSE** (Mean Squared Error)
- **MAE** (Mean Absolute Error)
- **R²** (Coeficiente de determinación)

---

### Ventajas y Desventajas

**Ventajas:**

- Modelos **interpretables**
- **Amplia** variedad de algoritmos
- Buena **precisión** con datos suficientes
- **Evaluación** clara y objetiva

---

**Desventajas:**

- Requiere datos **etiquetados** (costoso)
- Riesgo de **overfitting**
- Limitado por **calidad** de datos
- Requiere **balance** de clases

---

## Aprendizaje No Supervisado

### Definición

Trabaja con datos **sin etiquetas**, buscando patrones ocultos y estructuras intrínsecas.

---

### Características Principales

**Propiedades:**

- Datos **sin etiquetas**
- **Exploración** de datos
- Interpretación **subjetiva**
- Requiere **conocimiento** del dominio

---

### Tipos de Problemas

**Clustering:**

- **Objetivo:** agrupar datos similares
- **Ejemplos:** segmentación de clientes, agrupación de genes, organización de documentos

---

**Algoritmos:**

- **K-Means**
- **Jerárquico**
- **DBSCAN**
- **GMM** (Gaussian Mixture Models)

---

**Reducción de Dimensionalidad:**

- **Objetivo:** simplificar datos manteniendo información
- **Ejemplos:** compresión de imágenes, visualización, eliminación de redundancias

---

**Algoritmos:**

- **PCA** (Principal Component Analysis)
- **t-SNE**
- **UMAP**
- **Autoencoders**

---

**Detección de Anomalías:**

- **Objetivo:** identificar datos atípicos
- **Ejemplos:** fraudes, fallos industriales, intrusiones, control de calidad

---

**Algoritmos:**

- **Isolation Forest**
- **One-Class SVM**
- **LOF** (Local Outlier Factor)
- **Autoencoders**

---

**Reglas de Asociación:**

- **Objetivo:** encontrar relaciones entre elementos
- **Ejemplos:** market basket analysis, recomendaciones, patrones web

---

**Algoritmos:**

- **Apriori**
- **FP-Growth**
- **ECLAT**

---

### Proceso de Trabajo

**Flujo completo:**

1. **Exploración** de datos
2. **Preprocesamiento**
3. **Selección** del algoritmo
4. **Aplicación** del método
5. **Interpretación** de resultados
6. **Validación** de patrones
7. **Refinamiento** iterativo

---

### Métricas de Evaluación

**Para clustering:**

- **Inercia** (suma de distancias intra-cluster)
- **Silueta** (cohesión y separación)
- **Davies-Bouldin** Index
- **Calinski-Harabasz** Index

---

**Para reducción:**

- **Varianza explicada**
- **Error de reconstrucción**
- Métricas de **visualización**

---

### Ventajas y Desventajas

**Ventajas:**

- **No requiere** etiquetas
- Descubre patrones **inesperados**
- Útil para **exploración** inicial
- **Reduce** complejidad de datos

---

**Desventajas:**

- **Difícil** de evaluar objetivamente
- Requiere **expertise** del dominio
- Puede encontrar patrones **irrelevantes**
- **Interpretación** subjetiva

---

## Aprendizaje de Refuerzo

### Definición

Un **agente** aprende a tomar acciones en un entorno para **maximizar** recompensas acumulativas.

---

### Características Principales

**Propiedades:**

- Aprendizaje por **interacción**
- **Recompensas** diferidas
- Balance entre **exploración** y explotación
- Aprendizaje **secuencial**

---

### Componentes

**Elementos principales:**

- **Agente:** toma decisiones
- **Entorno:** proporciona feedback
- **Estado:** situación actual
- **Acción:** decisión tomada
- **Recompensa:** feedback numérico
- **Política:** estrategia de decisión

---

### Proceso de Interacción

**Ciclo de aprendizaje:**

1. **Observa** estado actual
2. **Elige** acción según política
3. **Ejecuta** acción en entorno
4. **Recibe** recompensa y nuevo estado
5. **Actualiza** conocimiento

---

### Tipos de Problemas

**Control:**

- **Aplicaciones:** juegos, robótica, vehículos autónomos, procesos industriales
- **Objetivo:** controlar sistemas complejos

---

**Optimización:**

- **Aplicaciones:** trading algorítmico, gestión de recursos, publicidad online, recomendaciones
- **Objetivo:** maximizar métricas de negocio

---

### Algoritmos Principales

**Basados en valor:**

- **Q-Learning**
- **SARSA**
- **DQN** (Deep Q-Networks)

---

**De política:**

- **REINFORCE**
- **Actor-Critic**
- **PPO** (Proximal Policy Optimization)

---

**Model-based:**

- **MCTS** (Monte Carlo Tree Search)
- **MPC** (Model Predictive Control)

---

### Conceptos Clave

**Exploración vs Explotación:**

- **Exploración:** probar nuevas acciones
- **Explotación:** usar conocimiento actual
- **Balance:** crítico para éxito

---

**Función de Valor:**

- **V(s):** valor de estar en estado s
- **Q(s,a):** valor de tomar acción a en estado s
- **Ecuación de Bellman:** recursión fundamental

---

**Descuento Temporal:**

- **γ (gamma):** factor de descuento (0-1)
- **Recompensas futuras** valen menos

---

### Aplicaciones Reales

**Juegos y Entretenimiento:**

- **AlphaGo:** dominó el juego de Go
- **OpenAI Five:** Dota 2 profesional
- **StarCraft II:** estrategia en tiempo real

---

**Robótica:**

- Control de **manipuladores**
- **Navegación** autónoma
- **Coordinación** multi-robot

---

**Finanzas:**

- **Trading** algorítmico
- **Gestión** de portafolio
- **Optimización** de precios

---

**Salud:**

- **Dosificación** de medicamentos
- **Planes** de tratamiento
- **Gestión** de recursos hospitalarios

---

### Ventajas y Desventajas

**Ventajas:**

- Aprende comportamientos **complejos**
- Se **adapta** a entornos cambiantes
- Puede **superar** desempeño humano
- **No requiere** conocimiento previo explícito

---

**Desventajas:**

- Requiere **muchas** interacciones
- Puede ser **inestable** durante entrenamiento
- **Difícil** de interpretar decisiones
- **Sensible** al diseño de recompensas

---****