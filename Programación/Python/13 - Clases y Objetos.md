## Clases y Objetos en Python

La programación orientada a objetos (POO) utiliza "objetos" y sus interacciones para diseñar aplicaciones. Python soporta completamente la POO, permitiendo crear clases que sirven como plantillas para crear objetos.

---

## Definir una clase

Una clase es una plantilla para crear objetos. Se define usando la palabra clave `class`.

```python
class Persona:
    pass

# Crear un objeto (instancia)
persona1 = Persona()
print(persona1)  # <__main__.Persona object at 0x...>
```

---

## Método **init** (Constructor)

El método `__init__` es el constructor de la clase. Se ejecuta automáticamente cuando se crea una nueva instancia.

```python
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad

persona1 = Persona("Juan", 30)
print(persona1.nombre)  # Juan
print(persona1.edad)    # 30
```

---

## El parámetro self

`self` representa la instancia de la clase y se utiliza para acceder a los atributos y métodos.

```python
class Persona:
    def __init__(self, nombre):
        self.nombre = nombre
    
    def saludar(self):
        print(f"Hola, mi nombre es {self.nombre}")

persona1 = Persona("María")
persona1.saludar()  # Hola, mi nombre es María
```

---

## Atributos

### Atributos de instancia

Variables que pertenecen a cada objeto individual.

```python
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad

persona1 = Persona("Juan", 30)
persona2 = Persona("María", 25)

print(persona1.nombre)  # Juan
print(persona2.nombre)  # María
```

### Atributos de clase

Variables que pertenecen a la clase y son compartidas por todas las instancias.

```python
class Persona:
    especie = "Humano"  # Atributo de clase

persona1 = Persona()
persona2 = Persona()

print(persona1.especie)  # Humano
print(persona2.especie)  # Humano
```

---

## Métodos de instancia

Funciones definidas dentro de una clase que operan sobre los atributos de la instancia.

```python
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad
    
    def presentarse(self):
        print(f"Hola, soy {self.nombre} y tengo {self.edad} años")
    
    def cumplir_años(self):
        self.edad += 1
        print(f"¡Feliz cumpleaños! Ahora tengo {self.edad} años")

persona1 = Persona("Juan", 30)
persona1.presentarse()     # Hola, soy Juan y tengo 30 años
persona1.cumplir_años()    # ¡Feliz cumpleaños! Ahora tengo 31 años
```

### Métodos con retorno

```python
class Rectangulo:
    def __init__(self, base, altura):
        self.base = base
        self.altura = altura
    
    def calcular_area(self):
        return self.base * self.altura
    
    def calcular_perimetro(self):
        return 2 * (self.base + self.altura)

rectangulo = Rectangulo(5, 10)
print(f"Área: {rectangulo.calcular_area()}")           # Área: 50
print(f"Perímetro: {rectangulo.calcular_perimetro()}") # Perímetro: 30
```

---

## Modificar atributos

### Modificación directa

```python
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad

persona1 = Persona("Juan", 30)
persona1.edad = 31
print(persona1.edad)  # 31
```

### Modificación mediante métodos

```python
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad
    
    def cambiar_edad(self, nueva_edad):
        self.edad = nueva_edad

persona1 = Persona("Juan", 30)
persona1.cambiar_edad(35)
print(persona1.edad)  # 35
```

---

## Encapsulamiento

El encapsulamiento oculta los detalles internos de una clase. Los atributos privados se definen con doble guion bajo `__`.

```python
class CuentaBancaria:
    def __init__(self, titular, saldo):
        self.titular = titular
        self.__saldo = saldo  # Atributo privado
    
    def depositar(self, cantidad):
        if cantidad > 0:
            self.__saldo += cantidad
            print(f"Depósito exitoso. Nuevo saldo: {self.__saldo}")
    
    def retirar(self, cantidad):
        if cantidad > 0 and cantidad <= self.__saldo:
            self.__saldo -= cantidad
            print(f"Retiro exitoso. Nuevo saldo: {self.__saldo}")
        else:
            print("Fondos insuficientes")
    
    def consultar_saldo(self):
        return self.__saldo

cuenta = CuentaBancaria("Juan", 1000)
cuenta.depositar(500)        # Depósito exitoso. Nuevo saldo: 1500
cuenta.retirar(200)          # Retiro exitoso. Nuevo saldo: 1300
print(cuenta.consultar_saldo())  # 1300
# print(cuenta.__saldo)      # Error: AttributeError
```

