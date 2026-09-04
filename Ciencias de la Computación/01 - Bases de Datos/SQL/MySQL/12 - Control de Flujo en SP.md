## IF-THEN-ELSE

Permite ejecutar bloques de código según condiciones.

```sql
DELIMITER //
CREATE PROCEDURE verificar_edad(IN edad INT)
BEGIN
    IF edad >= 18 THEN
        SELECT 'Mayor de edad' AS resultado;
    ELSE
        SELECT 'Menor de edad' AS resultado;
    END IF;
END //
DELIMITER ;
````

---

## IF-THEN-ELSEIF

Permite evaluar múltiples condiciones de manera secuencial.

```sql
DELIMITER //
CREATE PROCEDURE clasificar_nota(IN nota INT)
BEGIN
    IF nota >= 90 THEN
        SELECT 'Excelente' AS resultado;
    ELSEIF nota >= 70 THEN
        SELECT 'Bueno' AS resultado;
    ELSEIF nota >= 50 THEN
        SELECT 'Regular' AS resultado;
    ELSE
        SELECT 'Deficiente' AS resultado;
    END IF;
END //
DELIMITER ;
```

---

## Estructura CASE

CASE evalúa condiciones y devuelve resultados según el valor de una expresión.

```sql
DELIMITER //
CREATE PROCEDURE dia_semana(IN numero INT)
BEGIN
    CASE numero
        WHEN 1 THEN SELECT 'Lunes' AS dia;
        WHEN 2 THEN SELECT 'Martes' AS dia;
        WHEN 3 THEN SELECT 'Miércoles' AS dia;
        WHEN 4 THEN SELECT 'Jueves' AS dia;
        WHEN 5 THEN SELECT 'Viernes' AS dia;
        ELSE SELECT 'Número inválido' AS dia;
    END CASE;
END //
DELIMITER ;
```

---

## Tratamiento de errores en CASE

Si no se contemplan todas las opciones, se recomienda usar `ELSE` para evitar errores o resultados inesperados.

```sql
-- Siempre incluir ELSE para manejar valores no previstos
```

---

## CASE condicional (similar a IF-THEN-ELSEIF)

Permite evaluar condiciones directamente dentro de CASE.

```sql
DELIMITER //
CREATE PROCEDURE evaluar_salario(IN salario DECIMAL(10,2))
BEGIN
    CASE
        WHEN salario < 1000 THEN SELECT 'Bajo' AS categoria;
        WHEN salario BETWEEN 1000 AND 3000 THEN SELECT 'Medio' AS categoria;
        WHEN salario > 3000 THEN SELECT 'Alto' AS categoria;
        ELSE SELECT 'No definido' AS categoria;
    END CASE;
END //
DELIMITER ;
```

---

## Uso de Loops

Los bucles permiten repetir comandos hasta que una condición se cumpla.  
Tipos: `WHILE`, `REPEAT`, `LOOP`.

### Ejemplo con WHILE

```sql
DELIMITER //
CREATE PROCEDURE contar_hasta(IN limite INT)
BEGIN
    DECLARE contador INT DEFAULT 1;

    WHILE contador <= limite DO
        SELECT contador AS numero;
        SET contador = contador + 1;
    END WHILE;
END //
DELIMITER ;
```