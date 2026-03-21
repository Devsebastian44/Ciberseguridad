## Introducción

En JavaScript, las **plantillas de texto (Template Strings)** permiten incluir variables dentro de cadenas de texto de forma **sencilla y legible**. Se utilizan las **comillas invertidas (` `)** en lugar de las comillas simples (`' '`) o dobles (`" "`).

---

## ¿Qué son las Plantillas de Texto?

Las **Template Strings** permiten:

- Insertar variables **sin concatenación manual**
- Usar **saltos de línea directamente** en la cadena
- Incluir **expresiones** dentro de la cadena

```javascript
const nombre = "Sebastian";
const edad = 25;

// Concatenación tradicional
console.log("Hola, mi nombre es " + nombre + " y tengo " + edad + " años.");

// Uso de Template Strings
console.log(`Hola, mi nombre es ${nombre} y tengo ${edad} años.`);
````

**Ventajas:** Código más limpio y legible. Se pueden usar múltiples líneas sin necesidad de `\n`.

---

## Interpolación de Variables

La interpolación en JavaScript se logra con **`${variable}`** dentro de las **comillas invertidas**.

```javascript
const producto = "Laptop";
const precio = 1200;

console.log(`El producto ${producto} cuesta $${precio}.`);
```

También podemos hacer **cálculos directamente** dentro de `${ }`:

```javascript
const precioConIVA = precio * 1.21;
console.log(`El precio con IVA es $${precioConIVA}.`);
```

---

## Saltos de Línea

Con Template Strings podemos escribir **cadenas multilínea** fácilmente:

```javascript
const mensaje = `Hola,
Este es un mensaje
en varias líneas.`;

console.log(mensaje);
```

Esto es mucho más cómodo que usar `\n` en concatenaciones tradicionales.

---

## Plantillas con Funciones

Podemos retornar una **cadena interpolada** dentro de una función:

```javascript
function saludo(nombre) {
    return `Hola ${nombre}, bienvenido a JavaScript.`;
}

console.log(saludo("Sebastian"));
```

---

## Uso con Objetos

Podemos extraer valores de un objeto y usarlos en una plantilla:

```javascript
const usuario = {
    nombre: "Sebastian",
    edad: 25,
    profesion: "Desarrollador"
};

console.log(`Nombre: ${usuario.nombre}
Edad: ${usuario.edad}
Profesión: ${usuario.profesion}`);
```

---

## Uso con Arrays

Podemos recorrer un array dentro de una plantilla de texto:

```javascript
const lenguajes = ["JavaScript", "Python", "Java"];

console.log(`Lenguajes de programación:
- ${lenguajes[0]}
- ${lenguajes[1]}
- ${lenguajes[2]}`);
```

O con **map()** para recorrer dinámicamente:

```javascript
console.log(`Lenguajes disponibles:\n${lenguajes.map(lang => `- ${lang}`).join("\n")}`);
```