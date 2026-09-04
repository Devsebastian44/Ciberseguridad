## Conceptos clave

- **Conectar tablas con JOIN**  
  El comando `JOIN` permite combinar registros de dos o más tablas basadas en una relación entre sus campos.  

```sql
  SELECT empleados.nombre, departamentos.nombre 
  FROM empleados 
  INNER JOIN departamentos 
  ON empleados.depto_id = departamentos.id;
```

- **Tipos de JOIN en MySQL**
    
    - `INNER JOIN` : devuelve solo las filas que tienen coincidencias en ambas tablas.
    - `LEFT JOIN` : devuelve todas las filas de la tabla izquierda y las coincidencias de la derecha.
    - `RIGHT JOIN` : devuelve todas las filas de la tabla derecha y las coincidencias de la izquierda.
    - `CROSS JOIN` : devuelve el producto cartesiano de ambas tablas.
    
```sql
SELECT clientes.nombre, pedidos.fecha 
FROM clientes 
LEFT JOIN pedidos 
ON clientes.id = pedidos.cliente_id;
```

## Unión de consultas

- **UNION y UNION ALL**  
    Permiten unir resultados de dos o más consultas, siempre que tengan el mismo número y tipo de columnas.
    
    - `UNION` elimina duplicados.
    - `UNION ALL` conserva todos los registros, incluso duplicados.
    
```sql
SELECT nombre FROM empleados 
UNION 
SELECT nombre FROM clientes;
```
    

## Subconsultas

- **Consulta como filtro de otra consulta**

```sql
SELECT nombre, salario 
FROM empleados 
WHERE salario > (SELECT AVG(salario) FROM empleados);
```

- **Consulta dentro de otra consulta**  
    Se pueden usar subconsultas en el `SELECT`, `WHERE` o `FROM`.

```sql
    SELECT nombre, 
           (SELECT COUNT(*) 
            FROM pedidos 
            WHERE pedidos.cliente_id = clientes.id) AS total_pedidos
    FROM clientes;
```
    

## Vistas (Views)

- **Crear una vista**  
    Una vista es una consulta almacenada que se puede tratar como una tabla virtual.

```sql
CREATE VIEW vista_empleados AS 
SELECT nombre, salario, departamento 
FROM empleados 
WHERE salario > 2000;
```

- **Usar una vista**

```sql
SELECT * 
FROM vista_empleados;
```