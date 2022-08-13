---
title: Crear proyecto web con eleventy
description: Creando tu primer proyecto con Eleventy
date: 2018-09-30
tags: 
  - js
  - cms
layout: layouts/post.njk
---

1. Crea una carpeta para el proyecto
Para crear un nuevo proyecto de Eleventy, solo necesita crear una carpeta vacía:
````bash
$ mkdir eleventy-01
$ cd eleventy-01
````
2. Crear un archivo package.json
Dentro de esta carpeta de proyecto recién creada, debes crear un archivo inicial para json: package.json, de modo que puedas usar la herramienta de Node.js Package Manager (npm) posteriormente, para la administración de las dependencias:

````bash
$ npm init -y
````
3. Instalación de Eleventy
Habiendo creado el archivo package.json a continuación debemos agregar el paquete de Eleventy ( @11ty/eleventy ) como una dependencia de desarrollo, dentro de nuestro proyecto, usando el comando npm install:
````bash
$ npm install --save-dev @11ty/eleventy
````
4. Ejecutando Eleventy
Ahora solamente debes probar que Eleventy ya esta instalado. Ejecuta el comando, y la consola te mostrará una respuesta del número de ficheros creados y el tiempo que ha tardado en ello.
````bash
$ npx @11/eleventy
````
Como aún no se han creado archivos adicional a la carpeta del proyecto, el resultado debería ser de 0 archivos.
6.  También puedes iniciar Eleventy en modo de recarga en caliente, utilizando la opción –serve:
````bash
$ npx @11/eleventy --serve
````
En este caso, el comando sigue ejecutándose y está atento a cualquier cambio de archivo de los archivos dentro de la plantilla y dentro de la carpeta del proyecto actual. Si el contenido de un archivo se cambia y luego se guarda, Elevanty reconoce ese cambio automáticamente y genera un nuevo archivo de salida.

7. Adición de plantillas
Ahora es el momento de ver realmente a Eleventy en acción y eso requiere que agreguemos archivos de plantilla a nuestro proyecto. En primer lugar, estamos creando un archivo de plantilla especial, una plantilla de diseño. Al utilizar una plantilla de diseño, puedes ajustar el contenido con un diseño común. Para crear dicha plantilla, primero agregamos una nueva carpeta denominada _includes al proyecto:
````bash
$ mkdir _includes
````
Luego, dentro de esta nueva carpeta _includes, creamos un nuevo archivo vacío con el nombre de mylayout.njk e insertamos el siguiente código de plantilla:
````html
---
site_title: Mi Primer Sitio de Eleventy
---
<h1> {{ site-title | safe }}</h1>
 <hr/> 
 {{ content | safe }} <hr/> 
 <small>by
  <a href="https://ciberninjas.com">Ciberninjas.com</a> </small> </body>
````

Al usar la extensión de archivo njk, estamos indicando que estamos usando el lenguaje de plantillas Nunjucks dentro de este archivo. Si quieres saber más sobre Nunjucks puedes encontrar el sitio web del proyecto y la documentación correspondiente en Mozilla Nunjucks.

El código comienza con una sección preliminar al principio. Dentro de la sección de contenido inicial, puede definir datos que luego se pueden usar en el siguiente código de plantilla. En el ejemplo, estamos usando la sección principal para definir la propiedad site_title que contiene una cadena para el valor del título.

Dentro del código de la plantilla, accedemos a site_title utilizando llaves dobles. El valor de esta propiedad se utiliza para establecer el título de la página.

8. Creación de plantillas utilizando un diseño
Ahora creemos dos plantillas más (usando Markdown como el lenguaje de la plantilla) usando nuestra plantilla de diseño creada previamente: Cree un nuevo archivo post-01.md en la carpeta del proyecto e inserte el siguiente código de Markdown:

````html
---
layout: mylayout.njk
title: Mi primer post del blog.
---
{{ title }}


 
This is my first blog post! Have much fun using Eleventy, an easy and flexible JavaScript-based static site generator.
````
Estas plantillas, generan una publicación simple sobre un blog, que aún no posee ningun tipo de CSS ni estilo decorativo incluido.

