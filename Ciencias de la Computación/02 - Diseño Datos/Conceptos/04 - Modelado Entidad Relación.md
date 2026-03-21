## Introducción

El **Modelado Entidad-Relación** es una técnica para representar de forma conceptual la estructura de datos de un sistema de información.

---

## Concepto de Mini Mundo

**Definición:**

- El **mini mundo** es una representación simplificada de la realidad que se desea modelar
- Se centra en los aspectos **relevantes** para el sistema de información
- Permite **delimitar** el alcance del modelo

---

**Ejemplo de mini mundo (Librería):**

- **Entidades:** Cliente, Libro, Pedido
- **Relaciones:** Cliente compra Libro, Pedido contiene Libro

---

## Proceso de Abstracción

**Definición:**

La **abstracción** consiste en identificar los elementos esenciales del mini mundo y omitir detalles irrelevantes.

---

**Pasos del proceso:**

1. Identificar **entidades** principales
2. Determinar **atributos** relevantes
3. Definir **relaciones** entre entidades
4. Representar gráficamente en un **modelo conceptual**

---

**Beneficios:**

- Facilita la **comprensión** del sistema
- Reduce la **complejidad**
- Permite construir modelos más **claros** y manejables

---

## Importancia de las Entrevistas

**Propósito:**

Las entrevistas son una técnica fundamental para **recopilar información** del mini mundo.

---

**Permiten:**

- Conocer **procesos** reales
- Identificar **necesidades** de los usuarios
- Detectar **reglas** de negocio

---

**Tipos de entrevistas:**

- **Estructuradas:** preguntas definidas previamente
- **No estructuradas:** conversación abierta
- **Mixtas:** combinación de ambas

---

**Ejemplo de entrevista (Librería):**

- ¿Qué datos se registran de los **clientes**?
- ¿Cómo se gestionan los **pedidos**?
- ¿Qué información es necesaria para controlar el **inventario**?

---

## MER vs DER

### Modelo Entidad-Relación (MER)

**Características:**

- Es la **representación conceptual** del mini mundo
- Define **entidades**, **atributos** y **relaciones**
- Se centra en la **lógica** del negocio, no en la implementación

---

### Diagrama Entidad-Relación (DER)

**Características:**

- Es la **representación gráfica** del MER
- Utiliza **símbolos** y notaciones (rectángulos, óvalos, rombos)
- Facilita la **comunicación** visual entre analistas y usuarios

---

### Tabla Comparativa

|Aspecto|MER (Modelo)|DER (Diagrama)|
|---|---|---|
|**Naturaleza**|Conceptual|Gráfica|
|**Propósito**|Definir entidades y relaciones|Visualizar el modelo|
|**Nivel de detalle**|Abstracto|Concreto|
|**Uso principal**|Análisis y diseño|Comunicación y documentación|

---

## Ejemplo Integrado

**Proceso completo para una Librería:**

1. **Mini mundo:** Librería
2. **Abstracción:** Entidades (Cliente, Libro, Pedido)
3. **Entrevistas:** Recopilar reglas de negocio (ej. un cliente puede hacer varios pedidos)
4. **MER:** Definir entidades y relaciones
5. **DER:** Dibujar diagrama con símbolos:
    - **Rectángulo:** Cliente, Libro, Pedido
    - **Rombos:** Compra, Contiene
    - **Óvalos:** NombreCliente, TítuloLibro, FechaPedido

---