## Convención de nomenclatura

Las constantes se definen usando **MAYÚSCULAS** y palabras separadas por guiones bajos.

### Ejemplos

```python
PI = 3.14159
MENSAJE_ERROR = 'Se ha producido un error'
NOMBRE_USUARIO_VALIDO = 'admin'
NOMBRE_BASE_DATOS = 'Clientes_DB'
```

---

## Implementación

```python
import math

PI = 3.14159
MENSAJE_ERROR = 'Se ha producido un error'
NOMBRE_USUARIO_VALIDO = 'admin'
NOMBRE_BASE_DATOS = 'Clientes_DB'

print(f'El valor de PI es: {PI}')
print(f'Mensaje de error: {MENSAJE_ERROR}')
print(f'Nombre usuario válido: {NOMBRE_USUARIO_VALIDO}')
print(f'Nombre de la base de datos: {NOMBRE_BASE_DATOS}')

# Modificación (no recomendada)
NOMBRE_BASE_DATOS = 'Listado_Clientes_DB'
print(f'Nuevo valor de la constante (no recomendado): {NOMBRE_BASE_DATOS}')

# Constante del módulo math
print(f'Constante PI del módulo math: {math.pi}')
```

---

## Conceptos clave

- Convención: **MAYÚSCULAS + guiones bajos**
- Python permite modificar constantes, aunque no es recomendable
- `math.pi` ofrece mayor precisión que una constante definida manualmente

---

## Resultado esperado

```
El valor de PI es: 3.14159
Mensaje de error: Se ha producido un error
Nombre usuario válido: admin
Nombre de la base de datos: Clientes_DB
Nuevo valor de la constante (no recomendado): Listado_Clientes_DB
Constante PI del módulo math: 3.141592653589793
```

---