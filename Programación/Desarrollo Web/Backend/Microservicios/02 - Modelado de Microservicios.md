## Definición de un Servicio

### ¿Qué es un Servicio?

Un **servicio** representa una **unidad lógica y funcional** del sistema, diseñada para abordar una tarea específica o un conjunto de tareas relacionadas.

---

### Características Clave

- **Unidad lógica** - Coherente en su propósito
- **Unidad funcional** - Realiza funciones específicas
- **Tarea específica** - Enfocado en un objetivo
- **Tareas relacionadas** - Agrupa funcionalidad cohesiva

---

## Responsabilidades y Límites del Servicio

### Claridad en el Propósito

- Cada servicio debe tener una **razón clara** de existir
- Evitar servicios **"cajón de sastre"** con múltiples responsabilidades

---

### Reducción de Complejidad

- Mantener el servicio **simple y enfocado**
- **Un servicio = Una responsabilidad** principal

---

### Independencia y Cohesión

- **Alta cohesión** - Elementos relacionados juntos
- **Bajo acoplamiento** - Mínima dependencia externa
- Capacidad de funcionar de forma **autónoma**

---

### Escalabilidad y Flexibilidad

- Escalar **solo lo necesario**
- Cambios **sin afectar** otros servicios
- **Despliegue independiente**

---

### Reutilización y Modularidad

- Componentes **reutilizables**
- **Interfaces bien definidas**
- **Fácil integración**

---

## Ejercicio Práctico 1: Sistema de Agencia de Viajes

```
┌─────────────────────────────────────────┐
│     Sistema de Agencia de Viajes        │
└──────────────────┬──────────────────────┘
                   │
      ┌────────────┼────────────┐
      │            │            │
┌─────▼─────┐  ┌───▼────┐  ┌───▼────┐
│Búsqueda   │  │Reservas│  │ Pagos  │
│ Vuelos    │  │        │  │        │
└─────────┘  └────────┘  └────────┘
      │            │            │
┌─────▼─────┐  ┌───▼────┐  ┌───▼────┐
│Hoteles    │  │Clientes│  │Notific.│
└─────────┘  └────────┘  └────────┘
```

**Servicios potenciales:**

- **Búsqueda de Vuelos** - Consultar disponibilidad aérea
- **Búsqueda de Hoteles** - Consultar alojamiento
- **Reservas** - Gestionar reservaciones
- **Pagos** - Procesar transacciones
- **Clientes/Usuarios** - Gestionar perfiles
- **Notificaciones** - Enviar confirmaciones
- **Itinerarios** - Organizar viajes

---

## Domain-Driven Design (DDD)

### ¿Qué es DDD?

**Domain-Driven Design** se centra en **comprender el dominio del problema** y reflejar esa comprensión en el diseño del software.

---

## Principios Básicos de DDD

### Lenguaje Ubicuo

- **Vocabulario común** entre negocio y desarrollo
- **Elimina ambigüedades** en comunicación

---

### Contextos Delimitados (Bounded Contexts)

- **Límites explícitos** de cada modelo
- Cada microservicio representa un **bounded context**

---

### Entidades

Objetos con **identidad única** que persisten en el tiempo.

```python
class Reserva:
    def __init__(self, id, cliente, vuelo):
        self.id = id  # Identidad única
        self.cliente = cliente
        self.vuelo = vuelo
        self.estado = "PENDIENTE"
```

---

### Objetos de Valor (Value Objects)

**Inmutables** y comparados por valores, no por identidad.

```python
class Direccion:
    def __init__(self, calle, ciudad, codigo_postal):
        self.calle = calle
        self.ciudad = ciudad
        self.codigo_postal = codigo_postal
```

---

### Agregados (Aggregates)

Grupo de **entidades y objetos de valor** con una raíz de agregado.

- **Raíz de agregado** - Punto de entrada único
- **Consistencia** - Garantiza reglas de negocio

---

## Ventajas de DDD

|Ventaja|Descripción|
|---|---|
|**Proceso flexible**|Adaptable a cambios del negocio|
|**Claridad**|Simplifica problemas complejos|
|**Comunicación**|Puente entre negocio y desarrollo|
|**Código organizado**|Estructura clara y mantenible|
|**Alineación**|Código refleja reglas del negocio|

