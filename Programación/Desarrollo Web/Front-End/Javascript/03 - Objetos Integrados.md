## Objeto **Math** en JavaScript

`Math` es un **objeto integrado (built-in)** en JavaScript que proporciona propiedades y métodos para realizar **operaciones matemáticas**.

> Es un objeto **estático**: no se instancia (no se usa `new Math()`), simplemente se usa como `Math.función()`.

---

## Propiedades Comunes

| Propiedad | Descripción |
|---|---|
| `Math.PI` | Valor de π (pi ≈ 3.14159...) |
| `Math.E` | Base del logaritmo natural (≈ 2.718) |
| `Math.LN2` | Logaritmo natural de 2 |
| `Math.LN10` | Logaritmo natural de 10 |
| `Math.SQRT2` | Raíz cuadrada de 2 |

---

## Métodos Más Usados

### **Redondeo**

```javascript
Math.round(4.5);   // 5 → redondea al entero más cercano
Math.floor(4.9);   // 4 → redondea hacia abajo
Math.ceil(4.1);    // 5 → redondea hacia arriba
Math.trunc(4.7);   // 4 → elimina decimales
````

### **Mínimo y Máximo**

```javascript
Math.max(3, 7, 1); // 7
Math.min(3, 7, 1); // 1
```

### **Aleatorios**

```javascript
Math.random();                  // número aleatorio entre 0 y 1
Math.floor(Math.random() * 10); // número aleatorio entre 0 y 9
```

### **Potencias y Raíces**

```javascript
Math.pow(2, 3);    // 8 (2^3)
Math.sqrt(16);     // 4
Math.cbrt(27);     // 3 (raíz cúbica)
```

### **Valores Absolutos**

```javascript
Math.abs(-10);     // 10
```

### **Trigonometría**

```javascript
Math.sin(0);           // 0
Math.cos(Math.PI);     // -1
Math.tan(Math.PI / 4); // ≈ 1
```