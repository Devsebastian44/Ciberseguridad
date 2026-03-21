## Tipos de Datos Básicos

```elixir
# Integers
integer = 42
large_integer = 1_000_000

# Floats
float = 3.14

# Atoms
atom = :hello
boolean_true = true          # true es un atom
nil_value = nil              # nil es un atom

# Strings (binarios UTF-8)
string = "Hello, world!"

# Verificación de tipos
is_integer(42)           # true
is_float(3.14)           # true
is_atom(:hello)          # true
is_binary("hello")       # true
````

---

## Tuplas

Las tuplas son **estructuras de datos de tamaño fijo** que agrupan elementos.

```elixir
# Crear tuplas
coordinates = {10, 20}
result = {:ok, "success"}
error = {:error, "file not found"}

# Acceder a elementos
elem(coordinates, 0)     # 10
tuple_size(coordinates)  # 2

# Pattern matching
{:ok, message} = {:ok, "success"}  # message = "success"
```

---

## Listas

Las listas son **colecciones ordenadas** de elementos de longitud variable.

```elixir
# Crear listas
numbers = [1, 2, 3, 4, 5]

# Operaciones básicas
length(numbers)          # 5
hd(numbers)             # 1 (head)
tl(numbers)             # [2, 3, 4, 5] (tail)

# Agregar elementos
new_list = [0 | numbers]        # [0, 1, 2, 3, 4, 5]

# Pattern matching
[first | rest] = [1, 2, 3, 4]   # first = 1, rest = [2, 3, 4]

# Operaciones comunes
Enum.map([1, 2, 3], &(&1 * 2))     # [2, 4, 6]
Enum.filter([1, 2, 3, 4], &(&1 > 2)) # [3, 4]
```

---

## Maps

Los maps son **estructuras de datos clave-valor**.

```elixir
# Crear maps
person = %{name: "Juan", age: 30, city: "Madrid"}

# Acceder a valores
person[:name]           # "Juan"
person.name            # "Juan" (solo con atoms)

# Actualizar valores existentes
updated_person = %{person | age: 31}

# Agregar nuevas keys
Map.put(person, :salary, 50000)

# Pattern matching
%{name: person_name} = person    # person_name = "Juan"
```

---

## Date y Time

```elixir
# Fechas
today = Date.utc_today()
specific_date = ~D[2023-12-25]
Date.add(today, 7)               # Agregar 7 días

# Tiempo
now = Time.utc_now()
specific_time = ~T[14:30:00]
Time.add(now, 3600)              # Agregar 1 hora
```

---

## IEx (Interactive Elixir)

```elixir
# Iniciar IEx
iex

# Ayuda
h Enum.map               # Ayuda sobre función

# Información
i "hello"                # Información sobre valor

# Historial
v                        # Última expresión

# Salir
exit
```

---

## Convenciones

```elixir
# Variables y funciones: snake_case
user_name = "Juan"

# Módulos: PascalCase
defmodule UserController do
end

# Atoms: snake_case con :
:user_created
```

---

## Operadores Principales

```elixir
# Aritméticos
1 + 2                    # 3
div(10, 3)               # 3 (división entera)
rem(10, 3)               # 1 (residuo)

# Comparación
1 == 1.0                 # true (compara valores)
1 === 1.0                # false (compara tipos)

# Lógicos
true && false            # false
false || true            # true

# Pipe
"hello" |> String.upcase() |> String.reverse()  # "OLLEH"

# Concatenación
"Hello" <> " " <> "World"  # "Hello World"
[1, 2] ++ [3, 4]         # [1, 2, 3, 4]
```

---

## Sentencia `with`

La sentencia **`with`** permite **encadenar operaciones** que pueden fallar de manera elegante.

```elixir
# Ejemplo básico
with {:ok, file} <- File.read("config.txt"),
     {:ok, data} <- Jason.decode(file) do
  {:ok, data}
else
  {:error, reason} -> {:error, "Failed: #{reason}"}
end
```

### Ejemplo de Registro de Usuario

```elixir
defmodule UserRegistration do
  def register_user(params) do
    with {:ok, email} <- validate_email(params["email"]),
         {:ok, password} <- validate_password(params["password"]),
         {:ok, user} <- create_user(email, password) do
      {:ok, user}
    else
      {:error, :invalid_email} -> {:error, "Email is invalid"}
      {:error, :weak_password} -> {:error, "Password too weak"}
    end
  end
end
```

**Ventaja de `with`**: Permite manejar múltiples operaciones que pueden fallar sin anidar múltiples `case` statements.