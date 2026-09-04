## ¿Qué es MySQL Workbench?

MySQL Workbench es la herramienta gráfica oficial para diseñar, administrar y ejecutar consultas en bases de datos MySQL.

### ¿Para qué sirve?

- Crear y modificar esquemas.
- Diseñar modelos entidad-relación (ERD).
- Ejecutar consultas SQL.
- Administrar usuarios, permisos y copias de seguridad.

---

## Instalación y primera conexión

1. Descarga MySQL Workbench desde el sitio oficial.
2. Instala el programa y asegúrate de que el servidor MySQL esté en ejecución.
3. Abre Workbench y crea una nueva conexión.
4. Ingresa el host (por ejemplo, `localhost`), el puerto (`3306`) y el usuario (`root`).
5. Prueba la conexión y guarda el perfil.

---

## Panel principal

En la pantalla de inicio puedes:

- Crear nuevas conexiones.
- Abrir conexiones recientes.
- Acceder al modelador de datos.
- Ver tareas administrativas.

---

## Crear un esquema desde Workbench

1. Haz clic en el botón **+** junto a **MySQL Connections** o abre una conexión existente.
2. En el panel de la izquierda, haz clic derecho en **Schemas**.
3. Selecciona **Create Schema**.
4. Escribe el nombre y aplica los cambios.

---

## Crear una tabla visualmente

1. Dentro del esquema seleccionado, haz clic derecho en **Tables**.
2. Elige **Create Table**.
3. Define el nombre de la tabla.
4. Agrega columnas, tipos y restricciones.
5. Aplica los cambios para crear la tabla.

---

## Ejecutar consultas SQL

1. Abre una nueva pestaña de **SQL Editor**.
2. Escribe tu consulta.
3. Presiona el botón de ejecución.
4. Revisa los resultados en la sección inferior.

Ejemplo:

```sql
USE tienda;
SELECT * FROM empleados;
```

---

## Modelado de datos

- Workbench permite crear diagramas ERD.
- Puedes arrastrar tablas y definir relaciones visualmente.
- Genera el script SQL para crear el modelo.

---

## Administración del servidor

Desde el panel de administración puedes:

- Ver el estado del servidor.
- Controlar procesos y variables.
- Administrar usuarios y privilegios.
- Realizar backups y restauraciones.

---

## Uso con bases de datos de ejemplo

Bases como **Sakila** son útiles para practicar consultas reales.
Puedes importarlas y explorarlas desde Workbench.

---

## Consejos prácticos

- Usa el editor SQL para mantener tus consultas.
- Guarda scripts frecuentes en archivos `.sql`.
- Revisa el historial de consultas en Workbench.
- Aprovecha el modelador para diseñar esquemas complejos.
