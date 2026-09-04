## Introducción

El DML (Data Manipulation Language) se enfoca en manipular los datos dentro de las tablas ya creadas. Incluye insertar, actualizar y eliminar registros, además de transacciones para asegurar integridad.

---

## Conceptos clave

- **INSERT**: Agregar nuevos registros.
- **UPDATE**: Modificar registros existentes.
- **DELETE**: Eliminar registros.
- **TRUNCATE**: Vaciar tabla rápidamente.
- **Transacciones**: Agrupar operaciones para atomicidad (COMMIT/ROLLBACK).

---

## Insertar datos (INSERT)

### Insertar un registro

```sql
INSERT INTO personas (id, nombre, email)
VALUES (1, 'Carlos Pérez', 'carlos@mail.com');
```

### Insertar varios registros

```sql
INSERT INTO personas (id, nombre, email)
VALUES
  (2, 'Ana Torres', 'ana@mail.com'),
  (3, 'Luis Gómez', 'luis@mail.com');
```

- `INSERT INTO` añade nuevas filas a la tabla.
- Se define la lista de columnas y los valores correspondientes.

---

## Actualizar datos (UPDATE)

### Actualizar un registro específico

```sql
UPDATE personas
SET email = 'nuevo_correo@mail.com'
WHERE id = 1;
```

### Actualizar varias columnas

```sql
UPDATE personas
SET nombre = 'Carlos P. Díaz', email = 'carlos.diaz@mail.com'
WHERE id = 1;
```

- Si omites `WHERE`, todas las filas se actualizarán.
- Siempre filtra correctamente para evitar cambios no deseados.

---

## Eliminar datos (DELETE)

### Eliminar una fila específica

```sql
DELETE FROM personas
WHERE id = 2;
```

### Eliminar todas las filas

```sql
DELETE FROM personas;
```

- `DELETE` borra filas, pero conserva la estructura de la tabla.
- Usa `WHERE` para limitar la eliminación.

---

## Vaciar una tabla (TRUNCATE)

```sql
TRUNCATE TABLE personas;
```

- `TRUNCATE TABLE` elimina todos los registros de la tabla.
- Es más rápido que `DELETE` sin `WHERE`, pero no puede deshacerse fácilmente.

---

## Transacciones básicas

```sql
START TRANSACTION;
UPDATE cuentas SET saldo = saldo - 100 WHERE id = 1;
UPDATE cuentas SET saldo = saldo + 100 WHERE id = 2;
COMMIT;
```

- `START TRANSACTION` inicia una transacción.
- `COMMIT` guarda los cambios.
- `ROLLBACK` revierte los cambios realizados desde el inicio de la transacción.

---

## Buenas prácticas

- Siempre valida los datos antes de `INSERT` o `UPDATE`.
- Usa `WHERE` en `UPDATE` y `DELETE` para evitar efectos masivos.
- Para operaciones críticas, utiliza transacciones.

---

## Resumen

Con DML, puedes manipular datos en tablas existentes. El siguiente paso es consultar datos con SELECT. Recuerda que DML modifica datos, así que maneja con cuidado.
