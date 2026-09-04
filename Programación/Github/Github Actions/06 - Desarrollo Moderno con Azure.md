# Desarrollo Moderno con GitHub

## Integración de GitHub Actions con Azure

### Beneficios Clave de Azure

- **Escalabilidad elástica:** Ajuste automático de recursos según demanda.  
- **Seguridad empresarial:** Certificaciones ISO, SOC y cifrado de datos.  
- **Catálogo de servicios:** +200 servicios (IA, almacenamiento, cómputo).  
- **Alta disponibilidad:** SLA del 99.9% para servicios críticos.  

### Servicios Populares para Despliegue

1. **Azure App Service:** Hosting para aplicaciones web.  
2. **Azure Functions:** Computación sin servidor (serverless).  
3. **AKS (Azure Kubernetes Service):** Orquestación de contenedores.  
4. **Máquinas Virtuales:** Infraestructura como servicio (IaaS).  

**Tier Gratuito:** $200 USD de crédito para nuevos usuarios.

### Automatización total de CI/CD

Cada vez que hay un cambio en el código, se pueden disparar despliegues automáticos en Azure. Menos errores manuales y más consistencia.

### Acciones específicas de Azure

Microsoft provee acciones oficiales para App Service, AKS, Container Apps, etc. Se ahorra tiempo porque no necesitas escribir scripts complejos.

### Conexión nativa entre GitHub y Azure

Al ser ambos de Microsoft, la integración es directa y confiable.

## Sección 2: Beneficios de GitHub Actions + Azure

### Automatización CI/CD

- **Despliegue automático** en Azure ante cambios en el código (`push`/`pull_request`).  
- **Reducción de errores manuales:**  

```yaml
  - name: Deploy to Azure App Service
    uses: azure/webapps-deploy@v2
    with:
      app-name: 'mi-app'
      slot-name: 'production'
      publish-profile: ${{ secrets.AZURE_PUBLISH_PROFILE }}
```

### Acciones Oficiales de Azure

- **Pre-configuradas** para servicios como:
    - `azure/login@v1`: Autenticación en Azure.
    - `azure/aks-set-context@v1`: Gestión de Kubernetes.

### Ejemplo para AKS:

```yaml
- name: Deploy to AKS
  uses: azure/aks-deploy@v1
  with:
    resource-group: 'my-rg'
    cluster-name: 'my-cluster'
    namespace: 'prod'
```

## Sección 3: Configuración Práctica

### Pasos para Integración

1. Crear un Service Principal en Azure:

```bash
az ad sp create-for-rbac --name "github-actions-sp" --role contributor
```

2. Workflow de Ejemplo (App Service):

```bash
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}
      - run: az webapp up --name mi-app --resource-group my-rg
```