+++
title = "7. Recapitulación"
description = "Ejercicio final para recapitular el contenido del curso"
disabletoc = false
weight = 8
+++

## Introducción

Ahora que hemos aprendido sobre como usar las librerías de manipulación de datos,
visualizaciones y análisis estadístico, hagamos un pequeño ejercicio.

**Datos**

Usaremos el siguiente archivo para recapitular todo lo aprendido:

{{% attachments style="blue" title="Archivos" pattern=".*(csv|txt)"/%}}

Estos son datos recopilados por INEGI en su encuesta ENDUTIH de 2019. La
descripción de las columnas es la siguiente:

| Variable | Tipo variable | Descripción pregunta |
| -------- | ------------- | ---------------------|
| energia_electrica | Binaria | La vivienda dispone de energía eléctrica |
| refrigerador | Binaria | La vivienda dispone de refrigerador |
| lavadora | Binaria | La vivienda dispone de lavadora |
| auto_propio | Binaria | Las personas viviendo en esta vivienda disponen de automóvil o camioneta |
| personas_vivienda | Numérica | Número de personas viviendo normalmente en la vivienda |
| mismo_gasto | Binaria | El gasto para comer de todas las personas viviendo en la vivienda es el mismo |
| TLOC | Numérica (ordinal) | Tamaño de la Localidad (1: 100 000 y más habitantes, 2: 15 000 a 99 999 habitantes, 3: 2 500 a 14 999 habitantes, 4: menor a 2500 habitantes) |
| ESTRATO | Numérica (ordinal) | Estrato socioeconómico. (1: Bajo, 2: Medio bajo, 3: Medio alto, 4: Alto) |
| material_1 | Binaria | El material predominante del piso de esta vivienda es tierra |
| material_2 | Binaria | El material predominante del piso de esta vivienda es cemento |
| material_3 | Binaria | El material predominante del piso de esta vivienda es madera, mosaico u otro |
| fuente_agua_1 | Binaria | La fuente de agua es agua entubada dentro de la vivienda |
| fuente_agua_2 | Binaria | La fuente de agua es agua entubada fuera de la vivienda, pero dentro del terreno |
| fuente_agua_3 | Binaria | La fuente de agua es agua entubada de llave pública (o hidrante) |
| fuente_agua_4 | Binaria | La fuente de agua es agua entubada que acarrean de otra vivienda |
| fuente_agua_5 | Binaria | La fuente de agua es agua de pipa |
| fuente_agua_6 | Binaria | La fuente de agua de la vivienda es agua de un pozo, río, arroyo, lago u otro |
| conexion_drenaje_1 | Binaria | La vivienda tiene drenaje o desagüe conectado a la red pública |
| conexion_drenaje_2 | Binaria | La vivienda tiene drenaje o desagüe conectado a una fosa séptica |
| conexion_drenaje_3 | Binaria | La vivienda tiene drenaje o desagüe conectado a una tubería que va a dar a una barranca o grieta |
| conexion_drenaje_4 | Binaria | La vivienda tiene drenaje o desagüe conectado a una tubería que va a dar a un río, lago o mar |
| conexion_drenaje_5 | Binaria | La vivienda no tiene drenaje o desagüe |
| tipo_poblacion_R | Binaria | La vivienda se encuentra en una población rural |
| tipo_poblacion_U | Binaria | La vivienda se encuentra en una población urbana |

## Inspección de datos

