## Concepto

Un **Stored Procedure (SP)** es un bloque de código SQL almacenado en el servidor de base de datos. Permite encapsular lógica, reutilizar consultas y ejecutar procesos de manera eficiente.

## Lo que aprendimos en esta aula

- Crear un Stored Procedure que devuelve un texto.
- Cómo un SP devuelve un valor en su salida.
- Uso de funciones de MySQL y comentarios dentro del SP.
- Alterar un SP existente.
- Excluir (eliminar) un SP.

---

## Crear un Stored Procedure que devuelve un texto

```sql
DELIMITER //
CREATE PROCEDURE hola_mundo()
BEGIN
    SELECT 'Hola, mundo desde MySQL!' AS mensaje;
END //
DELIMITER ;
````

### Ejecución

```sql
CALL hola_mundo();
```

---

## Devolver un valor en la salida

Los SP pueden usar parámetros de salida para devolver valores.

```sql
DELIMITER //
CREATE PROCEDURE obtener_fecha_actual(OUT fecha_actual DATE)
BEGIN
    SET fecha_actual = CURDATE();
END //
DELIMITER ;
```

### Ejecución

```sql
CALL obtener_fecha_actual(@hoy);
SELECT @hoy;
```

---

## Uso de funciones y comentarios dentro del SP

Dentro de un SP se pueden usar funciones nativas de MySQL y agregar comentarios para documentar la lógica.

```sql
DELIMITER //
CREATE PROCEDURE saludo_personalizado(IN nombre VARCHAR(50))
BEGIN
    -- Este procedimiento devuelve un saludo personalizado
    SELECT CONCAT('Hola, ', nombre, '! Bienvenido a MySQL.') AS saludo;
END //
DELIMITER ;
```

### Ejecución

```sql
CALL saludo_personalizado('Sebastián');
```

---

## Alterar un Stored Procedure existente

MySQL no permite modificar directamente un SP con `ALTER PROCEDURE`.  
La práctica común es **eliminarlo y volver a crearlo** con los cambios.

```sql
DROP PROCEDURE IF EXISTS saludo_personalizado;

DELIMITER //
CREATE PROCEDURE saludo_personalizado(IN nombre VARCHAR(50))
BEGIN
    SELECT CONCAT('¡Saludos cordiales, ', nombre, '!') AS saludo;
END //
DELIMITER ;
```

---

## Excluir (eliminar) un Stored Procedure

```sql
DROP PROCEDURE nombre_del_procedimiento;
```

Ejemplo:

```sql
DROP PROCEDURE hola_mundo;
```