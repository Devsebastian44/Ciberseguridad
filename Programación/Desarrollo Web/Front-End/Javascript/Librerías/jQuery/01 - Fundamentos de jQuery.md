## ¿Qué es jQuery?

**jQuery** es una biblioteca (library) de JavaScript **rápida, pequeña y rica en funcionalidades**. Fue creada por **John Resig** en 2006 con el objetivo de simplificar la **manipulación del DOM**, el manejo de eventos, las animaciones y las peticiones **AJAX**.

---

## Características Principales

- **Simplifica JavaScript**: Convierte tareas complejas en líneas de código simples
- **Compatibilidad entre navegadores**: Maneja las diferencias entre navegadores automáticamente
- **Sintaxis sencilla**: Usa selectores CSS para manipular elementos HTML
- **Ligera y extensible**: Es pequeña en tamaño y permite plugins
- **Lema famoso**: "Write less, do more" (Escribe menos, haz más)

### Ejemplo de la Diferencia

**JavaScript puro:**

```javascript
document.getElementById("miElemento").style.display = "none";
````

**Con jQuery:**

```javascript
$("#miElemento").hide();
```

---

## Cómo Vincular jQuery

Existen **dos formas principales** de vincular jQuery:

### 1. Usando un CDN (Content Delivery Network)

Es la forma más **común y rápida**. Enlazas jQuery desde un servidor externo.

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Mi proyecto con jQuery</title>
</head>
<body>
    
    <h1>Hola jQuery</h1>
    <button id="miBoton">Haz clic</button>

    <!-- Vinculación de jQuery desde CDN -->
    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
    
    <!-- Tu código JavaScript -->
    <script>
        $(document).ready(function(){
            $("#miBoton").click(function(){
                alert("¡Funciona jQuery!");
            });
        });
    </script>

</body>
</html>
```

#### CDNs Populares

- **jQuery oficial:** `https://code.jquery.com/jquery-3.7.1.min.js`
- **Google CDN:** `https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js`

### 2. Descargando jQuery Localmente

Puedes **descargar el archivo** desde [jquery.com](https://jquery.com/download/) y guardarlo en tu proyecto.

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>jQuery Local</title>
</head>
<body>
    
    <h1>jQuery desde archivo local</h1>

    <!-- jQuery desde carpeta local -->
    <script src="js/jquery-3.7.1.min.js"></script>
    
    <!-- Tu código -->
    <script src="js/main.js"></script>

</body>
</html>
```

---

## Consejos Importantes

### Orden de Carga

**Siempre coloca jQuery ANTES** de tu código JavaScript que lo use.

### Ubicación del Script

**Antes de `</body>`**: Es mejor vincular jQuery al final del body para **mejor rendimiento**.

### Versión Minificada

**Usa `.min.js`** en producción (es más ligera).

### Document Ready

**Envuelve tu código jQuery** en `$(document).ready()` o `$(function(){})` para asegurar que el **DOM esté cargado**.

```javascript
// Forma completa
$(document).ready(function(){
    // Tu código aquí
});

// Forma corta (más común)
$(function(){
    // Tu código aquí
});
```