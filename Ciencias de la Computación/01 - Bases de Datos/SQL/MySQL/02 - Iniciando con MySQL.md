## Introducción

Este documento te guía en los primeros pasos con MySQL: cómo conectarte al servidor, gestionar bases de datos básicas y navegar por el entorno. Es esencial antes de trabajar con tablas y datos.

---

## Conceptos clave

- **Conexión**: Establecer comunicación con el servidor MySQL.
- **Base de datos**: Contenedor de tablas y objetos.
- **Selección de BD**: Cambiar el contexto de trabajo.
- **Herramientas**: Línea de comandos vs. gráficas como Workbench.

---

## Sintaxis y ejemplos

### Conexión básica por terminal

```bash
mysql -u root -p
```

- `-u root`: Especifica el usuario.
- `-p`: Solicita la contraseña.

### Mostrar y seleccionar bases de datos

#### Ver todas las bases de datos

```sql
SHOW DATABASES;
```

#### Seleccionar una base de datos

```sql
USE tienda;
```

- Cambia la base de datos activa.

### Crear y eliminar bases de datos

#### Crear una base de datos

```sql
CREATE DATABASE tienda;
```

#### Eliminar una base de datos

```sql
DROP DATABASE tienda;
```

- Borra la BD y todos sus contenidos; usa con precaución.

### Mostrar tablas

```sql
SHOW TABLES;
```

- Lista tablas en la BD activa.

---

## Buenas prácticas

- Siempre verifica la conexión antes de ejecutar comandos.
- Usa nombres descriptivos para bases de datos.
- Evita eliminar bases de datos en producción sin backups.
- Prueba comandos en entornos de desarrollo primero.

---

## Resumen

Has aprendido a conectarte a MySQL, gestionar bases de datos básicas y navegar por el servidor. El siguiente paso es definir estructuras con DDL (crear tablas). Para herramientas gráficas, revisa el documento de MySQL Workbench al final del curso.
