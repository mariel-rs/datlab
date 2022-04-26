+++
title = "2. Primer programa en Python"
description = "Operaciones aritméticas. Condicionales. Funciones"
disabletoc = false
weight = 2
+++

## Ejercicios

### Operaciones

```python
# Sumas
print(2 + 3)

# Restas
print(2 - 3)

# Multiplicaciones
print(2 * 3)

# Divisiones
print(2 / 3)

# Potencia
print(2 ** 3)

# Division
print(38 / 5)

# Cociente de la division
print(38 // 5)

# Residuo de la division
print(38 % 5)
```
### Comparadores

```python
# Dos numeros
x = 3
y = 4

# Menor que
print(x < y)

# Igual que
print(x == y)

# No es igual que 
print(x != y)

# O
print(x == y or 5 >= 2)

# Y
print(x == y and 5 >= 2)

# Una nueva variable
z = x > y
print(z)
```

### Condicionales

**If**

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

**If else**

```python
print("Entrada del BabyO")
edad = int(input("¿Cuántos años tiene? "))
if edad < 18:
    print("No puede entrar")
else:
    print("Aunque es mayor de edad, esta lleno...")
```

**If elif else**

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

### Funciones

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

**Ejercicio**

Escribir una funcion **media** que calcule la media de dos numeros `a` y `b`, y 
que imprima el resultado en pantalla.

```python
def media(a, b):
    # Aqui va tu codigo
```


## Tarea

1. Crea una función llamada **temp_convert** que toma la temperatura en grados
Farenheit `tf` como argumento y la convierte a grados Celsius `tc`. La función 
deberá **imprimir** la temperatura en grados Celsius. 

![t_convert](https://latex.codecogs.com/png.image?\large&space;\dpi{110}T_c&space;=&space;\frac{5}{9}(T_f&space;-&space;32))

```python
def temp_convert(tf):
    # Aqui va tu codigo
```

{{% notice tip %}}
Puedes usar la función **round(x, 2)** para redondear el valor de _x_ a 2 decimales
{{% /notice %}}


Para verificar tu función, puedes usar las siguientes pruebas:

| Prueba | Resultado |
| ------ | ----------- |
| temp_convert(59) | 15 |
| temp_convert(32) | 0 |

2. Crea una función llamada **contabilidad** que tome una lista `pagos` con los 
pagos del mes y una variable `ingresos` que indica el total de ingresos del mes 
como argumentos. La función deberá **regresar** el dinero que queda disponible.

```python
def contabilidad(pagos, ingresos):
    # Aqui va tu codigo
```

{{% notice tip %}}
Puedes usar la función **sum(lista)** para sumar todos los elementos de la lista
{{% /notice %}}

Para verificar tu función, puedes usar las siguientes pruebas:

| Prueba | Resultado |
| ------ | ----------- |
| print(contabilidad([100, 300, 20], 750)) | 330 |
| print(contabilidad([300, 39, 700, 500, 220, 740], 2500)) | 1 |

