## Introducción

La arquitectura de **Databricks** se basa en dos planos principales que separan la gestión de la computación.

---

## Planos Principales

### Control Plane

**Funciones:**

- **Gestión** de servicios: notebooks, clusters, jobs
- **Interfaz web:** Databricks workspace
- **Seguridad:** autenticación y autorización
- **Monitoreo:** métricas y logging

---

### Data Plane

**Funciones:**

- **Compute:** clusters de Apache Spark
- **Storage:** integración con sistemas de almacenamiento
- **Networking:** conectividad segura
- **Runtime:** entorno de ejecución optimizado

---

## Componentes Arquitectónicos

### Databricks Workspace

```
┌─────────────────────────────────────────────┐
│                 Workspace                   │
├─────────────────────────────────────────────┤
│  Notebooks  │  Dashboards  │  Experiments   │
├─────────────────────────────────────────────┤
│    Jobs     │   Clusters   │   Libraries    │
├─────────────────────────────────────────────┤
│   Data      │    Models    │    Repos       │
└─────────────────────────────────────────────┘
```

---

### Databricks Runtime

**Características:**

- **Optimized Spark:** versión mejorada de Apache Spark
- **Auto-scaling:** escalado automático de clusters
- **Caching:** sistema de caché inteligente
- **Photon:** motor de consultas vectorizado

---

## Tipos de Clusters

### All-Purpose Clusters

**Características:**

- **Uso:** desarrollo interactivo
- **Compartidos** por múltiples usuarios
- Ciclo de vida **manual** o programado

---

### Job Clusters

**Características:**

- **Uso:** ejecución de jobs automatizados
- **Efímeros:** creados y destruidos automáticamente
- **Optimización:** configuración específica para la tarea

---

### SQL Warehouses

**Características:**

- **Uso:** consultas SQL y análisis
- **Optimizados** para consultas analíticas
- **Auto-scaling** según demanda

---

## Databricks File System (DBFS)

### Características

**Funcionalidades:**

- **Abstracción:** interfaz unificada para múltiples sistemas de almacenamiento
- **Integración:** soporte nativo para S3, ADLS, GCS
- **Optimización:** caching y pre-fetching automático
- **Seguridad:** encriptación y control de acceso

---

### Estructura

```
/
├── FileStore/
├── databricks-datasets/
├── user/
├── tmp/
└── mnt/
```

---

## Integración con Proveedores Cloud

### AWS

**Servicios integrados:**

- **EC2:** instancias para compute
- **S3:** almacenamiento de datos
- **IAM:** gestión de identidades
- **VPC:** networking privado

---

### Azure

**Servicios integrados:**

- **Virtual Machines:** recursos de compute
- **Azure Data Lake:** almacenamiento
- **Azure AD:** autenticación
- **VNet:** networking

---

### Google Cloud

**Servicios integrados:**

- **Compute Engine:** instancias
- **Cloud Storage:** almacenamiento de objetos
- **Cloud IAM:** gestión de acceso
- **VPC:** networking privado

---