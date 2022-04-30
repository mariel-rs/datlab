+++
title = "7. Recapitulación"
description = "Ejercicio final para recapitular lo aprendido en el curso"
disabletoc = false
weight = 7
+++

## Introducción

Ahora que hemos aprendido sobre como usar las librerías de manipulacion de datos,
visualizaciones y análisis estadístico, haremos un pequeño ejercicio.

**Datos**

Usaremos los siguientes archivos para recapitular todos lo aprendido:

{{% attachments style="blue" title="Archivos" pattern=".*(csv|txt)"/%}}

Estos son datos de calidad de una muestra de vino tinto y vino blanco, y 
recopilados por P. Cortez, A. Cerdeira, F. Almeida, T. Matos y J. Reis.

## Inspección de datos

Empezamos importando los datos. Aunque estos datos estan en formato ***.csv**, usan como separador el simbolo de
punto y coma `;`. pandas tambien puede manejar esto en el argumento `sep`

```python
red_wine = pd.read_csv("winequality-red.csv", sep = ";")
white_wine = pd.read_csv("winequality-white.csv", sep = ";")
```
Ahora revisamos 

```python


```


###  Análisis exploratorio
### Matriz de correlaciones

### Visualizaciones

## Regresión lineal

## Referencias

{{% notice tip "Referencias"  %}}
- Wine Quality Dataset. UC Irvine Machine Learning Repository. Disponible en: 
https://archive.ics.uci.edu/ml/datasets/wine+quality 
Dataset de: P. Cortez, A. Cerdeira, F. Almeida, T. Matos y J. Reis. Modeling wine 
preferences by data mining from physicochemical properties. En Decision Support 
Systems, Elsevier, 47(4):547-553, 2009.
{{% /notice %}}