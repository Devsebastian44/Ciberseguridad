## Introducción

**Apache Spark** requiere configuración previa del sistema y entorno para su correcta instalación.

---

## Requisitos del Sistema

**Especificaciones mínimas:**

- **Java:** JDK 8 o superior
- **Scala:** 2.12.x (incluido con Spark)
- **Python:** 2.7+ o 3.4+ (para PySpark)
- **Memoria:** mínimo 2GB RAM recomendados
- **Espacio en disco:** 1GB para instalación básica

---

## Pasos de Instalación

### 1. Descargar Spark

**Instalación básica:**

```bash
wget https://downloads.apache.org/spark/spark-3.4.0/spark-3.4.0-bin-hadoop3.tgz
tar -xzf spark-3.4.0-bin-hadoop3.tgz
sudo mv spark-3.4.0-bin-hadoop3 /opt/spark
```

---

### 2. Configurar Variables de Entorno

**Configuración del PATH:**

```bash
# Agregar al ~/.bashrc o ~/.zshrc
export SPARK_HOME=/opt/spark
export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
export PYSPARK_PYTHON=python3
```

---

### 3. Verificar Instalación

**Comandos de verificación:**

```bash
spark-submit --version
run-example SparkPi 10
```

---

## Estructura de Directorios

**Organización de Spark:**

```
spark/
├── bin/           # Scripts ejecutables
├── conf/          # Archivos de configuración
├── data/          # Datos de ejemplo
├── examples/      # Aplicaciones de ejemplo
├── jars/          # Archivos JAR de Spark
├── python/        # Código fuente de PySpark
├── R/             # Código fuente de SparkR
├── sbin/          # Scripts de administración del clúster
└── yarn/          # Archivos para integración con YARN
```

---