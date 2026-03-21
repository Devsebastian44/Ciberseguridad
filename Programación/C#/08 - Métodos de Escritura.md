## Introducción

En C#, la clase `Console` proporciona varios métodos **`Write()`** para escribir datos en la consola.

---

## Console.Write()

Escribe el texto o valor especificado en la consola **sin salto de línea**.

```csharp
Console.Write(valor);
```

---

## Console.WriteLine()

Similar a `Write()`, pero **agrega un salto de línea** al final.

```csharp
Console.WriteLine(valor);
```

---

## Console.Write(char[] buffer)

Escribe un **arreglo de caracteres** en la consola.

```csharp
char[] mensaje = {'H', 'o', 'l', 'a'};
Console.Write(mensaje);  // Escribe "Hola"
```

---

## Console.Write(string format, params object[] args)

Escribe texto **formateado** con placeholders `{}`.

```csharp
int edad = 25;
string nombre = "Juan";
Console.Write("Mi nombre es {0} y tengo {1} años.", nombre, edad);
```

---

## Console.Write(object obj)

Escribe un objeto en la consola usando su método **`ToString()`**.

```csharp
object obj = 12345;
Console.Write(obj);  // Convierte el objeto a texto y lo escribe
```

---

## Pedir y Leer Datos del Usuario con ReadLine()

El método `ReadLine()` permite leer una **línea completa de texto** ingresada por el usuario.

---

### Sintaxis

```csharp
string input = Console.ReadLine();
```

---

### Ejemplo Básico

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("¿Cuál es tu nombre?");
        string nombre = Console.ReadLine();
        Console.WriteLine("Hola, " + nombre + "!");
    }
}
```

---

## Convertir Datos Ingresados

El valor obtenido con `ReadLine()` siempre es un **string**, por lo que debe convertirse si se requiere otro tipo.

---

### Convertir a Entero

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Introduce tu edad:");
        string input = Console.ReadLine();
        int edad = int.Parse(input);
        Console.WriteLine("Tu edad es: " + edad);
    }
}
```

---

### Convertir a Número Decimal

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Introduce el precio:");
        string input = Console.ReadLine();
        double precio = double.Parse(input);
        Console.WriteLine("El precio es: " + precio);
    }
}
```

---