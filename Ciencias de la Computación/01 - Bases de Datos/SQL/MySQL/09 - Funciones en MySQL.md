## Conceptos clave

### Funciones de tipo STRING (texto)

Permiten manipular y transformar cadenas de caracteres, muy útiles para limpiar datos, generar reportes más legibles o preparar información para análisis.

- `CONCAT()` : concatena valores

```sql
  SELECT CONCAT(nombre, ' ', apellido) AS nombre_completo 
  FROM empleados;
```

- `LENGTH()` : devuelve la longitud de la cadena.

```sql
SELECT nombre, LENGTH(nombre) AS caracteres 
FROM clientes;
```

- `UPPER()` y `LOWER()` : convierten texto a mayúsculas o minúsculas.

```sql
SELECT UPPER(nombre) AS nombre_mayuscula 
FROM clientes;
```

- `SUBSTRING()` : extrae una parte de la cadena.

```sql
SELECT SUBSTRING(correo, 1, 5) AS inicio_correo 
FROM usuarios;
```

- `TRIM()` : elimina espacios en blanco al inicio y al final.

```sql
SELECT TRIM(nombre) AS nombre_limpio 
FROM empleados;
```


---

### Funciones matemáticas

Se utilizan para realizar cálculos numéricos, desde operaciones simples hasta estadísticas básicas.

- `ROUND()` : redondea un número.

```sql
SELECT ROUND(salario, 2) AS salario_redondeado 
FROM empleados;
```

- `CEIL()` y `FLOOR()` : redondean hacia arriba o hacia abajo.

```sql
SELECT CEIL(precio) AS precio_arriba, FLOOR(precio) AS precio_abajo 
FROM productos;
```

- `ABS()` : devuelve el valor absoluto.

```sql
SELECT ABS(-150) AS valor_absoluto;
```

- `MOD()` : devuelve el resto de una división.

```sql
SELECT MOD(edad, 2) AS paridad 
FROM clientes;
```


---

### Funciones de tipo DATE (fechas)

Permiten trabajar con fechas y tiempos, fundamentales para reportes, auditorías y análisis temporales.

- `NOW()` : devuelve la fecha y hora actual.

```sql
SELECT NOW() AS fecha_actual;
```

- `CURDATE()` y `CURTIME()` : devuelven la fecha o la hora actual.

```sql
SELECT CURDATE() AS solo_fecha, CURTIME() AS solo_hora;
```

- `YEAR()`, `MONTH()`, `DAY()` : extraen partes de una fecha.

```sql
SELECT YEAR(fecha_contrato) AS anio, MONTH(fecha_contrato) AS mes 
FROM empleados;
```

- `DATEDIFF()` : calcula la diferencia en días entre dos fechas.

```sql
SELECT DATEDIFF(NOW(), fecha_registro) AS dias_transcurridos 
FROM clientes;
```

- `DATE_ADD()` y `DATE_SUB()` : suman o restan intervalos de tiempo.

```sql
SELECT DATE_ADD(fecha_pedido, INTERVAL 7 DAY) AS fecha_entrega 
FROM pedidos;
```


---

### Funciones de conversión

Permiten transformar tipos de datos, lo que facilita operaciones entre campos de distinta naturaleza.

- `CAST()` : convierte un valor a un tipo específico.

```sql
SELECT CAST(precio AS CHAR) AS precio_texto 
FROM productos;
```

- `CONVERT()` : similar a `CAST`, con soporte adicional para conjuntos de caracteres.

```sql
SELECT CONVERT('2026-04-17', DATE) AS fecha_convertida;
```

- `FORMAT()` : da formato a números, útil para reportes.

```sql
SELECT FORMAT(salario, 2) AS salario_formateado 
FROM empleados;
```
