## Enum

El módulo **Enum** es fundamental para **procesar colecciones** en Elixir.

```elixir
numbers = [1, 2, 3, 4, 5]

# map - transformar elementos
doubled = Enum.map(numbers, &(&1 * 2))  # [2, 4, 6, 8, 10]

# filter - filtrar elementos
evens = Enum.filter(numbers, &(rem(&1, 2) == 0))  # [2, 4]

# reduce - reducir a un valor único
sum = Enum.reduce(numbers, 0, &(&1 + &2))  # 15

# Operaciones complejas
users = [
  %{name: "Ana", age: 25, active: true},
  %{name: "Luis", age: 30, active: false},
  %{name: "María", age: 28, active: true}
]

# Encadenar operaciones
active_names = users
|> Enum.filter(&(&1.active))
|> Enum.map(&(&1.name))
|> Enum.sort()
# ["Ana", "María"]

# Otras funciones útiles
Enum.find(users, &(&1.age >= 30))           # Encontrar primer elemento
Enum.group_by(users, &(&1.active))          # Agrupar por criterio
Enum.sort_by(users, &(&1.age))              # Ordenar por criterio
````

---

## Streams

Los **Streams** son **enumerables perezosos (lazy)** que no evalúan inmediatamente.

```elixir
# Stream básico
stream = Stream.map([1, 2, 3, 4, 5], &(&1 * 2))
# No se ejecuta hasta que se evalúe

result = Enum.to_list(stream)  # [2, 4, 6, 8, 10]

# Generación infinita
infinite_numbers = Stream.iterate(1, &(&1 + 1))
first_10 = Enum.take(infinite_numbers, 10)  # [1, 2, 3, ..., 10]

# Procesamiento eficiente
big_range = 1..1_000_000
processed = big_range
|> Stream.map(&(&1 * &1))
|> Stream.filter(&(&1 > 100))
|> Enum.take(5)
```

### Diferencia entre Stream y Enum

```elixir
# Con Enum - evaluación inmediata (crea listas intermedias)
result_enum = 1..1_000_000
|> Enum.map(&(&1 * 2))        # Lista de 1M elementos
|> Enum.filter(&(&1 > 100))   # Nueva lista filtrada
|> Enum.take(10)

# Con Stream - evaluación perezosa (no crea intermedias)
result_stream = 1..1_000_000
|> Stream.map(&(&1 * 2))      # No crea lista
|> Stream.filter(&(&1 > 100)) # No crea lista
|> Enum.take(10)              # Solo evalúa lo necesario
```

**Ventaja de Streams**: Ahorra **memoria** al no crear estructuras intermedias, ideal para **datos grandes** o **infinitos**.

---

## Comprehensions

Las **comprehensions** proporcionan sintaxis concisa para **generar listas, maps y otros collectables**.

```elixir
# List comprehension básica
squares = for x <- 1..10, do: x * x
# [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

# Con filtros (guards)
even_squares = for x <- 1..10, rem(x, 2) == 0, do: x * x
# [4, 16, 36, 64, 100]

# Múltiples generadores
combinations = for a <- [1, 2], b <- [:x, :y], do: {a, b}
# [{1, :x}, {1, :y}, {2, :x}, {2, :y}]

# Map comprehension
map_comp = for {k, v} <- %{a: 1, b: 2, c: 3}, into: %{}, do: {k, v * 2}
# %{a: 2, b: 4, c: 6}

# En diferentes colectables
set_comp = for x <- 1..10, rem(x, 2) == 0, into: MapSet.new(), do: x
# MapSet con [2, 4, 6, 8, 10]

# Con pattern matching
users = [
  %{name: "Ana", age: 25, role: :admin},
  %{name: "Luis", age: 30, role: :user},
  %{name: "María", age: 28, role: :admin}
]

admin_names = for %{name: name, role: :admin} <- users, do: name
# ["Ana", "María"]

# Comprehension con reduce
sum = for x <- 1..100, reduce: 0 do
  acc -> acc + x
end
# 5050
```

---

## Strings

En Elixir, los **strings** son secuencias de bytes **UTF-8** representadas como binarios.

```elixir
# Strings básicos
name = "Juan"
greeting = "Hola, #{name}!"  # Interpolación

# Funciones básicas
String.length("Hola")          # 4
String.upcase("hola")          # "HOLA"
String.capitalize("juan")      # "Juan"

# Búsqueda y reemplazo
String.contains?("hello world", "world")    # true
String.starts_with?("elixir", "eli")        # true
String.replace("hello world", "world", "elixir")  # "hello elixir"

# División y unión
String.split("one,two,three", ",")          # ["one", "two", "three"]
Enum.join(["a", "b", "c"], "-")            # "a-b-c"

# Trim y padding
String.trim("  hello  ")                    # "hello"
String.pad_leading("42", 5, "0")           # "00042"
```

---

## Sigils

Los **sigils** proporcionan sintaxis alternativa para literales.

```elixir
# ~s - string sigil
simple = ~s(Este es un string con "comillas")

# ~w - word list sigil
words = ~w(uno dos tres)  # ["uno", "dos", "tres"]
atoms = ~w(uno dos tres)a # [:uno, :dos, :tres]

# ~r - regex sigil
regex = ~r/\d+/
Regex.scan(regex, "Hay 123 números")  # [["123"]]

# ~D - date, ~T - time, ~N - naive datetime
date = ~D[2023-12-25]
time = ~T[14:30:00]
datetime = ~N[2023-12-25 14:30:00]
```

---

## Binarios

Los **binarios** son secuencias de bytes. Los strings son un tipo especial de binario.

```elixir
# Binario básico
binary = <<1, 2, 3, 4>>
byte_size(binary)  # 4

# String como binario
string_binary = "hello"
byte_size(string_binary)   # 5

# Construcción de binarios
<<a, b, c>> = <<1, 2, 3>>  # a=1, b=2, c=3

# Pattern matching en strings
defmodule StringProcessor do
  def extract_prefix(<<"http://", rest::binary>>), do: {:http, rest}
  def extract_prefix(<<"https://", rest::binary>>), do: {:https, rest}
end

StringProcessor.extract_prefix("https://example.com")
# {:https, "example.com"}
```

**Conceptos clave**:

- **Enum**: Evaluación **inmediata**, crea estructuras intermedias
- **Stream**: Evaluación **perezosa**, eficiente con datos grandes
- **Comprehensions**: Sintaxis concisa para generar colecciones
- **Strings**: Binarios UTF-8 con funciones integradas