## Tipos de Shell

```bash
echo $SHELL          # Ver shell predeterminado
cat /etc/shells      # Ver todos los shells disponibles

bash                 # Cambiar temporalmente a bash
zsh                  # Cambiar temporalmente a zsh
fish                 # Cambiar temporalmente a fish

chsh -s /bin/bash    # Cambiar shell predeterminado
chsh -s /bin/zsh
```

---

## Configuración de Bash

### Archivos de configuración

```bash
~/.bashrc         # Configuración para sesiones interactivas
~/.bash_profile   # Configuración para sesiones de login
~/.bash_aliases   # Alias personalizados
~/.bash_history   # Historial de comandos

ls -alps | grep .bash
ls -la ~/.*bash*
```

---

### Gestión del historial

```bash
history                     # Ver historial
history | tail -20          # Últimos 20 comandos
history | grep "comando"    # Buscar en historial

history -c                  # Limpiar historial de sesión
cat /dev/null > ~/.bash_history  # Limpiar archivo de historial

export HISTSIZE=1000        # Comandos en memoria
export HISTFILESIZE=2000    # Comandos en archivo
export HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S "  # Timestamp
```

---

### Personalización del prompt

```bash
echo $PS1   # Prompt principal
echo $PS2   # Prompt secundario

# Ejemplos de personalización
PS1='\u@\h:\w\$ '  
PS1='\[\e[32m\]\u@\h\[\e[0m\]:\[\e[34m\]\w\[\e[0m\]\$ '  # Con colores
```

---

### Alias y funciones

```bash
alias ll='ls -la'
alias grep='grep --color=auto'
alias la='ls -la'
alias ..='cd ..'

alias                        # Ver alias existentes

# Alias permanentes
echo "alias ll='ls -la'" >> ~/.bashrc
echo "alias grep='grep --color=auto'" >> ~/.bashrc

# Función personalizada
function mkcd() {
    mkdir -p "$1" && cd "$1"
}

echo "function mkcd() { mkdir -p \"\$1\" && cd \"\$1\"; }" >> ~/.bashrc
```

---

### Variables de entorno

```bash
env
printenv
echo $PATH
echo $HOME
echo $USER

export MI_VARIABLE="valor"
export PATH=$PATH:/nueva/ruta

echo 'export MI_VARIABLE="valor"' >> ~/.bashrc
echo 'export PATH=$PATH:/nueva/ruta' >> ~/.bashrc

source ~/.bashrc   # Recargar configuración
```

---
