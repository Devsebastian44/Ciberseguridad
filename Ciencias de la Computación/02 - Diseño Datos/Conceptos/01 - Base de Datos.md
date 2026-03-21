## Modelos de Datos

### Modelo Lógico de Datos

Representa la **estructura abstracta** de la información.

**Características:**

- Se centra en **qué datos existen** y **cómo se relacionan**
- Independiente de la implementación física
- Ejemplo: Diagramas entidad-relación (ER)

---

### Modelo Físico de Datos

Describe **cómo se almacenan los datos** en el sistema.

**Incluye:**

- Tipos de datos
- Índices
- Tablas
- Espacio en disco

Depende del **SGBD específico**.

---

### Tabla Comparativa

|Aspecto|Modelo Lógico|Modelo Físico|
|---|---|---|
|Nivel de abstracción|Alto|Bajo|
|Enfoque|Relaciones y entidades|Implementación en el sistema|
|Independencia|Independiente del SGBD|Dependiente del SGBD|
|Ejemplo|Diagrama ER|Tablas, índices, tipos de datos|

---

## Modelos de Alto Nivel vs Bajo Nivel

### Modelos de Alto Nivel

También llamados **conceptuales**.

**Características:**

- Orientados a usuarios y analistas
- Usan representaciones gráficas (ej. diagramas ER)
- Fácil de entender sin conocimientos técnicos profundos

---

### Modelos de Bajo Nivel

También llamados **internos**.

**Características:**

- Orientados a programadores y administradores de BD
- Incluyen detalles técnicos de almacenamiento
- Ejemplo: Definición de tablas en SQL con tipos de datos específicos

---

## Sistemas de Gestión de Bases de Datos (SGBDs)

### Definición

Software que permite **crear, administrar y manipular** bases de datos.

Facilita la interacción entre usuarios, aplicaciones y datos.

---

### Funciones Principales

- Definir estructuras de datos
- Insertar, actualizar y eliminar información
- Controlar acceso y seguridad
- Optimizar consultas
- Garantizar integridad y consistencia

---

### Ejemplos de SGBDs

- MySQL
- PostgreSQL
- Oracle Database
- Microsoft SQL Server
- MongoDB (NoSQL)

---

## Herramientas CASE para Modelaje

### Definición

**CASE (Computer-Aided Software Engineering):** herramientas que apoyan el diseño y modelado de sistemas.

Permiten automatizar tareas de análisis y diseño.

---

### Aplicaciones en Bases de Datos

- Generación automática de diagramas ER
- Transformación de modelos lógicos a físicos
- Documentación del diseño
- Validación de integridad referencial

---

### Ejemplos de Herramientas CASE

- **MySQL Workbench**
- **Oracle SQL Developer Data Modeler**
- **ER/Studio**
- **IBM Data Architect**

---

## Ejemplo Práctico de Modelaje con CASE

**1. Definir entidades:** Cliente, Pedido, Producto

**2. Relacionar entidades:**

- Cliente realiza Pedido
- Pedido contiene Producto

**3. Generar diagrama ER** en la herramienta CASE

**4. Transformar a modelo físico:**

- Crear tablas: `Clientes`, `Pedidos`, `Productos`
- Definir claves primarias y foráneas
- Especificar tipos de datos (ej. `VARCHAR`, `INT`, `DATE`)

---