## Diccionarios de Contraseñas

### ¿Qué son?

Los **diccionarios de contraseñas** son listas compiladas de contraseñas comunes, palabras del diccionario y patrones utilizados en ataques de fuerza bruta y diccionario.

---

### Usos Principales

- **Auditorías de seguridad:** evaluar la fortaleza de contraseñas organizacionales
- **Pentesting:** identificar vulnerabilidades en sistemas de autenticación
- **Educación:** demostrar la importancia de contraseñas seguras

---

## Tipos de Diccionarios

### Diccionarios Base

- Palabras del diccionario en diferentes idiomas
- Nombres propios (personas, lugares, marcas)
- Fechas significativas (años, cumpleaños, aniversarios)

---

### Diccionarios Especializados

- Contraseñas filtradas en brechas de seguridad
- Patrones específicos de dominios particulares
- Variaciones comunes: `@` por `a`, `3` por `e`, `1` por `i`, `0` por `o`, `$` por `s`

---

## Herramientas para Crear Diccionarios

### CeWL (Custom Word List Generator)

**Instalación:**

```bash
sudo apt install cewl
```

**Uso básico:**

```bash
cewl -w diccionario.txt -d 2 -m 5 https://ejemplo.com
```

**Parámetros:**

- `-w` : Archivo de salida
- `-d` : Profundidad de crawling
- `-m` : Longitud mínima de palabra
- `-e` : Incluir direcciones de email

**Ejemplo avanzado:**

```bash
cewl -w empresa.txt -d 3 -m 6 --with-numbers -e https://empresa.com
```

---

### Crunch

**Instalación:**

```bash
sudo apt install crunch
```

**Sintaxis:**

```bash
crunch [min] [max] [caracteres] [opciones]
```

**Ejemplos:**

```bash
# Contraseñas de 8 caracteres
crunch 8 8 -o passwords.txt

# Patrón: 5 letras + 3 números
crunch 8 8 -t ,,,,,@@@ -o diccionario.txt

# Símbolos de patrón:
# , = letras minúsculas
# @ = números
# % = símbolos especiales
# ^ = letras mayúsculas

# Conjunto personalizado
crunch 6 10 abcdefghijklmnopqrstuvwxyz0123456789 -o passwords.txt
```

---

## Técnicas de Generación

### Mutaciones de Palabras

```python
def generar_mutaciones(palabra):
    mutaciones = []
    
    # Sustituciones leetspeak
    sustituciones = {'a': '@', 'e': '3', 'i': '1', 'o': '0', 's': '$'}
    for original, nuevo in sustituciones.items():
        mutaciones.append(palabra.replace(original, nuevo))
    
    # Números al final
    for i in range(100):
        mutaciones.append(palabra + str(i))
    
    return mutaciones
```

---

### Combinación de Palabras

```python
def combinar_palabras(lista1, lista2, separadores=['', '-', '_']):
    combinaciones = []
    for palabra1 in lista1:
        for palabra2 in lista2:
            for sep in separadores:
                combinaciones.append(f"{palabra1}{sep}{palabra2}")
    return combinaciones
```

---

## Optimización de Diccionarios

### Eliminar Duplicados

```bash
sort -u diccionario.txt -o diccionario_limpio.txt
```

---

### Filtrar por Criterios

**Por longitud:**

```bash
awk 'length($0) >= 8 && length($0) <= 16' diccionario.txt > filtrado.txt
```

**Por complejidad:**

```bash
grep -E '^(?=.*[0-9])(?=.*[a-zA-Z]).+$' diccionario.txt > complejas.txt
```

---

### Fusionar Diccionarios

```bash
cat dict1.txt dict2.txt dict3.txt | sort -u > diccionario_maestro.txt
```

---

## Mejores Prácticas

### Creación de Diccionarios

- Usar **CeWL** para generar diccionarios del objetivo
- Incluir **terminología** de la industria
- Aplicar **mutaciones inteligentes**
- Eliminar **duplicados** regularmente

---

### Uso Responsable

**Consideraciones éticas:**

- **Solo** usar en auditorías autorizadas
- Obtener **permiso por escrito**
- **No distribuir** contraseñas reales
- Seguir **disclosure responsable**

---