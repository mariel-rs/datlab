+++
title = "2. Primer programa en Python"
description = "Operaciones aritméticas. Condicionales. Funciones"
disabletoc = false
weight = 2
tags = ["python"]
+++

## Operaciones

Python puede realizar las siguientes operaciones matemáticas:

**Suma**

Se indica con el operador `+`

```python
print(2 + 3)
```

**Resta**

Se indica con el operador `-`

```python
print(2 - 3)
```

**Multiplicación**

Se indica con el operador `*`

```python
# Multiplicaciones
print(2 * 3)
```

**Potencias**

Las potencias se indican con el operador `**` (Python no usa ^ para indicar
potencias como otros lenguajes)

```python
# cuidado con el operador...
print(2 ** 3)
```

**Divisiones**

Dependiendo lo que se requiera, las divisiones se indican con el operador `/`, 
`//` o `%`

```python
# Division
print(38 / 5)

# Cociente de la division (devuelve un entero)
print(38 // 5)

# Residuo de la division
print(38 % 5)
```

## Comparadores / Operadores relacionales

Consideremos dos variables,  `x` y `y`.

```python
# Dos numeros
x = 3
y = 4
```

Los siguientes operadores devolverán un valor verdadero o falso, dependiendo de 
la comparación.

**Igualdad**

```python
# Igual que
print(x == y)
```

**Desigualdad**

```python
# No es igual que 
print(x != y)
```

**Menor que, estrictamente menor**

```python
# Menor que
print(x < y)
```

**Mayor que, estrictamente mayor**

```python
# Menor que
print(x > y)
```

**Menor o igual que**

```python
# Menor o igual que
print(x <= y)
```

**Mayor o igual que**

```python
# Mayor o igual que
print(x >= y)
```

## Operadores lógicos

Los operadores lógicos devuelven un resultado si se cumple o no una condición. 
Los valores a devolver sólo son dos: verdadero o falso. Estos operadores se
llaman también booleanos por usar álgebra de Boole.

**and, operador y**

Devuelve un valor verdadero si **todas** las premisas son verdaderas.

```python
# Y
print(x == y and 5 >= 2)
```

**or, operador o**

Devuelve un valor verdadero si **al menos una** de las premisas es verdadera.

```python
# O
print(x == y or 5 >= 2)
```

**not, operador no**

Este operador niega el valor de la premisa. Si el valor de la premisa es 
verdadero, el operador devolverá un valor falso. Si el valor de la premisa es
falso, el operador devolverá un valor verdadero.

```python
# not
z = x == y
print(not z)
```

## Estructuras de control

### if

if (si, en español) es una sentencia condicional que permite que un programa ejecute un
bloque de código si se cumple una condición (si la condición es verdadera).

```python
# Sintaxis de if
if condición:
    #Aquí va el código que se ejecutará si la condición es verdadera
```

```python
numero = int(input("Escribe un número positivo: "))

if numero < 0:
    print(f"{numero} no es un número positivo")
print(f"Ha escrito el número {numero}")
```

```python
numero = int(input("Escribe un número mayor que 5: "))

if numero <= 5:
    print(f"{numero} no es un número estrictamente mayor que 5")
print(f"Ha escrito el número {numero}")
```

### if ... else

if ... else es una sentencia condicional que permite que un programa ejecute un
bloque de código si se cumple una condición (si la condición es verdadera). Si
la condición no es verdadera, el programa ejecutará el bloque de código contenido
en _else_.

```python
# Sintaxis de if else
if condición:
    # Aquí va el código que se ejecutará si la condición es verdadera
else:
    # Aquí va el código que se ejecutará si la condición no es verdadera
```

```python
print("Entrada del BabyO")
edad = int(input("¿Cuántos años tiene? "))

if edad < 18:
    print("No puede entrar")
else:
    print("Aunque es mayor de edad, esta lleno...")
```

### if ... elif ... else

elif (contracción de _else if_) es una estructura de control útil cuando tenemos
más de una condición a evaluar. De esta manera, podemos encadenar varias
condiciones.

```python
# Sintaxis de if elif else
if condición1:
    # Aquí va el código que se ejecutará si la condición1 es verdadera
elif condición2:
    # Aquí va el código que se ejecutará si la condición2 es verdadera
else:
    # Aquí va el código si ninguna condición es verdadera

```

```python
# Multiples condiciones. Un banco con 3 cajeros
cajeros = 3

clientes = int(input("Escriba el numero de clientes esperando en la fila "))

# Calcular cuantos cajeros estan disponibles
cajeros_disp = cajeros - clientes

if (cajeros_disp == cajeros):
    print("Todos los cajeros estan disponibles!")

elif (1 <= cajeros_disp < cajeros):
    print(f"Hay {cajeros_disp} cajeros disponibles")

elif (cajeros_disp == 0):
    print(f"No hay cajeros disponibles")

else:
    print("Intenta un numero mayor que 0 pero menor o igual a 3")
```

## Funciones

Una función es un bloque de código que se ejecuta sólo cuando es llamada o
invocada. Se les puede transferir valores utilizando argumentos y a su vez, una 
función puede devolver valores.

**Estructura de una funcion**

```python
def mi_funcion(arg):
    # Aqui va el codigo
    return arg

def otra_funcion(mensaje):
    # Aqui va el codigo
    print(mensaje)
```

Más de un argumento

```python
def mi_funcion(arg1, arg2):

    # Guarda los argumentos en una lista
    arg_list = [arg1, arg2]

    return arg_list
```

## Ejercicios

1. Escribe una función **media** que calcule la media de dos numeros `a` y `b`, y 
que **imprima** el resultado en pantalla.

```python
def media(a, b):
    # Aqui va tu codigo
```

2. Crea una función **temp_convert** que tome la temperatura en grados
Farenheit `tf` como argumento y la convierta a grados Celsius. La función 
deberá mostrar en pantalla la temperatura en grados Celsius. 

    Puedes usar la siguiente ecuación para realizar la conversión de temperaturas: 

$$ T_c = \frac{5}{9}(T_f - 32)$$

```python
def temp_convert(tf):
    # Aqui va tu codigo
```

{{% notice info %}}
Puedes usar la función **round(x, 2)** para redondear el valor de _x_ a 2 
decimales.
{{% /notice %}}

Para verificar tu función, puedes usar las siguientes pruebas:

| Prueba | Resultado |
| ------ | ----------- |
| temp_convert(59) | 15 |
| temp_convert(32) | 0 |

3. Crea una función llamada **contabilidad** que tome una lista `pagos` con los 
pagos del mes y una variable `ingresos` que indica el total de ingresos del mes 
como argumentos. La función deberá regresar el dinero que queda disponible.

```python
def contabilidad(pagos, ingresos):
    # Aqui va tu codigo
```

{{% notice info %}}
Puedes usar la función **sum()** para sumar todos los elementos de la lista.
{{% /notice %}}

Para verificar tu función, puedes usar las siguientes pruebas:

| Prueba | Resultado |
| ------ | ----------- |
| print(contabilidad([100, 300, 20], 750)) | 330 |
| print(contabilidad([300, 39, 700, 500, 220, 740], 2500)) | 1 |

{{% notice tip "Referencias" %}}
- Introducción a la programación con Python. Bartolomé Sintes Marco. Disponible 
en: https://www.mclibre.org/consultar/python/index.html
{{% /notice %}}