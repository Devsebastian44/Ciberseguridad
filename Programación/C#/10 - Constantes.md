## Introducción

En C#, una **constante** es una variable cuyo valor **no puede cambiar durante la ejecución del programa**. Se usa cuando un dato es **fijo e inmutable** (ej. el número PI, días de la semana, IVA).

---

## Sintaxis

```csharp
const <tipo> NOMBRE = valor;
```

**Componentes:**

- `const` - Palabra clave para declarar la constante
- `tipo` - Tipo de dato (`int`, `double`, `string`, etc.)
- `NOMBRE` - El nombre de la constante, por convención en **MAYÚSCULAS**
- `valor` - Debe asignarse al momento de la declaración

---

## Ejemplo Básico

```csharp
const double PI = 3.1416;
const int DIAS_SEMANA = 7;
const string MENSAJE = "Bienvenido";

Console.WriteLine("El valor de PI es: " + PI);
Console.WriteLine("Una semana tiene " + DIAS_SEMANA + " días.");
Console.WriteLine(MENSAJE);
```

---

## Reglas Importantes

### 1. Siempre Deben Inicializarse

```csharp
const int x; // ❌ Error
const int y = 10; // ✅ Correcto
```

---

### 2. No Se Pueden Modificar Después

```csharp
const int EDAD = 18;
// EDAD = 20; ❌ Error: no se puede reasignar
```

---

### 3. Pueden Ser de Tipos Primitivos o String

```csharp
const bool ACTIVO = true;
const char INICIAL = 'A';
const string NOMBRE = "Juan";
```

---

### 4. Se Recomiendan para Valores Universales e Inmutables

Usar constantes para valores que **nunca cambiarán** durante la ejecución del programa.

---

## Constantes en Clases

```csharp
class Matematica
{
    public const double PI = 3.1416;
    public const double E = 2.718;
}
```

**Uso:**

```csharp
Console.WriteLine(Matematica.PI); // 3.1416
Console.WriteLine(Matematica.E);  // 2.718
```

---

## Diferencia entre const y readonly

|Característica|`const`|`readonly`|
|---|---|---|
|**Momento de asignación**|Tiempo de **compilación**|Tiempo de **ejecución**|
|**Modificación**|Nunca|Solo en constructor|
|**Valores dinámicos**|❌ No permitido|✅ Permitido|

### Ejemplo

```csharp
readonly int anio = DateTime.Now.Year; // ✅ Válido
const int anio = DateTime.Now.Year;    // ❌ Error: debe ser constante en compilación
```

---