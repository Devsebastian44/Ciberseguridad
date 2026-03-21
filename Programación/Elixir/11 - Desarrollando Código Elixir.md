## Estructura de Proyecto Elixir

```
proyecto/ 
├── lib/ 
│ └── mi_modulo.ex 
├── test/ 
│ └── mi_modulo_test.exs 
  └── mix.exs
````

---

## Ejemplo: Juego de Adivinanzas

```elixir
defmodule GuessingGame do
  @moduledoc """
  Juego simple de adivinanzas entre 1 y 100.
  """

  def start do
    secret_number = :rand.uniform(100)
    IO.puts("¡Bienvenido! He pensado un número entre 1 y 100.")
    play_game(secret_number)
  end

  def play_game(secret_number) do
    guess = get_guess()
    
    case compare_guess(guess, secret_number) do
      :correct ->
        IO.puts("¡Correcto! Has adivinado.")
      :too_high ->
        IO.puts("Muy alto. Intenta de nuevo.")
        play_game(secret_number)
      :too_low ->
        IO.puts("Muy bajo. Intenta de nuevo.")
        play_game(secret_number)
    end
  end

  defp get_guess do
    IO.gets("Ingresa tu adivinanza: ")
    |> String.trim()
    |> parse_guess()
  end

  defp parse_guess(input) do
    case Integer.parse(input) do
      {number, ""} when number >= 1 and number <= 100 ->
        number
      _ ->
        IO.puts("Número inválido. Intenta de nuevo.")
        get_guess()
    end
  end

  defp compare_guess(guess, secret) do
    cond do
      guess == secret -> :correct
      guess > secret -> :too_high
      guess < secret -> :too_low
    end
  end
end
````

---

## Testing con ExUnit

```elixir
# test/guessing_game_test.exs
defmodule GuessingGameTest do
  use ExUnit.Case
  doctest GuessingGame

  describe "compare_guess/2" do
    test "retorna :correct cuando acierta" do
      assert GuessingGame.compare_guess(50, 50) == :correct
    end

    test "retorna :too_high cuando es muy alto" do
      assert GuessingGame.compare_guess(75, 50) == :too_high
    end

    test "retorna :too_low cuando es muy bajo" do
      assert GuessingGame.compare_guess(25, 50) == :too_low
    end
  end
end
```

**Ejecutar tests:**

```bash
mix test                 # Todos los tests
mix test --verbose       # Con detalles
mix test --cover         # Con coverage
```

---

## Refactorización con Protocolos

```elixir
# Protocolo para extensibilidad
defprotocol FileAnalyzer do
  def analyze(analyzer, content)
end

# Implementación para texto
defmodule TextAnalyzer do
  defstruct []
  
  defimpl FileAnalyzer do
    def analyze(_analyzer, content) do
      %{
        type: :text,
        lines: String.split(content, "\n") |> length(),
        words: String.split(content, ~r/\s+/, trim: true) |> length(),
        characters: String.length(content)
      }
    end
  end
end

# Implementación para CSV
defmodule CSVAnalyzer do
  defstruct []
  
  defimpl FileAnalyzer do
    def analyze(_analyzer, content) do
      rows = String.split(content, "\n", trim: true)
      
      %{
        type: :csv,
        rows: length(rows),
        headers: parse_headers(List.first(rows, ""))
      }
    end
  end
  
  defp parse_headers(header_row) do
    header_row |> String.split(",") |> Enum.map(&String.trim/1)
  end
end

# Uso
def analyze_file(content, :text) do
  FileAnalyzer.analyze(%TextAnalyzer{}, content)
end

def analyze_file(content, :csv) do
  FileAnalyzer.analyze(%CSVAnalyzer{}, content)
end
```

**Ventajas de protocolos:**

- **Extensibilidad**: Fácil agregar nuevos tipos
- **Separación**: Cada analizador es independiente
- **Polimorfismo**: Comportamiento específico por tipo

---

## Comandos Mix Esenciales

```bash
# Crear proyecto
mix new mi_proyecto

# Gestión de dependencias
mix deps.get              # Instalar dependencias
mix deps.update --all     # Actualizar todas

# Compilación
mix compile               # Compilar proyecto
mix clean                 # Limpiar build

# Testing
mix test                  # Ejecutar tests
mix test --cover          # Con coverage
mix test test/archivo_test.exs:10  # Test específico

# Formateo y análisis
mix format                # Formatear código
mix credo                 # Análisis estático

# Documentación
mix docs                  # Generar documentación

# Ejecución
mix run                   # Ejecutar aplicación
iex -S mix                # IEx con proyecto cargado
```

---

## Setup de Tests

```elixir
defmodule FileProcessorTest do
  use ExUnit.Case

  @test_data_dir "test/fixtures"

  setup_all do
    File.mkdir_p!(@test_data_dir)
    
    # Crear archivos de prueba
    File.write!("#{@test_data_dir}/sample.txt", "Contenido de prueba")
    
    on_exit(fn ->
      File.rm_rf!(@test_data_dir)
    end)

    :ok
  end

  test "procesa archivo correctamente" do
    result = FileProcessor.process_file("#{@test_data_dir}/sample.txt")
    assert result.type == :text
  end
end
```

**Hooks importantes:**

- **`setup`**: Se ejecuta antes de cada test
- **`setup_all`**: Se ejecuta una vez antes de todos los tests
- **`on_exit`**: Cleanup después de los tests

---

## Buenas Prácticas

### Organización de Código

- Un módulo por archivo
- Funciones públicas primero, privadas después
- Documentación con `@moduledoc` y `@doc`

### Testing

- Un archivo de test por módulo
- Usar `describe` para agrupar tests relacionados
- Tests descriptivos y claros

### Refactorización

- Separar responsabilidades
- Usar protocolos para polimorfismo
- Funciones pequeñas y enfocadas