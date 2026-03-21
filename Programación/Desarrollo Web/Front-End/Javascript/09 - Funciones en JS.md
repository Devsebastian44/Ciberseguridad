## Introducción

Las **funciones en JavaScript** son bloques de código **reutilizables** que permiten ejecutar una tarea específica. Pueden recibir **parámetros**, devolver valores y facilitar la **modularidad del código**.

---

## ¿Qué es una Función?

Una función es un conjunto de instrucciones agrupadas que se pueden ejecutar cuando sea necesario. Se define una vez y se puede **reutilizar** en cualquier parte del programa.

### Sintaxis Básica

```javascript
function nombreFuncion() {
    // Código a ejecutar
}
````

Para llamar a una función, simplemente se usa su nombre seguido de paréntesis:

```javascript
nombreFuncion();
```

---

## Tipos de Funciones

### **Funciones Declaradas**

Son funciones definidas con la palabra clave `function`. Se pueden llamar antes de su declaración debido al **hoisting**.

```javascript
function saludar() {
    console.log("Hola, bienvenido a JavaScript!");
}

saludar();  // Llama a la función
```

También pueden recibir **parámetros**:

```javascript
function sumar(a, b) {
    return a + b;
}

console.log(sumar(5, 3));  // 8
```

### **Funciones Expresadas**

Son funciones almacenadas en una variable. No se pueden llamar antes de su declaración.

```javascript
const restar = function(a, b) {
    return a - b;
};

console.log(restar(10, 4));  // 6
```

### **Funciones de Flecha (Arrow Functions)**

Son una forma **más corta y moderna** de escribir funciones.

```javascript
const multiplicar = (a, b) => a * b;

console.log(multiplicar(4, 3));  // 12
```

Si solo hay un parámetro, se pueden omitir los paréntesis:

```javascript
const cuadrado = x => x * x;
console.log(cuadrado(5));  // 25
```

Si hay varias líneas, se usan llaves `{}`:

```javascript
const mensaje = () => {
    console.log("Esto es una función de flecha.");
};
mensaje();
```

### **Funciones con Valores Predeterminados**

Se pueden definir **valores por defecto** para los parámetros.

```javascript
function saludar(nombre = "Usuario") {
    console.log(`Hola, ${nombre}!`);
}

saludar();         // Hola, Usuario!
saludar("Sebas");  // Hola, Sebas!
```

### **Funciones Anónimas**

Son funciones sin nombre, normalmente usadas en **eventos** o como argumentos de otras funciones.

```javascript
setTimeout(function() {
    console.log("Esto se ejecuta después de 2 segundos");
}, 2000);
```

Con función de flecha:

```javascript
setTimeout(() => console.log("Esto también funciona!"), 2000);
```

---

## Funciones y el **return**

El `return` se usa para **devolver un valor** de la función.

```javascript
function obtenerMensaje() {
    return "Este es un mensaje de retorno.";
}

console.log(obtenerMensaje());  // "Este es un mensaje de retorno."
```

Si una función no tiene `return`, devuelve `undefined`:

```javascript
function sinRetorno() {
    console.log("Hola!");
}

console.log(sinRetorno());  // undefined
```

---

## Funciones como Parámetros

Las funciones pueden pasarse como **argumentos** a otras funciones.

```javascript
function procesarNumero(num, operacion) {
    return operacion(num);
}

const doble = x => x * 2;
console.log(procesarNumero(5, doble));  // 10
```

---

## Funciones Autoejecutables (IIFE)

Son funciones que se ejecutan **inmediatamente** después de ser definidas.

```javascript
(function() {
    console.log("Soy una función autoejecutable!");
})();
```

Con parámetros:

```javascript
(function(nombre) {
    console.log(`Hola, ${nombre}!`);
})("Sebas");
```

---

## Ámbito de Variables en Funciones

Las variables pueden ser **globales** (accesibles desde cualquier parte) o **locales** (solo dentro de una función).

```javascript
let global = "Soy global";

function ejemplo() {
    let local = "Soy local";
    console.log(global);  // Funciona
    console.log(local);   // Funciona
}

ejemplo();
console.log(local);  // Error: local is not defined
```

---

## Recursividad

Una función puede **llamarse a sí misma** para resolver problemas repetitivos.

```javascript
function factorial(n) {
    if (n === 0) return 1;
    return n * factorial(n - 1);
}

console.log(factorial(5));  // 120
```

---

## Métodos de Manipulación de Texto

JavaScript proporciona múltiples métodos para la **manipulación de texto**, desde la transformación de mayúsculas y minúsculas hasta la búsqueda y sustitución de palabras dentro de cadenas.

### **Transformación de Texto**

```javascript
var numero = 25;
var texto1 = '  bienvenido al curso javascript curso genial  ';
var texto2 = 'ES MUY BUEN CURSO';

// Convertir número a string
var dato = numero.toString();
console.log(dato);  // "25"

// Convertir a mayúsculas
dato = texto1.toUpperCase();
console.log(dato);  

// Convertir a minúsculas
dato = texto2.toLowerCase();
console.log(dato);
```

### **Calcular Longitud**

```javascript
var nombre1 = '';
var nombre2 = ['romina', 'malaspina'];

console.log(nombre1.length);  // 0
console.log(nombre2.length);  // 2
```

### **Concatenar y Unir Textos**

```javascript
var textoTotal = texto1.concat(texto2 + ' que bueno');
console.log(textoTotal);
```

### **Métodos de Búsqueda en Cadenas**

**Buscar la posición de una palabra:**

```javascript
var busqueda = texto1.indexOf('curso');  // Primer aparición
console.log(busqueda);

busqueda = texto1.lastIndexOf('curso');  // Última aparición
console.log(busqueda);

busqueda = texto1.search('curso');  // Igual que indexOf, pero más potente
console.log(busqueda);
```

**Buscar coincidencias:**

```javascript
busqueda = texto1.match('curso');  // Devuelve info de la primera coincidencia
console.log(busqueda);

busqueda = texto1.match(/curso/g);  // Devuelve todas las coincidencias como array
console.log(busqueda);
```

### **Extraer Partes de una Cadena**

```javascript
busqueda = texto1.substr(16,5);  // Extrae 5 caracteres desde el índice 16
console.log(busqueda);

busqueda = texto1.charAt(42);  // Devuelve el carácter en la posición 42
console.log(busqueda);
```

### **Métodos de Verificación**

```javascript
busqueda = texto1.startsWith('bienvenido');  // Verifica si comienza con la palabra
console.log(busqueda);

busqueda = texto1.endsWith('genial');  // Verifica si termina con la palabra
console.log(busqueda);

busqueda = texto1.includes('javascript');  // Verifica si contiene la palabra
console.log(busqueda);
```

### **Reemplazo y Modificación de Texto**

**Reemplazar una palabra:**

```javascript
busqueda = texto1.replace('javascript', 'Angular');
console.log(busqueda);
```

**Extraer una parte del string:**

```javascript
busqueda = texto1.slice(14, 22);  // Extrae desde el índice 14 hasta el 22
console.log(busqueda);
```

**Convertir un string en un array:**

```javascript
busqueda = texto1.split(' ');  // Separa por espacios
console.log(busqueda);
```

**Eliminar espacios al inicio y final:**

```javascript
busqueda = texto1.trim();  // Elimina espacios en blanco al inicio y al final
console.log(busqueda);
```