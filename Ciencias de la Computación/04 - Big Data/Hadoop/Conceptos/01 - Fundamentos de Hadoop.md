## Introducción a Hadoop

### ¿Qué es Hadoop?

**Definición:**

Hadoop es un framework de **código abierto** para procesamiento distribuido de grandes volúmenes de datos en clusters.

---

**Componentes principales:**

- **HDFS** (Hadoop Distributed File System)
- **MapReduce**

Escala desde servidores **individuales** hasta **miles** de máquinas con almacenamiento y computación local.

---

## Big Data y Hadoop

**Relación fundamental:**

Big Data implica manejar grandes volúmenes de datos que no pueden procesarse con herramientas **tradicionales**.

Hadoop es clave por su **escalabilidad**, **tolerancia a fallos** y soporte para datos estructurados y no estructurados.

---

## Software Relacionado con Hadoop

**Ecosistema Hadoop:**

- **Hive:** consultas SQL sobre Hadoop
- **Pig:** lenguaje de alto nivel para análisis
- **HBase:** base de datos NoSQL distribuida
- **Spark:** procesamiento en memoria
- **Flume:** recolección de datos en tiempo real
- **Sqoop:** importación/exportación con bases relacionales
- **Oozie:** orquestación de flujos de trabajo

---

## Hadoop en la Nube

**Servicios cloud:**

- **Amazon EMR**
- **Google Cloud Dataproc**
- **Azure HDInsight**

---

**Ventajas:**

- Menor coste de **infraestructura**
- **Escalabilidad** automática
- **Mantenimiento** simplificado

---

## Arquitectura de Hadoop

### Componentes Principales

**Stack de Hadoop:**

- **HDFS:** almacenamiento distribuido
- **MapReduce:** procesamiento por lotes
- **YARN:** gestor de recursos
- **Hadoop Common:** librerías compartidas

---

### Funcionamiento de HDFS

**Características:**

- Archivos divididos en **bloques** grandes (128 MB o 256 MB)
- **NameNode:** metadata y namespace
- **DataNode:** almacenamiento de bloques

---

### Patrones de Acceso

**Optimizaciones:**

- Optimizado para **acceso secuencial** y escritura única
- **No ideal** para acceso en tiempo real o edición frecuente

---

### Almacenamiento en Clúster

**Replicación de datos:**

- Bloques **replicados** (normalmente 3 veces)
- Replicación asegura **tolerancia a fallos**
- NameNode mantiene **metadatos**

---

## Administración de Hadoop

### Agregar/Quitar Nodos

**Gestión de nodos:**

- Configurar como **DataNode/NodeManager**
- Actualizar configuración (`slaves`)
- **Descomisionar** nodos para retirarlos

---

### Verificar Salud del Clúster

**Comandos de verificación:**

```bash
hdfs dfsadmin -report
yarn node -list
jps
```

---

### Iniciar/Detener Componentes

**Scripts de gestión:**

```bash
start-dfs.sh / stop-dfs.sh
start-yarn.sh / stop-yarn.sh
```

---

### Configuración

**Archivos de configuración:**

- `core-site.xml`
- `hdfs-site.xml`
- `yarn-site.xml`
- `mapred-site.xml`

---

### Topología de Rack

**Optimización de red:**

- Minimiza **tráfico** entre racks
- Mejora **tolerancia** a fallos
- Configuración con `topology.script.file.name`

---

## Componentes de Hadoop

### Filosofía de MapReduce

**Modelo de procesamiento:**

- **Map:** procesamiento paralelo por bloques
- **Reduce:** combinación de resultados

**Ejemplo:** conteo de palabras

---

### Pig y Hive

**Herramientas de consulta:**

- **Pig:** lenguaje Pig Latin, flexible para programadores
- **Hive:** sintaxis SQL (HiveQL), ideal para analistas
- Ambos convierten scripts en tareas **MapReduce**

---

### Flume y Sqoop

**Ingesta de datos:**

- **Flume:** ingesta de datos en tiempo real (ej. logs)
- **Sqoop:** transferencia entre bases relacionales y Hadoop

---

### Oozie

**Orquestación de workflows:**

- **Orquestación** de flujos de trabajo
- Control de **dependencias** entre tareas
- **Programación** por tiempo o eventos
- Definición en **XML**

---