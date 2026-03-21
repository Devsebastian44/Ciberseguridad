## Introducción

En C#, las variables pueden clasificarse según su **alcance, duración y forma de declaración**.

---

## Variables Locales

- Definidas dentro de un **método, constructor o bloque** (`{}`)
- Solo son accesibles **dentro de ese bloque**
- Deben ser **inicializadas antes de usarse**

### Ejemplo

```csharp
void Metodo()
{
    int numero = 10; // Variable local
    Console.WriteLine(numero);
}
```

---

## Variables de Instancia

- Declaradas dentro de una clase, pero **fuera de cualquier método**
- Cada objeto de la clase tiene su **propia copia**
- Pueden ser **privadas, públicas** u otro modificador de acceso
- **No requieren inicialización** explícita (reciben un valor por defecto)

### Ejemplo

```csharp
class Persona
{
    public string nombre; // Variable de instancia
    private int edad;     // Variable de instancia
}
```

---

## Variables Estáticas

- Definidas con la palabra clave **`static`**
- **Compartidas** entre todas las instancias de la clase
- Solo hay **una copia** para toda la clase

### Ejemplo

```csharp
class Contador
{
    public static int total = 0; // Variable estática
}
```

---

## Constantes

- Declaradas con la palabra clave **`const`**
- Su valor se asigna en la declaración y **no puede cambiar**
- Son implícitamente **`static`**

### Ejemplo

```csharp
class Constantes
{
    public const double PI = 3.14159; // Constante
}
```

---

## Variables de Solo Lectura (Read-Only)

- Declaradas con la palabra clave **`readonly`**
- Su valor se asigna en la **declaración o en el constructor**
- A diferencia de `const`, pueden depender de valores en **tiempo de ejecución**

### Ejemplo

```csharp
class Ejemplo
{
    public readonly int edad;

    public Ejemplo(int valor)
    {
        edad = valor; // Asignación permitida en el constructor
    }
}
```

---

## Variables Automáticamente Implementadas

- Usadas en **propiedades** de una clase
- Permiten declarar variables con **acceso y modificación automático**

### Ejemplo

```csharp
class Persona
{
    public string Nombre { get; set; } // Auto-implementada
}
```

---

## Variables Dinámicas

- Declaradas con la palabra clave **`dynamic`**
- El tipo se resuelve en **tiempo de ejecución**
- **Flexibles**, pero menos seguras

### Ejemplo

```csharp
dynamic variable = 10;
variable = "Hola"; // Permitido
```

---

## Variables Implícitas

- Declaradas con la palabra clave **`var`**
- El compilador **infiere el tipo** en tiempo de compilación
- El **valor inicial es obligatorio**

### Ejemplo

```csharp
var mensaje = "Hola, mundo"; // Tipo inferido: string
```

---

## Parámetros de Método

### Tipos de Parámetros

- **Por valor** - Por defecto
- **Por referencia** - Usan `ref` o `out`
- **Con valores predeterminados** - Valores opcionales
- **`params`** - Permiten número variable de argumentos

### Ejemplo

```csharp
void MostrarMensaje(ref string mensaje) { ... }
void Calcular(int x, out int resultado) { ... }
void Imprimir(params int[] numeros) { ... }
```

---

## Variables Globales

- C# **no admite variables globales** directas
- Se logra con **clases estáticas**

### Ejemplo

```csharp
static class Configuracion
{
    public static string RutaArchivo = "C:\\datos.txt"; // Variable "global"
}
```

---

## Mostrar el Valor de una Variable en Consola

Para mostrar el valor de una variable se usa su **nombre**.

### Ejemplo

```csharp
string saludo = "Hola";
Console.WriteLine(saludo);
```

---