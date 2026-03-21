## ¿Qué es Elixir?

Elixir es un **lenguaje de programación dinámico y funcional** diseñado para crear aplicaciones **mantenibles y escalables**. Fue creado por José Valim en 2011 y se ejecuta sobre la **máquina virtual de Erlang (BEAM)**.

### Características Principales

- **Concurrencia**: Elixir utiliza el modelo de actores de Erlang, permitiendo miles de procesos ligeros
- **Tolerancia a fallos**: Filosofía "let it crash" con supervisión de procesos
- **Inmutabilidad**: Los datos son inmutables por defecto
- **Pattern matching**: Potente sistema de coincidencia de patrones
- **Programación funcional**: Paradigma funcional con funciones de primera clase

### Ventajas de Elixir

- **Alto rendimiento** y escalabilidad
- Excelente para **sistemas distribuidos**
- Sintaxis **limpia y expresiva**
- **Comunidad activa** y ecosistema robusto
- **Herramientas de desarrollo** excepcionales

---

## Instalación de Elixir en Linux

### Método 1: Usando el Gestor de Paquetes del Sistema

#### Ubuntu/Debian

```bash
# Actualizar repositorios
sudo apt update

# Instalar Elixir
sudo apt install elixir

# Verificar instalación
elixir --version
````

#### CentOS/RHEL/Fedora

```bash
# Fedora
sudo dnf install elixir

# CentOS/RHEL (requiere EPEL)
sudo yum install epel-release
sudo yum install elixir

# Verificar instalación
elixir --version
```

---

### Método 2: Usando ASDF (Recomendado para desarrollo)

**ASDF** es un gestor de versiones que permite manejar **múltiples versiones** de Elixir.

```bash
# Instalar ASDF
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.10.2

# Agregar a shell (bash)
echo '. $HOME/.asdf/asdf.sh' >> ~/.bashrc
echo '. $HOME/.asdf/completions/asdf.bash' >> ~/.bashrc

# Recargar shell
source ~/.bashrc

# Agregar plugin de Erlang y Elixir
asdf plugin add erlang
asdf plugin add elixir

# Instalar Erlang (prerequisito)
asdf install erlang latest

# Instalar Elixir
asdf install elixir latest

# Establecer versiones globales
asdf global erlang [version]
asdf global elixir [version]
```

**Ventajas de ASDF:**

- Gestiona **múltiples versiones** de Elixir y Erlang
- Cambio fácil entre versiones por proyecto
- Instalación **aislada** del sistema

---

### Método 3: Compilación desde Código Fuente

```bash
# Dependencias necesarias
sudo apt install build-essential git

# Clonar repositorio
git clone https://github.com/elixir-lang/elixir.git
cd elixir

# Compilar
make clean test

# Agregar al PATH
export PATH="$PWD/bin:$PATH"
```

---

## Verificación de Instalación

```bash
# Verificar versiones
elixir --version
iex --version

# Iniciar shell interactivo
iex
```

**Herramientas incluidas:**

- **`elixir`**: Ejecuta scripts de Elixir
- **`iex`**: Shell interactivo (Interactive Elixir)
- **`mix`**: Herramienta de construcción y gestión de proyectos