---

## Herencia

La herencia permite crear una nueva clase basada en una clase existente.

```python
class Animal:
    def __init__(self, nombre):
        self.nombre = nombre
    
    def hacer_sonido(self):
        print("El animal hace un sonido")

class Perro(Animal):
    def hacer_sonido(self):
        print(f"{self.nombre} dice: ¡Guau!")

class Gato(Animal):
    def hacer_sonido(self):
        print(f"{self.nombre} dice: ¡Miau!")

perro = Perro("Firulais")
gato = Gato("Michi")

perro.hacer_sonido()  # Firulais dice: ¡Guau!
gato.hacer_sonido()   # Michi dice: ¡Miau!
```

### Herencia con super()

`super()` permite llamar métodos de la clase padre desde la clase hija.

```python
class Vehiculo:
    def __init__(self, marca, modelo):
        self.marca = marca
        self.modelo = modelo
    
    def describir(self):
        print(f"Vehículo: {self.marca} {self.modelo}")

class Coche(Vehiculo):
    def __init__(self, marca, modelo, puertas):
        super().__init__(marca, modelo)
        self.puertas = puertas
    
    def describir(self):
        super().describir()
        print(f"Número de puertas: {self.puertas}")

coche = Coche("Toyota", "Corolla", 4)
coche.describir()
# Vehículo: Toyota Corolla
# Número de puertas: 4
```

---

## Sobreescritura de métodos (Override)

La sobreescritura permite que una clase hija redefina un método de la clase padre.

```python
class Animal:
    def hacer_sonido(self):
        return "Algún sonido"

class Perro(Animal):
    def hacer_sonido(self):  # Sobreescribe el método del padre
        return "¡Guau!"

class Gato(Animal):
    def hacer_sonido(self):  # Sobreescribe el método del padre
        return "¡Miau!"

animal = Animal()
perro = Perro()
gato = Gato()

print(animal.hacer_sonido())  # Algún sonido
print(perro.hacer_sonido())   # ¡Guau!
print(gato.hacer_sonido())    # ¡Miau!
```

---

## Polimorfismo

El polimorfismo permite que objetos de diferentes clases respondan al mismo método de diferentes maneras.

```python
class Perro:
    def hacer_sonido(self):
        return "¡Guau!"

class Gato:
    def hacer_sonido(self):
        return "¡Miau!"

class Vaca:
    def hacer_sonido(self):
        return "¡Muuu!"

def animal_habla(animal):
    print(animal.hacer_sonido())

perro = Perro()
gato = Gato()
vaca = Vaca()

animal_habla(perro)  # ¡Guau!
animal_habla(gato)   # ¡Miau!
animal_habla(vaca)   # ¡Muuu!
```

---

## Duck Typing

"Si camina como un pato y grazna como un pato, entonces es un pato". Python verifica si un objeto tiene los métodos necesarios, no su tipo.

```python
class Archivo:
    def leer(self):
        return "Contenido del archivo"

class BaseDatos:
    def leer(self):
        return "Datos de la base de datos"

class API:
    def leer(self):
        return "Datos de la API"

def procesar_datos(fuente):
    datos = fuente.leer()
    print(f"Procesando: {datos}")

archivo = Archivo()
bd = BaseDatos()
api = API()

procesar_datos(archivo)  # Procesando: Contenido del archivo
procesar_datos(bd)       # Procesando: Datos de la base de datos
procesar_datos(api)      # Procesando: Datos de la API
```

---

## Métodos especiales (Dunder methods)

Métodos con nombres que comienzan y terminan con doble guion bajo.

### **str** y **repr**

