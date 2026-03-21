## Introducción

En JavaScript, la **conversión de tipos** se refiere a la capacidad de cambiar de un tipo de dato a otro, como convertir una **cadena de texto en un número** o viceversa.

---

## **parseInt()**

El método `parseInt()` se utiliza para convertir una cadena en un **número entero**. Si la cadena contiene caracteres no numéricos, el método ignorará los caracteres no válidos que se encuentran después de un número.

### Sintaxis

```javascript
parseInt(cadena, base);
````

- **`cadena`**: La cadena que se desea convertir en número entero
- **`base`**: Especifica la base en la que se encuentra el número (10 para decimal, 16 para hexadecimal)

**Ejemplo:**

```javascript
let numero1 = parseInt("42");        // 42
let numero2 = parseInt("42px");      // 42 (ignora 'px')
let numero3 = parseInt("3.14");      // 3 (solo toma la parte entera)
let numero4 = parseInt("1010", 2);   // 10 (interpreta '1010' en base 2)
```

---

## **parseFloat()**

El método `parseFloat()` se utiliza para convertir una cadena en un **número flotante** (decimal). Similar a `parseInt()`, también ignora caracteres no válidos después de un número.

### Sintaxis

```javascript
parseFloat(cadena);
```

**Ejemplo:**

```javascript
let numero1 = parseFloat("3.14");    // 3.14
let numero2 = parseFloat("42.5px");  // 42.5 (ignora 'px')
let numero3 = parseFloat("100");     // 100
```

---

## **Number()**

El método `Number()` convierte un valor en un número, ya sea **entero o flotante**. Si la cadena no puede convertirse a un número, devuelve **NaN** (Not a Number).

### Sintaxis

```javascript
Number(cadena);
```

**Ejemplo:**

```javascript
let numero1 = Number("42");         // 42
let numero2 = Number("3.14");       // 3.14
let numero3 = Number("Hola");       // NaN (no es un número)
let numero4 = Number("");           // 0 (cadena vacía se convierte en 0)
```

---

## **String()**

El método `String()` convierte un valor a una **cadena de texto**.

### Sintaxis

```javascript
String(valor);
```

**Ejemplo:**

```javascript
let texto1 = String(42);         // "42"
let texto2 = String(true);       // "true"
let texto3 = String(null);       // "null"
let texto4 = String(undefined);  // "undefined"
```

---

## **toString()**

El método `toString()` convierte cualquier valor a su **representación en cadena**.

### Sintaxis

```javascript
valor.toString();
```

**Ejemplo:**

```javascript
let numero = 42;
let texto = numero.toString();  // "42"
```

---

## Conversión de Tipos Automática (Coerción)

JavaScript realiza **conversiones automáticas de tipo** cuando se mezclan diferentes tipos de datos en una operación. Esto se llama **coerción de tipos**.

### De Cadena a Número (operaciones aritméticas)

```javascript
let resultado = "5" - 2;  // 3 (la cadena "5" se convierte en número)
```

### De Número a Cadena (concatenación)

```javascript
let mensaje = "El número es: " + 42;  // "El número es: 42"
```

### De **null** a Número

```javascript
let valor = null + 1;  // 1 (null se convierte en 0)
```

### De **undefined** a NaN

```javascript
let valor = undefined + 1;  // NaN (undefined no se puede convertir a número)
```