Empezamos importando las librerías que usaremos y los datos.

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from statsmodels.formula.api import ols
```

Ahora importemos los datos y revisemos el tamaño del DataFrame.

```python
encuesta_vivienda = pd.read_csv("endutih_vivienda_anual_2019_enc.csv")
encuesta_vivienda.shape
```

Esto nos devuelve la tupla (21163, 24). Es un set de datos grande. Pero no es
problema para Python.

###  Análisis exploratorio

Ahora veamos las medidas de estadistíca descriptiva.

```python
encuesta_vivienda.describe()
```

Tal vez estos resultados no nos ayuden mucho puesto que son datos con mayormente
variables binarias (0 y 1). 

#### Matriz de correlaciones

La matriz de correlaciones se puede obtener con pandas usando el método 
[**corr()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.corr.html).
Las correlaciones pueden calcularse usando distintos métodos como Pearson, 
Spearman y Kendall usando el argumento `method`.

Para este caso, utilizaremos Spearman como método puesto que la mayor parte de 
las variables son binarias y sólo dos son de tipo ordinal.

```python
corr_matrix = encuesta_vivienda.corr(method = "spearman")
```

Esto nos devuelve otro DataFrame con la matriz de correlaciones. Este nuevo
DataFrame tiene un tamaño de 24 x 24.

#### Visualizaciones

Podemos ver la matriz de correlaciones con una visualización llamada 
[**heatmap**](https://seaborn.pydata.org/generated/seaborn.heatmap.html).

```python
# Heatmap
plt.figure(figsize = (18,12)) # Hacer más grande la figura
sns.heatmap(corr_matrix, annot = True, cmap = "Blues")
```

Hemos pasado un par de argumentos nuevos. `annot` nos reportará el valor del
factor de correlación en la visualización. `cmap` es el mapa de colores que
que seaborn usará. Para mejorar la vista, hemos usado la paleta Blues. Si el 
factor de correlación se acerca más al valor 1, el cuadro tendrá un color azul
más fuerte. Si te interesa ver más opciones puedes ver la documentación de
[colormaps](https://matplotlib.org/stable/tutorials/colors/colormaps.html) de
matplotlib.

Adicionalmente, por ser una visualización de 24x24, el tamaño de la figura debe
ser más grande.

Enfoquémonos en las variables **ESTRATO** y **TLOC**, que son numéricas.

```python
sns.histplot(encuesta_vivienda["ESTRATO"])
```

Podemos ver que es una variable discreta, puesto que tiene valores enteros que
van del 1 al 5. Podemos ver que hay menos personas con un estrato 4 (estrato
alto), mientras que la mayor parte de las respuestas tienen un estrato 2 
(estrato medio bajo). 

```python
sns.histplot(encuesta_vivienda["TLOC"])
```

De igual manera, TLOC es una variable discreta. Los grupos de encuestados más
representativos en la muestra, son de localidades con 100,000 y más habitantes,
y de localidades con menos de 2500 habitantes. 

Tracemos una recta entre ambas variables para encontrar más relaciones.

```python
sns.lineplot(data = encuesta_vivienda, x = "TLOC", y = "ESTRATO")
```

Podemos ver que conforme aumenta TLOC, ESTRATO decrece. Parece tener sentido.

## Modelo de regresión lineal

Nos interesa entender cuáles son las variables que definen el estrato 
socioeconómico de una familia.

Podríamos empezar haciendo un modelo usando regresión paso a paso. O también,
usando las variables que tienen más correlación con el estrato socioeconómico.

```python
# Ajuste de datos 
formula = "ESTRATO ~ material_3 + fuente_agua_1 + TLOC + tipo_poblacion_U + \
        conexion_drenaje_1 + refrigerador + lavadora + auto_propio"