```python
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad
    
    def __str__(self):
        return f"Persona: {self.nombre}, {self.edad} años"
    
    def __repr__(self):
        return f"Persona('{self.nombre}', {self.edad})"

persona = Persona("Juan", 30)
print(persona)        # Persona: Juan, 30 años
print(repr(persona))  # Persona('Juan', 30)
```

### Operadores matemáticos

```python
class Numero:
    def __init__(self, valor):
        self.valor = valor
    
    def __add__(self, otro):
        return Numero(self.valor + otro.valor)
    
    def __sub__(self, otro):
        return Numero(self.valor - otro.valor)
    
    def __str__(self):
        return str(self.valor)

num1 = Numero(10)
num2 = Numero(5)

suma = num1 + num2
resta = num1 - num2

print(f"Suma: {suma}")    # Suma: 15
print(f"Resta: {resta}")  # Resta: 5
```

---

## Métodos de clase

Los métodos de clase trabajan con la clase en sí, no con las instancias. Se definen con `@classmethod`.

```python
class Persona:
    contador = 0  # Atributo de clase
    
    def __init__(self, nombre):
        self.nombre = nombre
        Persona.contador += 1
    
    @classmethod
    def obtener_contador(cls):
        return cls.contador
    
    @classmethod
    def crear_anonimo(cls):
        return cls("Anónimo")

persona1 = Persona("Juan")
persona2 = Persona("María")
persona3 = Persona.crear_anonimo()

print(f"Total de personas: {Persona.obtener_contador()}")  # Total de personas: 3
print(persona3.nombre)  # Anónimo
```

---

## Métodos estáticos

Los métodos estáticos no dependen de la clase ni de la instancia. Se definen con `@staticmethod`.

```python
class Matematicas:
    @staticmethod
    def sumar(a, b):
        return a + b
    
    @staticmethod
    def multiplicar(a, b):
        return a * b

print(Matematicas.sumar(5, 3))        # 8
print(Matematicas.multiplicar(4, 2))  # 8
```

---

## Property (Propiedades)

Las propiedades permiten acceder a métodos como si fueran atributos.

```python
class Persona:
    def __init__(self, nombre, edad):
        self._nombre = nombre
        self._edad = edad
    
    @property
    def nombre(self):
        return self._nombre
    
    @nombre.setter
    def nombre(self, valor):
        if isinstance(valor, str) and len(valor) > 0:
            self._nombre = valor
        else:
            print("Nombre inválido")
    
    @property
    def edad(self):
        return self._edad
    
    @edad.setter
    def edad(self, valor):
        if valor >= 0:
            self._edad = valor
        else:
            print("Edad inválida")

persona = Persona("Juan", 30)
print(persona.nombre)  # Juan

persona.nombre = "Pedro"
print(persona.nombre)  # Pedro

persona.edad = 35
print(persona.edad)    # 35

persona.edad = -5      # Edad inválida
```

---

## Resumen

|Concepto|Descripción|
|---|---|
|**Clase**|Plantilla para crear objetos|
|**`__init__`**|Constructor de la clase|
|**`self`**|Referencia a la instancia actual|
|**Atributos de instancia**|Variables específicas de cada objeto|
|**Atributos de clase**|Variables compartidas por todas las instancias|
|**Métodos de instancia**|Funciones que operan sobre la instancia|
|**Encapsulamiento**|Ocultar detalles internos (atributos privados `__`)|
|**Herencia**|Crear clases basadas en otras clases|
|**`super()`**|Llamar métodos de la clase padre|
|**Sobreescritura**|Redefinir métodos de la clase padre|
|**Polimorfismo**|Diferentes clases con métodos del mismo nombre|
|**Duck Typing**|Si tiene los métodos necesarios, funciona|
|**Métodos especiales**|`__str__`, `__repr__`, `__add__`, etc.|
|**`@classmethod`**|Métodos que trabajan con la clase|
|**`@staticmethod`**|Métodos independientes de clase e instancia|
|**`@property`**|Acceder a métodos como atributos|