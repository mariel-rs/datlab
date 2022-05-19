+++
title = "1. Introducción a Python"
description = "Variables, tipos de datos y estructuras de datos en Python"
disabletoc = false
weight = 2
tags = ["python"]
+++

## Introducción

Python es un lenguaje de programación fácil de aprender, con estructuras de
datos eficientes. Es considerado como el lenguaje más popular para aprender por
su versatilidad, su enfoque sencillo y la cantidad de librerías disponibles para
machine learning, análisis de datos y visualización de datos.

### Salida por pantalla

Lo primero que se suele hacer cuando aprendemos a programar es saludar. 
[Hello world](https://es.wikipedia.org/wiki/Hola_mundo). 

Creemos un Jupyter notebook y agreguemos un bloque de código con las siguientes 
líneas de código:

```python
print("Hello world")
print(1+1)
```

### Un comentario

Los comentarios son porciones del código que no se ejecutan. Python utiliza el
símbolo **#** para definir comentarios.

```python
# Hola, soy un comentario.
print("Hello world")
print(1+1)
```

```python
# Hola, soy un comentario.
# print("Hello world") # Acabo de comentar esta linea
print(1+1)
```

## Variables 

Una variable es una ubicación en memoria que tiene un nombre simbólico asociado 
y que puede guardar información.

Declarar una variable es tan fácil como definir un nombre y dar un valor.

```python
a = 2
print(a)
```

### Tipo de datos

Python es un lenguaje de tipado dinámico. Es decir, no tenemos que definir el
tipo de dato. Python asumirá el tipo de valor usando una regla llamada 
***duck typing***:

"Si veo un ave que camina como un pato, nada como un pato y suena como un pato, 
entonces a esa ave yo la llamo un pato."

#### Enteros (_int_)
   
```python
a = 1
print(a)
print(type(a))
```

#### Flotantes (_float_)
   
```python
a = 3.98
print(a)
print(type(a))
``` 

```python
a = 1.0
print(a)
print(type(a))
```  

#### Booleanos (_bool_)

```python
a = True
print(a)
print(type(a))
```

```python
a = 1
print(a)
print(type(a))
```   

#### Cadenas de texto (_str_)

```python
a = "Hola"
print(a)
```

### Convertir tipos de datos

Gracias al duck typing, a veces Python puede asumir un tipo de datos que no 
queremos. Sin embargo, podemos convertir datos.

```python
# Esto aunque parezca booleano, Python lo entendera como un entero
bool_test = 1
print(bool_test)
print(type(bool_test))
```
```python
# Conversion de datos usando bool(), int(), float()
real_bool = bool(1)
real_int = int(2.0)
```

## Entrada por teclado

Podemos permitir que el usuario introduzca información usando la función **input()**.
Esta función nos regresará lo que el usuario escribió como cadena de texto.

```python
# Entrada por teclado usando input()
print("Escriba su nombre")
nombre = input()

# f strings ;)
print(f"Hola, {nombre}")
print(f"La variable tiene el tipo de dato {type(nombre)}")
```

## Estructuras de datos

Una estructura de datos es un formato de organización, manejo y almacenamiento
de datos que permite acceder y modificar datos de forma eficiente.

Python tiene 4 estructuras de datos básicas: listas, sets, tuplas y dictionarios.
En este curso sólo veremos listas y diccionarios.

### Listas

Las listas son estructuras de datos que se usan para guardar ítems en una sola
variable. Las listas pueden guardar cualquier tipo de datos.

```python
# Una lista vacia
empty_list = []
```

```python
str_list = ["1", "2", "3"]
int_list = [1, 2, 3]
mixed_list = [1, 1.0, "2", "Hola", True, "True", [1, 2]]
```

- Imprimir en pantalla cada una de las listas

```python
# Aqui va tu codigo
```

- ¿Cuántos elementos tiene la lista?

```python
print(len(str_list))
```

- Acceder a los elementos de la lista usando índices
  
```python
# Todo empieza en cero...
print(str_list[0])
print(str_list[3])
```

- Agregar elementos usando **append()**

```python
str_list.append("4")
print(str_list[3])
```

- Eliminar elementos usando **remove()**

```python
str_list.remove("4")
print(str_list)
print(str_list[3])

```

### Diccionarios

Los diccionarios se usan para guardar datos usando parejas de llaves y valores 
(key: value). Los diccionarios no permiten repetición de llaves. Tal y como 
funciona un diccionario físico. 

```python
# Un diccionario vacio
empty_dict = {}
```

```python
# Un diccionario de una bolsa de frutas
fruit_bag = {'apples': 4, 'pears': 9, "bananas": 0}
```

También se puede escribir delimitando espacios (Mira la sangría)

```python
# Un diccionario de una bolsa de frutas, con espacios
fruit_bag = {
    'apples': 4, 
    'pears': 9, 
    "bananas": 0
    }
```

- Consultar las Keys (Llaves) existentes en el diccionario. Método **keys()**

```python
print(fruit_bag.keys())
```

- Values (Valores) Método **values()**

```python
print(fruit_bag.values())
```

- Comprobar si existe una llave en el diccionario

```python
print("kiwis" in fruit_bag)
```

- Acceder a valores usando una llave

```python
# Cuantas manzanas hay?
print(fruit_bag["apples"])
```

- Actualizar valores

```python
# Ahora hay 5 manzanas
fruit_bag["apples"] = 5
print(fruit_bag)
```
- Agregar nuevas llaves

```python
# Agregando kiwis a la bolsa de frutas
fruit_bag["kiwis"] = 1
print(fruit_bag)
```

- Eliminar una llave usando **del**

```python
# Ya no es temporada de kiwis
del fruits['kiwis']
print(fruits)
```

## Ejercicios

1. Crear una variable ```colegiatura``` que pida un valor al usuario. 
   1. Imprimir el valor que el usuario introduce
   2. Imprimir el tipo de dato que tiene ```colegiatura```
   3. Convertir el valor a _float_

2. Usando las listas ```mixed_list``` y ```str_list``` de los ejercicios:
    1. Agregar el último elemento de la lista ```str_list``` a la lista 
   ```mixed_list```
    2. Imprimir en pantalla:
       1. Tipo de dato del primer elemento de ```mixed_list```
       2. Elemento con índice 6 de de ```mixed_list```
    3. **Reto** Convertir el elemento con índice 1 de ```mixed_list```
        a tipo  _int_
    4. **Reto**  Verificar si los elementos con índices 0 y 1 de 
    ```mixed_list``` y ```str_list```son del mismo tipo

3. Seguir el ejercicio de frutas en **5.1. More on Lists** en el sitio de 
referencia de Python 
[Estructuras de Datos](https://docs.python.org/3/es/tutorial/datastructures.html)

4. Crear un diccionario llamado ```estudiante``` con 2 llaves:
   - "id"
   - "calificacion_final"

    Ejercicios:
    1. Llenar el diccionario con un ejemplo de un estudiante.
    2. **Reto** Llenar el diccionario con 3 estudiantes.

## Material adicional

- Introducción a la programación con Python. Bartolomé Sintes Marco. Disponible 
en: https://www.mclibre.org/consultar/python/index.html