---

## Desventajas de DDD

|Desventaja|Descripción|
|---|---|
|**Alto costo de tiempo**|Requiere mucho esfuerzo inicial|
|**Necesita experto**|Acceso a expertos del dominio|
|**Curva de aprendizaje**|Conceptos complejos de entender|
|**No para todo**|Solo recomendado en sistemas complejos|
|**Overhead**|Innecesario en CRUD simples|

---

## Ejercicio Práctico 2: E-commerce

```
┌─────────────────────────────────────────────┐
│      E-commerce Platform (DDD)              │
└──────────────┬──────────────────────────────┘
               │
    ┌──────────┼─────────┬─────────┐
    │          │         │         │
┌───▼───┐ ┌───▼───┐ ┌───▼────┐ ┌───▼──────┐
│Catálog│ │Pedidos│ │Pagos   │ │Inventario│
└───────┘ └───────┘ └────────┘ └──────────┘
```

**Bounded Contexts:**

- **Catálogo** - Productos y categorías
- **Pedidos** - Gestión de órdenes
- **Pagos** - Procesamiento de transacciones
- **Inventario** - Control de stock

---

## Acoplamiento en Microservicios

### ¿Qué es Acoplamiento?

Grado de **interdependencia** entre componentes.

- **Acoplamiento fuerte** → Alta dependencia
- **Acoplamiento débil** → Baja dependencia

---

### Acoplamiento Alto

**Ventajas:**

- Comunicación directa
- Implementación simple

**Desventajas:**

- Alta dependencia
- Mantenimiento complejo
- Difícil escalabilidad

---

### Acoplamiento Bajo

**Ventajas:**

- Independencia de servicios
- Reutilización
- Despliegue independiente

**Desventajas:**

- Esfuerzo inicial mayor
- Complejidad arquitectónica

---

## Tips para Lograr Acoplamiento Bajo

- **Interfaces claras** - Contratos bien definidos
- **Segregar base de datos** - Cada servicio su BD
- **Patrones de mensajería** - Comunicación asíncrona
- **Principios SOLID** - Diseño orientado a objetos
- **Evitar acoplamiento directo** - No llamadas síncronas innecesarias
- **Descomponer funcionalidades** - Servicios pequeños y enfocados

---

## Descomposición de Monolitos

### Razones para Migrar

- **Escalabilidad independiente** - Escalar solo lo necesario
- **Flexibilidad tecnológica** - Diferentes stacks por servicio
- **Despliegue rápido** - Actualizaciones sin downtime
- **Resiliencia** - Fallos aislados
- **Colaboración** - Equipos independientes
- **Evolución del sistema** - Adaptación continua
- **Alineación con la nube** - Aprovechar cloud-native

---

## Estrategias de Descomposición

- **Descomposición gradual** - No todo a la vez
- **Identificar bounded contexts** - Usar DDD
- **Crear capas de servicios** - Separación lógica
- **Usar Facade/Adaptadores** - Abstraer complejidad
- **Patrones Gateway** - Punto de entrada único
- **Separar módulos** - Por funcionalidad
- **Refactorizar gradualmente** - Iterativo

---

## Checklist de Migración

### Pre-migración

- [ ] Identificar bounded contexts
- [ ] Analizar dependencias
- [ ] Evaluar base de datos
- [ ] Definir prioridades
- [ ] Establecer métricas

---

### Durante la Migración

- [ ] Implementar API Gateway
- [ ] Crear servicio
- [ ] Comunicación sync/async
- [ ] Estrategia de datos
- [ ] Feature flags
- [ ] Monitoreo

---

### Post-migración

- [ ] Validar funcionalidad
- [ ] Monitorear performance
- [ ] Verificar logs
- [ ] Eliminar legacy
- [ ] Documentar cambios
- [ ] Retrospectiva

---

## Conceptos Clave para Recordar

- **Un servicio = Una responsabilidad clara**
- **DDD = Lenguaje ubicuo + bounded contexts**
- **Bajo acoplamiento = independencia y flexibilidad**
- **Descomposición = gradual, nunca todo a la vez**

---