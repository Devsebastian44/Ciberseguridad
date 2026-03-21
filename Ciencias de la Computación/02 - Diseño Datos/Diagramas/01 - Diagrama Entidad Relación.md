## Introducción

El **Diagrama Entidad-Relación (DER)** representa gráficamente las entidades, relaciones y cardinalidades de un sistema de información.

---

## Tipos de Relación

### Uno a Uno (1:1)

**Definición:**

Cada instancia de una entidad se relaciona con **una sola** instancia de otra entidad.

**Ejemplo:** Persona ── Pasaporte

---

### Uno a Muchos (1:N)

**Definición:**

Una instancia de una entidad puede relacionarse con **varias** instancias de otra entidad.

**Ejemplo:** Cliente ── Pedido

---

### Muchos a Muchos (M:N)

**Definición:**

Varias instancias de una entidad pueden relacionarse con **varias** instancias de otra entidad.

**Ejemplo:** Estudiante ── Curso

---

## Grado de una Relación

**Definición:**

El **grado** indica el número de entidades que participan en una relación.

---

**Tipos:**

- **Binaria:** relación entre **dos** entidades (ej. Cliente ── Pedido)
- **Ternaria:** relación entre **tres** entidades (ej. Proveedor ── Producto ── Almacén)
- **N-aria:** relación entre **más de tres** entidades

---

## Cardinalidad

**Definición:**

La **cardinalidad** define el número mínimo y máximo de ocurrencias de una entidad en una relación.

---

**Tipos de cardinalidad:**

- **(0,1):** puede **no participar** o participar una sola vez
- **(1,1):** debe participar **exactamente una vez**
- **(0,N):** puede **no participar** o participar muchas veces
- **(1,N):** debe participar **al menos una vez** y puede hacerlo muchas veces

---

**Ejemplo:**

Cliente **(1,N)** ── realiza ── Pedido **(1,1)**

Un cliente puede realizar **muchos** pedidos, pero cada pedido pertenece a **un solo** cliente.

---

## Representación en el DER

### Convenciones Gráficas

**Símbolos principales:**

- **Entidades:** Rectángulos
- **Relaciones:** Rombos conectando entidades
- **Atributos:** Óvalos conectados a entidades o relaciones
- **Cardinalidad:** Números o símbolos cerca de las entidades

---

### Ejemplo Práctico

**Mini mundo:** Sistema de ventas

**Entidades:** Cliente, Pedido, Producto

**Relaciones:**

- Cliente ── realiza ── Pedido **(1:N)**
- Pedido ── contiene ── Producto **(M:N)**

---

**Representación ASCII:**

```
[Cliente]──(realiza)──[Pedido]──(contiene)──[Producto]

Cardinalidades:
Cliente (1,N) ── Pedido (1,1)
Pedido (1,N) ── Producto (M,N)
```

---