## Contenedores

### Características Principales

- **Virtualización a nivel de SO**: Comparten el kernel del host, más ligeros que VMs
- **Portabilidad**: "Build once, run anywhere" - mismo comportamiento en diferentes entornos
- **Aislamiento**: Procesos, redes y sistemas de archivos separados
- **Eficiencia**: Arranque rápido (segundos vs minutos), menor overhead de recursos

### Docker

- **Componentes clave**:
    - **Dockerfile**: Instrucciones para construir imágenes
    - **Imagen**: Template inmutable con aplicación y dependencias
    - **Contenedor**: Instancia en ejecución de una imagen
    - **Docker Hub**: Registro público de imágenes

### Contenedores vs VMs

- **Contenedores**: Comparten SO, más ligeros, arranque rápido
- **VMs**: SO completo por instancia, mayor aislamiento, más pesadas

## Orquestación de Contenedores

### Kubernetes (K8s)

- **Funcionalidad**: Automatiza despliegue, escalado y gestión de aplicaciones contenerizadas
    
- **Componentes principales**:
    
    - **Pod**: Unidad mínima, uno o más contenedores
    - **Node**: Máquina (física/virtual) que ejecuta pods
    - **Cluster**: Conjunto de nodes
    - **Control Plane**: Gestiona el cluster (API Server, Scheduler, Controller Manager)
    - **Service**: Expone pods con IP estable
    - **Deployment**: Define estado deseado de la aplicación
- **Capacidades**:
    
    - Auto-scaling horizontal y vertical
    - Self-healing (reinicia contenedores fallidos)
    - Rolling updates y rollbacks
    - Load balancing
    - Service discovery automático

## Serverless / FaaS (Function as a Service)

### Conceptos

- **Definición**: Ejecutar código sin gestionar servidores
- **Modelo de pago**: Por tiempo de ejecución y recursos consumidos (no por servidor activo)
- **Escalado automático**: De 0 a N instancias según demanda

### Características

- **Event-driven**: Funciones se activan por eventos (HTTP, cambios en BD, mensajes)
- **Stateless**: Cada ejecución es independiente
- **Límites de ejecución**: Timeouts típicos (AWS Lambda: 15 min máx)
- **Cold starts**: Primera ejecución puede ser más lenta

### Ejemplos de Servicios

- **AWS Lambda**
- **Azure Functions**
- **Google Cloud Functions**

### Casos de Uso

- APIs y microservicios ligeros
- Procesamiento de eventos (uploads, cambios en BD)
- Tareas programadas (cron jobs)
- Procesamiento de datos en tiempo real

## Microservicios

### Arquitectura

- **Definición**: Aplicación dividida en servicios pequeños e independientes
- **Características**:
    - Cada servicio tiene una responsabilidad específica
    - Desarrollo y despliegue independiente
    - Comunicación vía APIs (REST, gRPC, mensajería)
    - Diferentes tecnologías por servicio si es necesario

### Ventajas vs Monolitos

- Mayor agilidad en desarrollo
- Escalado independiente por servicio
- Resiliencia (fallo de un servicio no tumba toda la app)
- Facilita CI/CD

### Desafíos

- Mayor complejidad operacional
- Gestión de comunicación entre servicios
- Monitoreo distribuido
- Transacciones distribuidas

## CI/CD (Continuous Integration/Continuous Deployment)

### Continuous Integration

- Integración frecuente de código en repositorio compartido
- Builds y tests automáticos en cada commit
- Detección temprana de errores

### Continuous Deployment

- Automatización del despliegue a producción
- Pipeline: Build → Test → Deploy
- Reduce errores humanos y acelera releases

### Herramientas Comunes

- Jenkins, GitLab CI/CD, GitHub Actions, Azure DevOps, CircleCI