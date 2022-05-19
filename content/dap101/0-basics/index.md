+++
title = "0. Primeros pasos"
description = "Introducción a VS Code y Jupyter notebooks"
disabletoc = false
weight = 1
tags = ["python", "VSCode", "Jupyter"]
+++

## Introducción

En esta sección se detallarán los pasos para empezar a trabajar con el material 
del curso usando VS Code y Jupyter notebooks.

Se asume que se han seguido los pasos detallados en 
[Instalación](/datlab/basics/configuration/) y 
[Configuración](/datlab/basics/configuration/).

## Guía de uso express 

### VS Code

La pantalla de inicio de VS Code es simple. En el lado izquierdo se encuentra el 
_ribbon_ con botones para trabajar. En el centro tenemos accesos directos a 
crear o abrir archivos, abrir carpetas o clonar repositorios. También tendremos 
la sección _Recent_ donde se verán los archivos o carpetas usados recientemente.

![Pantalla inicial VSCode](files/vscode_start.PNG?height=400px&width=700px)

En este curso y en general en nuestro camino en análisis de datos, necesitaremos
organizar nuestro trabajo. Para esto, podemos crear o usar una carpeta dedicada. 

#### Crear o abrir carpeta
   
Para crear/abrir una carpeta, usamos la opción **Open Folder...**

VSCode abrirá el Explorador de archivos. Navegamos hasta la carpeta donde
queramos guardar nuestro trabajo. En este caso, cree una carpeta llamada 
`example_folder` en Documentos.

![Open Folder VSCode](files/vscode_folder.PNG?height=350px&width=500px)

Seleccionamos esta carpeta con el botón **Select Folder**. Esto nos 
regresará a VSCode y veremos algo similar a esto.

![Explorer VSCode](files/vscode_explorer.PNG?height=250px&width=700px)

Aquí estamos en la vista **Explorer** de VSCode, donde podemos explorar lo 
que hay en la carpeta que elegimos del lado izquierdo de la ventana. Puesto 
que mi carpeta está vacía, (aún) no hay nada que mostrar.

#### Crear archivos

Una vez que VSCode ha abierto la carpeta donde queremos trabajar,
crearemos un archivo desde VSCode. Para esto, movamos el mouse a la parte
donde se ve el nombre de la carpeta, esto activará cuatro botones. Usaremos
el primer botón **New File**.

![New File VSCode](files/vscode_file.PNG?height=400px&width=550px)

Esto nos permitirá escribir el nombre del archivo. **Tip** No olvides 
escribir la extensión. En este caso, cree un archivo llamado `ejemplo.txt`.
Presionamos la tecla Enter y listo. 

![New File VSCode - name](files/vscode_file2.PNG?height=400px&width=550px)

Para editar el archivo, damos click en el nombre del archivo en el 
explorador. El archivo se abre como una pestaña en VS Code.

![New File VSCode - edit](files/vscode_file3.PNG?height=250px&width=700px)

### Jupyter notebooks

Jupyter es un entorno donde podemos interactuar con Python de una manera más 
sencilla. Con Jupyter podemos ejecutar bloques de código y agregar texto usando 
bloques **Markdown**. La extensión de los archivos es ***.ipynb**.

#### Crear Jupyter notebook
    
Podemos crear un notebook usando el mismo botón **New File**. En este caso, 
cree un archivo llamado `ejemplo.ipynb`. Presionamos la tecla Enter y listo. 
Al abrir el archivo, se mostrará la siguiente interfaz:

![Jupyter Notebook VSCode](files/vscode_jupyter.PNG?height=250px&width=670px)

#### Selección de kernel

Lo primero que tenemos que hacer es seleccionar el Kernel. Kernel es el 
intérprete de Python que Jupyter utilizará para ejecutar los bloques de
código. Damos click al botón **Select Kernel**. Esto nos mostrará la lista 
de intérpretes de Python instalados en nuestra máquina.

En mi caso, tengo varios intérpretes, pero elegiré el intérprete **base**, 
que es una distribución de Anaconda.

![Jupyter kernel](files/jupyter_kernel.png?height=180px&width=700px)

{{% notice tip %}}
El nombre del intérprete en tu máquina puede ser distinto, asegúrate de 
seleccionar el que sea una distribución de Anaconda. La ruta mostrada del 
intérprete debe contener la carpeta **anaconda3**.
{{% /notice %}}

#### Bloque Markdown

Markdown es un lenguaje de marcado simple para dar formato a un texto usando un 
editor de texto. Jupyter nos permite agregar bloques Markdown para describir 
nuestro trabajo y crear una experiencia similar a trabajar con una libreta de 
apuntes.

Creamos una celda Markdown usando el botón **+ Markdown**. Podemos ver que el 
bloque Markdown tiene escrito en la esquina inferior derecha la palabra 
**Markdown**.

![Markdown text](files/jupyter_markdown.PNG?height=200px&width=600px)

Para guardar lo que acabamos de escribir, damos click en el símbolo
<i class="fas fa-check"></i>, o usando el atajo `Ctrl+Enter`

Podemos agregar encabezados anteponiendo el símbolo **#** al texto.

![Markdown header](files/jupyter_markdown2.png?height=250px&width=600px)

{{% notice info "Más formatos"%}}
Copiemos el siguiente ejemplo en un bloque Markdown.

```markdown
# Encabezado 1

## Encabezado 2

### Encabezado 3

Este es un texto simple.

*Este es un texto en cursiva*

**Este es un texto en negrita**

***Este es un texto en negrita y cursiva***
```

Este es un ejemplo de los niveles de encabezados que podemos definir con 
Markdown. También podemos agregar énfasis al texto usando cursiva y negrita.

[The Markdown Guide](https://www.markdownguide.org/basic-syntax/) es una buena 
referencia para consultar la sintaxis y buenas prácticas de Markdown.
{{% /notice %}}
    
#### Bloque de código
   
Creamos un bloque de código usando el botón **+ Code**. Usaremos este tipo de 
bloque para los ejercicios de este curso. 

![Code cell](files/jupyter_code.PNG?height=200px&width=590px)

Podemos ver que este tipo de bloque tiene escrito en la esquina inferior 
derecha la palabra **Python**.

## Material adicional

- Markdown Basic Syntax. The Markdown Guide. Matt Cone. Disponible en:
https://www.markdownguide.org/basic-syntax/