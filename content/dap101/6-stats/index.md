+++
title = "6. Análisis estadístico"
description = "Pruebas de hipótesis y regresiones"
disabletoc = false
weight = 6
tags = ["pandas", "scipy", "statsmodels", "estadistica"]
+++

## Introducción

Python tiene bastantes librerías para realizar análisis estadístico. En esta
sección nos concentraremos en SciPy y statsmodels.

**Datos**

Usaremos los siguientes archivos para los ejercicios de este tema:

{{% attachments title="Archivos" pattern=".*csv"/%}}

**Librerias**

Para esta seccion usaremos las siguientes librerias

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import scipy.stats as stats
```

## Prueba de hipótesis

Usaremos el archivo `precipitacion_guerrero.csv` que contiene datos historicos 
mensuales y anuales de precipitacion en Guerrero desde 1985 hasta 2020. Estos 
datos tambien usan comas para separar miles. 

```python
# Datos precipitacion
precipitacion = pd.read_csv("precipitacion_guerrero.csv", thousands = ",")
```

Inspeccionamos las medidas de estadistica descriptiva

```python
# Estadistica descriptiva
precipitacion.describe()
```

### t-test

#### Una muestra

#### Dos muestras

Utilizaremos la funcion `ttest_ind` para comparar las medias de dos muestras `a`
y `b`.

$$\mu_{a} = \mu_{b}$$

Definimos la hipotesis nula como:

$$H_{0}: \mu_{a} = \mu_{b} $$

Dependiendo el tipo de hipotesis alternativa, podemos tener las siguientes 
opciones:

$$H_{1}: \mu_{a} \neq \mu_{b} \ \ \ (\text{dos colas}) $$
$$H_{1}: \mu_{a} < \mu_{b} \ \ o \ \ \mu_{a} > \mu_{b} \ \ \ (\text{una cola}) $$


```python
# sintaxis
stats.ttest_ind(a, b, equal_var, alternative)
```

donde 

`a` y `b`: Muestras a contrastar

`equal_var`: Parametro opcional que define si las muestras tienen varianzas iguales.
En caso de que sean iguales, SciPy hara la prueba de hipotesis usando t-Student. 
En caso de que no sean iguales, SciPy usara la prueba Welch. Por defecto, este
parametro tiene un valor de True.

`alternative`: Parametro opcional donde se define el tipo de hipotesis alternativa.
Las opciones disponibles son 'two-sided', 'less' y 'greater'. Por defecto, este
parametro tiene un valor de 'two-sided'.

SciPy nos retornara el estadistico y el valor-p.

Hagamos una pequena funcion.

```python
def t_test(muestra_a, muestra_b, equal_var):

    t_test = stats.ttest_ind(a = muestra_a, b = muestra_b, equal_var= equal_var)

    if t_test.pvalue < 0.05:
        print("Rechazar hipotesis nula")
    else:
        print("No hay evidencia suficiente para rechazar hipotesis nula")
    
    print(t_test)
```

Probemos contrastando las medias de precipitacion de enero y marzo.

```python
t_test(precipitacion["ENE"], precipitacion["MAR"], True)
```

Ahora probemos contrastando las medidas de precipitacion de enero y julio. Es
importante recordar que la varianza entre ambos meses no es igual.

```python
t_test(precipitacion["ENE"], precipitacion["JUL"], False)
```

## Regresión

## Ejercicios

{{% notice tip "Referencias"  %}}

- Derrama económica por destino turístico generada por el turismo en el estado de 
Puebla por año. Datos abiertos de Puebla. Disponible en: http://datos.puebla.gob.mx/datos/derrama-economica-destino-turistico-generada-turismo-estado-puebla-anio-20181231-csv

- Selección de aspirantes. INECOL. Datos abiertos de México. Disponible en: 
https://datos.gob.mx/busca/dataset/seleccion-de-aspirantes

- Títulos proyectado con asistencia. Cineteca Nacional. Datos abiertos de México. 
Disponible en: https://datos.gob.mx/busca/dataset/titulos-proyectado-con-asistencia

- Precipitacion. CONAGUA. Datos abiertos de Mexico. Disponible en: 
https://datos.gob.mx/busca/dataset/precipitacion

- Temperatura maxima. CONAGUA. Datos abiertos de Mexico. Disponible en:
https://datos.gob.mx/busca/dataset/temperatura-maxima-excel

- Temperatura minima. CONAGUA. Datos abiertos de Mexico. Disponible en:
https://datos.gob.mx/busca/dataset/temperatura-minima-excel


- SciPy documentation. The SciPy community. Disponible en: 
https://docs.scipy.org/doc/scipy/

- T-test con Python. Ciencia de datos. Disponible en: 
https://www.cienciadedatos.net/documentos/pystats10-t-test-python.html

-  Statistics in Python. Scipy lecture notes. Disponible en: 
https://scipy-lectures.org/packages/statistics/index.html

- Statistical hypothesis tests in Python cheat sheet. Machine learning mastery.
Disponible en: 
https://machinelearningmastery.com/statistical-hypothesis-tests-in-python-cheat-sheet/
{{% /notice %}}