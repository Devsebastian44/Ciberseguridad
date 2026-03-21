Las funciones anónimas son funciones sin nombre que pueden ser asignadas a variables y pasadas como argumentos.

## Sintaxis básica:

```elixir
# Sintaxis completa
add = fn x, y -> x + y end
result = add.(5, 3)  # 8 (nota el punto antes del paréntesis)

# Función sin parámetros
greet = fn -> "¡Hola!" end
message = greet.()   # "¡Hola!"

# Función con un parámetro
square = fn x -> x * x end
result = square.(4)  # 16

# Función con múltiples líneas
complex_function = fn x, y ->
  sum = x + y
  product = x * y
  {sum, product}
end

{sum, product} = complex_function.(3, 4)  # {7, 12}
```

## Sintaxis abreviada con &:

```elixir
# Usando la sintaxis &
add = &(&1 + &2)
multiply = &(&1 * &2)
square = &(&1 * &1)

# Con funciones existentes
double = &(&1 * 2)
upcase = &String.upcase/1  # Referencia a función existente

# Ejemplos de uso
Enum.map([1, 2, 3], &(&1 * 2))        # [2, 4, 6]
Enum.filter([1, 2, 3, 4], &(&1 > 2))  # [3, 4]
```

## Funciones y Pattern Matching

Las funciones anónimas pueden usar pattern matching en sus parámetros.

```elixir
# Pattern matching básico
handle_result = fn
  {:ok, value} -> "Success: #{value}"
  {:error, reason} -> "Error: #{reason}"
end

handle_result.({:ok, "data loaded"})    # "Success: data loaded"
handle_result.({:error, "file not found"})  # "Error: file not found"

# Pattern matching con listas
process_list = fn
  [] -> "Lista vacía"
  [head] -> "Un elemento: #{head}"
  [head | tail] -> "Primer elemento: #{head}, resto: #{inspect(tail)}"
end

process_list.([])           # "Lista vacía"
process_list.([1])          # "Un elemento: 1"
process_list.([1, 2, 3])    # "Primer elemento: 1, resto: [2, 3]"

# Pattern matching con tuplas
handle_coordinates = fn
  {0, 0} -> "Origen"
  {x, 0} -> "En el eje X: #{x}"
  {0, y} -> "En el eje Y: #{y}"
  {x, y} -> "Punto: (#{x}, #{y})"
end

handle_coordinates.({0, 0})    # "Origen"
handle_coordinates.({5, 0})    # "En el eje X: 5"
handle_coordinates.({3, 4})    # "Punto: (3, 4)"
```

## Funciones con Múltiples Cuerpos

Las funciones anónimas pueden tener múltiples cláusulas, similar a las funciones nombradas.

```elixir
# Múltiples cláusulas con pattern matching
factorial = fn
  0 -> 1
  n when n > 0 -> n * factorial.(n - 1)
end

factorial.(5)  # 120

# Función para clasificar números
classify_number = fn
  n when n < 0 -> :negative
  0 -> :zero
  n when n > 0 and n < 10 -> :small_positive
  n when n >= 10 -> :large_positive
end

classify_number.(-5)   # :negative
classify_number.(0)    # :zero
classify_number.(3)    # :small_positive
classify_number.(15)   # :large_positive

# Procesador de comandos
command_processor = fn
  {"quit"} -> {:stop, "Goodbye!"}
  {"help"} -> {:continue, "Available commands: quit, help, echo"}
  {"echo", message} -> {:continue, "Echo: #{message}"}
  {unknown} -> {:continue, "Unknown command: #{unknown}"}
end

command_processor.({"echo", "Hello"})  # {:continue, "Echo: Hello"}
```

## Funciones que Pueden Retornar Funciones

Las funciones anónimas pueden retornar otras funciones, permitiendo crear closures y funciones de orden superior.

```elixir
# Función que retorna función
create_multiplier = fn factor ->
  fn number -> number * factor end
end

double = create_multiplier.(2)
triple = create_multiplier.(3)

double.(5)   # 10
triple.(4)   # 12

# Función que crea validadores
create_validator = fn rule ->
  case rule do
    :positive -> fn x -> x > 0 end
    :even -> fn x -> rem(x, 2) == 0 end
    :range -> fn {min, max} -> fn x -> x >= min and x <= max end end
  end
end

is_positive = create_validator.(:positive)
is_even = create_validator.(:even)
in_range = create_validator.(:range).({1, 10})

is_positive.(5)     # true
is_even.(4)         # true
in_range.(7)        # true

# Función de configuración
create_formatter = fn format ->
  case format do
    :json -> fn data -> Jason.encode!(data) end
    :string -> fn data -> inspect(data) end
    :csv -> fn data when is_list(data) -> Enum.join(data, ",") end
  end
end

json_formatter = create_formatter.(:json)
string_formatter = create_formatter.(:string)
```

## Parametrizar Funciones

