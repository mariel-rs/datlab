+++
title = "6. Análisis estadístico"
description = "Pruebas de hipótesis y regresión"
disabletoc = false
weight = 6
tags = ["pandas", "scipy", "statsmodels", "estadistica"]
+++

## Introducción

Python tiene bastantes librerías para realizar análisis estadístico. En esta
sección nos concentraremos en SciPy y statsmodels.

**Datos**

Usaremos los siguientes archivos para los ejercicios de este tema:

{{% attachments style="blue" title="Archivos" pattern=".*(csv|txt)"/%}}

**Librerías**

Para esta sección usaremos las siguientes librerías:

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import scipy.stats as stats
```

**Datos de precipitación**

Usaremos el archivo `precipitacion_guerrero.csv` que contiene datos históricos 
mensuales y anuales de precipitación en Guerrero desde 1985 hasta 2020. La 
descripción de las columnas es la siguiente:

| Variable | Tipo variable | Descripción pregunta |
| -------- | ------------- | ---------------------|
| PERIODO | Numérica | Año en el que se reporta información de precipitación |
| ENE | Numérica | Precipitación observada durante el mes de enero, en mm |
| FEB | Numérica | Precipitación observada durante el mes de febrero, en mm  |
| MAR | Numérica | Precipitación observada durante el mes de marzo, en mm  |
| ABR | Numérica | Precipitación observada durante el mes de abril, en mm  |
| MAY | Numérica | Precipitación observada durante el mes de mayo, en mm  |
| JUN | Numérica | Precipitación observada durante el mes de junio, en mm  |
| JUN | Numérica | Precipitación observada durante el mes de junio, en mm  |
| JUL | Numérica | Precipitación observada durante el mes de julio, en mm  |
| AGO | Numérica | Precipitación observada durante el mes de agosto, en mm  |
| SEP | Numérica | Precipitación observada durante el mes de septiembre, en mm  |
| OCT | Numérica | Precipitación observada durante el mes de octubre, en mm  |
| NOV | Numérica | Precipitación observada durante el mes de noviembre, en mm  |
| DIC | Numérica | Precipitación observada durante el mes de diciembre, en mm  |
| ANUAL | Numérica | Precipitación observada durante todo el periodo (año), en mm  |

Puesto que estos datos usan comas para separar miles, el argumento `thousands` 
indica a pandas el separador usado en estos datos. Ahora, importemos estos datos.

```python
# Datos precipitacion
precipitacion = pd.read_csv("precipitacion_guerrero.csv", thousands = ",")
```

Inspeccionamos las medidas de estadística descriptiva.

```python
# Estadistica descriptiva
precipitacion.describe()
```

## Prueba de normalidad

Podemos observar normalidad utilizando histogramas como los que ofrece seaborn, 
pero también podemos comprobar normalidad usando SciPy.

SciPy ofrece varias pruebas de normalidad, por ahora veremos la prueba
Shapiro-Wilk y D'Agostino-Pearson en sus funciones
[**stats.shapiro**](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.shapiro.html) y 
[**stats.normaltest**](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.normaltest.html)
respectivamente.

Ambas pruebas se definen con las siguientes hipótesis:

Hipotesis nula:
$$H_{0}: \text{La muestra proviene de una distribución normal} $$

Hipotesis alternativa:
$$H_{1}: \text{La muestra no proviene de una distribución normal} $$

```python
# Sintaxis de prueba de Shapiro-Wilk
stats.shapiro(muestra)

# Sintaxis de prueba D'Agostino-Pearson
stats.normaltest(muestra)
```

Para ambas pruebas, SciPy nos retornará el valor del estadístico y el valor-p

Hagamos una función para hacer prueba de normalidad con ambos métodos.

```python
def normal_test(datos, option = "shapiro"):

    if option != "shapiro":
        test = stats.normaltest(datos)
    else:
        test = stats.shapiro(datos)

    if test.pvalue < 0.05 :
        print("Rechazar hipotesis nula")
    else:
        print("No hay evidencia suficiente para rechazar hipotesis nula")
    
    print(test)
