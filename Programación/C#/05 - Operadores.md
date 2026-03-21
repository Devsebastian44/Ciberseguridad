## Introducción

Los operadores aritméticos en C# se utilizan para realizar **cálculos matemáticos básicos** como suma, resta, multiplicación, etc.

---

## Operadores Aritméticos

### Tabla de Operadores

|Operador|Descripción|Ejemplo|Resultado|
|---|---|---|---|
|`+`|Suma|`5 + 3`|`8`|
|`-`|Resta|`5 - 3`|`2`|
|`*`|Multiplicación|`5 * 3`|`15`|
|`/`|División|`5 / 2`|`2` (int) o `2.5` (double)|
|`%`|Módulo (Residuo)|`5 % 2`|`1`|

---

### Suma (`+`)

```csharp
int a = 5;
int b = 3;
int resultado = a + b; // Resultado: 8
```

---

### Resta (`-`)

```csharp
int a = 5;
int b = 3;
int resultado = a - b; // Resultado: 2
```

---

### Multiplicación (`*`)

```csharp
int a = 5;
int b = 3;
int resultado = a * b; // Resultado: 15
```

---

### División (`/`)

```csharp
int a = 5;
int b = 2;
int resultado = a / b; // Resultado: 2 (entero)

double x = 5.0;
double y = 2.0;
double resultadoDecimal = x / y; // Resultado: 2.5
```

---

### Módulo (`%`)

```csharp
int a = 5;
int b = 2;
int resultado = a % b; // Resultado: 1
```

---

## Jerarquía de Operaciones

En C#, las operaciones siguen una **jerarquía de precedencia**:

---

### 1. Paréntesis `()`

```csharp
int resultado = (3 + 2) * 5; // Evalúa primero (3 + 2)
```

---

### 2. Incremento y Decremento `++`, `--`

```csharp
int a = 5;
int b = a++;  // b = 5, a = 6
int c = ++a;  // c = 7, a = 7
```

---

### 3. Multiplicación, División y Módulo `*`, `/`, `%`

```csharp
int resultado = 10 + 3 * 2; // Multiplica primero: 10 + 6 = 16
int resultado2 = 10 / 3 * 2; // Divide primero: 3 * 2 = 6
```

---

### 4. Suma y Resta `+`, `-`

```csharp
int resultado = 10 + 3 - 5; // De izquierda a derecha
```

---

### 5. Comparación `==`, `!=`, `<`, `<=`, `>`, `>=`

```csharp
int a = 5, b = 10;
bool resultado = a < b; // true
```

---

### 6. Lógicos `&&`, `||`

```csharp
bool resultado = true && false || true; // false || true = true
```

---

### 7. Asignación `=`, `+=`, `-=`, `*=`, `/=`, `%=`

```csharp
int a = 10;
a += 5; // Equivale a: a = a + 5
```

---

## Operadores Relacionales

### Igual `==`

```csharp
int x = 10, y = 10;
Console.WriteLine(x == y);  // true
```

---

### Diferente `!=`

```csharp
int x = 10, y = 5;
Console.WriteLine(x != y);  // true
```

---

### Mayor `>`

```csharp
int x = 10, y = 5;
Console.WriteLine(x > y);  // true
```

---

### Menor `<`

```csharp
int temperatura = 15;
Console.WriteLine(temperatura < 20);  // true
```

---

### Mayor o Igual `>=`

```csharp
int nota = 70;
Console.WriteLine(nota >= 60);  // true
```

---

### Menor o Igual `<=`

```csharp
int velocidad = 80;
Console.WriteLine(velocidad <= 100);  // true
```

---

## Operadores Lógicos Booleanos

### AND `&&`

Ambas condiciones deben ser **verdaderas**.

```csharp
bool tieneUsuario = true;
bool tieneContraseña = true;

if (tieneUsuario && tieneContraseña)
{
    Console.WriteLine("Inicio de sesión exitoso.");
}
```

---

### OR `||`

Al menos **una condición** debe ser verdadera.

```csharp
bool esAdmin = false;
bool tienePermiso = true;

if (esAdmin || tienePermiso)
{
    Console.WriteLine("Acceso permitido.");
}
```

---

### NOT `!`

**Invierte** el valor booleano.

```csharp
bool esMayor = false;

if (!esMayor)
{
    Console.WriteLine("No eres mayor de edad.");
}
```

---

## Uso con `if` y `while`

### Ejemplo con `if`

```csharp
int edad = 20;
bool tieneIdentificación = true;

if (edad >= 18 && tieneIdentificación)
{
    Console.WriteLine("Puedes entrar al evento.");
}
else
{
    Console.WriteLine("No puedes entrar.");
}
```

---

### Ejemplo con `while`

```csharp
int intentos = 0;
bool accesoPermitido = false;

while (!accesoPermitido && intentos < 3)
{
    Console.WriteLine("Intento de inicio de sesión...");
    intentos++;
}
```

---