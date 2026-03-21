## Programa Hola Mundo en C#

Este es un programa simple en C# que imprime el mensaje **"Hola Mundo"** en la consola.

---

### Explicación del Código

1. **`using System;`** - Importa el espacio de nombres `System`, que contiene clases fundamentales como `Console`
2. **`namespace HolaMundo`** - Define un espacio de nombres llamado `HolaMundo` para organizar el código
3. **`internal class Program`** - Clase llamada `Program` dentro del espacio de nombres `HolaMundo`. `internal` indica que solo puede ser accedida dentro del mismo ensamblado
4. **`static void Main(string[] args)`** - Método principal, punto de entrada de la aplicación
5. **`Console.WriteLine("Hola Mundo");`** - Imprime el texto en la consola

---

### Código

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace HolaMundo
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hola Mundo");
        }
    }
}
```

---

### ¿Para qué sirve?

Este código muestra cómo crear una aplicación básica en C# que imprima un mensaje en la consola. Es el ejemplo introductorio más común para aprender los fundamentos de la programación en C#.

---

## Compilar y Ejecutar una Aplicación de Consola

### Compilar

Ir a **Compilar > Compilar solución**.  
Después, abrir **Ver > Otras Ventanas > Salida** para revisar el resultado.

---

### Ejecutar

Ir a **Depurar > Iniciar sin Depurar**.  
Esto permite ver el programa en ejecución sin cerrar la consola inmediatamente.

---

### Compilar y Ejecutar con Depuración

**`Console.ReadKey();`** - Detiene la ejecución hasta que el usuario presione una tecla, evitando que la ventana se cierre de inmediato.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace HolaMundo
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hola Mundo");

            Console.ReadKey();
        }
    }
}
```

---