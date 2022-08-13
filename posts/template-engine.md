---
title: template engine
description: software que nos permite mezclar datos con una plantilla.
date: 2022-07-24
tags:
  - utilidades
  - programación
layout: layouts/post.njk
---


Los motores de plantillas se utilizan cuando desea crear rápidamente aplicaciones web que se dividen en diferentes componentes. Las plantillas también permiten una representación rápida de los datos del lado del servidor que deben pasarse a la aplicación.

Por ejemplo, es posible que desee tener componentes como el cuerpo, la navegación, el pie de página, el tablero, etc.

## Motores de plantillas populares
Los motores de plantillas se utilizan principalmente para aplicaciones del lado del servidor que se ejecutan en un solo servidor y no se crean como API. Los más populares  Handlebars (para JavaScript), Twig y Blade (para Laravel / PHP), JSP (para Java) o Ninja (de python).

  

## Cómo funcionan los motores de plantillas
Cuando crea una aplicación del lado del servidor con un motor de plantillas, el motor de plantillas reemplaza las variables en un archivo de plantilla con valores reales y muestra este valor al cliente. Esto facilita la construcción rápida de nuestra aplicación.

### Ejemplo con un motor expressJS de plantillas ejs 
Para una aplicación del lado del servidor escrita con el tiempo de ejecución de NodeJS, puede usar un motor de plantilla.

Los siguientes pasos demuestran cómo funcionan los motores de plantillas utilizando express Js y el motor de plantillas ejs. El ejemplo que se proporciona a continuación representa los datos de un usuario en la página web.
#### Paso 1: Instalación express y el motor de plantillas ejs
El siguiente comando instala el ejsmotor de plantilla y el expressmarco:
````bash
npm install express ejs
````
#### Paso 2: Configuración del motor de visualización
````js
const express = require("express")
const app = express();


// Set the View Engine or Template Engine
app.set('view engine', 'ejs');

app.listen(3000)
````
En el código anterior, creamos nuestra aplicación express. La aplicación escucha en el puerto 3000.

Esta línea de código: app.set('view engine', 'ejs')le dice a nuestra aplicación express que queremos usar EJS como nuestro motor de plantillas.

#### Paso 3: Configuración de la carpeta de visualización
Cree una carpeta llamada "view". La carpeta de vista debe contener nuestras plantillas. Una de estas plantillas es index.ejs, que generará nuestra portada. La segunda plantilla es user.ejs, que se usará para pasar datos de usuario desde el lado del servidor para que se muestren inmediatamente en la página web.
````
index.js
>view
   index.ejs
   user.ejs
````
#### Paso 4: Configuración de las rutas
Vamos a crear las rutas para nuestra página de inicio y página de usuario.

Tenga en cuenta el res.render()método a continuación. Así es como renderizas una plantilla en expressJS.

````js
app.get('/', function (req, res) {
  res.render("index");
})
 
app.get("/user", function(req,res){
  const user = {
    name: "Theodore Kelechukwu O.",
    stack: "MERN",
    email: "theodoreonyejiaku@gmail.com",
    hubby: ["singing", "playing guitar", "reading", "philosoph"]
````
Como hemos visto, la ruta predeterminada “\”, cuando se accede, muestra o renderiza la index.ejspágina. Mientras tanto, el “\usuario” muestra la user.ejspágina.

Pasamos el userobjeto al objeto renderizado para pasar las userpropiedades a la página web y renderizarla.

#### Paso 5: Plantillas de nuestros archivos de vista
Ahora que hemos pasado los datos de usuario desde el lado del servidor, debemos mostrarlos de inmediato en nuestra interfaz o página web.

index.ejs

usuario.ejs
````html
<html>
  <head>
    <title>This is the title</title>
  </head>

  <body>
    <h1>Welcome to User Details</h1>
    <p><b>Name:</b> <%= user.name %></p>
    <p><b>Email:</b> <%= user.email %></p>
    <p><b>Stack:</b> <%= user.stack %></p>
````
Tenga en cuenta el <%= variable %>patrón de visualización de valores. Esa es la forma en que se usa en ejs. Observe también el user.forEach(); esto es para mostrar cuán poderosos pueden ser los motores de plantillas.


````html

{% block header %}
<h1>{{ title }}</h1>
{% endblock %}

{% block content %}
<ul>
  {% for name, item in items %}
  <li>{{ name }}: {{ item }}</li>
  {% endfor %}
</ul>
{% endblock %}
````