## Head y Tail

En Elixir, las listas se componen de un **head (cabeza)** y un **tail (cola)**.

```elixir
list = [1, 2, 3, 4, 5]

# Head es el primer elemento
hd(list)          # 1

# Tail es el resto de la lista
tl(list)          # [2, 3, 4, 5]

# Pattern matching
[h | t] = [1, 2, 3, 4, 5]
# h = 1, t = [2, 3, 4, 5]

# Extraer múltiples elementos
[first, second | rest] = [1, 2, 3, 4, 5]
# first = 1, second = 2, rest = [3, 4, 5]
````

---

## Procesamiento de Listas con Recursión

La **recursión** con head y tail es fundamental para procesar listas.

```elixir
defmodule ListProcessor do
  # Contar elementos
  def count([]), do: 0
  def count([_head | tail]), do: 1 + count(tail)
  
  # Sumar elementos
  def sum([]), do: 0
  def sum([head | tail]), do: head + sum(tail)
  
  # Verificar si existe un elemento
  def member?([], _element), do: false
  def member?([element | _tail], element), do: true
  def member?([_head | tail], element), do: member?(tail, element)
end

# Ejemplos
ListProcessor.count([1, 2, 3, 4])        # 4
ListProcessor.sum([1, 2, 3, 4])          # 10
ListProcessor.member?([1, 2, 3], 2)      # true
```

### Con Acumuladores (Tail Call Optimization)

```elixir
defmodule ListAccumulator do
  # Contar con acumulador
  def count(list), do: count(list, 0)
  defp count([], acc), do: acc
  defp count([_head | tail], acc), do: count(tail, acc + 1)
  
  # Reversar lista
  def reverse(list), do: reverse(list, [])
  defp reverse([], acc), do: acc
  defp reverse([head | tail], acc), do: reverse(tail, [head | acc])
  
  # Filtrar elementos
  def filter(list, fun), do: filter(list, fun, [])
  defp filter([], _fun, acc), do: reverse(acc)
  defp filter([head | tail], fun, acc) do
    if fun.(head) do
      filter(tail, fun, [head | acc])
    else
      filter(tail, fun, acc)
    end
  end
end

# Ejemplos
ListAccumulator.reverse([1, 2, 3, 4, 5])         # [5, 4, 3, 2, 1]
ListAccumulator.filter([1, 2, 3, 4, 5], &(&1 > 3))  # [4, 5]
```

**Ventaja de acumuladores**: Optimización de **tail call** que evita desbordamiento de pila en listas grandes.

---

## Construir Listas

```elixir
defmodule ListBuilder do
  # Duplicar cada elemento
  def double([]), do: []
  def double([head | tail]), do: [head * 2 | double(tail)]
  
  # Concatenar dos listas
  def concat([], list2), do: list2
  def concat([head | tail], list2), do: [head | concat(tail, list2)]
  
  # Tomar los primeros n elementos
  def take([], _n), do: []
  def take(_list, 0), do: []
  def take([head | tail], n) when n > 0 do
    [head | take(tail, n - 1)]
  end
end

# Ejemplos
ListBuilder.double([1, 2, 3, 4])           # [2, 4, 6, 8]
ListBuilder.concat([1, 2], [3, 4])         # [1, 2, 3, 4]
ListBuilder.take([1, 2, 3, 4, 5], 3)       # [1, 2, 3]
```

---

## Implementar `map` Personalizada

```elixir
defmodule CustomMap do
  # Versión básica recursiva
  def map([], _fun), do: []
  def map([head | tail], fun) do
    [fun.(head) | map(tail, fun)]
  end
  
  # Versión con acumulador (tail recursive)
  def map_acc(list, fun), do: map_acc(list, fun, [])
  defp map_acc([], _fun, acc), do: Enum.reverse(acc)
  defp map_acc([head | tail], fun, acc) do
    map_acc(tail, fun, [fun.(head) | acc])
  end
  
  # Map con índice
  def map_with_index(list, fun), do: map_with_index(list, fun, 0, [])
  defp map_with_index([], _fun, _index, acc), do: Enum.reverse(acc)
  defp map_with_index([head | tail], fun, index, acc) do
    result = fun.(head, index)
    map_with_index(tail, fun, index + 1, [result | acc])
  end
end

