+++
title = "Extras"
description = "Temas extras"
disabletoc = false
weight = 99
tags = ["instalacion", "pip", "conda", "pingouin"]
+++


## Introducción

En esta sección se presentan temas adicionales que pueden ser de interés para
grupos específicos.

## Instalación de paquetes

Anaconda es una distribución que trae muchos paquetes y librerías de Python
precargados, facilitando el uso del lenguaje para varias tareas. Sin embargo, a
veces es necesario instalar otros paquetes que Anaconda no trae.

La instalación de paquetes se realiza en una sesión de Terminal (macOS / Linux) 
o Anaconda Prompt (Windows) con el siguiente comando.

```py
pip install <nombre-paquete>
```

`pip` es el gestor de paquetes predeterminado de Python y se encargará de traer
los archivos necesarios (y dependencias) de los paquetes que instalemos. 

También existe `conda`, que es el gestor predeterminado de Anaconda. 
A veces conda es más eficiente para ciertos paquetes...

```python
conda install -<opciones> conda-forge <nombre-paquete>
```

## Alfa de Cronbach

Esta medida la podemos calcular rápidamente usando el paquete 
[pingouin](https://pingouin-stats.org/index.html). pingouin es una librería 
mucho más nueva que statsmodels y Scipy, que busca hacer más accesibles cálculos 
estadísticos. Pingouin puede procesar DataFrames de pandas nativamente. 

### Instalación

En una sesión de Terminal (macOS / Linux) o Anaconda Prompt 
(Windows), lancemos el siguiente comando.

```python
pip install pingouin
```

o también

```python
conda install -c conda-forge pingouin
```

### Uso

El siguiente ejemplo contiene los resultados de una encuesta ficticia de 3 
preguntas con escala Likert de 3 puntos. 

```python
import pandas as pd
import pingouin as pg

# Respuestas de una encuesta
encuesta = pd.DataFrame({'Q1': [1, 2, 2, 3, 2, 2, 3, 3, 2, 3],
                   'Q2': [1, 1, 1, 2, 3, 3, 2, 3, 3, 3],
                   'Q3': [1, 1, 2, 1, 2, 3, 3, 3, 2, 3]})
```

Para calcular el alfa de Cronbach, usamos la función 
[cronbach_alpha()](https://pingouin-stats.org/generated/pingouin.cronbach_alpha.html)
de pingouin.

```python
# Calculo de alfa de Cronbach
pg.cronbach_alpha(data = encuesta)
```

Esto nos devolverá una tupla que contiene el valor calculado del alfa de
Cronbach, y su intervalo de confianza al 95%.

```
(0.7734375, array([0.336, 0.939]))
```

Si uno desea cambiar el intervalo de confianza, se puede hacer con el argumento
`ci`. El intervalo de confianza se expresa como fracción.

```python
# Alfa de Cronbach e intervalo de confianza al 99%
pg.cronbach_alpha(data = encuesta, ci = 0.99)
```

## Referencias y material adicional

- Understanding pip and conda. Anaconda. Disponible en:
https://www.anaconda.com/blog/understanding-conda-and-pip