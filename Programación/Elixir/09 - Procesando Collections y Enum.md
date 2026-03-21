## Qué son los Types

En Elixir, existen varios **tipos de colecciones** que implementan protocolos específicos:

```elixir
# Enumerable - tipos que pueden ser enumerados
list = [1, 2, 3]
map = %{a: 1, b: 2}
range = 1..10
mapset = MapSet.new([1, 2, 3])

# Todos implementan el protocolo Enumerable
Enum.count(list)    # 3
Enum.count(map)     # 2
Enum.count(range)   # 10
Enum.count(mapset)  # 3

# Collectable - tipos que pueden recibir elementos
Enum.into([1, 2, 3], %{})     # %{0 => 1, 1 => 2, 2 => 3}
Enum.into([1, 2, 3], MapSet.new())  # MapSet con [1, 2, 3]
```

### Enum

El módulo **Enum** es fundamental para procesar colecciones en Elixir.

```elixir
# Operaciones básicas
numbers = [1, 2, 3, 4, 5]

# map - transformar elementos
doubled = Enum.map(numbers, fn x -> x * 2 end)  # [2, 4, 6, 8, 10]
doubled_short = Enum.map(numbers, &(&1 * 2))   # Sintaxis corta

# filter - filtrar elementos
evens = Enum.filter(numbers, fn x -> rem(x, 2) == 0 end)  # [2, 4]
evens_short = Enum.filter(numbers, &(rem(&1, 2) == 0))

# reduce - reducir a un valor único
sum = Enum.reduce(numbers, 0, fn x, acc -> x + acc end)  # 15
sum_short = Enum.reduce(numbers, 0, &(&1 + &2))

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

# find - encontrar primer elemento que cumple condición
first_adult = Enum.find(users, &(&1.age >= 30))

# group_by - agrupar por criterio
by_status = Enum.group_by(users, &(&1.active))
# %{true => [%{name: "Ana"...}, %{name: "María"...}], false => [%{name: "Luis"...}]}

# sort_by - ordenar por criterio
by_age = Enum.sort_by(users, &(&1.age))

# chunk_by - agrupar elementos consecutivos similares
numbers = [1, 1, 2, 2, 3, 1, 1]
chunks = Enum.chunk_by(numbers, &(&1))  # [[1, 1], [2, 2], [3], [1, 1]]
```

### Streams

Los **Streams** son enumerables perezosos (lazy) que no evalúan inmediatamente.

```elixir
# Stream básico
stream = Stream.map([1, 2, 3, 4, 5], &(&1 * 2))
# No se ejecuta hasta que se evalúe

# Evaluación
result = Enum.to_list(stream)  # [2, 4, 6, 8, 10]

# Generación infinita
infinite_numbers = Stream.iterate(1, &(&1 + 1))
first_10 = infinite_numbers |> Enum.take(10)  # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Stream desde función
random_stream = Stream.repeatedly(fn -> :rand.uniform(100) end)
random_10 = Enum.take(random_stream, 10)

# Stream desde rango
big_range = 1..1_000_000
processed = big_range
|> Stream.map(&(&1 * &1))
|> Stream.filter(&(&1 > 100))
|> Enum.take(5)
```

### Ejemplo de Streams

```elixir
# Procesamiento eficiente de archivo grande
defmodule LogProcessor do
  def process_large_file(filename) do
    File.stream!(filename)
    |> Stream.map(&String.trim/1)
    |> Stream.filter(&String.contains?(&1, "ERROR"))
    |> Stream.map(&parse_log_line/1)
    |> Stream.filter(&(&1.severity >= 3))
    |> Enum.into([])
  end
  
  defp parse_log_line(line) do
    # Parsing logic aquí
    %{message: line, severity: 3, timestamp: DateTime.utc_now()}
  end
end

# Pipeline de transformación de datos
defmodule DataPipeline do
  def process_users(users) do
    users
    |> Stream.filter(&(&1.age >= 18))
    |> Stream.map(&normalize_user/1)
    |> Stream.chunk_every(100)  # Procesar en lotes de 100
    |> Stream.map(&process_batch/1)
    |> Enum.to_list()
  end
  
  defp normalize_user(user) do
    %{user | name: String.trim(user.name)}
  end
  
  defp process_batch(batch) do
    # Procesar lote
    Enum.count(batch)
  end
end
```

### Streams más Complejos

elixir

