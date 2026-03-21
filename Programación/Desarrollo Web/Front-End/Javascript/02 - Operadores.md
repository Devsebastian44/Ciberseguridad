## Operadores Aritméticos

Se utilizan para realizar **operaciones matemáticas**.

- **`+`**: Suma
- **`-`**: Resta
- **`*`**: Multiplicación
- **`/`**: División
- **`%`**: Módulo (resto de la división)
- **`++`**: Incremento (suma 1 a la variable)
- **`--`**: Decremento (resta 1 a la variable)

**Ejemplo:**

```javascript
let a = 5;
let b = 3;
console.log(a + b); // 8
console.log(a - b); // 2
console.log(a * b); // 15
console.log(a / b); // 1.6667
console.log(a % b); // 2
a++;
console.log(a); // 6
a--;
console.log(a); // 5
````

---

## Operador **typeof**

El operador `typeof` se usa para obtener una cadena que indica el **tipo de dato** de una variable o valor.

### Sintaxis

```javascript
typeof valor;
```

### Posibles Resultados de **typeof**

- `"undefined"`: Si la variable no está definida o no se le ha asignado un valor
- `"boolean"`: Si el valor es un booleano (`true` o `false`)
- `"number"`: Si el valor es un número (ya sea entero o flotante)
- `"string"`: Si el valor es una cadena de texto
- `"object"`: Si el valor es un objeto o `null`
- `"function"`: Si el valor es una función

**Ejemplo:**

```javascript
let numero = 42;
console.log(typeof numero);  // "number"

let texto = "Hola Mundo";
console.log(typeof texto);   // "string"

let esVerdadero = true;
console.log(typeof esVerdadero);  // "boolean"

let objeto = { nombre: "Juan", edad: 30 };
console.log(typeof objeto);  // "object"

let funcion = function() {};
console.log(typeof funcion);  // "function"

let indefinido;
console.log(typeof indefinido);  // "undefined"

let nulo = null;
console.log(typeof nulo);  // "object" (comportamiento especial de `null`)
```

### Diferencia entre **typeof** y **instanceof**

- `typeof` se usa para obtener el **tipo primitivo** de un valor
- `instanceof` se usa para comprobar si un objeto es una **instancia de una clase** o constructor específico

**Ejemplo de instanceof:**

```javascript
let objeto = new Date();
console.log(objeto instanceof Date);  // true
```

---

## Operador **isNaN()**

El método `isNaN()` se utiliza para determinar si un valor es **NaN** (no es número).

### Sintaxis

```javascript
isNaN(valor);
```

### Comportamiento de **isNaN()**

- Si el valor es **NaN**, `isNaN()` devuelve `true`
- Si el valor **no es NaN** (es un número válido o puede ser convertido en uno), devuelve `false`

**Ejemplo:**

```javascript
console.log(isNaN(123));        // false (es un número)
console.log(isNaN("123"));      // false (se puede convertir a número)
console.log(isNaN("Hola"));     // true (no se puede convertir a número)
console.log(isNaN(undefined));  // true (indefinido no es un número)
console.log(isNaN(NaN));        // true (NaN siempre es NaN)
console.log(isNaN(true));       // false (true se convierte a 1)
console.log(isNaN(false));      // false (false se convierte a 0)
```

---

## Operadores Lógicos

Los **operadores lógicos** se utilizan para **combinar o invertir condiciones**. Devuelven valores booleanos (`true` o `false`).

### **AND** (`&&`)

Devuelve `true` si **todas** las condiciones son verdaderas.

**Sintaxis:**

```javascript
condición1 && condición2
```

**Ejemplo:**

```javascript
let esAdulto = true;
let tieneID = true;

if (esAdulto && tieneID) {
  console.log("Puedes entrar.");
} else {
  console.log("No puedes entrar.");
}
// Salida: "Puedes entrar."
```

### **OR** (`||`)

Devuelve `true` si **al menos una** de las condiciones es verdadera.

**Sintaxis:**

```javascript
condición1 || condición2
```

**Ejemplo:**

```javascript
let tienePermiso = false;
let esAdministrador = true;

