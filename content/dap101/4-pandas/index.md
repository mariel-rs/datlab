+++
title = "4. Manejo de datos"
description = "Manejo de datos con pandas"
disabletoc = false
weight = 4
+++

## Ejercicios

## Datos

Para los ejercicios de este tema, usaremos los siguientes archivos:

{{% attachments title="Archivos" pattern=".*csv"/%}}

### Introducción

1. Creamos un Jupyter notebook como `pandas.ipynb` y creamos un cuadro con 
código. Analizaremos el archivo `inah_visitantes_2022.csv`.

Este archivo es especial por la presencia de tildes y porque usa , para separar
miles. Esto se puede hacer usando las keywords `encoding` y `thousands`, 
respectivamente. 

```python
import pandas as pd
import os # interfaces de sistemas operativos

# definir la ubicacion del archivo
path = os.path.join(os.getcwd(), "inah_visitantes_2022.csv")

# Método read_csv() para leer el CSV y procesarlo como dataframe
inah_visitantes2022 = pd.read_csv(path, thousands = ",", encoding = "latin-1")

# Miramos lo que contiene el dataframe
inah_visitantes2022
```

```python
# ver solo las primeras n filas
inah_visitantes2022.head(5)
```

#### Dimensiones

Para inspeccionar las dimensiones de los datos importados, usamos el método `shape`
```python
# Dimensiones
inah_visitantes2022.shape
```

Esto nos devuelve una tupla (277, 10) que contiene el numero de (filas, columnas)
que tienen estos datos. 

#### Columnas
Para inspeccionar el nombre de las columnas, usamos el método `columns`

```python
# Columnas
inah_visitantes2022.columns
```

### Ordenar datos

1. Ordenar por una columna, en orden ascendente

```python
# Ordenar por una sola columna, "enero_nac". ascending = True por defecto
inah_visitantes2022.sort_values(by=['enero_nac'])
```

2. Ordenar por dos columnas, en orden descendente

```python
# Ordenar por "enero_nac, febrero_nac" en orden descendente
inah_visitantes2022.sort_values(by=['enero_nac', 'febrero_nac'], ascending = False)
```
### Series

Podemos crear un DataFrame más pequeño sólo con algunas columnas.

```python
# Un dataframe con datos nacionales
inah_visitantes_nac = inah_visitantes2022[["Centro INAH", "enero_nac", "febrero_nac", "marzo_nac"]]

# Mostrar 5 primeras filas
inah_visitantes_nac.head(5)
```

Series - Arreglo unidimensional de datos

```python
# Una serie con los datos de los centros INAH
centros_inah = inah_visitantes2022["Centro INAH"]
centros_inah
```

```python
# Series pueden ser convertidas a lista
enero_nac = inah_visitantes2022["enero_nac"].to_list()
```

### Estadística descriptiva

#### DataFrame
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

#### Serie

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

### Selección de datos

#### Condicionales

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
df[(df["columna"] condición1) operador_lógico df["columna"] condición2) ... ]
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

#### Ver valores por su label, o utilizando con condiciones, .loc[ ]

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

#### Ver valores por índices, .iloc[ ]

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

### Agrupación de datos

```python
# Sintaxis
df.groupby(by = "columna").funcion()
```

La funcion puede ser:
- count() – Conteo
- sum() – Suma
- mean() – Media
- median() – Mediana
- min() – Valor minimo
- max() – Valor maximo
- std() – Desviacion tipica
- var() – Varianza

```python
# Agrupar datos por estado, sumando valores
inah_visitantes2022.groupby(by = "Estado").sum()
```


## Tarea

Usando los datos en `estudiantes_mxuk2021.csv`, realizar los siguientes 
ejercicios. Puedes utilizar un jupyter notebook.

1. ¿Cuántos estudiantes de Puebla estudian un posgrado?
2. ¿Cuál es la edad promedio de los estudiantes que estudian un posgrado?
3. Seleccionar los registros que satisfagan las siguientes condiciones:
   1. Estudiantes mayores de 27 años y que no son de CDMX
   2. Estudiantes menores de 28 años y, que estudian en University of York y en University of Sussex
4. Calcular (tal vez sea útil usar _groupby_):
   1. Número de estudiantes por universidad
   2. Número de estudiantes por estado
   3. ¿Cuál es la universidad con más estudiantes mexicanos?

{{% notice info "Fuentes de datos" %}}
1. Visitantes a museos y zonas arqueologicas abiertas al publico. https://datos.gob.mx/busca/dataset/visitantes-a-museos-y-zonas-arqueologicas-abiertas-al-publico

2. Estudiantes de posgrado en el Reino Unido en 2021. Sin publicar

Sitios mayas
https://www.kaggle.com/datasets/ujwalkandi/archaeological-sites-with-maya-inscriptions

{{% /notice %}}