```elixir
# Stream de números fibonacci
fibonacci = Stream.unfold({0, 1}, fn {a, b} -> {a, {b, a + b}} end)
first_20_fib = Enum.take(fibonacci, 20)

# Stream cíclico
cycle_stream = Stream.cycle([:red, :green, :blue])
colors = Enum.take(cycle_stream, 10)  # [:red, :green, :blue, :red, ...]

# Stream con estado
stateful_stream = Stream.transform(1..10, 0, fn element, acc ->
  new_acc = acc + element
  {[{element, new_acc}], new_acc}
end)
result = Enum.to_list(stateful_stream)
# [{1, 1}, {2, 3}, {3, 6}, {4, 10}, ...]

# Stream con recursos
file_stream = File.stream!("data.txt")
|> Stream.map(&String.upcase/1)
|> Stream.into(File.stream!("output.txt"))
# Se ejecuta solo cuando se evalúa
```

### Viendo la Diferencia entre Stream y Enum

elixir

```elixir
# Con Enum - evaluación inmediata
list = 1..1_000_000

# Esto crea listas intermedias en memoria
result_enum = list
|> Enum.map(&(&1 * 2))        # Lista de 1M elementos
|> Enum.filter(&(&1 > 100))   # Nueva lista filtrada
|> Enum.take(10)              # Finalmente toma 10

# Con Stream - evaluación perezosa
result_stream = list
|> Stream.map(&(&1 * 2))      # No crea lista intermedia
|> Stream.filter(&(&1 > 100)) # No crea lista intermedia
|> Enum.take(10)              # Solo evalúa lo necesario

# Medición de rendimiento
defmodule Performance do
  def measure_enum do
    :timer.tc(fn ->
      1..1_000_000
      |> Enum.map(&(&1 * 2))
      |> Enum.filter(&(&1 > 100))
      |> Enum.take(10)
    end)
  end
  
  def measure_stream do
    :timer.tc(fn ->
      1..1_000_000
      |> Stream.map(&(&1 * 2))
      |> Stream.filter(&(&1 > 100))
      |> Enum.take(10)
    end)
  end
end
```

### Protocolo Collectable

El protocolo **Collectable** permite que tipos de datos reciban elementos.

```elixir
# Implementar Collectable para tipo personalizado
defmodule MyList do
  defstruct items: []
  
  defimpl Collectable do
    def into(my_list) do
      collector_fun = fn
        my_list_acc, {:cont, elem} -> 
          %{my_list_acc | items: [elem | my_list_acc.items]}
        my_list_acc, :done -> 
          %{my_list_acc | items: Enum.reverse(my_list_acc.items)}
        _my_list_acc, :halt -> 
          :ok
      end
      {my_list, collector_fun}
    end
  end
end

# Uso del protocolo
my_list = Enum.into([1, 2, 3], %MyList{})
# %MyList{items: [1, 2, 3]}

# Otros ejemplos de Collectable
Enum.into([{:a, 1}, {:b, 2}], %{})          # %{a: 1, b: 2}
Enum.into([1, 2, 3], MapSet.new())          # MapSet con [1, 2, 3]
Enum.into(["hello", " ", "world"], "")      # "hello world"
```

### Comprehensions

Las **comprehensions** proporcionan una sintaxis concisa para generar listas, maps y otros collectables.

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

# Comprehension con pattern matching
users = [
  %{name: "Ana", age: 25, role: :admin},
  %{name: "Luis", age: 30, role: :user},
  %{name: "María", age: 28, role: :admin}
]

admin_names = for %{name: name, role: :admin} <- users, do: name
# ["Ana", "María"]

# Comprehension anidada
matrix = for i <- 1..3, j <- 1..3, do: {i, j}
# [{1, 1}, {1, 2}, {1, 3}, {2, 1}, {2, 2}, {2, 3}, {3, 1}, {3, 2}, {3, 3}]

# Procesamiento de strings
chars = for <<c <- "hello">>, do: c
# [104, 101, 108, 108, 111] (códigos ASCII)

uppercase = for <<c <- "hello">>, do: <<c - 32>>
# ["H", "E", "L", "L", "O"]
```

### Scope y Comprehensions

Las variables en comprehensions tienen scope limitado.

```elixir
# Variables no "leak" fuera de comprehensions
x = 1
list = for x <- [1, 2, 3], do: x * 2
IO.puts(x)  # Sigue siendo 1

# Usar variables del scope exterior
multiplier = 10
result = for x <- [1, 2, 3], do: x * multiplier
# [10, 20, 30]

# Pattern matching en comprehensions
data = [ok: 1, error: "bad", ok: 2, error: "wrong", ok: 3]
successes = for {:ok, value} <- data, do: value
# [1, 2, 3]

