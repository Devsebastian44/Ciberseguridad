## Introducción

Los **bucles en JavaScript** permiten ejecutar un bloque de código **repetidamente**, mientras se cumpla una condición.

---

## Bucle **for**

El bucle `for` se utiliza cuando sabes **cuántas veces** debe ejecutarse el código.

### Sintaxis

```javascript
for (inicialización; condición; actualización) {
  // Código a ejecutar
}
````

**Ejemplo:**

```javascript
for (let i = 1; i <= 5; i++) {
  console.log("Número:", i);
}
```

---

## Bucle **while**

El bucle `while` ejecuta el código mientras la condición sea `true`.

### Sintaxis

```javascript
while (condición) {
  // Código a ejecutar
}
```

**Ejemplo:**

```javascript
let i = 1;

while (i <= 5) {
  console.log("Número:", i);
  i++;
}
```

---

## Bucle **do...while**

El bucle `do...while` ejecuta el código **al menos una vez**, y luego repite mientras la condición sea `true`.

### Sintaxis

```javascript
do {
  // Código a ejecutar
} while (condición);
```

**Ejemplo:**

```javascript
let i = 1;

do {
  console.log("Número:", i);
  i++;
} while (i <= 5);
```

---

## Bucle **for...of**

El bucle `for...of` se utiliza para recorrer elementos de un **iterable**, como arreglos o cadenas.

### Sintaxis

```javascript
for (variable of iterable) {
  // Código a ejecutar
}
```

**Ejemplo:**

```javascript
let frutas = ["manzana", "naranja", "uva"];

for (let fruta of frutas) {
  console.log("Fruta:", fruta);
}
```

---

## Bucle **for...in**

El bucle `for...in` se utiliza para recorrer las **propiedades de un objeto**.

### Sintaxis

```javascript
for (clave in objeto) {
  // Código a ejecutar
}
```

**Ejemplo:**

```javascript
let persona = { nombre: "Sebastián", edad: 25, país: "México" };

for (let clave in persona) {
  console.log(clave + ":", persona[clave]);
}
```

---

## Palabras Clave **break** y **continue**

### **break**

Finaliza la ejecución del bucle.

**Ejemplo:**

```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 3) {
    break; // Sale del bucle cuando i es 3
  }
  console.log(i);
}
```

### **continue**

Salta a la **siguiente iteración** sin ejecutar el resto del código.

**Ejemplo:**

```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 3) {
    continue; // Salta cuando i es 3
  }
  console.log(i);
}
```