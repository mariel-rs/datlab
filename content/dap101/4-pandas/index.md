+++
title = "4. Manejo de datos"
description = "Manejo de datos con pandas"
disabletoc = false
weight = 4
tags = ["pandas"]
+++


## Introducción

pandas es la librería de Python más utilizada para procesar datos. pandas puede
leer datos de archivos CSV, xls, xlsx, json, entre otros. La estructura de datos 
más común de esta librería es DataFrame, que es una estructura de datos tabular 
bidimensional con ejes etiquetados (filas y columnas).

**Datos**

Usaremos los siguientes archivos para los ejercicios de este tema:

{{% attachments title="Archivos" pattern=".*csv"/%}}

## Primeros pasos

Creamos un Jupyter notebook como `pandas.ipynb` y creamos un cuadro con 
código. Analizaremos el archivo `inah_visitantes_2022.csv`.

Este archivo es especial porque usa comas para separar miles. pandas puede 
procesar esto usando la keywords `thousands`. 

### Importar datos

Importamos el CSV usando el método `read_csv`. El nombre del archivo debe ir
entre comillas.

```python
import pandas as pd

# Método read_csv() para leer el CSV y procesarlo como dataframe
inah_visitantes2022 = pd.read_csv("inah_visitantes_2022.csv", thousands = ",")
```

`inah_visitantes2022` es un objeto DataFrame que contiene los datos de este CSV.

Podemos ver lo que contiene el dataframe:

```python
# Miramos lo que contiene el dataframe
inah_visitantes2022
```

### head or tail

Ver sólo ver las primeras _n_ filas con el método `head`. O las últimas _n_ 
filas con el método `tail`.

```python
# ver solo las primeras 5 filas
inah_visitantes2022.head(5)
```

### Resumen general

El método `info` muestra información general del DataFrame como el tipo de datos
por columna, conteo de valores no nulos y uso de memoria.

```python
# Informacion general
inah_visitantes2022.info()
```

### Dimensiones

Para inspeccionar las dimensiones de los datos importados, usamos el método 
`shape`

```python
# Dimensiones
inah_visitantes2022.shape
```

Esto nos devuelve una tupla (277, 10) que contiene el numero de (filas, columnas)
que tienen estos datos. 

### Columnas

Para inspeccionar el nombre de las columnas, usamos el método `columns`

```python
# Columnas
inah_visitantes2022.columns
```

### Ordenar datos

Ordenar por una columna, en orden ascendente.

```python
# Ordenar por una sola columna, "enero_nac". ascending = True por defecto
inah_visitantes2022.sort_values(by=['enero_nac'])
```

Ordenar por dos columnas, en orden descendente.

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

Accedemos a las medidas descriptivas de los datos usando el método describe()
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

## Selección de datos

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
# Mostrar centros con mas de 1000 visitantes nacionales en enero

inah_visitantes2022[inah_visitantes2022["enero_nac"] >= 10000]
```

2. Múltiples condiciones

```python
# Sintaxis
df[(df["columna"] condición1) operador_lógico (df["columna"] condición2) ... ]
```

donde el operador lógico puede ser `&` (operador "y") o `|` (operador "o")

```python
# Mostrar los centros con mas de 1000 visitantes nacionales en Guerrero
inah_visitantes2022[(inah_visitantes2022["Estado"] == "Guerrero") & (inah_visitantes2022["enero_nac"] > 1000)]
```

3. Método isin para múltiples valores a comparar de una misma columna

```python
# Sintaxis
df[df["columna"].isin(lista)]
```

Mostrar los centros con mas de 1000 visitantes nacionales en Guerrero y Quintana Roo en el mes de marzo

```python
# Seleccion de centros en Guerrero y Quintana Roo usando el metodo isin
inah_visitantes2022[(inah_visitantes2022["Estado"].isin(["Guerrero", "Quintana Roo"])) & (inah_visitantes2022["marzo_nac"] > 1000)]
```

4. Método query

Cuando se tienen más de una condición, query puede ser más elegante

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
# Mas de una fila, en distinto orden
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

```python
# Sintaxis
df.groupby(by = "columna").funcion()
```

La función puede ser:

- `count` – Conteo
- `sum` – Suma
- `mean` – Media
- `median` – Mediana
- `min` – Valor mínimo
- `max` – Valor máximo
- `std` – Desviación tipica
- `var` – Varianza

```python
# Agrupar datos por estado, sumando valores
inah_visitantes2022.groupby(by = "Estado").sum()
```

## Remodelación usando "Melt"

A veces necesitaremos de "masajear" un DataFrame para convertir de un formato
ancho a un formato largo. Es de utilidad cuando se tienen una o más columnas que
pueden ser usadas como identificadores, y las demás columnas como valores.

```python
# Remodelando el df
pd.melt(inah_visitantes2022)
```

## Ejercicios

Usando los datos en `estudiantes_mxuk2021.csv`, realizar los siguientes 
ejercicios. Puedes utilizar un jupyter notebook.

1. ¿Cuántos estudiantes de Puebla estudian un posgrado?
2. ¿Cuál es la edad promedio de los estudiantes que estudian un posgrado?
3. Seleccionar los registros que satisfagan las siguientes condiciones:
   - Estudiantes mayores de 27 años y que no son de CDMX
   - Estudiantes menores de 28 años y, que estudian en University of York y en University of Sussex
4. Calcular (tal vez sea útil usar `groupby`):
   - Número de estudiantes por universidad
   - Número de estudiantes por estado
   - ¿Cuál es la universidad con más estudiantes mexicanos?

{{% notice tip "Referencias" %}}
- Visitantes a museos y zonas arqueologicas abiertas al público. Datos abiertos
de México. Disponible en: 
https://datos.gob.mx/busca/dataset/visitantes-a-museos-y-zonas-arqueologicas-abiertas-al-publico

- Estudiantes de posgrado en el Reino Unido en 2021. Sin publicar.

- Filtrado y uso de query con pandas en Python. Naps Tecnología y educación.
Disponible en: https://naps.com.mx/blog/uso-de-query-con-pandas-en-python/

- Pandas I. Curso Ciencia de Datos con Python CIDE. Disponible en: 
https://rafneta.github.io/CienciaDatosPythonCIDE/Laboratorios/Lab9/PandasI.html

- loc vs iloc pandas. Analytics Vidhya. Disponible en: 
https://www.analyticsvidhya.com/blog/2020/02/loc-iloc-pandas/

- pandas documentation. the pandas development team. Disponible en: 
https://pandas.pydata.org/pandas-docs/stable/ 

- How to use iloc and loc for indexing and slicing pandas dataframes. Marsja.
Disponible en: https://www.marsja.se/how-to-use-iloc-and-loc-for-indexing-and-slicing-pandas-dataframes/
{{% /notice %}}