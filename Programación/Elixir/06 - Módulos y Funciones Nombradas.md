## Llamada de Funciones

```elixir
defmodule Calculator do
  # Función pública
  def add(a, b), do: a + b
  
  # Función con múltiples cláusulas
  def divide(a, 0), do: {:error, "Division by zero"}
  def divide(a, b), do: {:ok, a / b}
  
  # Función privada
  defp multiply_by_two(x), do: x * 2
end

# Llamadas
Calculator.add(5, 3)           # 8

# Con pipe operator
result = 5
|> Calculator.multiply(3)
|> Calculator.add(2)
````

---

## Guard Clauses

Las **guard clauses** permiten añadir **condiciones adicionales** a las funciones.

```elixir
defmodule NumberChecker do
  def check(x) when is_integer(x) and x > 0 do
    "Positive integer: #{x}"
  end
  
  def check(x) when is_integer(x) and x < 0 do
    "Negative integer: #{x}"
  end
  
  def check(x) when is_float(x) do
    "Float: #{x}"
  end
  
  def check(_) do
    "Unknown type"
  end
end
```

### Expresiones Permitidas en Guards

```elixir
# ✅ Comparaciones
def compare(x) when x > 10, do: "greater than 10"

# ✅ Operadores lógicos
def logical(x) when x > 0 and x < 100, do: "between 0 and 100"

# ✅ Funciones type-checking
def type_check(x) when is_atom(x), do: "atom"
def type_check(x) when is_list(x), do: "list"

# ✅ Funciones matemáticas básicas
def math_ops(x) when rem(x, 2) == 0, do: "even number"

# ❌ NO permitido: funciones personalizadas
# def custom_check(x) when my_function(x), do: "valid"
```

---

## Parámetros por Default

```elixir
defmodule DefaultParams do
  # Parámetros por defecto
  def greet(name, greeting \\ "Hello") do
    "#{greeting}, #{name}!"
  end
  
  # Múltiples parámetros por defecto
  def create_user(name, age \\ 25, role \\ :user, active \\ true) do
    %{name: name, age: age, role: role, active: active}
  end
end

# Uso
DefaultParams.greet("Ana")                # "Hello, Ana!"
DefaultParams.greet("Ana", "Hi")          # "Hi, Ana!"
DefaultParams.create_user("Juan")         # Usa todos los defaults
DefaultParams.create_user("Juan", 30)     # Sobrescribe solo age
```

---

## Funciones Privadas

Las funciones privadas solo pueden ser llamadas **desde dentro del mismo módulo**.

```elixir
defmodule BankAccount do
  # Función pública
  def create_account(initial_balance) when initial_balance >= 0 do
    %{
      id: generate_account_id(),
      balance: initial_balance,
      transactions: []
    }
  end
  
  def withdraw(account, amount) when amount > 0 do
    if can_withdraw?(account, amount) do
      new_balance = account.balance - amount
      {:ok, %{account | balance: new_balance}}
    else
      {:error, "Insufficient funds"}
    end
  end
  
  # Funciones privadas (defp)
  defp generate_account_id do
    :crypto.strong_rand_bytes(8) |> Base.encode16()
  end
  
  defp can_withdraw?(account, amount) do
    account.balance >= amount
  end
end

# ❌ Esto no funciona
# BankAccount.generate_account_id()  # Error: undefined function
```

---

## Operador Pipe (`|>`)

El operador pipe permite **encadenar llamadas a funciones** de manera legible.

```elixir
# ❌ Sin pipe (difícil de leer)
result = String.trim(String.downcase(String.reverse("  HELLO  ")))

# ✅ Con pipe (legible de arriba a abajo)
result = "  HELLO  "
|> String.reverse()
|> String.downcase()
|> String.trim()
```

### Ejemplos Prácticos

```elixir
defmodule DataProcessor do
  def process_users(users) do
    users
    |> Enum.filter(&(&1.active))
    |> Enum.map(&normalize_user/1)
    |> Enum.sort_by(&(&1.name))
    |> Enum.take(10)
  end
  
  def process_text(text) do
    text
    |> String.trim()
    |> String.downcase()
    |> String.split()
    |> Enum.map(&String.capitalize/1)
    |> Enum.join(" ")
  end
end
```

---

## Módulos

Los módulos son la **unidad básica de organización** de código en Elixir.

```elixir
defmodule Calculator do
  @moduledoc """
  Un módulo para operaciones matemáticas básicas.
  """
  
  # Atributos como constantes
  @default_timeout 5000
  @max_retries 3
  
  @doc """
  Suma dos números.
  
  ## Ejemplos
  
      iex> Calculator.add(2, 3)
      5
  """
  def add(a, b) when is_number(a) and is_number(b) do
    a + b
  end
end
```

### Atributos de Módulo

```elixir
defmodule Configuration do
  @default_timeout 5000
  @max_retries 3
  @supported_formats ["json", "xml", "csv"]
  
  def get_timeout, do: @default_timeout
  
  # Usar atributos en guards
  def valid_format?(format) when format in @supported_formats do
    true
  end
  def valid_format?(_), do: false
end
```

### Importación y Aliases

```elixir
defmodule DataAnalyzer do
  # Alias para módulos largos
  alias MyApp.DataProcessor, as: Processor
  alias MyApp.Utils.{FileHelper, DateHelper}
  
  # Importar funciones específicas
  import Enum, only: [map: 2, filter: 2]
  
  def analyze_data(raw_data) do
    raw_data
    |> Processor.clean_data()
    |> map(&transform_item/1)       # Sin prefijo Enum
    |> filter(&valid_item?/1)
  end
end
```

**Diferencias clave:**

- **`alias`**: Acorta nombres de módulos
- **`import`**: Permite usar funciones sin prefijo del módulo
- **`use`**: Inyecta código del módulo (macros)