```

Ahora comprobemos si los datos de precipitación del mes de julio provienen de
una distribución normal.

```python
# Prueba D'Agostino-Pearson
normal_test(precipitacion["JUL"], "dagostino")
```

## Pruebas de hipótesis

### t-test

#### Una muestra

Esta prueba nos sirve para determinar si la media de la población estudiada es 
igual a un valor conocido. 

$$\mu = \mu_{0}$$

Definimos la hipótesis nula como:

$$H_{0}: \mu = \mu_{0} $$

Dependiendo el tipo de hipótesis alternativa, podemos tener las siguientes 
opciones:

$$H_{0}: \mu \neq \mu_{0} \ \ \ (\text{dos colas}) $$

$$H_{0}: \mu < \mu_{0} \ \ o \ \ \mu >  \mu_{0} \ \ \ (\text{una cola}) $$

Utilizaremos la función [**ttest_1samp**](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_1samp.html) 
de SciPy.

```python
# sintaxis
stats.ttest_1samp(a, popmean, alternative)
```

donde

`a`: Muestra

`popmean`: Valor de media conocido.

`alternative`: Parámetro opcional donde se define la hipótesis alternativa. Las 
opciones disponibles son 'two-sided' (dos colas), 'less' y 'greater'. El valor 
predeterminado es 'two-sided'.

Hagamos una función para realizar la prueba de hipótesis.

```python
def t_test_1samp(datos, media):

    test = stats.ttest_1samp(datos, popmean = media)

    if test.pvalue < 0.05:
        print("Rechazar hipótesis nula")
    else:
        print("No hay evidencia suficiente para rechazar hipótesis nula")
    
    print(test)
```

Probemos si la media de precipitación en julio es igual a 150.

```python
t_test_1samp(precipitacion["JUL"], 150)
```

#### Dos muestras independientes

Esta prueba nos sirve para comparar las medias de dos muestras independientes 
`a` y `b`, y determinar si son iguales.

$$\mu_{a} = \mu_{b}$$

Definimos la hipótesis nula como:

$$H_{0}: \mu_{a} = \mu_{b} $$

Dependiendo el tipo de hipótesis alternativa, podemos tener las siguientes 
opciones:

$$H_{1}: \mu_{a} \neq \mu_{b} \ \ \ (\text{dos colas}) $$
$$H_{1}: \mu_{a} < \mu_{b} \ \ o \ \ \mu_{a} > \mu_{b} \ \ \ (\text{una cola}) $$

Utilizaremos la función [**ttest_ind**](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_ind.html) de SciPy.

```python
# sintaxis
stats.ttest_ind(a, b, equal_var, alternative)
```

donde 

`a` y `b`: Muestras a contrastar

`equal_var`: Parámetro opcional que define si las muestras tienen varianzas 
iguales.En caso de que sean iguales, SciPy hará la prueba de hipótesis usando la 
prueba t-Student. Si las varianzas no son iguales, SciPy usará la prueba Welch. 
El valor predeterminado es True.

`alternative`: Parámetro opcional donde se define la hipótesis alternativa. Las 
opciones disponibles son 'two-sided', 'less' y 'greater'. El valor 
predeterminado es 'two-sided'.

SciPy nos retornará el estadístico y el valor-p.

Hagamos una pequeña función.

```python
def t_test(muestra_a, muestra_b, equal_var):

    t_test = stats.ttest_ind(a = muestra_a, b = muestra_b, equal_var= equal_var)

    if t_test.pvalue < 0.05:
        print("Rechazar hipótesis nula")
    else:
        print("No hay evidencia suficiente para rechazar hipótesis nula")
    
    print(t_test)
```

Probemos contrastando las medias de precipitación de enero y marzo.

```python
t_test(precipitacion["ENE"], precipitacion["MAR"], True)
```

Ahora probemos contrastando las medidas de precipitación de enero y julio. Es
importante recordar que la varianza entre ambos meses no es igual.

```python
t_test(precipitacion["ENE"], precipitacion["JUL"], False)
```

#### Dos muestras dependientes (Prueba t pareada)

Esta prueba nos sirve para comparar las medias de dos muestras dependientes 
`a` y `b`, y determinar si son iguales. Se considera que dos muestras son 
dependientes o pareadas cuando existe una relación entre las observaciones. Por
ejemplo:

- Comprobar el nivel de satisfacción del mismo grupo de clientes, antes y después,
de cambiar detalles en el servicio.
- Comparar el progreso del mismo grupo de pacientes, antes y después, de 
introducir un medicamento en su tratamiento.

En esta prueba se contrasta la diferencia entre las medias $\mu_d$. Si son 
iguales, la diferencia será igual a 0.

Entonces, las hipótesis contrastadas son:

$$H_{0}: \mu_{d} = 0$$
$$H_{1}: \mu_{d} \neq 0$$

Es importante destacar que para que este tipo de pruebas sean relevantes, los
datos deben provenir de una distribución normal. Sin embargo, no es necesario 
que las varianzas sean iguales. 

SciPy tiene la función [**ttest_rel**](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_rel.html) 
para realizar este tipo de pruebas.

```python
# sintaxis
stats.ttest_rel(a, b, alternative)
```

donde 

`a` y `b`: Muestras a contrastar.

`alternative`: Parámetro opcional donde se define la hipótesis alternativa. Las 
opciones disponibles son 'two-sided', 'less' y 'greater'. El valor 
predeterminado es 'two-sided'.

Escribimos una función para realizar esta prueba.

```python
def t_test_dep(muestra_a, muestra_b):

    t_test = stats.ttest_rel(a = muestra_a, b = muestra_b)

    if t_test.pvalue < 0.05:
        print("Rechazar hipotesis nula")
    else:
        print("No hay evidencia suficiente para rechazar hipotesis nula")
    print(t_test)
