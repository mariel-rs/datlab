+++
title = "1. Introducción a Python"
description = "Ejercicios y tareas del material introductorio a Python"
disabletoc = false
weight = 1
+++

## Introducción

### Salida por pantalla

Lo primero que se suele hacer cuando aprendemos a programar es saludar... 
[Hello world](https://es.wikipedia.org/wiki/Hola_mundo)

```python
print("Hello world")
print(1+1)
```

### Un comentario

Los comentarios no se ejecutan. Son eso, comentarios.

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

Declarar una variable es tan fácil como definir un nombre y dar un valor.

```python
a = 2
print(a)
```

### Tipo de datos

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

```python
# Entrada por teclado usando input()
print("Escriba su nombre")
nombre = input()

# f strings ;)
print(f"Hola, {nombre}")
print(f"La variable tiene el tipo de dato {type(nombre)}")
```

## Estructuras
### Listas

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

- Cuantos elementos tiene la lista?

```python
print(len(str_list))
```

- Acceder a los elementos de la lista usando índices
  
```python
# Todo empieza en cero...
print(str_list[0])
print(str_list[3])
```

- Agregar elementos usando _append_

```python
str_list.append("4")
print(str_list[3])
```

- Eliminar elementos usando _remove_

```python
str_list.remove("4")
print(str_list)
print(str_list[3])

```

### Diccionarios

```python
# Un diccionario vacio
empty_list = {}
```

```python
# Un diccionario de una bolsa de frutas
fruit_bag = {'apples': 4, 'pears': 9, "bananas": 0}
```

Tambien se puede escribir delimitando espacios (Mira la sangría)

```python
# Un diccionario de una bolsa de frutas, con espacios
fruit_bag = {
    'apples': 4, 
    'pears': 9, 
    "bananas": 0
    }
```

- Consultar las Keys (Llaves) existentes en el diccionario. Método _keys()_

```python
print(fruit_bag.keys())
```

- Values (Valores) Método _values()_

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

- Eliminar una llave usando _del_

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

2. Usando las listas ```mixed_list``` y ```str_list``` de los ejercicios, 
realizar los siguientes ejercicios:
    1. Agregar el último elemento de la lista ```str_list``` a la lista ```mixed_list```
    2. Imprimir en pantalla:
       1. Tipo de dato del primer elemento de ```mixed_list```
       2. Elemento con índice 6 de de ```mixed_list```
    3. **Reto** Convertir el elemento con índice 1 a tipo  _int_
    4. **Reto**  Verificar si los elementos con índices 0 y 1 son del mismo tipo

3. Seguir el ejercicio de frutas en **5.1. More on Lists** en el sitio de 
referencia de Python [Estructuras de Datos](https://docs.python.org/3/es/tutorial/datastructures.html)

4. Crear un diccionario llamado ```estudiante``` con 3 llaves:
   - "id"
   - "clave_materia"
   - "calificacion_final"

    Ejercicios:
    1. Llenar el diccionario con un ejemplo de un estudiante
    2. **Reto** Llenar el diccionario con 3 estudiantes.

5. **Opcional** Consultar el sitio [McLibre](https://www.mclibre.org/consultar/python/index.html)
sobre los temas vistos en la sesión.

{{% notice info %}}
Las tareas se pueden realizar en un Jupyter notebook, o en un archivo .py. 
{{% /notice %}}

