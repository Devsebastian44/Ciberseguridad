## ¿Qué es MySQL Workbench?

**MySQL Workbench** es una herramienta visual para **administración y diseño** de bases de datos MySQL.

### Funcionalidades

- **Modelado** de bases de datos (ERD)
- **Ejecución** de consultas SQL
- **Administración** de usuarios y permisos
- **Backups** y monitoreo

---

## Base de Datos Sakila

**Sakila** es una base de datos de ejemplo que simula un **videoclub**, ideal para practicar consultas SQL reales.

### Consultas de Ejemplo

```sql
-- Ver todas las películas
SELECT * FROM film;

-- Listar películas y su categoría
SELECT f.title, c.name 
FROM film f
JOIN film_category fc ON f.film_id = fc.film_id
JOIN category c ON fc.category_id = c.category_id;
```

---