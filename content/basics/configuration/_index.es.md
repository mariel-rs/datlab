+++
title = "Configuración"
weight = 20
+++

Una vez que todo está instalado, recomiendo reiniciar el sistema antes de empezar. 
En sistemas Windows, reiniciar forza a que el sistema reconozca el contenido de
las variables de entorno.

VSCode va a ser nuestro editor de código. Como se mencionó anteriormente, es 
liviano y diseñado de tal manera que podemos personalizarlo con lo que 
necesitemos, haciéndolo muy cómodo incluso con computadoras con pocos recursos.

## Extensiones VSCode
Para instalar extensiones, podemos hacerlo de dos formas:

- Visitando el sitio [Marketplace](https://marketplace.visualstudio.com/vscode) 
de VSCode y buscando la extensión que deseamos instalar.

![VSCode Marketplace](images/vscode_marketplace.png?height=110px&width=510px)

- Directamente desde VSCode, visitando la tab de Extensions.
![VSCode Marketplace](images/vscode_extensions.png?width=300px)


### Soporte a Python

Esto se logra instalando la extensión de 
[Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) 
para VSCode. La instalación es rápida. Esta extensión ya tiene integrados 
PyLance (nos dará tips para autocompletar expresiones mientras programemos) y 
soporte a Jupyter :)

Una vez que esté instalada esta extensión, tenemos que asegurarnos que VSCode 
reconozca que Anaconda es nuestro intérprete de Python.

Para esto, accedemos a la paleta de comando de VSCode usando los siguientes 
atajos:
- Windows / Linux:  `Ctrl+Shift+P` o `F1` 
- MacOS: `⇧⌘P` o `F1`
 
Buscamos interpreter y seleccionamos la opción _Python: Select Interpreter_

![Python interpreter](images/python_interpreter.png?width=350px)

Allí buscamos la opción _'base': conda_. En una instalación nueva, sólo aparecerá 
esta opción. En mi caso tengo un ambiente adicional que cree para un proyecto de 
datos geoespaciales.

![Python interpreter list](images/python_interpreter_list.png?width=350px)

### Soporte a idioma español (opcional)

VSCode se instala sólo con idioma inglés. Si deseas tener el software en español, 
puedes instalar la extensión [Spanish Language Pack](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-es&amp;ssr=false#overview) para que la interfaz esté en español. Es importante recalcar
que la mayoría de la documentación y de los foros con tips estarán en inglés.

### Temas (opcional)

Los temas son un conjunto de colores que se aplican en la interfaz, tanto en el 
fondo como en el texto en el editor. VSCode tiene bastantes temas para 
personalizar la experiencia. Es importante que esto se haga de acuerdo al gusto 
personal.

Mis temas favoritos son:

- [Visual Studio Blue](https://marketplace.visualstudio.com/items?itemName=DanijelMalinovic.visual-studio-blue-theme)
Este es un tema claro y el que uso durante el día o en habitaciones con muy 
buena iluminación. Blue fue el tema que usaba cuando aprendí a programar en VS 
2017, entonces estoy sesgada <i class="fas fa-grin-wink"></i>
- [Dracula](https://marketplace.visualstudio.com/items?itemName=dracula-theme.theme-dracula)
Este es un kit de temas oscuros que uso cuando estoy programando por las noches 
o en habitaciones con poca iluminación.

Para ver más temas, puedes consultar [VSCode Themes](https://vscodethemes.com/) 
o directamente desde las extensiones en VSCode.

## Git y GitHub (opcional)</h4>

Es una buena práctica llevar una gestión de cambios en todos los archivos que 
generemos con código. A veces pueden pasar desastres en nuestras computadoras y 
podemos perder todo. GitHub es un sitio donde se pueden gestionar todos los 
repositorios Git en la nube, gestionar colaboraciones entre equipos, entre 
otras cosas. 

Muchos desarrolladores usan GitHub como un portafolio para mostrar a posibles 
empleadores los proyectos en los que han trabajado.

Para configurar GitHub y Git, seguiremos estos pasos:

1. Registro en [GitHub](https://github.com/). Es muy simple.
2. Configuración de Git en nuestro sistema con el usuario y el correo utilizado
al registrarnos en GitHub. 

Abrimos `Git CMD` en Windows o `Terminal` en MacOS / Linux. Los siguientes 
comandos modifican la identidad. 

```cmd
$ git config --global user.name "Mi Usuario GitHub"
$ git config --global user.email correo@ejemplo.com
```

Revisamos que los cambios se hayan hecho con el siguiente comando:

```cmd
$ git config --list
```


