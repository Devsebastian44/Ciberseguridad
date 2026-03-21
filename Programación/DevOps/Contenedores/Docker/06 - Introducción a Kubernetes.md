## ¿Qué son los Orquestadores?

Los orquestadores de contenedores son plataformas que **automatizan el despliegue, gestión, escalado y operación** de aplicaciones en contenedores a través de múltiples hosts.

### Problemas que Resuelven

- **Gestión de contenedores** a escala
- **Alta disponibilidad** y tolerancia a fallos
- **Escalado automático** basado en demanda
- **Balanceo de carga** entre instancias
- **Actualizaciones sin tiempo de inactividad**
- **Gestión de configuración** y secretos
- **Monitoreo y logging** centralizado

### Orquestadores Populares

- **Kubernetes** - El estándar de facto
- **Docker Swarm** - Orquestador nativo de Docker
- **Apache Mesos** - Para grandes escalas
- **Nomad** - De HashiCorp
- **Amazon ECS** - Servicio de AWS

---

## Conceptos Básicos

### Arquitectura de Kubernetes

```

┌─────────────────────────────────────────────────────────┐ │ Control Plane │ ├─────────────────────────────────────────────────────────┤ │ API Server │ etcd │ Scheduler │ Controller Mgr │ └─────────────────────────────────────────────────────────┘ │ ┌─────────────────────────────────────────────────────────┐ │ Worker Nodes │ ├─────────────────────────────────────────────────────────┤ │ kubelet │ kube-proxy │ Container Runtime (Docker) │ └─────────────────────────────────────────────────────────┘

````

### Objetos Principales

- **Pod**: Unidad básica de despliegue, contiene uno o más contenedores
- **Service**: Abstracción para acceder a pods
- **Deployment**: Gestiona el ciclo de vida de pods
- **ConfigMap**: Configuración de aplicaciones
- **Secret**: Información sensible
- **Namespace**: Aislamiento lógico de recursos

---

## Instalación

### Opciones de Instalación

**Para Desarrollo:**
- **minikube** - Cluster local de un solo nodo
- **kind** - Kubernetes en Docker
- **Docker Desktop** - Incluye Kubernetes
- **k3s** - Distribución ligera

**Para Producción:**
- **kubeadm** - Herramienta oficial
- **kops** - Para AWS
- **Managed Services** - EKS, GKE, AKS

### Instalar minikube

```bash
# Linux
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# macOS
brew install minikube

# Windows
choco install minikube

# Verificar instalación
minikube version
````

### Instalar kubectl

```bash
# Linux
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

# macOS
brew install kubectl

# Windows
choco install kubernetes-cli

# Verificar instalación
kubectl version --client
```

### Iniciar Cluster

```bash
# Iniciar minikube
minikube start

# Verificar estado
minikube status

# Ver información del cluster
kubectl cluster-info

# Ver nodos
kubectl get nodes
```

---

## Primer Pod

### Crear Pod con kubectl

```bash
# Crear pod simple
kubectl run mi-pod --image=nginx --port=80

# Ver pods
kubectl get pods

# Descripción detallada
kubectl describe pod mi-pod

# Ver logs
kubectl logs mi-pod

# Eliminar pod
kubectl delete pod mi-pod
```

### Crear Pod con YAML

```yaml
# pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: mi-primer-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:alpine
    ports:
    - containerPort: 80
    env:
    - name: ENV_VAR
      value: "valor-ejemplo"
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```

```bash
# Aplicar configuración
kubectl apply -f pod.yaml

# Ver el pod
kubectl get pod mi-primer-pod

# Descripción completa
kubectl describe pod mi-primer-pod
```

**Ventajas del enfoque YAML:**

- **Declarativo**: Define el estado deseado
- **Versionable**: Se puede guardar en Git
- **Reproducible**: Fácil de compartir y replicar

---

## Port Forward

### Acceder a Pods desde el Host

```bash
# Port forward a un pod
kubectl port-forward pod/mi-primer-pod 8080:80

# Port forward a un service
kubectl port-forward service/mi-servicio 8080:80

# Port forward con IP específica
kubectl port-forward --address 0.0.0.0 pod/mi-primer-pod 8080:80

# Port forward en segundo plano
kubectl port-forward pod/mi-primer-pod 8080:80 &
```

### Ejemplo Práctico

```bash
# Crear pod con aplicación web
kubectl run web-app --image=nginx --port=80

# Hacer port forward
kubectl port-forward pod/web-app 8080:80

# Acceder desde el navegador
# http://localhost:8080
```

**Uso de port-forward:**

- **Desarrollo**: Acceder a servicios sin exponerlos públicamente
- **Debugging**: Probar aplicaciones localmente
- **Temporal**: No es para producción, solo para pruebas

---

## Terminal Interactiva

### Ejecutar Comandos en Pods

```bash
# Ejecutar comando en pod
kubectl exec mi-primer-pod -- ls -la

# Terminal interactiva
kubectl exec -it mi-primer-pod -- /bin/bash

# Con múltiples contenedores
kubectl exec -it mi-pod -c contenedor-especifico -- /bin/bash

# Ejecutar como usuario específico
kubectl exec -it mi-pod --user=1000 -- /bin/bash
```

### Ejemplo con Debugging

```bash
# Crear pod para debugging
kubectl run debug-pod --image=busybox --rm -it --restart=Never -- /bin/sh

# Dentro del pod de debugging
nslookup kubernetes.default
ping google.com
wget -O- http://mi-servicio:80

# Salir (el pod se elimina automáticamente)
exit
```

**Opciones útiles:**

- **`-it`**: Modo interactivo con terminal
- **`--rm`**: Elimina el pod al salir
- **`-c`**: Especifica el contenedor en pods multi-contenedor

---

## Eliminar Pods

### Formas de Eliminar Pods

```bash
# Eliminar pod específico
kubectl delete pod mi-pod

# Eliminar múltiples pods
kubectl delete pods pod1 pod2 pod3

# Eliminar por etiqueta
kubectl delete pods -l app=nginx

# Eliminar todos los pods
kubectl delete pods --all

# Eliminar forzadamente
kubectl delete pod mi-pod --force --grace-period=0

# Eliminar usando archivo YAML
kubectl delete -f pod.yaml
```

**Opciones de eliminación:**

- **Por nombre**: Eliminación específica
- **Por etiqueta**: Eliminación masiva basada en labels
- **Forzada**: Útil para pods atascados (usar con precaución)

---

## Logs en Pods

### Visualizar Logs

```bash
# Ver logs de un pod
kubectl logs mi-pod

# Logs en tiempo real
kubectl logs -f mi-pod

# Logs con timestamp
kubectl logs --timestamps mi-pod

# Últimas 100 líneas
kubectl logs --tail=100 mi-pod

# Logs de contenedor específico
kubectl logs mi-pod -c contenedor-especifico

# Logs anteriores (si el pod se reinició)
kubectl logs mi-pod --previous
```

### Logs de Múltiples Pods

```bash
# Logs de todos los pods con etiqueta
kubectl logs -l app=nginx

# Logs de todos los pods en un namespace
kubectl logs --all-containers=true -l app=nginx

# Exportar logs a archivo
kubectl logs mi-pod > logs.txt
```

**Opciones importantes:**

- **`-f`**: Sigue los logs en tiempo real (follow)
- **`--tail=N`**: Muestra las últimas N líneas
- **`--previous`**: Logs del contenedor anterior (útil tras reinicios)
- **`--timestamps`**: Agrega marcas de tiempo