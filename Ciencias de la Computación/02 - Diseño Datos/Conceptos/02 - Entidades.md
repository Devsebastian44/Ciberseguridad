## ¿Qué son las Entidades?

Una **entidad** es cualquier objeto, persona, lugar, evento o concepto del **mini mundo** que se desea representar en la base de datos.

Se caracteriza por tener **existencia independiente** y por poseer **atributos** que describen sus propiedades.

En el **Modelo Entidad-Relación (MER)**, las entidades son los elementos principales que permiten organizar y estructurar la información.

---

### Características de una Entidad

**Nombre único** dentro del modelo (ej. Cliente, Producto, Pedido)

**Atributos** que describen sus propiedades (ej. NombreCliente, PrecioProducto, FechaPedido)

**Clave primaria** que permite identificar de manera única cada instancia de la entidad

Puede ser **fuerte** o **débil**, dependiendo de su independencia

---

### Ejemplos de Entidades

**Persona:** con atributos como Nombre, Edad, Dirección

**Producto:** con atributos como Código, Descripción, Precio

**Pedido:** con atributos como NúmeroPedido, Fecha

---

## Tipos de Entidades

### Entidades Fuertes

Tienen **existencia independiente** dentro del modelo.

Se identifican mediante una **clave primaria propia**.

No dependen de otras entidades para existir.

**Ejemplo:** Cliente, Producto, Empleado

---

### Entidades Débiles

Su existencia depende de una **entidad fuerte**.

No poseen clave primaria propia; requieren una **clave compuesta** que incluye la clave de la entidad fuerte.

**Ejemplo:** DetallePedido (depende de Pedido), Dependiente (depende de Empleado)

---

### Entidades Asociativas

Surgen de relaciones **muchos a muchos**.

Se convierten en entidades para almacenar atributos adicionales.

**Ejemplo:** Matricula (relación entre Estudiante y Curso)

---

## Diferencias entre Entidades Fuertes y Débiles

|Aspecto|Entidad Fuerte|Entidad Débil|
|---|---|---|
|Existencia|Independiente|Depende de otra entidad|
|Identificación|Clave primaria propia|Clave compuesta (incluye clave externa)|
|Ejemplo|Cliente, Producto|DetallePedido, Dependiente|
|Representación gráfica|Rectángulo simple|Rectángulo doble|

---

## Representación en diagrams.net

### Convenciones Gráficas

**Entidades fuertes:** Rectángulo con el nombre de la entidad

**Entidades débiles:** Rectángulo doble

**Relaciones:** Rombos conectando entidades

**Atributos:** Óvalos conectados a las entidades

---

### Ejemplo Práctico

**Mini mundo:** Sistema de ventas

**Entidad fuerte:** Cliente

**Entidad fuerte:** Pedido

**Entidad débil:** DetallePedido

**Relación:** Cliente realiza Pedido

**Relación:** Pedido contiene DetallePedido

**En diagrams.net:**

1. Crear rectángulos para Cliente y Pedido
2. Crear rectángulo doble para DetallePedido
3. Conectar con rombos (Relaciones)
4. Añadir atributos como NombreCliente, FechaPedido, Cantidad

---