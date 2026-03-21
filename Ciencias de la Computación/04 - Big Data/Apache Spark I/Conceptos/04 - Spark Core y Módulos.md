## Introducción

**Spark** está compuesto por un motor central (Spark Core) y múltiples módulos especializados.

---

## Spark Core

**Funcionalidades base:**

Motor de ejecución subyacente que proporciona:

- Gestión de **memoria distribuida**
- **Programación** de tareas
- **Recuperación** ante fallos
- Interacción con **sistemas de almacenamiento**

---

## Spark SQL

**Procesamiento de datos estructurados:**

Módulo para trabajar con datos estructurados:

- **DataFrame API:** abstracción de datos estructurados
- **Catalyst Optimizer:** optimizador de consultas
- **Soporte SQL:** sintaxis estándar
- **Conectores:** integración con diversas fuentes de datos

---

**Ejemplo de consulta:**

```sql
SELECT department, AVG(salary) as avg_salary
FROM employees
WHERE age > 25
GROUP BY department
ORDER BY avg_salary DESC;
```

---

## Spark Streaming

**Procesamiento en tiempo real:**

Procesamiento de flujos de datos en tiempo real:

- **DStreams:** Discretized Streams por micro-lotes
- **Structured Streaming:** API de alto nivel
- **Integración:** Kafka, Flume, TCP sockets, etc.

---

## MLlib (Machine Learning Library)

**Biblioteca de Machine Learning:**

Biblioteca de machine learning escalable:

- **Algoritmos:** clasificación, regresión, clustering, filtrado colaborativo
- **Utilidades:** evaluación de modelos, pipelines de ML
- **Optimización:** algoritmos distribuidos para grandes datasets

---

## GraphX

**Procesamiento de grafos:**

Procesamiento y computación paralela de grafos:

- **Graph abstraction:** representación distribuida de grafos
- **Algoritmos:** PageRank, Connected Components, Triangle Counting
- **Transformaciones:** operaciones sobre vértices y aristas