modelo_ols = ols(formula, encuesta_vivienda).fit()
```

{{% notice tip "Trivia"  %}}
¿Por qué no agregar tipo_poblacion_R también?
{{% /notice %}}

Con este modelo, estamos teorizando que el estrato depende de dichas variables. 
Inspeccionemos el modelo.

```python
# Revisar modelo
modelo_ols.summary()
```

Obtuvimos un modelo con un $R^2$ ajustado de 0.527. Adicionalmente, statsmodels
nos devuelve los parámetros $\beta_i$ con su respectivo intervalo de confianza,
y una prueba t sobre cada parámetro. 

{{% notice info "Prueba t en coeficientes de regresión"  %}}
La prueba t contrasta si el parámetro $\beta_i$ calculado es relevante para 
ajustar los datos o no. Las hipótesis están definidas como:

$$H_0: \beta_i = 0 $$
$$H_1: \beta_i \neq 0 $$

Asimismo, nos regresa los valores-p de dicha prueba. (¿Cuándo rechazábamos la 
hipótesis nula?)
{{% /notice  %}}


### Evaluación del modelo

Veamos qué tal predice nuestro modelo el estrato socioeconómico.

Para acceder a las predicciones de nuestro modelo, llamamos al método predict() 
del modelo de regresión.

```python
# Predicción del modelo
Y_pred = modelo_ols.predict()
```

Esta prediccion es un arreglo de NumPy, que es un tipo de datos optimizado
para contener matrices. 

Para evaluar nuestro modelo, tenemos que contrastar los valores observados de
la variable dependiente con los valores predecidos por el modelo. Para esto,
podemos crear un nuevo DataFrame conteniendo esta informacion como columnas.

He creado la siguiente función que se encargará de todo.

```python
# Una funcion para evaluar nuestro modelo
def model_evaluation(y_obs, y_pred):
    '''
    Esta función calculara las métricas RMSE y MAE de un modelo de regresión
    lineal.

    inputs:
    y_obs: una serie de pandas que contiene los valores observados
    de la variable dependiente 
    y_pred: un arreglo que contiene los valores predecidos
    de la variable dependiente utilizando el modelo de regresion de
    statsmodels

    output:
    model_eval: un dataframe de pandas que contiene los errores de
    regresion, asi como los valores observados y predecidos de la 
    variable dependiente. 
    '''

    # Convertir variable predecida a una serie
    y_pred = pd.Series(y_pred)

    # Concatenar valores en un solo dataframe
    model_eval = pd.concat([y_obs, y_pred], keys = ["y_obs", "y_pred"], axis = 1)
    
    # Calcular errores
    model_eval["error"] = model_eval["y_obs"] - model_eval["y_pred"]
    model_eval["sq_error"] = (model_eval["error"])**2
    model_eval["abs_error"] = abs(model_eval["error"])

    # Calculo de MAE y RMSE
    MAE = model_eval["abs_error"].sum()/model_eval["abs_error"].count()
    RMSE = (model_eval["sq_error"].sum()/model_eval["sq_error"].count())**(1/2)

    print("Métricas")
    print("MAE: {} \t RMSE: {}".format(MAE, RMSE))
    
    return model_eval
```

En esta función estamos concatenando ("juntando") las series usando 
[**concat()**](https://pandas.pydata.org/docs/reference/api/pandas.concat.html).

Después se calcularon 3 columnas de error. El error se define como la diferencia
del valor observado $y_i$ menos valor predecido $\hat{y}_i$.

- Error: $y_i - \hat{y}_i$
- Error cuadrado: $(y_i - \hat{y}_i)^2$
- Error absoluto: $| y_i - \hat{y}_i |$

Estos errores nos sirven para definir las siguientes métricas:

$$\text{MAE} = \frac{\sum_{i=1}^{N}| y_i - \hat{y}_i |}{N} \ \ \ \ \ \ \ \text{(Error absoluto medio)}$$

$$\text{RMSE} = \sqrt{\frac{\sum_{i=1}^{N}( y_i - \hat{y}_i )^2}{N}} \ \ \ \ \ \ \ \text{(Raíz del error cuadrático medio)}$$

Estas métricas son utilizadas para determinar la calidad del modelo de regresión
implementado.

Ahora usemos la función con nuestros datos.

```python
comparison = model_evaluation(encuesta_vivienda["ESTRATO"], modelo_ols.predict())
comparison
```

Esto nos devuelve el DataFrame con los valores observados, predecidos, errores e
imprime las métricas del modelo.

```
Métricas
MAE: 0.5490078148166975 	 RMSE: 0.7043990103948065
```

{{% notice tip "Trivia"  %}}
¿Qué nos dice cada métrica?
{{% /notice %}}

## Conclusión

Si bien la variable dependiente es una variable numérica, es una variable ordinal. 
Una regresión lineal asume que la variable dependiente es una variable númerica 
continua. Este ejercicio fue diseñado para demostrar como utilizar Python para
analizar datos, encontrar tendencias usando visualizaciones, e implementar un
modelo de regresión basándonos en estas tendencias.

Lo más correcto para estos datos sería implementar un modelo de regresión 
ordinal. Pero esos son otros temas de modelos de regresión generalizados... 

```python
# Aqui van tus comentarios ;)
```

## Referencias y material adicional

- Encuesta Nacional sobre Disponibilidad y Uso de Tecnologías de la Información
en los Hogares (ENDUTIH) 2019. INEGI. Disponible en:
https://www.inegi.org.mx/programas/dutih/2019/

- Modelos Lineales. Jesús Montanero Fernández. 
Disponible en: http://matematicas.unex.es/~jmf/Archivos/MODELOS_LINEALES.pdf

- Linear Regression - statsmodels. Josef Perktold, Skipper Seabold y Jonathan 
Taylor. Disponible en: https://www.statsmodels.org/stable/regression.html