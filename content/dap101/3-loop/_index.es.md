+++
title = "3. Bucles"
description = "Bucles: For, While"
disabletoc = false
weight = 3
+++

## Bucles

### For

Accesando una lista por sus elementos

```python
# Una lista con numeros
a = [1, 2, 10, 0, 6]

for el in a:
    print(el)
```

**Range**

```python
range(j)             # 0, 1, 2, ..., j-1
range(i, j)          # i, i+1, i+2, ..., j-1
range(i, j, k)       # i, i+k, i+2k, ..., i+m
```

Algunos ejemplos

```python
range_list = list(range(5))
print(range_list)
```

```python
ten_hundred = list(range(10, 101, 10))
print(ten_hundred)
```

Accesando a la lista usando indices

```python
# Ahora usamos indice
for i in range(len(a)):
    print(a[i])
```

**Ejercicio**

1. Usando un bucle **For**, calcular la media de un estudiante con las siguientes 
calificaciones:


| Materia | Calificaciones |
| ------ | ----------- |
| Quimica | 9 |
| Biologia | 8 |
| Matematicas | 9.5 |
| Psicologia | 8.5 |



{{% notice tip %}}
Representa las calificaciones como una lista. Primero sumar y al final, dividir.

$$ \bar{x} = \frac{1}{N}\sum_{i=1}^N x $$
{{% /notice %}}


```python
# Aqui va tu codigo
```

### While

```python
i = 1
while i <= 3:
    print(0)
    i += 1
print("Hasta que se acabe el dedo")
```

Otro ejemplo

```python
i = 10
while i >= 0:
    print(i)
    i -= 1
print("Cuenta terminada")
```

Un infinito

```python
i = 1
while i <= 10:
    print(i)
```

Casi infinito

```python
# Are you human?
print("Eres una persona? Responde Si o No")
answer = input().lower()

while(answer == "si"):
    print("En serio? Intenta otra vez. Responde Si o No")
    answer = input().lower()
```

Romper un bucle while con _break_

```python
def break_loop():
    
    contador = 0
    
    while True:
        
        print("Deseas terminar el programa? Escribe Si o No")
        respuesta = input()
        
        # Actualizar el contador
        contador += 1
        
        if contador >= 5:
            print("Ya me ejecute muchas veces. Voy a descansar.")
            break
```

## Ejercicios

##### Aprobado / No Aprobado
Consideremos el caso de un estudiante que tiene que presentar tres exámenes. 
La escala de evaluación es de 0 a 100 puntos. 

Un estudiante aprueba el año si:

- Se aprueban todos los exámenes con 40 puntos o más, o
- Se aprueban al menos dos exámenes con 40 puntos o más, y que la media de los
tres exámenes sea estrictamente mayor a 50. (Es decir, una media de 50 puntos no 
es aprobatoria).

Escribe una función `student_pass` que tome tres argumentos, las calificaciones 
de los exámenes (como enteros), y determinar si el estudiante ha aprobado el año, 
utilizando dichas calificaciones. La función debería imprimir "Aprobado" o 
"No aprobado".

Puedes utilizar la siguientes pruebas para verificar tu función:

| Prueba | Resultado |
| ------ | ----------- |
| student_pass(70, 50, 30) | "No aprobado" |
| student_pass(70, 50, 35) | "Aprobado" |


##### "Dile que no"
Escribe un programa que imprima en pantalla la pregunta

"¿Desea continuar el programa?:"

Y que termine el programa solo cuando el usuario escriba "no". 

```python
def dile_no():
    # Aqui va tu codigo
```