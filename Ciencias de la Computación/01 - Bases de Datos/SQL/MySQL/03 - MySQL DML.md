## ¿Qué es DML?

El **DML (Data Manipulation Language)** permite trabajar directamente con los datos dentro de las tablas: **insertar, actualizar y eliminar** registros.

---

## Insertar Datos (INSERT)

### Insertar Valores en Todas las Columnas

```sql
INSERT INTO personas (id, nombre, email)
VALUES (1, 'Carlos Pérez', 'carlos@mail.com');
```

---

### Insertar Varios Registros

```sql
INSERT INTO personas (id, nombre, email)
VALUES 
(2, 'Ana Torres', 'ana@mail.com'),
(3, 'Luis Gómez', 'luis@mail.com');
```

---

## Actualizar Datos (UPDATE)

### Actualizar una Fila Específica

```sql
UPDATE personas
SET email = 'nuevo_correo@mail.com'
WHERE id = 1;
```

---

### Actualizar Múltiples Columnas

```sql
UPDATE personas
SET nombre = 'Carlos P. Díaz', email = 'carlos.diaz@mail.com'
WHERE id = 1;
```

**⚠️ Advertencia:** Si omites el `WHERE`, se actualizan **todas** las filas de la tabla.

---

## Borrar Datos (DELETE)

### Borrar una Fila Específica

```sql
DELETE FROM personas
WHERE id = 2;
```

---

### Borrar Todas las Filas

```sql
DELETE FROM personas;
```

**Nota:** Esto elimina todos los registros, pero **no** la estructura de la tabla (para eso se usa `TRUNCATE`).

---