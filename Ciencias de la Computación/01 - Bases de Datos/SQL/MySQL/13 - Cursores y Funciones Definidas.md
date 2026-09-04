## Estructura de CURSOR

Un **cursor** permite recorrer los resultados de una consulta fila por fila, útil cuando se necesita procesar múltiples registros dentro de un SP.

### Ejemplo básico

```sql
DELIMITER //
CREATE PROCEDURE recorrer_usuarios()
BEGIN
    DECLARE fin_cursor BOOLEAN DEFAULT FALSE;
    DECLARE id_usuario INT;
    DECLARE nombre_usuario VARCHAR(50);

    DECLARE cur CURSOR FOR
        SELECT id, nombre FROM usuarios;

    DECLARE CONTINUE HANDLER FOR NOT FOUND
        SET fin_cursor = TRUE;

    OPEN cur;

    bucle: LOOP
        FETCH cur INTO id_usuario, nombre_usuario;
        IF fin_cursor THEN
            LEAVE bucle;
        END IF;

        SELECT CONCAT('Usuario: ', id_usuario, ' - ', nombre_usuario) AS resultado;
    END LOOP bucle;

    CLOSE cur;
END //
DELIMITER ;
````

---

## Atribuir más de una columna al CURSOR

En el ejemplo anterior, el cursor obtiene tanto el `id` como el `nombre`.  
Se pueden incluir tantas columnas como sea necesario en el `FETCH`.

---

## Uso del CURSOR con Loop

El cursor se combina con estructuras de control como `LOOP`, `WHILE` o `REPEAT` para procesar registros uno por uno.  
El **handler** `NOT FOUND` es esencial para indicar cuándo se han terminado los registros.

---

## Crear y utilizar una función

Una **función** en MySQL devuelve un valor único y puede ser utilizada en consultas como cualquier otra función nativa.

### Ejemplo de función

```sql
DELIMITER //
CREATE FUNCTION calcular_descuento(precio DECIMAL(10,2), porcentaje INT)
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    DECLARE resultado DECIMAL(10,2);
    SET resultado = precio - (precio * porcentaje / 100);
    RETURN resultado;
END //
DELIMITER ;
```

### Uso de la función

```sql
SELECT calcular_descuento(100, 15) AS precio_con_descuento;
```