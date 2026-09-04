## Introducción

El DDL (Data Definition Language) se usa para definir y modificar la estructura de la base de datos, como crear tablas, definir tipos de datos y establecer restricciones. Es fundamental antes de manipular datos.

---

## Conceptos clave

- **DDL**: Lenguaje para definir estructuras (CREATE, ALTER, DROP).
- **Tipos de datos**: Definen qué tipo de información almacena cada columna.
- **Restricciones**: Reglas para mantener integridad (PRIMARY KEY, FOREIGN KEY, UNIQUE, NOT NULL).
- **Modificación**: Cambiar estructuras existentes sin perder datos.

---

## Sintaxis y ejemplos

### Crear una base de datos

```sql
CREATE DATABASE tienda;
```

- Crea un esquema vacío.

### Tipos de datos comunes

#### Numéricos
- `INT`, `BIGINT`: Enteros.
- `DECIMAL(p, s)`: Decimales precisos.
- `FLOAT`, `DOUBLE`: Reales.

#### Texto
- `CHAR(n)`: Longitud fija.
- `VARCHAR(n)`: Longitud variable.
- `TEXT`: Texto largo.

#### Fecha y hora
- `DATE`: Solo fecha.
- `DATETIME`: Fecha y hora.
- `TIMESTAMP`: Marca de tiempo.

#### Lógico
- `BOOLEAN` o `TINYINT(1)`: Verdadero/falso.

### Crear una tabla

```sql
CREATE TABLE empleados (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  correo VARCHAR(150) UNIQUE,
  fecha_registro DATE
);
```

- `AUTO_INCREMENT`: Valor único automático.
- `NOT NULL`: No permite nulos.
- `UNIQUE`: Valores únicos.

### Claves y restricciones

#### Primary Key
```sql
CREATE TABLE categorias (id INT PRIMARY KEY, nombre VARCHAR(100));
```

#### Foreign Key
```sql
CREATE TABLE pedidos (
  id INT PRIMARY KEY,
  empleado_id INT,
  FOREIGN KEY (empleado_id) REFERENCES empleados(id)
);
```

### Modificar una tabla

#### Agregar columna
```sql
ALTER TABLE empleados ADD salario DECIMAL(10,2);
```

#### Eliminar columna
```sql
ALTER TABLE empleados DROP COLUMN salario;
```

#### Cambiar columna
```sql
ALTER TABLE empleados CHANGE nombre nombre_completo VARCHAR(120);
ALTER TABLE empleados MODIFY nombre_completo TEXT;
```

### Agregar restricciones
```sql
ALTER TABLE empleados ADD PRIMARY KEY (id);
ALTER TABLE empleados ADD CONSTRAINT unique_correo UNIQUE (correo);
```

### Eliminar y vaciar tablas
```sql
DROP TABLE empleados;  -- Elimina tabla y datos
TRUNCATE TABLE empleados;  -- Borra datos, mantiene estructura
```

---

## Buenas prácticas

- Elige tipos de datos precisos para optimizar espacio.
- Define PRIMARY KEY en todas las tablas.
- Usa FOREIGN KEY para relaciones.
- Modifica esquemas en desarrollo; en producción, haz backups.
- Evita DROP TABLE sin confirmación.

---

## Resumen

Con DDL, has creado la estructura de tu base de datos. Ahora puedes pasar a DML para insertar y manipular datos. Recuerda que cambios en DDL afectan la integridad de los datos.

---

## Índices

```sql
CREATE INDEX idx_nombre ON empleados(nombre);
DROP INDEX idx_nombre ON empleados;
```

- Los índices aceleran consultas sobre columnas usadas frecuentemente.

---

## Buenas prácticas DDL

- Define claramente `PRIMARY KEY` y `FOREIGN KEY`.
- Usa tipos de datos adecuados para cada columna.
- Evita columnas demasiado grandes si no son necesarias.
- Modifica esquemas con cuidado en bases de datos en producción.