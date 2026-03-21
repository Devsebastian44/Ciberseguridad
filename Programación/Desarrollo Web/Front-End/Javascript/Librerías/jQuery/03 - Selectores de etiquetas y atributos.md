## Selectores de Etiquetas y Atributos en jQuery

Los **selectores en jQuery** permiten identificar y manipular elementos del **DOM** de forma sencilla. En esta sección nos enfocaremos en los **selectores de etiquetas** y **selectores de atributos**, fundamentales para trabajar con HTML dinámicamente.

---

## Selectores de Etiquetas

El **selector de etiquetas** se utiliza para seleccionar **todos los elementos** de un tipo específico de etiqueta HTML.

### Sintaxis
```javascript
$("etiqueta")
```

### Ejemplos
```javascript
$("p")        // Selecciona todos los párrafos <p>
$("div")      // Selecciona todos los contenedores <div>
$("span")     // Selecciona todos los elementos <span>
```

### Uso Práctico
```javascript
$("p").css("color", "blue");  
// Cambia el color de todos los párrafos a azul
```

---

## Selectores de Atributos

Los **selectores de atributos** permiten seleccionar elementos en función de los **atributos definidos en el HTML**.

### Sintaxis General
```javascript
$("[atributo]")
$("[atributo='valor']")
$("[atributo!='valor']")
$("[atributo^='valor']")
$("[atributo$='valor']")
$("[atributo*='valor']")
```

### Tipos de Selectores de Atributos

#### **Presencia de Atributo**
```javascript
$("[href]")  
// Selecciona todos los elementos que tengan el atributo href
```

#### **Atributo con Valor Exacto**
```javascript
$("[type='text']")  
// Selecciona todos los inputs cuyo atributo type sea exactamente "text"
```

#### **Atributo con Valor Distinto**
```javascript
$("[type!='text']")  
// Selecciona todos los inputs cuyo atributo type NO sea "text"
```

#### **Valor que Comienza con una Cadena**
```javascript
$("[src^='img/']")  
// Selecciona todos los elementos cuyo atributo src comience con "img/"
```

#### **Valor que Termina con una Cadena**
```javascript
$("[src$='.jpg']")  
// Selecciona todos los elementos cuyo atributo src termine en ".jpg"
```

#### **Valor que Contiene una Cadena**
```javascript
$("[title*='tutorial']")  
// Selecciona todos los elementos cuyo atributo title contenga la palabra "tutorial"
```

---

## Combinación de Selectores

Es posible **combinar selectores** de etiquetas y atributos para mayor precisión.

### Ejemplos
```javascript
$("input[type='text']")  
// Selecciona todos los inputs de tipo texto

$("a[target='_blank']")  
// Selecciona todos los enlaces que abren en una nueva pestaña

$("img[alt*='logo']")  
// Selecciona todas las imágenes cuyo atributo alt contenga "logo"
```

---

## Casos de Uso Comunes

### Validación de Formularios
```javascript
$("input[required]").css("border", "2px solid red");
// Resalta todos los campos obligatorios
```

### Manipulación de Enlaces
```javascript
$("a[href^='https']").addClass("seguro");
// Añade una clase a todos los enlaces que comiencen con https
```

### Gestión de Imágenes
```javascript
$("img[src$='.png']").hide();
// Oculta todas las imágenes con extensión .png
```