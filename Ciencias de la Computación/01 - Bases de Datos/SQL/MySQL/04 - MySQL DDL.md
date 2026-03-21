## ¿Qué es DDL?

El **DDL (Data Definition Language)** permite definir, modificar y eliminar la **estructura** de las bases de datos (tablas, columnas, llaves, etc.).

---

## Tipos de Datos en SQL

### Numéricos

- `INT` / `INTEGER` - Entero
- `DECIMAL(p,s)` / `NUMERIC` - Decimales exactos
- `FLOAT`, `DOUBLE` - Reales de punto flotante

---

### Texto

- `CHAR(n)` - Cadena de longitud fija
- `VARCHAR(n)` - Cadena de longitud variable
- `TEXT` - Texto largo

---

### Fechas y Tiempos

- `DATE` - Fecha (YYYY-MM-DD)
- `DATETIME` - Fecha y hora (YYYY-MM-DD HH:MM:SS)
- `TIMESTAMP` - Marca de tiempo

---

### Booleano

- `BOOLEAN` / `TINYINT(1)` - Verdadero (1) o Falso (0)

---

## Primary Key

Una **Primary Key** identifica de forma **única** cada fila de una tabla.

### Características

- **No puede ser NULL**
- Debe ser **única**
- Una tabla solo puede tener **una clave primaria**

```sql
CREATE TABLE empleados (
    id INT PRIMARY KEY,
    nombre VARCHAR(100)
);
```

---

## Foreign Key

Una **Foreign Key** establece una **relación** entre dos tablas.

### Características

- Enlaza la columna de una tabla con la **clave primaria** de otra
- Mantiene la **integridad referencial**

```sql
CREATE TABLE pedidos (
    id INT PRIMARY KEY,
    empleado_id INT,
    FOREIGN KEY (empleado_id) REFERENCES empleados(id)
);
```

---

## Operaciones con Tablas

### Agregar Columna

```sql
ALTER TABLE empleados ADD correo VARCHAR(100);
```

---

### Quitar Columna

```sql
ALTER TABLE empleados DROP COLUMN correo;
```

---

### Eliminar Tabla

```sql
DROP TABLE empleados;
```

---

### Truncar Tabla

```sql
TRUNCATE TABLE empleados;
```

**Nota:** Elimina todos los datos pero mantiene la estructura.

---

## ALTER TABLE - Restricciones

### Primary Key

```sql
-- Agregar Primary Key
ALTER TABLE empleados ADD PRIMARY KEY (id);

-- Quitar Primary Key
ALTER TABLE empleados DROP PRIMARY KEY;
```

---

### Foreign Key

```sql
-- Agregar Foreign Key
ALTER TABLE pedidos 
ADD CONSTRAINT fk_empleado 
FOREIGN KEY (empleado_id) REFERENCES empleados(id);

-- Quitar Foreign Key
ALTER TABLE pedidos DROP FOREIGN KEY fk_empleado;
```

---

### Unique Constraint

```sql
ALTER TABLE empleados ADD CONSTRAINT unique_correo UNIQUE (correo);
```

---

## ALTER TABLE - Modificaciones de Columnas

### Cambiar Nombre de Columna

```sql
ALTER TABLE empleados CHANGE nombre nombre_completo VARCHAR(100);
```

---

### Cambiar Tipo de Dato

```sql
ALTER TABLE empleados MODIFY nombre_completo TEXT;
```

---