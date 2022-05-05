+++
title = "5. Visualización"
description = "Creación de gráficos y visualizaciones con matplotlib y seaborn"
disabletoc = false
weight = 5
tags = ["visualizaciones", "matplotlib", "seaborn", "pandas"]
+++

## Introducción

La información que hemos procesado previamente se puede visualizar usando
gráficos. En esta sección veremos como crear gráficos profesionales con 
matplotlib y seaborn.

**Datos**

Usaremos los siguientes archivos para los ejercicios de este tema:

{{% attachments style="blue" title="Archivos" pattern=".*(csv|txt)"/%}}

**Librerías**

Usaremos las siguientes librerías para los ejercicios de este tema:

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

plt.rcParams["figure.figsize"] = (10,8) # Definicion de tamaño en pulgadas
```

**Descripción de datos**

Estos son datos abiertos de aspirantes a posgrados ofrecidos en el Instituto de 
Ecología, A.C. (INECOL). La descripción de las columnas es la siguiente:

| Columna | Tipo de dato | Descripción |
| -------- | ------------- | ---------------------|
| id_aspirante | Numérico | Número de identificación interno asignado al aspirante |
| calificacion_ingles | Numérico | Calificación obtenida en prueba de inglés. Escala 0 - 10 |
| calificacion_conocimientos_tecnicos | Numérico | Calificación obtenida en prueba conocimientos técnicos. Escala 0 - 10  |
| entrevista | Numérico | Calificación obtenida en entrevista. Escala 0 - 10  |
| desempeno_academico | Numérico | Calificación obtenida por desempeño académico. Escala 0 - 10  |
| calificacion_final | Numérico | Calificación final asignada al aspirante. Escala 0 - 10  |
| resultado | Texto | Resultado del proceso de admisión |

## matplotlib

matplotlib es una librería de bajo nivel, es decir, necesitamos definir muchas
cosas, pero tendremos más libertad y flexibilidad en nuestros gráficos. 
Revisaremos las gráficas de dispersión en este paquete.  

### Dispersión

Vamos a utilizar datos artificiales de una variable `x`, y creamos dos funciones 
de `x`.

```python
import numpy as np # Libreria para acceder a funciones matematicas

x = np.linspace(-3, 3, 100) # crear 100 valores en un rango -3 a 3
y1 = 3*x
y2 = x**3 + x**2 - x + 1

# Crear un grafico con ambas curvas en el mismo eje
fig, ax = plt.subplots()
ax.plot(x, y1, 'g--', label=r'$y_1$') # Trazos
ax.plot(x, y2, 'y.', label=r'$y_2$') # Puntos

# .legend() utiliza el argumento "label" para cada curva
ax.legend(loc='lower right', fontsize=14)

# Mostrar el grafico
plt.show()
```

## seaborn

seaborn es una librería basada en matplotlib, pero es de alto nivel. Es decir,
no tendremos que escribir tanto para crear gráficos.

Ahora usaremos los datos de aspirantes a posgrado de INECOL, que están en el 
archivo `aspirantes_inecol2020.csv`. 

```python
# Importar datos aspirantes INECOL
inecol_df = pd.read_csv("aspirantes_inecol2020.csv")
```

### Pairplot

Este gráfico nos puede server para encontrar relaciones entre variables y como
primer paso en nuestro análisis de datos. 

```python
# Dale unos segundos...
sns.pairplot(inecol_df)
```

### Gráfico de dispersión

En lugar de escribir un montón de código, seaborn tiene un método que simplifica
esta tarea. Al ser un gráfico de dispersión, no une los puntos.

```python
# Dispersion
sns.scatterplot(data = inecol_df, x = "calificacion_ingles", y = "calificacion_final")
```

### Gráfico de línea

Este gráfico es similar al de dispersión, pero en este gráfico, seaborn une los
puntos. Debido a que las medidas pueden ser ruidosas, seaborn estima la
tendencia central de los datos y es lo que nos muestra trazado en una línea. 
Además, muestra el intervalo de confianza de 95% de dicha tendencia.

```python
# Lineplot
sns.lineplot(data = inecol_df, x = "calificacion_ingles", y = "calificacion_final")
```

Esta gráfica puede graficar la desviación típica, en lugar del intervalo de 
confianza, usando el argumento `ci = "sd"`, o no mostrar nada con `ci = None`.

### Histograma

```python
# Sintaxis
sns.histplot(data = df, x = "columna", stat, kde)
```

Un ejemplo de un histograma utilizando porcentaje como medida estadística.

```python
sns.histplot(data = inecol_df, x = "calificacion_final", stat = "percent")
```

La medida estadística `stat` utilizada en el eje puede ser:

- `count`: número de observaciones en cada segmento
- `frequency`: muestra el número de observaciones dividido entre el "ancho" (intervalo) del segmento
- `probability`: normaliza el eje para que la altura de las barras sumen 1
- `percent`: normaliza el eje para que la altura de las barras sumen 100
- `density`: normaliza el eje para que el total del área del histograma sea 1

`kde` es un parámetro opcional donde podemos obtener una distribución estimada
de los datos. Para activarlo pasamos el siguiente argumento cuando creemos el 
objeto histoplot: `kde = True`

### Diagramas de caja y bigotes (boxplot)

Muestra la distribución de datos cuantitativos utilizando sus medidas de
localización.

```python
# Ver la distribución de calificaciones finales de los aspirantes con boxplot
# (Se ve mejor así, que si invirtieramos los ejes...)
sns.boxplot(data = inecol_df, y = "resultado", x = "calificacion_final", whis = 1.5)
```

`whis` es un parámetro opcional que define la extensión de los "bigotes" de las
cajas, respecto al rango intercuartílico. En el ejemplo de arriba, 1.5 es 1.5 
veces el rango intercuartílico.

### Diagrama de violín

Visualización combinada de un diagrama de cajas y de la distribución estimada de
los datos.

```python
# Ver la distribución de calificaciones finales de los aspirantes con violinplot
sns.violinplot(data = inecol_df, y = "resultado", x = "calificacion_final")
```

### Gráfico de barras

Podemos agrupar los datos usando la columna "resultado", contando el número de 
registros.

```python
# Agrupar por Resultado y recrear el indice
inecol_resultado = inecol_df.groupby(by = "resultado").count()

