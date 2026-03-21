## Introducción

C# incluye varios tipos de datos divididos en **tipos de valor**, **tipos de referencia**, y **tipos nulos**.

---

## Tipos de Valor (Primitivos)

### Enteros (Para números sin decimales)

|Tipo|Tamaño|Rango|Uso|
|---|---|---|---|
|`byte`|8 bits|0 a 255|Valores pequeños sin signo (ej. RGB)|
|`sbyte`|8 bits|-128 a 127|Valores pequeños con signo|
|`short`|16 bits|-32,768 a 32,767|Números enteros pequeños|
|`ushort`|16 bits|0 a 65,535|Enteros positivos más grandes|
|`int`|32 bits|-2,147,483,648 a 2,147,483,647|**Enteros comunes en cálculos**|
|`uint`|32 bits|0 a 4,294,967,295|Conteo de objetos sin negativos|
|`long`|64 bits|-9E18 a 9E18|Números enteros muy grandes|
|`ulong`|64 bits|0 a 18E18|Solo positivos extremadamente grandes|

---

#### ¿Cuándo usarlos?

- **`int`** es el más común para enteros
- **`long`** se usa para números muy grandes (ej. distancias astronómicas)
- **`byte`** es ideal para valores entre 0 y 255, como datos en imágenes

---

### Números Decimales (Para valores con punto flotante)

|Tipo|Tamaño|Rango|Uso|
|---|---|---|---|
|`float`|32 bits|±1.5E−45 a ±3.4E38|Cálculos aproximados (gráficos)|
|`double`|64 bits|±5E−324 a ±1.7E308|**Matemáticas avanzadas**|
|`decimal`|128 bits|±1E−28 a ±7.9E28|**Finanzas con precisión alta**|

---

#### ¿Cuándo usarlos?

- **`float`** para gráficos y videojuegos (ej. Unity usa `float`)
- **`double`** para cálculos matemáticos
- **`decimal`** para dinero y finanzas

```csharp
float valorFloat = 3.14f;
double valorDouble = 3.14;
decimal valorDecimal = 3.14m;
```

---

### Booleanos (Verdadero o falso)

|Tipo|Tamaño|Valores|Uso|
|---|---|---|---|
|`bool`|8 bits|`true` o `false`|Condiciones (`if`, `while`)|

---

### Caracteres y Cadenas (Texto)

|Tipo|Tamaño|Uso|
|---|---|---|
|`char`|16 bits|Almacenar un **solo carácter** Unicode|
|`string`|Variable|Almacenar **texto completo**|

---

## Tipos de Referencia

### `object` (Cualquier tipo de dato)

- Puede almacenar **cualquier tipo de dato**
- Útil cuando no se sabe qué tipo se manejará

---

### `dynamic` (Flexible)

- Cambia de tipo en **tiempo de ejecución**
- Permite flexibilidad, pero puede generar errores

---

### Tipos Nullable (Valores opcionales)

|Tipo|Uso|
|---|---|
|`int?`|Permite **`null`** en tipos de valor|

**Ejemplo:**

```csharp
int? numero = null; // Permitido
```

---

|Tipo|Tamaño|Uso|
|---|---|---|
|`char`|16 bits|Almacenar un solo carácter Unicode|
|`string`|Variable|Almacenar texto completo|

---

## Tipos de Referencia

### `object` (Cualquier tipo de dato)

- Puede almacenar cualquier tipo de dato.
- Útil cuando no se sabe qué tipo se manejará.

---

### `dynamic` (Flexible)

- Cambia de tipo en tiempo de ejecución.
- Permite flexibilidad, pero puede generar errores.

---

### Tipos Nullable (Valores opcionales)

|Tipo|Uso|
|---|---|
|`int?`|Permite `null` en tipos de valor|

---