```

Probemos esta función con los valores de medias de precipitación en julio. 
Dividiremos la columna en dos series. Una serie para años anteriores a 2003, y 
otra serie para años posteriores a 2003. 

```python
# Obtenemos los valores de precipitacion en julio, y los dividimos en dos partes
julio_85_02 = precipitacion.query('PERIODO <= 2002')["JUL"]
julio_03_20 = precipitacion.query('PERIODO >= 2003')["JUL"]
```

Ahora, probemos nuestra función.

```python
# H0: La diferencia de medias es igual a 0
# H1: La diferencia de medias no es igual a 0

t_test_dep(julio_85_02, julio_03_20)
```

## Prueba de Levene (Homogeneidad de varianzas)

La prueba de Levene es una prueba utilizada para evaluar la igualdad
(homogeneidad) de las varianzas para una variable calculada para dos o más 
grupos. La prueba de Levene está definida como:

$$H_{0}: \sigma_{a} = \sigma_{b} = \sigma_{c} = ... $$
$$H_{1}: \sigma_{a} \neq \sigma_{b} \neq \sigma_{c} \neq ... \ \  \text{para al menos un par} $$

SciPy tiene implementada esta prueba en su función 
[**stats.levene**](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.levene.html).

```python
# Sintaxis
stats.levene(*muestras, center)
```

donde 

`muestras`: las muestras a contrastar sus varianzas

`center`: este parámetro indica la medida de localización para centrar las 
muestras. Los valores posibles son:

- `median` - para muestras que provienen de distribuciones asimétricas. Este es
el valor predeterminado.

- `mean` - para muestras que provienen de distribuciones simétricas

- `trimmed` - para muestras que provienen de distribuciones con colas largas 
(p. ej. distribución Cauchy)

SciPy nos retornará el estadístico y el valor-p.

Hagamos una pequeña función para verificar si las varianzas de la precipitación
promedio de los meses enero y marzo son iguales.

```python
def levene_test(muestra_a, muestra_b, center):

    levene_test = stats.levene(muestra_a, muestra_b, center= center)

    if levene_test.pvalue < 0.05:
        print("Rechazar hipotesis nula")
    else:
        print("No hay evidencia suficiente para rechazar hipotesis nula")
    
    print(levene_test)