# Ejemplos
CustomMap.map([1, 2, 3, 4], &(&1 * 2))
# [2, 4, 6, 8]

CustomMap.map_with_index(["a", "b", "c"], fn item, index -> 
  "#{index}: #{item}" 
end)
# ["0: a", "1: b", "2: c"]
```

---

## Implementar `reduce` Personalizada

```elixir
defmodule CustomReduce do
  # Reduce básico (fold left)
  def reduce([], acc, _fun), do: acc
  def reduce([head | tail], acc, fun) do
    reduce(tail, fun.(head, acc), fun)
  end
  
  # Scan - mantiene estados intermedios
  def scan([], _acc, _fun), do: []
  def scan([head | tail], acc, fun) do
    new_acc = fun.(head, acc)
    [new_acc | scan(tail, new_acc, fun)]
  end
  
  # Reduce con terminación temprana
  def reduce_while([], acc, _fun), do: acc
  def reduce_while([head | tail], acc, fun) do
    case fun.(head, acc) do
      {:cont, new_acc} -> reduce_while(tail, new_acc, fun)
      {:halt, final_acc} -> final_acc
    end
  end
end

# Ejemplos
CustomReduce.reduce([1, 2, 3, 4], 0, &(&1 + &2))
# 10

CustomReduce.scan([1, 2, 3, 4], 0, &(&1 + &2))
# [1, 3, 6, 10] (suma acumulada)

CustomReduce.reduce_while([1, 2, 3, 4, 5], 0, fn
  x, acc when acc + x < 6 -> {:cont, acc + x}
  _, acc -> {:halt, acc}
end)
# 6 (detiene cuando suma >= 6)
```

---

## Patrones Avanzados

```elixir
defmodule AdvancedListPatterns do
  # Trabajar con listas de tuplas
  def extract_names([]), do: []
  def extract_names([{name, _age} | rest]) do
    [name | extract_names(rest)]
  end
  
  # Pattern matching con guards
  def filter_adults([]), do: []
  def filter_adults([{name, age} | rest]) when age >= 18 do
    [name | filter_adults(rest)]
  end
  def filter_adults([_minor | rest]) do
    filter_adults(rest)
  end
  
  # Separar pares e impares
  def separate_even_odd(list), do: separate_even_odd(list, [], [])
  defp separate_even_odd([], evens, odds) do
    {Enum.reverse(evens), Enum.reverse(odds)}
  end
  defp separate_even_odd([head | tail], evens, odds) when rem(head, 2) == 0 do
    separate_even_odd(tail, [head | evens], odds)
  end
  defp separate_even_odd([head | tail], evens, odds) do
    separate_even_odd(tail, evens, [head | odds])
  end
end

# Ejemplos
people = [{"Juan", 25}, {"Ana", 17}, {"Luis", 30}]
AdvancedListPatterns.extract_names(people)
# ["Juan", "Ana", "Luis"]

AdvancedListPatterns.filter_adults(people)
# ["Juan", "Luis"]

AdvancedListPatterns.separate_even_odd([1, 2, 3, 4, 5, 6])
# {[2, 4, 6], [1, 3, 5]}
```

---

## Listas Anidadas

```elixir
defmodule NestedLists do
  # Aplanar un nivel
  def flatten_one_level([]), do: []
  def flatten_one_level([head | tail]) when is_list(head) do
    head ++ flatten_one_level(tail)
  end
  def flatten_one_level([head | tail]) do
    [head | flatten_one_level(tail)]
  end
  
  # Transponer matriz
  def transpose([[] | _]), do: []
  def transpose(matrix) do
    [Enum.map(matrix, &hd/1) | transpose(Enum.map(matrix, &tl/1))]
  end
end

# Ejemplos
nested = [[1, 2], [3, 4], [5]]
NestedLists.flatten_one_level(nested)
# [1, 2, 3, 4, 5]

matrix = [[1, 2, 3], [4, 5, 6]]
NestedLists.transpose(matrix)
# [[1, 4], [2, 5], [3, 6]]
```

**Conceptos clave de recursión**:

- **Caso base**: Condición que detiene la recursión (lista vacía)
- **Caso recursivo**: Procesa head y llama recursivamente con tail
- **Acumuladores**: Optimizan la recursión (tail call optimization)