---
title: Instalación (Windows)
weight: 15
disableToc: false
---

Aquí se detallan los pasos para la instalación de los programas sugeridos en la 
sección de [Prerrequisitos](../requirements/). Las recomendaciones mostradas
aquí son válidas para computadoras con sistema operativo **Windows**. 
Afortunadamente macOS y Linux son mucho más simples para instalar y configurar, 
aunque puedes usar el orden sugerido.

En matemáticas, el orden de los factores no altera la suma ni el producto.
Desafortunadamente, aquí sí afecta el orden de instalación :( Para evitar 
modificar [variables de entorno](https://es.wikipedia.org/wiki/Variable_de_entorno) 
posteriormente (y a mano), recomiendo el siguiente orden:

1. Notepad++
2. Anaconda
3. VSCode
4. Git (**Sólo si se necesita usar control de versiones**)

### Notepad++

 Notepad++ es muy rápido de instalar y no causa problemas. Con seguir los pasos 
de la instalación es suficiente. <i class="fas fa-smile"></i>

### Anaconda

En algún punto de la instalación de Anaconda, veremos las opciones avanzadas:

![Opciones Anaconda](https://docs.anaconda.com/_images/win-install-options.png?height=300px&width=400px)

Encarecidamente recomiendo **activar** la casilla "Add Anaconda3 to my PATH 
environment variable". Aunque el instalador dice que no es recomendable, es la 
mejor opción para que VSCode encuentre a Anaconda.

### VSCode

Esta instalación es muy amigable. Sólo recomiendo revisar que la casilla "Add to 
PATH" esté activada.

![Opciones VSCode](images/vscode_options.png?height=300px&width=400px)

### Git

Cuando instalemos Git, el instalador pedirá seleccionar el editor de texto
predeterminado. En la lista desplegable, elegir Notepad++ (Aquí es una de las 
razones por las que seguimos este orden de instalación). No pasa nada si no se 
cambia, pero en caso de necesitar hacer troubleshooting de un cambio hecho 
directamente en la consola de Git, Vim puede ser complicado al inicio.

![Opciones VSCode](images/git_options.png?height=300px&width=400px)