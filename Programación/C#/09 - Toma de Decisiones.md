## Introducción

En C#, la toma de decisiones se basa en **estructuras condicionales** que permiten ejecutar diferentes bloques de código dependiendo de una condición.

---

## if (Condición Simple)

Ejecuta un bloque de código **solo si la condición es verdadera**.

```csharp
int edad = 18;

if (edad >= 18)
{
    Console.WriteLine("Eres mayor de edad.");
}
```

---

## if-else (Condición Alternativa)

Ejecuta un bloque si la condición es **verdadera**, y otro si es **falsa**.

```csharp
int edad = 16;

if (edad >= 18)
{
    Console.WriteLine("Eres mayor de edad.");
}
else
{
    Console.WriteLine("Eres menor de edad.");
}
```

---

## if-else if-else (Múltiples Condiciones)

Evalúa **múltiples condiciones** en secuencia.

```csharp
int nota = 85;

if (nota >= 90)
{
    Console.WriteLine("Excelente");
}
else if (nota >= 70)
{
    Console.WriteLine("Aprobado");
}
else
{
    Console.WriteLine("Reprobado");
}
```

---

## switch (Múltiples Casos)

Evalúa una variable contra **múltiples valores posibles**.

```csharp
int opcion = 2;

switch (opcion)
{
    case 1:
        Console.WriteLine("Seleccionaste la opción 1.");
        break;
    case 2:
        Console.WriteLine("Seleccionaste la opción 2.");
        break;
    case 3:
        Console.WriteLine("Seleccionaste la opción 3.");
        break;
    default:
        Console.WriteLine("Opción no válida.");
        break;
}
```

---

## switch con Expresiones (C# 8+)

Versión **más moderna y concisa** del switch tradicional.

```csharp
int dia = 3;

string nombreDia = dia switch
{
    1 => "Lunes",
    2 => "Martes",
    3 => "Miércoles",
    4 => "Jueves",
    5 => "Viernes",
    6 => "Sábado",
    7 => "Domingo",
    _ => "Día no válido"
};

Console.WriteLine(nombreDia);  // Salida: Miércoles
```

---

## Operador Ternario (? :)

Forma **compacta** de escribir un if-else en una sola línea.

**Sintaxis:** `condición ? valor_si_verdadero : valor_si_falso`

```csharp
int edad = 20;
string mensaje = (edad >= 18) ? "Eres mayor de edad." : "Eres menor de edad.";
Console.WriteLine(mensaje);
```

---

## if Anidados

Estructuras **if dentro de if** para evaluar múltiples condiciones jerárquicas.

```csharp
bool tieneUsuario = true;
bool tieneContraseña = false;

if (tieneUsuario)
{
    if (tieneContraseña)
    {
        Console.WriteLine("Inicio de sesión exitoso.");
    }
    else
    {
        Console.WriteLine("Falta la contraseña.");
    }
}
else
{
    Console.WriteLine("Falta el usuario.");
}
```

---