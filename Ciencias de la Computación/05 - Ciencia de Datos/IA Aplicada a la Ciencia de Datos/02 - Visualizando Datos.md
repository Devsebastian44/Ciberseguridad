## Actividades con ChatGPT

Con la asistencia de ChatGPT logramos:

- **Generación de código para visuales**  
  - Gráficos de comparación (ej. barras).  
  - Gráficos de composición (ej. pie charts, stacked bars).  

- **Creación de visuales sin especificar el tipo de gráfico**  
  - A partir de instrucciones sobre columnas y relaciones de datos.  
  - Ejemplo: indicar “mostrar ventas por mes” y obtener un gráfico adecuado.  

- **Transformación de datos para visualización**  
  - Traducción de nombres de meses mediante un diccionario.  
  - Representación en un gráfico de líneas para mostrar tendencias.  

---

## Ejemplo de Prompt Usado

```
Tengo una tabla con las columnas 'mes' y 'ventas'. Genera un gráfico de líneas que muestre la evolución de las ventas a lo largo de los meses, usando Matplotlib.
```

### Ejemplo de Prompt Optimizado

```
Usa Matplotlib para crear un gráfico de líneas con la columna 'mes' traducida a nombres completos (enero, febrero, etc.) y la columna 'ventas'. Agrega título y etiquetas en español.
```