## Introducción

Los formatos **HTML** y **XML** son estructuras de texto utilizadas para representar datos.  
- **HTML (HyperText Markup Language):** describe páginas web con etiquetas para contenido y estructura.  
- **XML (eXtensible Markup Language):** organiza datos en un formato jerárquico y flexible, usado para intercambio de información.

---

## Inspeccionar una página web

- Usa el navegador (ej. Chrome, Firefox) → clic derecho → *Inspeccionar*.  
- Permite ver el código fuente HTML y localizar tablas, listas o etiquetas específicas.  
- Útil para identificar qué parte de la página contiene los datos que queremos leer.

---

## Leer datos de una página web (HTML)

```python
import pandas as pd

url = "https://es.wikipedia.org/wiki/Anexo:Países_por_población"
tablas = pd.read_html(url)

df = tablas[0]  # Selecciona la primera tabla encontrada
````

- `pd.read_html(url)` → devuelve una lista de DataFrames con las tablas de la página.
- Se puede filtrar con `match="texto"` para buscar tablas específicas.

---

## Escribir archivos HTML

```python
df.to_html("datos.html", index=False)
```

- Convierte un DataFrame en una tabla HTML.
- Útil para generar reportes web.
- Parámetros:
    - `index=False` → evita incluir la columna de índices.
    - `border=1` → añade borde a la tabla.

---

## Comprender cómo está estructurado el formato XML

- **Jerárquico:** datos organizados en etiquetas anidadas.
- **Ejemplo:**

```xml
<clientes>
  <cliente>
    <nombre>Ana</nombre>
    <edad>23</edad>
  </cliente>
  <cliente>
    <nombre>Luis</nombre>
    <edad>30</edad>
  </cliente>
</clientes>
```

- Cada etiqueta define un campo o grupo de datos.
- Similar a JSON, pero más verboso y con etiquetas explícitas.

---

## Leer datos en formato XML

```python
import pandas as pd

df = pd.read_xml("clientes.xml")
```

- Convierte el archivo XML en un DataFrame.
- Pandas interpreta las etiquetas como columnas.
- Se puede especificar la ruta de las etiquetas con `xpath`.

Ejemplo con `xpath`:

```python
df = pd.read_xml("clientes.xml", xpath="//cliente")
```

---

## Escribir archivos en formato XML

Pandas no tiene un método directo como `to_xml`, pero se puede exportar con otras librerías:

```python
import xml.etree.ElementTree as ET

root = ET.Element("clientes")

for _, row in df.iterrows():
    cliente = ET.SubElement(root, "cliente")
    ET.SubElement(cliente, "nombre").text = str(row["Nombre"])
    ET.SubElement(cliente, "edad").text = str(row["Edad"])

tree = ET.ElementTree(root)
tree.write("clientes.xml", encoding="utf-8", xml_declaration=True)
```

- Se construye un árbol XML con `ElementTree`.
- Se exporta con `tree.write()`.