if (tienePermiso || esAdministrador) {
  console.log("Acceso concedido.");
} else {
  console.log("Acceso denegado.");
}
// Salida: "Acceso concedido."
```

### **NOT** (`!`)

Invierte el valor de una condición. Si es `true`, se convierte en `false`, y viceversa.

**Sintaxis:**

```javascript
!condición
```

**Ejemplo:**

```javascript
let esVisible = true;

if (!esVisible) {
  console.log("El elemento está oculto.");
} else {
  console.log("El elemento es visible.");
}
// Salida: "El elemento es visible."
```

---

## Operadores Relacionales

Los **operadores relacionales** comparan dos valores y devuelven un **valor booleano** (`true` o `false`).

### **`>`** (Mayor que)

Devuelve `true` si el valor de la izquierda es mayor que el de la derecha.

**Ejemplo:**

```javascript
let a = 10;
console.log(a > 5);  // true
console.log(a > 15); // false
```

### **`<`** (Menor que)

Devuelve `true` si el valor de la izquierda es menor que el de la derecha.

**Ejemplo:**

```javascript
let b = 8;
console.log(b < 10); // true
console.log(b < 5);  // false
```

### **`>=`** (Mayor o igual que)

Devuelve `true` si el valor de la izquierda es mayor o igual que el de la derecha.

**Ejemplo:**

```javascript
let c = 15;
console.log(c >= 15); // true
console.log(c >= 20); // false
```

### **`<=`** (Menor o igual que)

Devuelve `true` si el valor de la izquierda es menor o igual que el de la derecha.

**Ejemplo:**

```javascript
let d = 12;
console.log(d <= 15); // true
console.log(d <= 10); // false
```

---

## Operadores de Igualdad

Los **operadores de igualdad** comparan si dos valores son iguales o diferentes.

### **`==`** (Igualdad débil)

Compara los valores **sin tener en cuenta el tipo de dato**. Convierte automáticamente los valores si son de diferente tipo.

**Ejemplo:**

```javascript
console.log(5 == "5"); // true (porque convierte el string "5" a número)
console.log(5 == 5);   // true
console.log(5 == 10);  // false
```

### **`===`** (Igualdad estricta)

Compara los valores **y el tipo de dato**. No realiza conversión automática.

**Ejemplo:**

```javascript
console.log(5 === "5"); // false (diferente tipo: número y string)
console.log(5 === 5);   // true
```

### **`!=`** (Diferente débil)

Compara si dos valores son diferentes **sin tener en cuenta el tipo de dato**.

**Ejemplo:**

```javascript
console.log(5 != "5"); // false (porque "5" se convierte a número y son iguales)
console.log(5 != 10);  // true
```

### **`!==`** (Diferente estricta)

Compara si dos valores son diferentes, **teniendo en cuenta el tipo de dato**.

**Ejemplo:**

```javascript
console.log(5 !== "5"); // true (diferente tipo: número y string)
console.log(5 !== 5);   // false
```

---

## Operador Ternario

El **operador ternario** (`? :`) es una forma corta de escribir una estructura `if...else` simple. Evalúa una condición y devuelve uno de dos valores dependiendo si es **verdadera o falsa**.

### Sintaxis

```javascript
condición ? valorSiVerdadero : valorSiFalso;
```

### Funcionamiento

- Si la **condición** es verdadera (`true`), retorna `valorSiVerdadero`
- Si es falsa (`false`), retorna `valorSiFalso`

**Ejemplo básico:**

```javascript
let edad = 20;
let mensaje = (edad >= 18) ? "Eres mayor de edad" : "Eres menor de edad";
console.log(mensaje); // "Eres mayor de edad"
```

### Equivalente con **if...else**

```javascript
// Usando if...else
let mensaje;
if (edad >= 18) {
  mensaje = "Eres mayor de edad";
} else {
  mensaje = "Eres menor de edad";
}

// Usando operador ternario
let mensaje = (edad >= 18) ? "Eres mayor de edad" : "Eres menor de edad";
```

### Ternarios Anidados

**Nota:** No recomendado por legibilidad.

```javascript
let nota = 85;
let resultado = (nota >= 90) ? "Excelente" :
                (nota >= 70) ? "Bueno" :
                (nota >= 50) ? "Regular" : "Insuficiente";
console.log(resultado); // "Bueno"
```