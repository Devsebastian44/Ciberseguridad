## Introducción

JavaScript tiene diferentes tipos de datos, que se pueden clasificar en dos categorías principales: **tipos primitivos** y **tipos no primitivos** (objetos).

---

## Tipos Primitivos

Los **tipos primitivos** son valores **inmutables**. Cuando se asigna un valor a una variable, el valor es copiado directamente.

### **String**

Representa **secuencias de caracteres** (texto).

**Ejemplo:**

```javascript
let saludo = "Hola, mundo";
console.log(saludo); // "Hola, mundo"
````

---

### **Number**

Representa **valores numéricos**, tanto enteros como decimales.

**Ejemplo:**

```javascript
let edad = 25;
let precio = 19.99;
console.log(edad);   // 25
console.log(precio); // 19.99
```

---

### **Boolean**

Representa un **valor de verdad**, puede ser `true` o `false`.

**Ejemplo:**

```javascript
let esMayorDeEdad = true;
console.log(esMayorDeEdad); // true
```

---

### **Undefined**

Indica que una variable ha sido **declarada pero no tiene valor asignado**.

**Ejemplo:**

```javascript
let nombre;
console.log(nombre); // undefined
```

---

### **Null**

Representa la **ausencia intencional de valor** o la falta de objeto.

**Ejemplo:**

```javascript
let persona = null;
console.log(persona); // null
```

---

### **Symbol**

Representa un valor **único e inmutable**. Usado para crear **identificadores únicos** para propiedades de objetos.

**Ejemplo:**

```javascript
let simbolo = Symbol("identificador");
console.log(simbolo); // Symbol(identificador)
```

---

### **BigInt**

Representa **números enteros muy grandes** que no pueden ser representados por el tipo `Number`.

**Ejemplo:**

```javascript
let numeroGrande = 1234567890123456789012345678901234567890n;
console.log(numeroGrande); // 1234567890123456789012345678901234567890n
```