+++
title = "4. Manejo de datos"
description = "Manejo de datos con pandas"
disabletoc = false
weight = 5
tags = ["pandas"]
+++

## Introducción

pandas es la librería de Python más utilizada para procesar datos. pandas puede
leer datos de archivos CSV, JSON, txt, xls, xlsx, entre otros. La estructura de 
datos más común de esta librería es DataFrame, que es una estructura de datos 
tabular bidimensional con ejes etiquetados (filas y columnas).

**Datos**

Usaremos los siguientes archivos para los ejercicios de este tema:

{{% attachments style="blue" title="Archivos" pattern=".*(csv|txt)"/%}}

## Primeros pasos

Creamos un Jupyter notebook y creamos un cuadro con código. Analizaremos el 
archivo `inah_visitantes_2022.csv`.

Este archivo contiene la información de visitantes a museos y zonas arqueológicas
manejadas por el INAH durante el año 2022. La descripción de las columnas es la 
siguiente:

| Variable | Tipo de variable | Descripción |
| -------- | ------------- | ---------------------|
| Estado | Cadena de texto | Estado de la República donde se encuentra el centro INAH |
| Clave_SIINAH | Numérica | Clave interna asociada al centro INAH |
| Tipo | Cadena de texto | Tipo de centro. Z.A. - Zona arqueológica. M. M.H. - Museo o Museo histórico |
| Centro_INAH | Cadena de texto | Nombre del centro INAH |
| Enero_nac | Numérica | Número de visitantes nacionales en el mes de enero |
| Enero_ext | Numérica | Número de visitantes extranjeros en el mes de enero |
| Febrero_nac | Numérica | Número de visitantes nacionales en el mes de febrero |
| Febrero_ext | Numérica | Número de visitantes extranjeros en el mes de febrero |
| Marzo_nac | Numérica | Número de visitantes nacionales en el mes de marzo |
| Marzo_ext | Numérica | Número de visitantes extranjeros en el mes de marzo |

### Importar datos

Importamos el CSV usando el método 
[**read_csv()**](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html). 
El nombre del archivo debe ir entre comillas.

```python
import pandas as pd

# Leer el CSV y procesarlo como dataframe
inah_visitantes2022 = pd.read_csv("inah_visitantes_2022.csv")
```

`inah_visitantes2022` es un objeto DataFrame que contiene los datos de este CSV.

Podemos ver lo que contiene el dataframe:

```python
# Miramos lo que contiene el dataframe
inah_visitantes2022
```

### head or tail

Ver sólo ver las primeras _n_ filas con el método 
[**head()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.head.html). 
O las últimas _n_ filas con el método [**tail()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.tail.html).

```python
# ver las primeras 5 filas
inah_visitantes2022.head(5)
```

```python
# ver las últimas 5 filas
inah_visitantes2022.tail(5)
```

### Resumen general

El método [**info()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.info.html) 
muestra información general del DataFrame como el tipo de datos que contiene la
columna, conteo de valores no nulos y uso de memoria.

```python
# Informacion general
inah_visitantes2022.info()
```

### Dimensiones