```

Como prueba de cordura, veamos las distribuciones de la precipitación en ambos
meses usando histogramas.

```python
sns.histplot(precipitacion["ENE"])
```

```python
sns.histplot(precipitacion["MAR"])
```

Ahora hagamos la prueba de Levene.

```python
levene_test(precipitacion["ENE"], precipitacion["MAR"], "median")
```

## Regresión lineal

La regresión lineal es un instrumento matemático usado para modelar las 
relaciones entre una variable dependiente (o variable de respuesta), y una o más
variables independientes (o variables explicatorias). El modelo lineal tiene la
siguiente forma,

$$y = \beta_{0} + \beta_{i}x_i + ... + \epsilon_i \ \ \ \ \ i = 1, ... n $$

donde,

$\beta_i$ representan los coeficientes que describen la relación o la influencia
que tiene la variable $x_i$ sobre la variable dependiente.

$\beta_0$ representa el intercepto. Este valor describe la relación entre la
variable dependiente y las variables independientes $x_i$, cuando $x_i$ = 0.

$x_i$ son las variables independientes utilizadas en el modelo.

$\epsilon_i$ representa el error aleatorio que se introduce en el modelo por cada
variable independiente $x_i$. Estos errores son independientes y siguen una 
distribución normal. $\epsilon_i \sim \mathcal{N}(0, \sigma^2) $

### Mínimos cuadrados ordinarios

Existen distintos métodos para determinar los coeficientes $\beta$, uno de ellos es
mínimos cuadrados ordinarios. **statsmodels** es una librería de Python que 
contiene una colección grande de modelos estadísticos. Para ajustar un modelo
lineal usando mínimos cuadrados ordinarios, usaremos la función 
[**ols**](https://www.statsmodels.org/devel/generated/statsmodels.formula.api.ols.html) 
(ordinary least squares, en inglés).

```python
from statsmodels.formula.api import ols
```

Ahora usaremos los datos `edadpesograsas.txt` que nos servirá para entender el 
uso de **ols**. Este archivo contiene información de edad, peso y cantidad de 
grasas en 25 pacientes.  La descripción de las columnas es la siguiente:

| Variable | Tipo variable | Descripción pregunta |
| -------- | ------------- | ---------------------|
| peso | Numérica | Peso corporal, en kg |
| edad | Numérica | Edad |
| grasas | Numérica | Colesterol, en mg/dl |


Lo primero que haremos es importar los datos. Como estos datos provienen de un
archivo de texto (*.txt), usaremos ahora el método 
[**read_table()**](https://pandas.pydata.org/docs/reference/api/pandas.read_table.html) 
de pandas. El separador usado en este archivo es un tabulador. Daremos esta 
información al método para que el archivo se importe correctamente usando el
argumento `sep`.

```python
# Importar datos
edad_peso = pd.read_table("edadpesograsas.txt", sep="\t")
```

La sintaxis de `ols` es la siguiente:

```python
model = ols('variable_dependiente ~ variable1 + variable2 + ... +', df).fit()
```

Intentemos modelar la cantidad de grasas respecto a la edad:

```python
model = ols('grasas ~ edad', edad_peso).fit()
```

Para revisar la información del modelo de regresion, usamos el método **summary()**

```python
# Ver resultados
model.summary()
```

Ahora agreguemos la variable peso al modelo de regresión:

```python
model = ols('grasas ~ edad + peso', edad_peso).fit()
```

¿Mejoró el modelo?

{{% notice tip "Regresión paso a paso"  %}}
Lo que acabamos de hacer se llama regresión paso a paso (_stepwise regression_,
en inglés). Esta metodología es iterativa, pues implica seleccionar variables
de forma automática y ver como mejora (o empeora) el modelo. Existen dos tipos
de selección:

- Selección hacia adelante (_Forward selection_, en inglés): En este tipo de 
selección, el modelo se inicia sin ninguna variable. Después se agrega una 
variable a la vez y se prueba si mejoró la calidad del modelo con la inclusión 
de dicha variable.

- Selección hacia atrás (_Backward selection_, en inglés) En este tipo de 
selección, se inicia con un modelo que incluye todas las variables. Después se
elimina una variable a la vez y se prueba si mejoró la calidad del modelo con la 
eliminación de dicha variable.

Este método es adecuado cuando se tiene una cantidad significativa de variables
que explican el fenómeno a modelar y se desea empezar a eliminar variables 
irrelevantes. Sin embargo, siempre se preferirá analizar y entender los datos 
antes de crear modelos.
{{% /notice %}}

Con esto concluimos este tema. 

## Referencias y material adicional

- Precipitacion. CONAGUA. Datos abiertos de México. Disponible en: 
https://datos.gob.mx/busca/dataset/precipitacion

- Datos para la docencia. José Ramón Berrendero Díaz. Disponible en: 
https://verso.mat.uam.es/~joser.berrendero/datos.html

- SciPy documentation. The SciPy community. Disponible en: 
https://docs.scipy.org/doc/scipy/

- T-test con Python. Ciencia de datos. Disponible en: 
https://www.cienciadedatos.net/documentos/pystats10-t-test-python.html

-  Statistics in Python. Scipy lecture notes. Disponible en: 
https://scipy-lectures.org/packages/statistics/index.html

- Statistical hypothesis tests in Python cheat sheet. Machine learning mastery.
Disponible en: 
https://machinelearningmastery.com/statistical-hypothesis-tests-in-python-cheat-sheet/