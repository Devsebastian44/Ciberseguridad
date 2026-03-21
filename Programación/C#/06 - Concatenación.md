## Introducción

La concatenación en C# se refiere a la **unión de cadenas de texto** (`string`). Existen varias formas de concatenar cadenas en C#:

---

## Usando el Operador `+`

La forma más **simple y común** de concatenar strings.

```csharp
string nombre = "Sebastian";
string saludo = "Hola, " + nombre + "!";
Console.WriteLine(saludo); // Salida: Hola, Sebastian!
```

---

## Usando `string.Concat()`

Método **explícito** para concatenar múltiples cadenas.

```csharp
string nombre = "Sebastian";
string saludo = string.Concat("Hola, ", nombre, "!");
Console.WriteLine(saludo); // Salida: Hola, Sebastian!
```

---

## Usando `string.Format()`

Permite usar **marcadores de posición** para insertar valores.

```csharp
string nombre = "Sebastian";
string saludo = string.Format("Hola, {0}!", nombre);
Console.WriteLine(saludo); // Salida: Hola, Sebastian!
```

---

## Usando Interpolación de Cadenas `$`

La forma más **moderna y legible** (C# 6.0+).

```csharp
string nombre = "Sebastian";
string saludo = $"Hola, {nombre}!";
Console.WriteLine(saludo); // Salida: Hola, Sebastian!
```

---

## Usando `StringBuilder`

**Recomendado** para concatenaciones grandes o en bucles (mejor rendimiento).

```csharp
using System.Text;

StringBuilder sb = new StringBuilder();
sb.Append("Hola, ");
sb.Append("Sebastian!");
Console.WriteLine(sb.ToString()); // Salida: Hola, Sebastian!
```

**Ventaja:** Más eficiente cuando se concatenan muchas cadenas, ya que evita crear múltiples objetos string en memoria.

---