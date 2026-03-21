## Selectores en jQuery

Los **selectores en jQuery** permiten acceder a elementos del DOM de forma sencilla para manipularlos. Los más comunes son los **selectores de ID** y los **selectores de Clase**.

---

## Selector de ID

Se utiliza para seleccionar un **único elemento** con un identificador único en el documento. En jQuery, se usa el símbolo `#` seguido del nombre del ID.

### Sintaxis

```javascript
$("#idElemento")
````

### Ejemplo

```html
<!DOCTYPE html>
<html>
<head>
  <title>Ejemplo Selector ID</title>
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
  <script>
    $(document).ready(function(){
      $("#titulo").css("color", "blue");
    });
  </script>
</head>
<body>
  <h1 id="titulo">Hola Mundo</h1>
</body>
</html>
```

En este ejemplo, el texto del `h1` con ID `titulo` se mostrará en **azul**.

---

## Selector de Clase

Se utiliza para seleccionar **uno o varios elementos** que comparten la misma clase. En jQuery, se usa el símbolo `.` seguido del nombre de la clase.

### Sintaxis

```javascript
$(".nombreClase")
```

### Ejemplo

```html
<!DOCTYPE html>
<html>
<head>
  <title>Ejemplo Selector Clase</title>
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
  <script>
    $(document).ready(function(){
      $(".resaltado").css("background-color", "yellow");
    });
  </script>
</head>
<body>
  <p class="resaltado">Este párrafo está resaltado.</p>
  <p class="resaltado">Este también tiene la clase resaltado.</p>
  <p>Este párrafo no tiene clase.</p>
</body>
</html>
```

Todos los elementos con la clase `resaltado` tendrán **fondo amarillo**.

---

## Diferencias entre ID y Clase

|Característica|Selector ID (`#`)|Selector Clase (`.`)|
|---|---|---|
|**Unicidad**|Debe ser único en el documento|Puede repetirse en múltiples elementos|
|**Símbolo en jQuery**|`#`|`.`|
|**Uso recomendado**|Identificar un único elemento|Agrupar varios elementos con estilo o comportamiento común|

---

## Combinación de Selectores

jQuery permite combinar selectores para mayor precisión.

### Ejemplo: ID + Clase

```javascript
$("#contenedor .item").hide();
```

Selecciona todos los elementos con clase `item` que estén dentro del elemento con ID `contenedor`.