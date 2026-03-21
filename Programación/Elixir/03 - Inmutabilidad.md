## Inmutabilidad en Elixir

En Elixir, todos los datos son **inmutables** por defecto. Esto significa que una vez que se crea un valor, **no puede ser modificado**. En su lugar, se crean nuevos valores.

### Conceptos Clave

```elixir
# Las variables pueden ser "reasignadas", pero los valores no cambian
list = [1, 2, 3]
new_list = [0 | list]  # Crea una nueva lista
# list sigue siendo [1, 2, 3]
# new_list es [0, 1, 2, 3]

# Con maps
person = %{name: "Juan", age: 30}
older_person = %{person | age: 31}  # Crea un nuevo map
# person sigue siendo %{name: "Juan", age: 30}
# older_person es %{name: "Juan", age: 31}
````

### Ejemplo con Listas

```elixir
original = [1, 2, 3]

# Estas operaciones NO modifican la lista original
prepended = [0 | original]     # [0, 1, 2, 3]
appended = original ++ [4]     # [1, 2, 3, 4]
reversed = Enum.reverse(original)  # [3, 2, 1]

# original sigue siendo [1, 2, 3]
IO.inspect(original)  # [1, 2, 3]
```

### Ejemplo con Maps

```elixir
user = %{name: "Ana", email: "ana@example.com", age: 25}

# Actualizar campos crea un nuevo map
updated_user = %{user | age: 26, email: "ana.nueva@example.com"}

# El map original no cambia
IO.inspect(user)         # %{name: "Ana", email: "ana@example.com", age: 25}
IO.inspect(updated_user) # %{name: "Ana", email: "ana.nueva@example.com", age: 26}
```

---

## Implicaciones de Inmutabilidad en Performance

### Ventajas de Rendimiento

#### 1. Compartición Estructural

```elixir
# Elixir comparte memoria entre estructuras similares
original = [1, 2, 3, 4, 5]
new_list = [0 | original]
# new_list reutiliza la memoria de original, solo agrega el nuevo elemento
```

**Ventaja**: No se copia toda la estructura, solo se agregan referencias a los elementos existentes.

#### 2. Garbage Collection Eficiente

```elixir
# Al no haber referencias mutables, el GC es más eficiente
defmodule ProcessData do
  def process_large_list(list) do
    list
    |> Enum.map(&(&1 * 2))
    |> Enum.filter(&(&1 > 10))
    |> Enum.sum()
  end
  # Las listas intermedias pueden ser liberadas rápidamente
end
```

#### 3. Concurrencia Segura

```elixir
# Los datos pueden ser compartidos entre procesos sin locks
defmodule SharedData do
  def start_processes(data) do
    # Múltiples procesos pueden acceder al mismo data sin problemas
    Enum.map(1..10, fn i ->
      spawn(fn -> 
        IO.puts("Proceso #{i}: #{inspect(data)}")
      end)
    end)
  end
end
```

**Ventaja clave**: Sin **race conditions** ni necesidad de **locks** o **mutexes**.

---

### Consideraciones de Rendimiento

#### 1. Copias Costosas

```elixir
# Operaciones que requieren copiar toda la estructura son costosas
large_map = Enum.into(1..1000, %{}, fn i -> {i, i * 2} end)

# Esto es costoso porque crea una nueva estructura completa
updated_map = Map.put(large_map, :new_key, :new_value)
```

#### 2. Optimizaciones Recomendadas

```elixir
defmodule OptimizedOperations do
  # Mejor: usar Enum.reduce para acumular
  def sum_squares(numbers) do
    Enum.reduce(numbers, 0, fn x, acc -> acc + x * x end)
  end
  
  # Evitar: crear listas intermedias innecesarias
  def sum_squares_inefficient(numbers) do
    numbers
    |> Enum.map(&(&1 * &1))  # Crea lista intermedia
    |> Enum.sum()
  end
end
```

**Recomendación**: Usar **`Enum.reduce`** cuando sea posible para evitar crear estructuras intermedias.

#### 3. Uso de Streams para Datos Grandes

```elixir
# Stream para procesamiento lazy
1..1_000_000
|> Stream.map(&(&1 * 2))
|> Stream.filter(&(&1 > 100))
|> Enum.take(10)
# Solo procesa los elementos necesarios
```

**Ventaja de Streams**: **Evaluación perezosa** (lazy evaluation) que procesa solo los elementos necesarios, ahorrando memoria y tiempo.