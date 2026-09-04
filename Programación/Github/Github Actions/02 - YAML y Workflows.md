# YAML y Workflows

## ¿Qué es YAML?

**YAML** significa *YAML Ain’t Markup Language*  
Es un lenguaje de serialización de datos, usado para escribir archivos de configuración.

### Comparación YAML vs JSON
| Característica  | YAML                             | JSON                 |
| --------------- | -------------------------------- | -------------------- |
| **Sintaxis**    | Legible, menos símbolos          | Estricta, con llaves |
| **Comentarios** | Sí (`#`)                         | No                   |
| **Tamaño**      | Compacto                         | Verboso              |
| **Parsing**     | Complejo                         | Fácil                |
| **Uso común**   | Configs (GitHub Actions, Docker) | APIs, JavaScript     |
### Características de YAML

1. **Formato clave-valor**  
2. **Indentación con espacios** (no tabs)  
3. **Tipos de datos**: strings, números, booleanos, null.  
4. **Texto multilínea**: Usa `|` (preserva saltos) o `>` (une líneas).

### Herramientas que usan YAML

- GitHub Actions
- Docker Compose
- Kubernetes
- Ansible

### Ejemplos

Tipos primitivos:

```yaml
ciudad: Madrid
edad: 25
activo: true  
descripcion: null
```

Listas:

```yaml
colores:
  - rojo
  - verde
  - azul
```

Mapas/Diccionarios:

```yaml
persona:
  nombre: Juan
  edad: 30
```

Lista de Valores:

```yaml
usuarios:
  - nombre: Ana
    edad: 30
  - nombre: Luis
    edad: 25
```

Modificadores string multimedia:

```yaml
mensaje: |
  Hola ,
  Esto es un texto multilínea,
```

```yaml
texto: >
  Esta es una línea
  que continuará en la siguiente
```

Herencia (anchors):

```yaml
defaults: &defaults
  color: blue
  size: medium

item1:
  <<: *defaults
  color: red  # Sobrescribe color

item2:
  <<: *defaults
  size: small  # Sobrescribe size

# item1 hereda de defaults y sobrescribe el color
```

### Ejemplo práctico: Docker Compose

```yaml
version: '3.8'
services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - .:/var/www/html
  php:
    image: php:8.2-fpm
    volumes:
      - .:/var/www/html
```

### Ejemplo completo:

```yaml
name: CI
on:
    push:
    branches: [ main ]
jobs:
    build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout repository to
    uses: actions/checkout@v3
    - name: Configurar Node.js
    uses: actions/setup-node@v3
    with:
    node-version: '18'
```