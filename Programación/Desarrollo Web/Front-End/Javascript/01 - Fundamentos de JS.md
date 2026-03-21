## Tipos de Variables en JavaScript

### **var**

- **Qué es**: Una forma antigua de declarar variables
- **Para qué sirve**: Se usa para declarar variables que pueden cambiar de valor
- **Características**:
    - **Ámbito de función**
    - Se puede redeclarar y reasignar
    - Soporta **hoisting** (se eleva al inicio)

**Ejemplo:**

```javascript
var x = 10;
x = 20; // Reasignación válida
````

---

### **let**

- **Qué es**: Forma moderna de declarar variables
- **Para qué sirve**: Se usa cuando el valor de la variable **cambiará dentro de un bloque**
- **Características**:
    - **Ámbito de bloque** (solo dentro de `{}`)
    - No se puede usar antes de ser declarada (**no hay hoisting**)

**Ejemplo:**

```javascript
let y = 30;
y = 40; // Reasignación válida
```

---

### **const**

- **Qué es**: Forma de declarar variables cuyo valor no debe cambiar
- **Para qué sirve**: Se usa cuando el valor de la variable **no debe cambiar** una vez asignado
- **Características**:
    - **Ámbito de bloque** (solo dentro de `{}`)
    - **No se puede reasignar** (aunque los objetos pueden modificarse)

**Ejemplo:**

```javascript
const z = 50;
z = 60; // Error: no se puede reasignar
```

---

## Métodos de Salida en JavaScript

Los **métodos de salida en JavaScript** permiten mostrar información al usuario o al desarrollador.

### **console.log()** – Salida en la Consola

El método `console.log()` se usa para **imprimir mensajes en la consola** del navegador. Es útil para **depuración** y ver valores de variables.

```javascript
console.log("Hola, mundo!"); 
console.log(5 + 3); // 8
```

**Ejemplo con variables:**

```javascript
let nombre = "Sebas";
console.log("Bienvenido, " + nombre);
```

Se usa principalmente para **depurar código** y ver valores en la **consola del navegador** (F12/Consola en Chrome/Firefox).

---

### **alert()** – Ventana Emergente de Alerta

`alert()` muestra un **cuadro de diálogo** con un mensaje. Se usa para **notificaciones rápidas**.

```javascript
alert("¡Bienvenido a mi página web!");
```

**Ejemplo con variables:**

```javascript
let mensaje = "Error: Contraseña incorrecta.";
alert(mensaje);
```

Se usa para mostrar **mensajes informativos al usuario**, pero no es recomendable abusar de él, ya que **bloquea la interacción** hasta que se cierre.

---

### **document.write()** – Escribir en la Página Web

`document.write()` se usa para **insertar texto directamente** en el documento HTML. No es recomendado en producción, ya que puede **sobrescribir el contenido** de la página.

```javascript
document.write("Hola, bienvenido a mi sitio web!");
```

**Ejemplo con HTML dinámico:**

```javascript
let nombre = "Sebas";
document.write("<h1>Bienvenido, " + nombre + "</h1>");
```