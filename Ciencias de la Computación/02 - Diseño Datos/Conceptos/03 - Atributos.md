## ¿Qué son los Atributos?

Los **atributos** son las propiedades o características que describen a una entidad o relación dentro del modelo Entidad-Relación (ER).

Cada atributo aporta información adicional que permite diferenciar y detallar las instancias de una entidad.

**Ejemplo:**

- Entidad **Cliente** → atributos: Nombre, Dirección, Teléfono
- Entidad **Producto** → atributos: Código, Descripción, Precio

---

## Tipos de Atributos

### Atributos Simples

No pueden dividirse en componentes más pequeños.

**Ejemplo:** Edad, DNI

---

### Atributos Compuestos

Pueden descomponerse en subatributos.

**Ejemplo:** Dirección → Calle, Número, Ciudad, Código Postal

---

### Atributos Derivados

Su valor puede calcularse a partir de otros atributos.

**Ejemplo:** Edad (derivada de la Fecha de Nacimiento)

---

### Atributos Multivaluados

Pueden tener más de un valor para una misma entidad.

**Ejemplo:** Teléfonos de un Cliente, Correos electrónicos

---

### Atributos Clave

Identifican de manera única cada instancia de la entidad.

**Ejemplo:** Número de Cliente, Código de Producto

---

## Representación Gráfica en el DER

**Simples:** Óvalo con el nombre del atributo

**Compuestos:** Óvalo principal conectado a subóvalos

**Derivados:** Óvalo con línea discontinua

**Multivaluados:** Óvalo doble

**Clave primaria:** Subrayado en el nombre del atributo

---

### Ejemplo

```
[Cliente]
|── Nombre (simple)
|── Dirección (compuesto)
|   |── Calle
|   |── Ciudad
|── FechaNacimiento
|   |── Edad (derivado)
|── Teléfono (multivaluado)
|── NúmeroCliente (clave primaria)
```

---