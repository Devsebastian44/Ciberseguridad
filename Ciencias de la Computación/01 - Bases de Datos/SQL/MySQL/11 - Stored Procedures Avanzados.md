## Manipular comandos SQL dentro del SP

Un SP puede ejecutar cualquier instrucción SQL como `INSERT`, `UPDATE`, `DELETE` o `SELECT`.

```sql
DELIMITER //
CREATE PROCEDURE insertar_usuario(IN nombre VARCHAR(50), IN correo VARCHAR(100))
BEGIN
    INSERT INTO usuarios (nombre, correo) VALUES (nombre, correo);
END //
DELIMITER ;
````

### Ejecución

```sql
CALL insertar_usuario('Ana', 'ana@example.com');
```

---

## Ingresar parámetros para un SP

Los parámetros permiten que el SP reciba valores dinámicos.  
Tipos de parámetros:

- `IN`: Entrada.
- `OUT`: Salida.
- `INOUT`: Entrada y salida.

```sql
DELIMITER //
CREATE PROCEDURE buscar_usuario(IN id_usuario INT)
BEGIN
    SELECT * FROM usuarios WHERE id = id_usuario;
END //
DELIMITER ;
```

### Ejecución

```sql
CALL buscar_usuario(1);
```

---

## Tratamiento de errores

MySQL permite manejar errores con **handlers**.  
Un _handler_ captura condiciones específicas y define cómo actuar.

```sql
DELIMITER //
CREATE PROCEDURE eliminar_usuario(IN id_usuario INT)
BEGIN
    DECLARE CONTINUE HANDLER FOR SQLEXCEPTION
    BEGIN
        SELECT 'Ocurrió un error al intentar eliminar el usuario.' AS error;
    END;

    DELETE FROM usuarios WHERE id = id_usuario;
END //
DELIMITER ;
```

### Ejecución

```sql
CALL eliminar_usuario(5);
```

---

## Atribución de variables con SELECT

Se pueden asignar valores de una consulta a variables internas del SP.

```sql
DELIMITER //
CREATE PROCEDURE obtener_correo(IN id_usuario INT, OUT correo_usuario VARCHAR(100))
BEGIN
    SELECT correo INTO correo_usuario
    FROM usuarios
    WHERE id = id_usuario;
END //
DELIMITER ;
```

### Ejecución

```sql
CALL obtener_correo(1, @correo);
SELECT @correo;
```