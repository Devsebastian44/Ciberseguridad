## Arquitectura Monolítica

### ¿Qué es un Monolito?

Un **monolito** es un sistema tradicional desarrollado y desplegado como una **sola entidad**.

---

### Características Principales

- **Sistema único** y unificado
- **Una sola base de código**
- Todos los componentes en la **misma instancia**
- **Despliegue** como unidad completa

---

### Ventajas de los Monolitos

|Ventaja|Descripción|
|---|---|
|**Stack tecnológico limitado**|Uso de tecnologías específicas y consistentes|
|**Fácil despliegue**|Un solo artefacto para desplegar|
|**Fácil monitoreo**|Todo el sistema en un mismo lugar|
|**Sin latencia**|No hay latencia de red entre componentes|
|**Base de código única**|Todo centralizado en un repositorio|

---

### Desventajas de los Monolitos

|Desventaja|Descripción|
|---|---|
|**Escalabilidad costosa**|Difícil escalar áreas específicas sin escalar todo|
|**Tecnologías limitadas**|Atado a un stack tecnológico específico|
|**Continuous Delivery complejo**|Pequeños cambios pueden afectar todo el sistema|
|**Difícil de modificar**|Acoplamiento entre componentes|

---

### Ejemplo de Aplicación Monolítica

**Caso típico:** Aplicación Django completa

**Componentes integrados:**

- Listado de artículos (catálogo)
- Pasarela de pagos integrada
- Sistema de envío de libros físicos
- API interna

**Nota:** Todos estos componentes viven en la misma aplicación Django, se despliegan juntos y comparten la misma base de datos.

---

### ¿Cuándo Usar Monolitos?

**Regla de oro:** Todas las aplicaciones comienzan siendo monolitos.

#### Escenarios Ideales

- **Recursos limitados**
- **Tiempo de desarrollo** limitado
- **Equipo pequeño**
- **Presupuesto reducido**
- **MVP** o producto inicial
- Proyecto con **alcance bien definido**

---

## Arquitectura de Microservicios

### ¿Qué son los Microservicios?

Los **microservicios** son una arquitectura basada en un conjunto de **pequeñas aplicaciones independientes**.

---

### Características Fundamentales

1. **Independencia** - Cada servicio funciona por sí solo
2. **Procesos propios** - Recursos dedicados
3. **Recursos dedicados** - Base de datos propia
4. **Comunicación HTTP** - APIs RESTful o GraphQL

---

### Ventajas de los Microservicios

|Ventaja|Descripción|
|---|---|
|**Independencia**|Cada aplicación funciona de manera autónoma|
|**Escalabilidad granular**|Escalar solo los servicios que lo necesiten|
|**Flexibilidad tecnológica**|Diferentes tecnologías por servicio|
|**Datos descentralizados**|Cada servicio maneja su propia información|
|**Despliegues independientes**|Actualizar servicios sin afectar a otros|
|**Equipos autónomos**|Equipos especializados por servicio|

---

### Desventajas de los Microservicios

|Desventaja|Descripción|
|---|---|
|**Complejidad en comunicación**|Gestión de APIs y protocolos|
|**Sincronización de datos**|Mantener consistencia entre servicios|
|**Latencia de red**|Overhead en llamadas HTTP|
|**Monitoreo robusto**|Necesidad de tracing y logging|
|**Versionamiento**|Control de versiones de APIs|
|**Costos de mantenimiento**|Infraestructura más compleja|
|**Equipo más grande**|Requiere más personal|
|**Seguridad compleja**|Múltiples puntos de entrada|
|**SSH y gestión**|Más servidores y accesos|

---

## Comparación y Decisión

### ¿Monolitos o Microservicios?

**Respuesta:** ¡Ambos!  
Pueden **coexistir** en una arquitectura híbrida.

---

## Arquitectura Híbrida - Ejemplo Práctico

**Caso:** Aplicación web moderna

```
┌─────────────────┐
│  React Client   │  ← Frontend (SPA)
└────────┬────────┘
         │
    ┌────▼─────┐
    │   API    │
    │ Gateway  │
    └────┬─────┘
         │
    ┌────┴───────────────────┐
    │                        │
┌───▼──────────┐    ┌────────▼──────────┐
│ Django Server│    │ Microservicios    │
│  (Monolito)  │    │ Especializados    │
└──────────────┘    └───────────────────┘
```

**Componentes:**

- **React Client** - Frontend moderno
- **Django Server** - Monolito core para funcionalidad principal
- **Microservicios** - Servicios especializados (pagos, notificaciones, etc.)

---

## Tabla Comparativa

|Aspecto|Monolito|Microservicios|
|---|---|---|
|**Complejidad inicial**|Baja|Alta|
|**Escalabilidad**|Vertical|Horizontal|
|**Tecnologías**|Stack único|Stack diverso|
|**Despliegue**|Todo junto|Independiente|
|**Equipo requerido**|Pequeño|Grande|
|**Costos iniciales**|Bajos|Altos|
|**Mantenimiento**|Simple|Complejo|
|**Latencia**|Mínima|Mayor|
|**Testing**|Más simple|Más complejo|

---