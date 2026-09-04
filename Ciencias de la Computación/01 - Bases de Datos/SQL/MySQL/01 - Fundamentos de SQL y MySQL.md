## Introducción

Este documento cubre los fundamentos de SQL y MySQL, proporcionando una base sólida para entender bases de datos relacionales y el sistema de gestión MySQL. Es el punto de partida para cualquier persona que quiera aprender a trabajar con datos de manera estructurada.

---

## Conceptos clave

### ¿Qué es SQL?

SQL (Structured Query Language) es el lenguaje estándar para interactuar con bases de datos relacionales. Permite realizar operaciones como definir estructuras, manipular datos y consultar información.

### Operaciones principales de SQL

- **DDL (Data Definition Language)**: Crear y modificar estructuras (bases de datos, tablas).
- **DML (Data Manipulation Language)**: Insertar, actualizar y eliminar datos.
- **DQL / SELECT**: Consultar y recuperar datos.
- **DCL**: Administrar permisos y usuarios.

### ¿Qué es una base de datos relacional?

Una base de datos relacional organiza la información en tablas conectadas por relaciones. Cada tabla tiene columnas (campos) y filas (registros).

- **Tabla**: Estructura principal para almacenar datos.
- **Columna**: Campo con un tipo de dato específico.
- **Fila**: Registro individual.
- **Esquema**: Conjunto de tablas relacionadas.
- **Clave primaria (PRIMARY KEY)**: Identifica de forma única cada fila.
- **Clave foránea (FOREIGN KEY)**: Crea relaciones entre tablas.
- **Índice**: Mejora el rendimiento de consultas.

### ¿Qué es MySQL?

MySQL es un sistema de gestión de bases de datos relacional (RDBMS) de código abierto, creado en 1995 por MySQL AB y actualmente mantenido por Oracle.

#### Características principales

- Código abierto con licencia dual (GPL y comercial).
- Multiplataforma (Windows, Linux, macOS).
- Amplio uso en aplicaciones web.
- Integración con lenguajes como PHP, Python, Java, Node.js.

#### Componentes de MySQL

- **MySQL Server**: Motor principal de la base de datos.
- **Herramientas**: MySQL Workbench (gráfica), línea de comandos, phpMyAdmin, DBeaver.

---

## Sintaxis y ejemplos básicos

### Conectar a MySQL (línea de comandos)

```bash
mysql -u root -p
```

### Crear una base de datos

```sql
CREATE DATABASE tienda;
USE tienda;
```

### Crear una tabla simple

```sql
CREATE TABLE productos (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(100),
  precio DECIMAL(10,2)
);
```

---

## Buenas prácticas

- Usa nombres descriptivos para bases de datos y tablas (en minúsculas, sin espacios).
- Define siempre claves primarias para integridad.
- Elige tipos de datos apropiados para optimizar espacio y rendimiento.
- Instala MySQL con contraseñas seguras y configura backups regulares.

---

## Resumen

SQL es el lenguaje universal para bases de datos relacionales, y MySQL es una implementación poderosa y accesible. Entender estos fundamentos es esencial antes de pasar a operaciones prácticas como crear tablas o consultar datos. En el siguiente documento, aprenderás a iniciar con MySQL y ejecutar comandos básicos.