Para inspeccionar las dimensiones de los datos importados, usamos el atributo 
[**shape**](https://pandas.pydata.org/pandas-docs/version/1.3.0/reference/api/pandas.DataFrame.shape.html).

```python
# Dimensiones
inah_visitantes2022.shape
```

Esto nos devuelve una tupla (277, 10) que contiene el numero de (filas, columnas)
de este DataFrame. 

### Columnas

Para inspeccionar el nombre de las columnas, usamos el atributo 
[**columns**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.columns.html).

```python
# Columnas
inah_visitantes2022.columns
```

### Ordenar datos

Podemos ordenar datos usando el método 
[**sort_values()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html).

En el siguiente ejemplo, ordenamos por una columna, en orden ascendente.

```python
# Ordenar por una sola columna, "enero_nac". ascending = True por defecto
inah_visitantes2022.sort_values(by=['enero_nac'])
```

También podemos ordenar por más de una columna, en orden descendente.

```python
# Ordenar por "enero_nac, febrero_nac" en orden descendente
inah_visitantes2022.sort_values(by=['enero_nac', 'febrero_nac'], ascending = False)
```

## DataFrame vs Series

### Selección de columnas
Podemos crear un DataFrame más pequeño sólo con algunas columnas.

```python
# Un dataframe con datos nacionales
inah_visitantes_nac = inah_visitantes2022[["Centro INAH", "enero_nac", "febrero_nac", "marzo_nac"]]

# Mostrar 5 primeras filas
inah_visitantes_nac.head(5)
```

### Series

Una serie es un arreglo unidimensional de datos (vector columna).

```python
# Una serie con los datos de los centros INAH
centros_inah = inah_visitantes2022["Centro INAH"]
centros_inah
```

```python
# Series pueden ser convertidas a lista
enero_nac = inah_visitantes2022["enero_nac"].to_list()
```

## Estadística descriptiva

### DataFrame

Accedemos a las siguientes medidas descriptivas de los datos usando el método 
[**describe()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.describe.html):

- Conteo
- Media
- Desviación típica
- Valor mínimo
- Primer cuartil (25%)
- Segundo cuartil o mediana (50%)
- Tercer cuartil (75%)
- Valor máximo

```python
# Mostrar estadistica descriptiva de un DataFrame
inah_visitantes2022.describe()
```

### Series

Para una serie con valores numéricos, se reportan las mismas medidas que en un
DataFrame. Pero para una serie con valores de texto, se reportan:

- Conteo
- Valores únicos
- Top (Valor más frecuente)
- Frecuencia

```python
# Mostrar estadistica descriptiva de una Serie
inah_visitantes2022["Estado"].describe()
```

## Operaciones

Hemos visto hasta ahora como importar datos y ver sus medidas de estadística
descriptiva, pero también podemos realizar operaciones con los DataFrames.

### Crear columnas

Crear columnas es tan simple como declarar el nombre de la columna y los valores
que queremos guardar en esta columna. 

Por ejemplo, creemos la columna "prueba_columna" en el DataFrame de visitantes
a centros INAH. Le asignaremos a esta columna un valor arbitrario.

```python
inah_visitantes2022["prueba_columna"] = 1
```

Lo que hizo este instrucción fue crear la columna y asignar a todas las filas el
valor de 1. Pero, también podemos crear columnas usando valores de otras columnas 
usando operaciones matemáticas. 

Creemos una nueva columna llamada `enero_visitantes` que contenga la suma de
todos los visitantes (tanto nacionales como extranjeros) de cada centro INAH en
el mes de enero. 

```python
# enero_visitantes es la suma de visitantes nacionales y visitantes extranjeros
inah_visitantes2022["enero_visitantes"] = inah_visitantes2022["enero_nac"] + inah_visitantes2022["enero_ext"]
```

### Eliminar columnas

Para eliminar columnas innecesarias o que fueron creadas por error, se puede 
hacer con el método 
[**drop()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop.html).

La sintaxis es la siguiente:

```python
df = df.drop(columns)
```

donde el argumento `columns` puede aceptar un valor único con el nombre de la 
columna, o una lista con los nombres de columnas a eliminar.

Para eliminar la columna que acabamos de crear, introducimos la siguiente
instrucción:

```python
inah_visitantes2022 = inah_visitantes2022.drop(columns = "prueba_columna")
```

### Crear columnas usando funciones

Para usar una función basada en una columna podemos usar el método 
[**map()**](https://pandas.pydata.org/docs/reference/api/pandas.Series.map.html).

La sintaxis es la siguiente:

```python
# Sintaxis de map
df['nueva_col'] = df['col'].map(funcion)
```

Tenemos la siguiente función que escribe una cadena de texto si la columna tiene
valores de 0 o distintos de 0.

```python
def test_function(col):

    if col == 0:
        col = "No visitantes"
    else:
        col = "Visitantes"

    return col
```

Usemos map para aplicar esta función a una nueva columna "respuesta".

```python
inah_visitantes2022["respuesta"] = inah_visitantes2022["enero_nac"].map(test_function)
inah_visitantes2022.head()
```

{{% notice info %}}
Si la función es más compleja y requiere más de una columna, está el método 
[**apply()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.apply.html).
{{% /notice %}}

## Selección de datos

Podemos hacer una selección de datos del DataFrame, dependiendo si queremos ver 
un subconjunto que satisfaga una o más condiciones, o la ubicación dentro del 
DataFrame.

### Condicionales

1. Una condición

```python
# Sintaxis
df[df["columna"] condición]

```
donde la condición puede ser una igualdad `==`, diferente de `!=`, mayor o igual
`>=`, menor o igual `<=`, estrictamente mayor `>` o estrictamente menor `<`.

```python
# Mostrar datos solo para el estado Guerrero
inah_visitantes2022[inah_visitantes2022["Estado"] == "Guerrero"]
```

```python
# Mostrar centros con más de 1000 visitantes nacionales en enero
inah_visitantes2022[inah_visitantes2022["enero_nac"] >= 10000]
```

2. Múltiples condiciones

```python
# Sintaxis
df[(df["columna"] condición1) operador_lógico (df["columna"] condición2) ... ]
```

donde el operador lógico puede ser `&` (operador "y") o `|` (operador "o")

```python
# Mostrar los centros con más de 1000 visitantes nacionales en Guerrero
inah_visitantes2022[(inah_visitantes2022["Estado"] == "Guerrero") & (inah_visitantes2022["enero_nac"] > 1000)]
```

1. Múltiples valores a comparar de una misma columna

El método [**isin()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.isin.html) 
nos permite utilizar una lista para comparar valores.

```python
# Sintaxis
df[df["columna"].isin(lista)]
```

Mostrar los centros con más de 1000 visitantes nacionales en Guerrero y Quintana 
Roo en el mes de marzo.

```python
# Seleccion de centros en Guerrero y Quintana Roo usando el metodo isin
inah_visitantes2022[(inah_visitantes2022["Estado"].isin(["Guerrero", "Quintana Roo"])) & (inah_visitantes2022["marzo_nac"] > 1000)]
```

4. Query

Cuando se tiene más de una condición, 
[**query()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.query.html) 
puede ser más elegante.

```python
# Sintaxis
df.query('expresion')
```

Para seleccionar los datos de centros INAH del estado de Guerrero con visitantes
nacionales en enero mayores o igual a 1000, podriamos escribirlo como en el
ejemplo 2, o usando query:

```python
# Seleccion usando query
inah_visitantes2022.query('Estado == "Guerrero" & enero_nac >= 1000')
```

### Ver valores por su label, o utilizando con condiciones, .loc

[**loc**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html) es
una propiedad que nos permite ver valores usando el label (o índice) de las filas,
o usar condiciones para generar vistas.

```python
# Vistas por condiciones. Tambien se pueden definir cuantas columnas mostrar
inah_visitantes2022.loc[inah_visitantes2022["Estado"] == "Guerrero", ["enero_nac", "febrero_nac"]]
```

Parece igual...

```python
# Un DataFrame con labels en lugar de indices
df_label = pd.DataFrame([[1, 2], [4, 5], [7, 8]],
     index=['cobra', 'viper', 'sidewinder'],
     columns=['max_speed', 'shield'])
```

```python
# loc, vistas por label
df_label.loc["cobra"]
```

### Ver valores por índices, .iloc

[**iloc**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.iloc.html)
es una propiedad que nos permitirá acceder a filas y columnas usando sus índices.

```python
# Sintaxis general
df.iloc[fila_a: fila_b, columna_a: columna_b]
```

1. Una fila

```python
# Primera fila, una serie
inah_visitantes2022.iloc[0] 

# Primera fila, pero un dataframe
inah_visitantes2022.iloc[[0]] 
```

2. Más de una fila, en desorden
   
```python
# Más de una fila, en distinto orden
inah_visitantes2022.iloc[[7, 2, 0]]
```

3. Celdas

```python
# Celda ubicada en la fila 0, columna 3
inah_visitantes2022.iloc[0,3] 
```

4. Mostrar una selección de filas, en orden. 
```python
# Mostrar las filas 0, 1 y 2
inah_visitantes2022.iloc[0:3]
```

5. Mostrar selección de filas y de columnas

```python
# Mostrar las primeras (0:2) filas, las primeras 3 columnas (0:3)
inah_visitantes2022.iloc[0:2,0:3]
```

## Agrupación de datos

[**groupby()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html) 
es un método que permite agrupar datos por columnas y crear un DataFrame más 
compacto.

La sintaxis de este método es:

```python
# Sintaxis
df.groupby(by = "nombre_columna").funcion()
```

Se requiere que definamos una función para que pandas pueda aplicar una 
operación matemática para presentar los valores agrupados. La función puede ser:

- count() – Conteo
- sum() – Suma
- mean() – Media
- median() – Mediana
- min() – Valor mínimo
- max() – Valor máximo
- std() – Desviación tipica
- var() – Varianza

Agrupemos los datos de visitantes a centros INAH usando la columna estado, 
sumando los valores.

```python
# Agrupar datos por estado, sumando valores
inah_visitantes2022.groupby(by = "Estado").sum()
```

## Remodelación usando "Melt"

A veces necesitaremos de "masajear" un DataFrame para convertir de un formato
ancho a un formato largo. Esto se logra con el método 
[**melt()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.melt.html).
Este tipo de remodelación de DataFrames es de utilidad cuando se tienen una o 
más columnas que pueden ser usadas como identificadores, y las demás columnas 
como valores.

```python
# Remodelando el df
pd.melt(inah_visitantes2022)
```

## Ejercicios

Usando los datos en `estudiantes_mxuk.csv`, contestar las siguientes 
preguntas.

1. ¿Cuántos estudiantes de Puebla estudian un posgrado?
2. ¿Cuál es la edad promedio de los estudiantes que estudian un posgrado?
3. Seleccionar los registros que satisfagan las siguientes condiciones:
   - Estudiantes mayores de 27 años y que no son de CDMX.
   - Estudiantes menores de 28 años y, que estudian en University of York y en 
      University of Sussex.
4. Calcular (tal vez sea útil usar `groupby()`):
   - Número de estudiantes por universidad
   - Número de estudiantes por estado
   - ¿Cuál es la universidad con más estudiantes mexicanos?

## Referencias
- Visitantes a museos y zonas arqueologicas abiertas al público. Datos abiertos
de México. Disponible en: 
https://datos.gob.mx/busca/dataset/visitantes-a-museos-y-zonas-arqueologicas-abiertas-al-publico

- Estudiantes de posgrado en el Reino Unido. Sin publicar.

- Filtrado y uso de query con pandas en Python. Naps Tecnología y educación.
Disponible en: https://naps.com.mx/blog/uso-de-query-con-pandas-en-python/

- Pandas I. Curso Ciencia de Datos con Python CIDE. Disponible en: 
https://rafneta.github.io/CienciaDatosPythonCIDE/Laboratorios/Lab9/PandasI.html

- pandas documentation. the pandas development team. Disponible en: 
https://pandas.pydata.org/pandas-docs/stable/ 

- How to use iloc and loc for indexing and slicing pandas dataframes. Marsja.
Disponible en: https://www.marsja.se/how-to-use-iloc-and-loc-for-indexing-and-slicing-pandas-dataframes/