Las funciones anónimas pueden ser parametrizadas para crear comportamientos flexibles.

```elixir
# Función parametrizada para operaciones matemáticas
create_operation = fn operation ->
  case operation do
    :add -> fn x, y -> x + y end
    :subtract -> fn x, y -> x - y end
    :multiply -> fn x, y -> x * y end
    :divide -> fn x, y -> if y != 0, do: x / y, else: :error end
  end
end

add_func = create_operation.(:add)
multiply_func = create_operation.(:multiply)

add_func.(10, 5)      # 15
multiply_func.(4, 3)  # 12

# Función parametrizada para filtros
create_filter = fn condition, threshold ->
  case condition do
    :greater -> fn x -> x > threshold end
    :less -> fn x -> x < threshold end
    :equal -> fn x -> x == threshold end
    :between -> fn {min, max} -> fn x -> x >= min and x <= max end end
  end
end

greater_than_5 = create_filter.(:greater, 5)
less_than_10 = create_filter.(:less, 10)
between_1_and_100 = create_filter.(:between, {1, 100})

Enum.filter([1, 6, 3, 12, 8], greater_than_5)  # [6, 12, 8]

# Función parametrizada para transformaciones
create_transformer = fn type, options ->
  case type do
    :string -> 
      case options[:case] do
        :upper -> &String.upcase/1
        :lower -> &String.downcase/1
        :title -> &String.capitalize/1
      end
    :number ->
      case options[:operation] do
        :double -> &(&1 * 2)
        :square -> &(&1 * &1)
        :abs -> &abs/1
      end
  end
end

uppercase_transformer = create_transformer.(:string, case: :upper)
square_transformer = create_transformer.(:number, operation: :square)

uppercase_transformer.("hello")  # "HELLO"
square_transformer.(5)           # 25
```


# & en Funciones

El operador `&` proporciona una sintaxis concisa para crear funciones anónimas.

## Sintaxis básica con &:

```elixir
# Función simple
double = &(&1 * 2)
sum = &(&1 + &2)
greet = &("Hello, #{&1}!")

double.(5)         # 10
sum.(3, 4)         # 7
greet.("Ana")      # "Hello, Ana!"

# Con múltiples parámetros
calculate = &(&1 * &2 + &3)
calculate.(2, 3, 4)  # 10

# Funciones más complejas
format_person = &("#{&1} (#{&2} años)")
format_person.("Juan", 30)  # "Juan (30 años)"
```

## Captura de funciones existentes:

```elixir
# Capturar funciones de módulos
upcase = &String.upcase/1
length = &String.length/1
split = &String.split/2

upcase.("hello")              # "HELLO"
length.("hello")              # 5
split.("a,b,c", ",")         # ["a", "b", "c"]

# Usar en Enum
words = ["hello", "world", "elixir"]
Enum.map(words, &String.upcase/1)     # ["HELLO", "WORLD", "ELIXIR"]
Enum.map(words, &String.length/1)     # [5, 5, 6]

# Capturar funciones propias
defmodule Math do
  def square(x), do: x * x
  def cube(x), do: x * x * x
end

square_func = &Math.square/1
cube_func = &Math.cube/1

Enum.map([1, 2, 3], square_func)  # [1, 4, 9]
```

## Combinando & con operadores:

```elixir
# Operaciones aritméticas
add_10 = &(&1 + 10)
multiply_by_3 = &(&1 * 3)
is_even = &(rem(&1, 2) == 0)

# Operaciones con strings
starts_with_a = &String.starts_with?(&1, "a")
length_greater_than_5 = &(String.length(&1) > 5)

# Operaciones con listas
first_element = &hd/1
list_length = &length/1
reverse_list = &Enum.reverse/1

# Uso práctico
numbers = [1, 2, 3, 4, 5]
Enum.map(numbers, add_10)          # [11, 12, 13, 14, 15]
Enum.filter(numbers, is_even)      # [2, 4]

words = ["apple", "banana", "apricot", "cherry"]
Enum.filter(words, starts_with_a)  # ["apple", "apricot"]
```

## Casos avanzados con &:

```elixir
# Funciones anidadas
transform_and_filter = fn list ->
  list
  |> Enum.map(&(&1 * 2))
  |> Enum.filter(&(&1 > 10))
end

transform_and_filter.([3, 5, 7, 9])  # [14, 18]

# Combinando con pattern matching
extract_name = &(elem(&1, 0))
extract_age = &(elem(&1, 1))

people = [{"Ana", 25}, {"Juan", 30}, {"Luis", 35}]
names = Enum.map(people, extract_name)  # ["Ana", "Juan", "Luis"]
ages = Enum.map(people, extract_age)    # [25, 30, 35]

# Con maps
get_name = &(&1[:name])
get_age = &(&1.age)  # Solo si las keys son atoms

users = [%{name: "Ana", age: 25}, %{name: "Juan", age: 30}]
Enum.map(users, get_name)  # ["Ana", "Juan"]
```