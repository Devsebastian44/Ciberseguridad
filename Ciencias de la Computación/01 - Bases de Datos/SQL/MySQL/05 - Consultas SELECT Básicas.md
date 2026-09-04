## Introducción

SELECT es la base de las consultas en SQL. Permite recuperar datos de tablas, filtrarlos y presentarlos de manera organizada. Este documento cubre SELECT básico con filtros simples.

---

## Conceptos clave

- **SELECT**: Elegir columnas y filas de una tabla.
- **WHERE**: Filtrar registros con condiciones.
- **Operadores**: Comparadores (=, >, <) y lógicos (AND, OR).
- **LIKE e IN**: Búsqueda de patrones y listas.
- **ORDER BY y LIMIT**: Ordenar y limitar resultados.

---

## Sintaxis y ejemplos

### Seleccionar todas las filas
```sql
SELECT * FROM usuarios;
```

- Muestra todas las columnas.

### Seleccionar columnas específicas
```sql
SELECT nombre, correo FROM usuarios;
```

- Especifica columnas para claridad.

### Filtrar con WHERE
```sql
SELECT * FROM usuarios WHERE id > 5;
SELECT * FROM usuarios WHERE id < 10;
```

#### Comparadores
- `=`, `<>`, `>`, `<`, `>=`, `<=`

### Patrones y listas
```sql
SELECT * FROM usuarios WHERE correo LIKE '%@example.com';
SELECT * FROM usuarios WHERE nombre IN ('Ana', 'Carlos');
```

- `LIKE` usa `%` para comodines.
- `IN` para listas.

### Ordenar y limitar
```sql
SELECT nombre, correo FROM usuarios ORDER BY nombre ASC LIMIT 10;
```

- `ORDER BY` ordena; `LIMIT` restringe filas.

---

## Buenas prácticas

- Usa `SELECT *` solo para exploración; especifica columnas en producción.
- Combina WHERE con AND/OR para filtros complejos.
- Limita resultados con LIMIT para evitar sobrecargas.

---

## Resumen

SELECT básico te permite consultar y filtrar datos simples. Para agregaciones y JOINs, revisa los siguientes documentos. Practica con tablas de ejemplo como Sakila.