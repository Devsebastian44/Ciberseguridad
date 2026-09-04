## Conceptos clave

- **Filas distintas en una selección**  
  El comando `DISTINCT` permite mostrar únicamente registros únicos, eliminando duplicados en la salida.  

```sql
  SELECT DISTINCT ciudad 
  FROM clientes;
```

- **Ordenar la salida de la selección**  
    Se utiliza `ORDER BY` para organizar los resultados en orden ascendente (`ASC`) o descendente (`DESC`).
    
```sql
SELECT nombre, salario 
FROM empleados 
ORDER BY salario DESC;
```
    

## Agrupamiento de registros

- **Agrupar por campos**  
    El comando `GROUP BY` permite agrupar registros según uno o más campos.

```sql
SELECT departamento, COUNT(*) AS total_empleados 
FROM empleados 
GROUP BY departamento;
```

- **Funciones de agregación**  
    Se aplican sobre los grupos creados:
    
    - `SUM()` : suma de valores
    - `MIN()` : valor mínimo
    - `MAX()` : valor máximo
    - `AVG()` : promedio
    
```sql
SELECT departamento, AVG(salario) AS promedio_salario 
FROM empleados 
GROUP BY departamento;
```

## Filtrar agrupamientos con HAVING

- `HAVING` se utiliza para aplicar condiciones sobre los resultados de funciones de agregación.

```sql
SELECT departamento, SUM(salario) AS total_salarios 
FROM empleados 
GROUP BY departamento 
HAVING SUM(salario) > 50000;
```

## Limitar la salida de las consultas

- El comando `LIMIT` restringe la cantidad de filas devueltas.

```sql
SELECT * 
FROM productos 
ORDER BY precio DESC 
LIMIT 10;
```

## Clasificación con CASE

- El comando `CASE` permite crear condiciones dentro de la consulta para clasificar valores.

```sql
    SELECT nombre, 
           CASE 
             WHEN salario < 1000 THEN 'Bajo'
             WHEN salario BETWEEN 1000 AND 3000 THEN 'Medio'
             ELSE 'Alto'
           END AS categoria_salario
    FROM empleados;
```