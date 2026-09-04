## Introducción

Este documento explora filtros avanzados en consultas SELECT, incluyendo operadores complejos y patrones. Asume conocimientos básicos de WHERE.

---

## Conceptos clave

- **Filtros avanzados**: Combinar condiciones con AND/OR, NOT.
- **LIKE**: Búsqueda de patrones con comodines (% y _).
- **BETWEEN, IS NULL**: Rangos y valores nulos.
- **Subconsultas en WHERE**: Consultas anidadas.

---

## Sintaxis y ejemplos

### Operadores condicionales avanzados
```sql
SELECT nombre, edad FROM empleados WHERE edad >= 30;
```

### Combinación de filtros
- **AND**: Todas las condiciones.
```sql
SELECT * FROM productos WHERE precio > 100 AND stock > 50;
```
- **OR**: Al menos una.
```sql
SELECT * FROM clientes WHERE ciudad = 'Quito' OR ciudad = 'Guayaquil';
```
- **NOT**: Niega condición.
```sql
SELECT * FROM empleados WHERE NOT ciudad = 'Quito';
```

### LIKE para patrones
- `%`: Cero o más caracteres.
- `_`: Un carácter.
```sql
SELECT * FROM empleados WHERE nombre LIKE 'A%';
SELECT * FROM usuarios WHERE correo LIKE '%.com';
```

### Otros operadores
```sql
SELECT * FROM productos WHERE precio BETWEEN 50 AND 100;
SELECT * FROM empleados WHERE ciudad IS NULL;
```

### Subconsultas
```sql
SELECT * FROM empleados WHERE salario > (SELECT AVG(salario) FROM empleados);
```

---

## Buenas prácticas

- Usa paréntesis para combinar AND/OR.
- LIKE es sensible a mayúsculas; considera LOWER().
- Evita subconsultas complejas; usa JOINs cuando posible.

---

## Resumen

Filtros avanzados permiten consultas precisas. Combina con ORDER BY y LIMIT para resultados óptimos. Siguiente: presentación de datos con GROUP BY.