# Comprehensions con reduce
sum = for x <- 1..100, reduce: 0 do
  acc -> acc + x
end
# 5050

# Reduce con acumulador complejo
word_count = for word <- String.split("hello world hello"), 
                 reduce: %{} do
  acc -> Map.update(acc, word, 1, &(&1 + 1))
end
# %{"hello" => 2, "world" => 1}
```


# Strings y Binarios

### Strings

En Elixir, los **strings** son secuencias de bytes UTF-8 representadas como binarios.

```elixir
# Strings básicos
name = "Juan"
greeting = "Hola, #{name}!"  # Interpolación

# Strings multilínea
multiline = """
Este es un string
que abarca múltiples
líneas.
"""

# Escape sequences
escaped = "Línea 1\nLínea 2\tTabulada"
quoted = "Dijo: \"Hola mundo\""

# Concatenación
full_name = "Juan" <> " " <> "Pérez"
# También: full_name = "Juan #{" "} Pérez"

# Funciones básicas de String
String.length("Hola")          # 4
String.upcase("hola")          # "HOLA"
String.downcase("MUNDO")       # "mundo"
String.capitalize("juan")      # "Juan"

# Búsqueda y reemplazo
String.contains?("hello world", "world")    # true
String.starts_with?("elixir", "eli")        # true
String.ends_with?("programming", "ing")     # true
String.replace("hello world", "world", "elixir")  # "hello elixir"

# División y unión
String.split("one,two,three", ",")          # ["one", "two", "three"]
Enum.join(["a", "b", "c"], "-")            # "a-b-c"

