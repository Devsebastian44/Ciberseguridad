## `if` y `unless`

### `if`

La expresión **`if`** evalúa una condición y ejecuta código basado en si es **verdadera o falsa**.

```elixir
# Sintaxis básica
if condition do
  # código si es verdadero
else
  # código si es falso
end

# Ejemplo
age = 18
if age >= 18 do
  "Eres mayor de edad"
else
  "Eres menor de edad"
end

# If en una línea
if age >= 18, do: "Mayor", else: "Menor"

# If sin else
if user_logged_in? do
  redirect_to_dashboard()
end
````

**Valores truthy y falsy:**

- **`false`** y **`nil`** son falsy
- **Todo lo demás es truthy** (incluyendo 0, "", [], {})

```elixir
if 0, do: "0 es truthy"        # => "0 es truthy"
if [], do: "[] es truthy"      # => "[] es truthy"
if nil, do: "no se ejecuta"    # => nil
```

### `unless`

`unless` es lo **opuesto a `if`** - ejecuta el código cuando la condición es **falsa**.

```elixir
# Equivalente a if not condition
unless user_banned? do
  allow_access()
end

unless password_valid? do
  "Contraseña inválida"
else
  "Contraseña válida"
end
```

---

## `cond`

`cond` permite evaluar **múltiples condiciones** en secuencia, similar a `else if` en otros lenguajes.

```elixir
# Sintaxis
cond do
  condition1 -> result1
  condition2 -> result2
  true -> default_result  # catch-all
end

# Clasificación de notas
def grade_letter(score) do
  cond do
    score >= 90 -> "A"
    score >= 80 -> "B"
    score >= 70 -> "C"
    score >= 60 -> "D"
    true -> "F"
  end
end

# Ejemplo con múltiples condiciones
def describe_weather(temp, humidity) do
  cond do
    temp > 30 and humidity > 80 -> "Caluroso y húmedo"
    temp > 30 -> "Caluroso y seco"
    temp < 10 -> "Frío"
    humidity > 80 -> "Húmedo"
    true -> "Clima agradable"
  end
end
```

**Importante**: Siempre incluir un **catch-all** (`true ->`) o se lanzará un error si ninguna condición es verdadera.

---

## `case`

`case` permite hacer **pattern matching** contra un valor específico.

```elixir
# Sintaxis
case expression do
  pattern1 -> result1
  pattern2 -> result2
  pattern3 when guard -> result3
  _ -> default_result
end
```

### Ejemplos Básicos

```elixir
# Pattern matching con tuplas
def describe_tuple(tuple) do
  case tuple do
    {1, x} -> "Tupla que empieza con 1, segundo: #{x}"
    {x, 1} -> "Tupla que termina con 1, primero: #{x}"
    {x, y} -> "Tupla genérica: {#{x}, #{y}}"
    _ -> "No es una tupla de dos elementos"
  end
end

# Con listas
def process_list(list) do
  case list do
    [] -> "Lista vacía"
    [head] -> "Un elemento: #{head}"
    [head | tail] -> "Cabeza: #{head}, Cola: #{inspect(tail)}"
  end
end

# Con mapas
def process_user(user) do
  case user do
    %{name: name, age: age} when age >= 18 ->
      "Usuario adulto: #{name}"
    %{name: name, age: age} ->
      "Usuario menor: #{name}, edad: #{age}"
    %{name: name} ->
      "Usuario sin edad: #{name}"
    _ ->
      "Datos inválidos"
  end
end
```

### Guards en `case`

```elixir
def categorize_number(x) do
  case x do
    n when n < 0 -> "Negativo"
    n when n == 0 -> "Cero"
    n when n > 0 and n <= 10 -> "Pequeño positivo"
    n when n > 10 and n <= 100 -> "Mediano positivo"
    n when n > 100 -> "Grande positivo"
  end
end
```

### Case con Resultados de Funciones

```elixir
def handle_file_read(filename) do
  case File.read(filename) do
    {:ok, content} -> 
      "Archivo leído: #{String.length(content)} caracteres"
    {:error, :enoent} -> 
      "Archivo no encontrado"
    {:error, reason} -> 
      "Error leyendo archivo: #{reason}"
  end
end
```

---

## Excepciones

Elixir prefiere el patrón **"let it crash"** y usa tuplas `{:ok, result}` o `{:error, reason}`, pero también tiene excepciones.

### Tipos Comunes

```elixir
# RuntimeError (por defecto)
raise "Algo salió mal"

# Excepciones específicas
raise ArgumentError, "Argumento inválido"
raise ArithmeticError, "División por cero"
raise KeyError, "Clave no encontrada"
```

### `try/rescue/after`

```elixir
def safe_divide(a, b) do
  try do
    result = a / b
    {:ok, result}
  rescue
    ArithmeticError -> {:error, "División por cero"}
    error -> {:error, inspect(error)}
  after
    # Se ejecuta siempre, para cleanup
    IO.puts "Operación completada"
  end
end

# Parsing seguro
def parse_integer_safe(string) do
  try do
    result = String.to_integer(string)
    {:ok, result}
  rescue
    ArgumentError -> {:error, "No es un número válido"}
  end
end
```

### `throw/catch`

Para **control de flujo no local** (menos común):

```elixir
def find_in_nested_list(list, target) do
  try do
    search_nested(list, target)
    :not_found
  catch
    {:found, value} -> {:ok, value}
  end
end

defp search_nested([target | _tail], target) do
  throw({:found, target})
end
```

**Recomendación**: Usar tuplas `{:ok, result}` / `{:error, reason}` en lugar de excepciones para flujo normal del programa.