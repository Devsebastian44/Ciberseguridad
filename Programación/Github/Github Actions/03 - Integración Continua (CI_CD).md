# Integración Continua (CI/CD)

## Sección 1: Conceptos Fundamentales CI/CD

### CI/CD (Clase 3)

- **CI (Integración Continua):** 
  Proceso donde los desarrolladores integran cambios frecuentemente en el repositorio, disparando builds y pruebas automáticas.  
  **Beneficios:** 
  - Detección temprana de errores.  
  - Reduce conflictos entre ramas.  

- **CD (Entrega Continua):** 
  Extensión de CI que prepara el código para despliegue en entornos de staging/pre-producción. 
  **Características:**
  - Artefacto siempre listo para despliegue manual.  
  - Liberación confiable bajo demanda.  

- **CD (Despliegue Continuo):**
  Automatización completa hasta producción.  
  **Flujo:**
  `Cambio aprobado → Despliegue automático a producción`.  

### Beneficios de CI/CD (Clase 3)

- Entregas más rápidas y frecuentes.  
- Mejor calidad de software con pruebas automáticas.  
- Reducción de errores y conflictos.  
- Feedback inmediato.  

## Sección 2: GitHub Actions

### CI/CD

- **CI (Integración Continua):** Automatización de builds y pruebas.
- **CD (Despliegue Continuo):** Automatización de despliegues.

### Conceptos clave

1. **Workflow:** Archivo YAML en `.github/workflows/`.
2. **Eventos/Triggers:** Ejecutan workflows (ej: `push`, `pull_request`).
3. **Jobs/Steps:**

    - **Job:** Unidad de trabajo (ejecutada en paralelo o secuencialmente).
    - **Step:** Acción individual dentro de un job.
    
4. **Actions:** Bloques reutilizables (ej: `actions/checkout@v3`).
5. **Runners:** Entornos de ejecución (Ubuntu, Windows, macOS).

### Ejemplo de Workflow

```yaml
name: CI Pipeline
on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
      - name: Configurar Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
```

**Diagrama:** [[Integración.excalidraw]]  

### Pasos Clave en CD

1. **Promoción:** Mover código de QA a producción.
2. **Pruebas en Prod:** Soak tests, Canary releases.

## Sección 3: GitHub Actions Avanzado

### Temas Cubiertos

1. Variables de entorno

```yaml
env:
  NODE_ENV: production
```

2. Secretos

```yaml
steps:
  - name: Deploy
    env:
      API_KEY: ${{ secrets.API_KEY }}
```

3. Instalación de paquetes

```yaml
- run: npm install
```

4. Servicios (ej: Docker, Redis)

```yaml
services:
  redis:
    image: redis
    ports:
      - 6379:6379
```

5. Deploy

```yaml
- name: Deploy to AWS
  uses: aws-actions/configure-aws-credentials@v1
```