# Trim y padding
String.trim("  hello  ")                    # "hello"
String.pad_leading("42", 5, "0")           # "00042"
String.pad_trailing("hello", 8, "!")       # "hello!!!"
```

### Sigils

Los **sigils** proporcionan sintaxis alternativa para literales textuales.

```elixir
# ~s - string sigil (permite interpolación)
simple = ~s(Este es un string con "comillas")
interpolated = ~s(Hola #{name})

# ~S - string sigil sin interpolación
literal = ~S(#{name} no se interpola aquí)

# ~r - regex sigil
regex = ~r/\d+/
matches = Regex.scan(regex, "Hay 123 números y 456 más")
# [["123"], ["456"]]

# ~R - regex sigil sin interpolación
literal_regex = ~R/\d+/

# ~w - word list sigil
words = ~w(uno dos tres)  # ["uno", "dos", "tres"]
atoms = ~w(uno dos tres)a # [:uno, :dos, :tres]
chars = ~w(a b c)c        # ['a', 'b', 'c']

# ~D - date sigil
date = ~D[2023-12-25]

# ~T - time sigil
time = ~T[14:30:00]

# ~N - naive datetime sigil
datetime = ~N[2023-12-25 14:30:00]

# Sigils personalizados
defmodule MySigils do
  def sigil_u(string, []), do: String.upcase(string)
  def sigil_u(string, [?r]), do: String.reverse(String.upcase(string))
end

# Uso: ~u(hello) -> "HELLO"
# Con modificador: ~u(hello)r -> "OLLEH"
```

### String Comillas Simples

Las **comillas simples** en Elixir crean **char lists**, no strings.

```elixir
# Char list (no es string)
char_list = 'hello'  # [104, 101, 108, 108, 111]
string = "hello"     # "hello"

# Conversión entre tipos
String.to_charlist("hello")    # [104, 101, 108, 108, 111]
List.to_string([104, 105])     # "hi"

# Char lists son listas de enteros
char_list = 'ABC'  # [65, 66, 67]
[first | rest] = char_list
IO.puts(first)     # 65 (código ASCII de 'A')

# Útil para interfaz con Erlang
:os.getenv('HOME')  # Erlang espera char list
```

### Binary

Los **binarios** son secuencias de bytes. Los strings son un tipo especial de binario.

elixir

```elixir
# Binario básico
binary = <<1, 2, 3, 4>>
byte_size(binary)  # 4

# String como binario
string_binary = "hello"
byte_size(string_binary)   # 5
bit_size(string_binary)    # 40 (5 bytes * 8 bits)

# Construcción de binarios
<<a, b, c>> = <<1, 2, 3>>  # a=1, b=2, c=3

# Especificación de tipos y tamaños
<<number::16>> = <<0, 42>>  # number = 42 (16 bits big-endian)
<<x::8, y::8>> = <<256, 1>>  # x = 0 (256 mod 256), y = 1

# Diferentes tipos
<<float_num::float>> = <<64, 9, 33, 251, 84, 68, 45, 24>>
<<int_32::32>> = <<0, 0, 1, 0>>  # int_32 = 256

# Endianness
<<big::16-big>> = <<1, 0>>     # big = 256
<<little::16-little>> = <<1, 0>>  # little = 1

# Signed vs unsigned
<<signed::8-signed>> = <<255>>    # signed = -1
<<unsigned::8-unsigned>> = <<255>>  # unsigned = 255

# Binarios de strings UTF-8
<<codepoint::utf8>> = "ñ"  # codepoint para ñ
```

### Procesamiento de Strings con Binarios

```elixir
# Pattern matching en strings
defmodule StringProcessor do
  # Procesar carácter por carácter
  def process_chars(<<>>), do: []
  def process_chars(<<char::utf8, rest::binary>>) do
    [char | process_chars(rest)]
  end
  
  # Extraer prefijo
  def extract_prefix(<<"http://", rest::binary>>), do: {:http, rest}
  def extract_prefix(<<"https://", rest::binary>>), do: {:https, rest}
  def extract_prefix(other), do: {:unknown, other}
  
  # Parsing simple
  def parse_header(<<"Content-Length: ", length::binary>>) do
    case Integer.parse(String.trim(length)) do
      {num, ""} -> {:ok, :content_length, num}
      _ -> {:error, :invalid_length}
    end
  end
  
  def parse_header(<<"Content-Type: ", type::binary>>) do
    {:ok, :content_type, String.trim(type)}
  end
  
  def parse_header(_), do: {:error, :unknown_header}
  
  # Validación de formato
  def validate_email(email) do
    case email do
      <<name::binary, "@", domain::binary>> when byte_size(name) > 0 and byte_size(domain) > 0 ->
        case String.contains?(domain, ".") do
          true -> {:ok, email}
          false -> {:error, :invalid_domain}
        end
      _ -> {:error, :invalid_format}
    end
  end
  
  # Extraer números de string
  def extract_numbers(binary, acc \\ [])
  def extract_numbers(<<>>, acc), do: Enum.reverse(acc)
  def extract_numbers(<<char, rest::binary>>, acc) when char >= ?0 and char <= ?9 do
    {number, remaining} = extract_number(<<char, rest::binary>>, "")
    extract_numbers(remaining, [String.to_integer(number) | acc])
  end
  def extract_numbers(<<_char, rest::binary>>, acc) do
    extract_numbers(rest, acc)
  end
  
  defp extract_number(<<char, rest::binary>>, acc) when char >= ?0 and char <= ?9 do
    extract_number(rest, acc <> <<char>>)
  end
  defp extract_number(remaining, acc), do: {acc, remaining}
end

# Ejemplos de uso
StringProcessor.process_chars("Hola")  # [72, 111, 108, 97]
StringProcessor.extract_prefix("https://example.com")  # {:https, "example.com"}
StringProcessor.validate_email("user@domain.com")  # {:ok, "user@domain.com"}
StringProcessor.extract_numbers("abc123def456")  # [123, 456]

# Manipulación avanzada de binarios
defmodule BinaryUtils do
  # Invertir bytes de un binario
  def reverse_bytes(binary) do
    binary
    |> :binary.bin_to_list()
    |> Enum.reverse()
    |> :binary.list_to_bin()
  end
  
  # XOR de dos binarios
  def xor_binaries(<<>>, <<>>), do: <<>>
  def xor_binaries(<<a, rest_a::binary>>, <<b, rest_b::binary>>) do
    <<Bitwise.bxor(a, b), xor_binaries(rest_a, rest_b)::binary>>
  end
  
  # Comprimir usando run-length encoding
  def rle_compress(binary), do: rle_compress(binary, <<>>, nil, 0)
  
  defp rle_compress(<<>>, acc, nil, 0), do: acc
  defp rle_compress(<<>>, acc, char, count) do
    acc <> <<count, char>>
  end
  defp rle_compress(<<char, rest::binary>>, acc, char, count) do
    rle_compress(rest, acc, char, count + 1)
  end
  defp rle_compress(<<char, rest::binary>>, acc, prev_char, count) when prev_char != nil do
    new_acc = acc <> <<count, prev_char>>
    rle_compress(rest, new_acc, char, 1)
  end
  defp rle_compress(<<char, rest::binary>>, acc, nil, 0) do
    rle_compress(rest, acc, char, 1)
  end
end
```