## Introducción

En JavaScript, puedes **interactuar con el navegador** y manipular las ventanas de diferentes maneras. Esto incluye abrir nuevas ventanas, cerrar ventanas y manejar **alertas, confirmaciones** y otros diálogos.

---

## **window.alert()**

El método `alert()` se utiliza para mostrar un **cuadro de diálogo** con un mensaje en el navegador. Este cuadro requiere que el usuario lo cierre antes de continuar con la ejecución del código.

### Sintaxis

```javascript
window.alert("Mensaje");
````

**Ejemplo:**

```javascript
alert("¡Hola, Mundo!");
```

---

## **window.confirm()**

El método `confirm()` se utiliza para mostrar un cuadro de diálogo con un mensaje y dos botones: **Aceptar** y **Cancelar**. Devuelve un **valor booleano** (`true` si el usuario hace clic en Aceptar, `false` si hace clic en Cancelar).

### Sintaxis

```javascript
let resultado = window.confirm("¿Estás seguro?");
```

**Ejemplo:**

```javascript
let confirmacion = confirm("¿Deseas continuar?");

if (confirmacion) {
  alert("Has elegido continuar.");
} else {
  alert("Has cancelado.");
}
```

---

## **window.prompt()**

El método `prompt()` se utiliza para mostrar un **cuadro de entrada** donde el usuario puede escribir un valor. Este método devuelve el texto que el usuario ingresa, o `null` si el usuario cancela la entrada.

### Sintaxis

```javascript
let valor = window.prompt("¿Cuál es tu nombre?");
```

**Ejemplo:**

```javascript
let nombre = prompt("¿Cómo te llamas?");

if (nombre) {
  alert("Hola, " + nombre + "!");
} else {
  alert("No has ingresado un nombre.");
}
```

---

## **window.open()**

El método `window.open()` se utiliza para **abrir una nueva ventana** del navegador o una nueva pestaña.

### Sintaxis

```javascript
window.open("url", "nombre", "características");
```

### Parámetros

- **`url`**: La dirección que se abrirá (puede ser una página web)
- **`nombre`**: El nombre de la nueva ventana o pestaña (puede ser un nombre único)
- **`características`**: Características adicionales como el tamaño de la ventana

**Ejemplo:**

```javascript
window.open("https://www.ejemplo.com", "_blank", "width=800, height=600");
```

---

## **window.close()**

El método `window.close()` se utiliza para **cerrar la ventana o pestaña** actual o una ventana que fue abierta mediante `window.open()`.

### Sintaxis

```javascript
window.close();
```

**Ejemplo:**

```javascript
// Este código cierra la ventana actual
window.close();
```

---

## Redirigir con **window.location**

Puedes cambiar la **URL de la ventana actual** utilizando `window.location`.

### Sintaxis

```javascript
window.location.href = "nueva_url";
```

**Ejemplo:**

```javascript
// Redirige a otra página
window.location.href = "https://www.ejemplo.com";
```