# Recrear el indice para que "resultado" no sea indice
inecol_resultado = inecol_resultado.reset_index()
```

{{% notice info "¿Por qué reset_index()?" %}}
Al agrupar los valores con groupby(), la columna usada como argumento de `by` se 
convierte en el índice del DataFrame compacto. 

Si deseamos que el índice sea numérico y no la columna, la función 
[**reset_index()** ](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html)
nos sirve para recrear el índice numérico.
{{% /notice %}}

```python
# Gráfico de barras resumiendo el resultado final de aspirantes
sns.barplot(data = inecol_resultado, y = "resultado", x = "calificacion_final")
```

Usando los datos del INAH, creemos un gráfico de barras el número de centros 
INAH por estado.

```python
# Usando los datos de visitantes a los centros INAH en 2022
inah_df = pd.read_csv("inah_visitantes_2022.csv")

# Agrupando por estado y usando la función count()
inah_grouped = inah_df.groupby(by = "Estado").count()
inah_grouped = inah_grouped.reset_index() # Para que Estado no sea índice/label

# Mostrar grafico
sns.barplot(data = inah_grouped, x = "Tipo", y = "Estado")
```

{{% notice tip "Histograma vs gráfico de barras" %}}
Ambos gráficos parecen iguales, ambos usan barras, pero no son lo mismo.

Un histograma es un diagrama que muestra la frecuencia de datos numéricos,
mientras que el gráfico de barras compara tamaños de diferentes variables 
categóricas.
{{% /notice %}}

## Edición de gráficos

Modificar etiquetas de los ejes y exportar imagen como PNG.

```python
# Declarar el grafico
ax = sns.barplot(data = inah_grouped, x = "Tipo", y = "Estado")

# Modificar las etiquetas de los ejes
ax.set_xlabel("Estado", fontsize = 12)
ax.set_ylabel("Número de Centros INAH", fontsize = 12)

# Ajustes para exportar imagen
plt.tight_layout()
plt.savefig('barplot_inah.png')

# Mostrar imagen
plt.show()
```

Girar ejes para mejorar la visualización.

```python
# Misma boxplot de calificaciones de INECOL pero ahora los ejes invertidos
sns.boxplot(data = inecol_df, x = "resultado", y = "calificacion_final", whis = 1.5)

# Rotamos las etiquetas del eje x, 45 grados
plt.xticks(rotation=45)

plt.show()
```

## Ejercicios

1. Usando los datos `estudiantes_mxuk.csv`, crear gráficos que muestren:
   - Distribución de edad por universidad. 
   - Becas que tienen los estudiantes.

2. Usando los datos `inah_visitantes_2022.csv`:
   - ¿Cuál es la visualización más representativa para mostrar el flujo de
   visitantes en los meses reportados para un Centro INAH (o estado!) 
   determinado?

## Referencias y material adicional

- Visitantes a museos y zonas arqueologicas abiertas al público. Datos abiertos 
de México. Disponible en: 
https://datos.gob.mx/busca/dataset/visitantes-a-museos-y-zonas-arqueologicas-abiertas-al-publico

- Selección de aspirantes. Datos abiertos de México. Disponible en: 
https://datos.gob.mx/busca/dataset/seleccion-de-aspirantes

- Estudiantes de posgrado en el Reino Unido. Sin publicar.

- The Python graph gallery. Disponible en: https://python-graph-gallery.com/

- seaborn documentation. Michael Waskom. Disponible en: 
https://seaborn.pydata.org/