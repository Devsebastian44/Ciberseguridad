## Signo Igual en Elixir

En Elixir, el signo **`=`** no es un operador de asignación tradicional, sino un **operador de match** (coincidencia). Esto significa que Elixir trata de hacer coincidir el lado izquierdo con el lado derecho.

```elixir
# Esto no es asignación, es pattern matching
x = 1
1 = x  # Esto funciona porque x vale 1
2 = x  # Esto falla: ** (MatchError) no match of right hand side value: 1
````

### Comportamiento del Operador de Match

```elixir
# Si la variable no existe, se "asigna" el valor
a = 1

# Si la variable existe, se verifica la coincidencia
1 = a  # Funciona
2 = a  # Falla

# Con estructuras de datos
{x, y} = {1, 2}  # x = 1, y = 2
{1, z} = {1, 3}  # z = 3
{2, w} = {1, 3}  # Falla: no coinciden
```

**Diferencia clave**: En lugar de "asignar" un valor, Elixir **verifica coincidencias** y extrae valores cuando es posible.

---

## Pattern Matching

Pattern matching es una **característica fundamental** de Elixir que permite **desestructurar datos** y hacer coincidir patrones específicos.

### Pattern Matching Básico

```elixir
# Con tuplas
{a, b, c} = {1, 2, 3}
# a = 1, b = 2, c = 3

# Con listas
[head | tail] = [1, 2, 3, 4]
# head = 1, tail = [2, 3, 4]

[first, second | rest] = [1, 2, 3, 4, 5]
# first = 1, second = 2, rest = [3, 4, 5]
```

### Pattern Matching con Valores Específicos

```elixir
# Hacer match con valores específicos
{:ok, result} = {:ok, "success"}
# result = "success"

{:error, _reason} = {:error, "file not found"}
# _reason es ignorado con el guión bajo

# Con maps
%{name: person_name} = %{name: "Juan", age: 30}
# person_name = "Juan"
```

**Uso del guión bajo `_`**: Indica que no nos interesa ese valor específico.

---

## Pattern Matching en Funciones

```elixir
defmodule Calculator do
  def divide({:ok, a}, {:ok, b}) do
    {:ok, a / b}
  end
  
  def divide({:error, reason}, _) do
    {:error, reason}
  end
  
  def divide(_, {:error, reason}) do
    {:error, reason}
  end
end

# Uso
Calculator.divide({:ok, 10}, {:ok, 2})  # {:ok, 5.0}
Calculator.divide({:error, "invalid"}, {:ok, 2})  # {:error, "invalid"}
```

**Ventaja**: Elixir selecciona automáticamente la función correcta según el **patrón que coincida**.

---

## El Operador Pin (`^`)

```elixir
# El operador ^ fuerza el match con el valor actual de la variable
x = 1
{^x, y} = {1, 2}  # y = 2, funciona porque x ya vale 1
{^x, z} = {2, 3}  # Falla porque x vale 1, no 2
```

**Uso del operador `^`**: Evita que una variable sea "reasignada" y en su lugar verifica que el valor coincida con el existente.

---

## Pattern Matching con Guardas

```elixir
case {1, 2, 3} do
  {a, b, c} when a + b == c -> "suma correcta"
  {a, b, c} when a * b == c -> "multiplicación correcta"
  _ -> "ningún patrón coincide"
end
```

**Guardas (`when`)**: Agregan condiciones adicionales al pattern matching para validaciones más complejas.