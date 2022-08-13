---
title: GDPR Cookie Notice
description: Implementar un aviso de cookies para cumplir con la normativa RGPD en el 2021
date: 2022-07-26
tags: 
  - cookies
  - cms
  - wordpress
  
layout: layouts/post.njk
---


Es posible tener sitios web que no utilicen cookies, pero a veces alguna  funcionalidad  incorpora cookies (emergentes, llamadas a la acción, analítica).

Hasta no hace mucho el aviso de cookies se limitaba a informar de que el sitio web usaba cookies, informando de qué tipo de cookies usabas y su propósito. Y aquí se cumplía lo de «hecha la ley, hecha la trampa». Un inocente aviso de cookies podía servir para cargar infinidad de cookies de terceros. Para aclararnos. Estás en el año 2021 y en cuestión de cookies necesitas:

1.  Informar de qué  cookies usas, el tipo de cookies y su propósito.
2. Diferenciar su propósito.
3. Dar opción al visitante de seleccionar las cookies que acepta y las que no (esta es la novedad)
4. Evitar consentimientos tácitos o generados por defecto (si tú, no hagas trampas).

Si usas cookies de terceros, necesitas a partir de estos requerimientos necesitas implementar un código que te permita solucionar los puntos C y D. En el mundo WordPress existen multitud de plugins que gestionan estas cuestiones. Quizás muchos sufran de problemas de personalización o como ya ha pasado de seguridad y mantenimiento. Existen [servicios externos especializados](https://www.osano.com/cookieconsent) en cookies o lo que es casi mejor, soluciones listas para personalizar con un poco de código.

La ventaja de personalizar un código genérico es que suele darnos más opciones de personalización, nos permite ajustar la carga diferida y realizar a veces también traducciones. En este caso el ejemplo parte de una utilidad llamada [GDPR Cookie Notice](https://github.com/passatgt/gdpr-cookie-notice). Se trata de una sencilla solución basada en JavaScript que permite mostrar un aviso de cookies en nuestro sitio, cumpliendo con los requerimientos de la ley europea.


## Pasos para configurar el aviso de cookies con GDPR Cookie Notice
Como podrás comprobar esta misma web utiliza este código con alguna personalización adicional. Lo que necesitamos es cargar diferentes elementos:

- El propio código JavaScript que gestiona el mensaje (script.js, antes de la etiqueta final body )
- Una hoja de estilo con el CSS (style.css, en la cabecera antes del final del head)
- Un archivo JS con las traducciones (es.js, en mi caso español, después de script.js antes de la etiqueta final body )
- Finalmente cargar al final de la etiqueta body, un script con la llamada a la función gdprCookieNotice, pasando como argumento un objeto de opciones (ver en la documentación las opciones disponibles).
A continuación dejo una estructura básica de cómo quedarían los archivos:
````html
<!doctype html>
<html lang="es">
  <head>
  <!-- CSS con estilos de GDPR Cookie Notice -->
  <!-- https://github.com/passatgt/gdpr-cookie-notice -->
  <link rel="stylesheet" href="/assets/gdpr/style.css">
  
  <!-- JS para cargar selectivamente Google Analytics según las preferencias del visitante -->
  <script>
  document.addEventListener('gdprCookiesEnabled', function (e) {
        if(e.detail.analytics) { 
          
          var script = document.createElement('script');
          script.src = "https://www.googletagmanager.com/gtag/js?id=UA-XXXX-X";
	  script.async = true;
          document.head.appendChild(script);
          
          window.dataLayer = window.dataLayer || [];
          function gtag(){dataLayer.push(arguments);}
          gtag('js', new Date());
          gtag('config', 'UA-XXX-X'); 
        }
  });
  </script>
  
  </head>
  <body>
  <p>Aquí tu fantástico contenido</p>
  
  <!-- Script principal de GDPR Cookie Notice -->
  <script src="/assets/gdpr/script.js?ver=5.7" id="gdpr-js-js"></script>
  
  <!-- Script con las traducciones al español -->
  <script src="/assets/gdpr/lang/es.js?ver=5.7" id="gdpr-lang-js"></script>
  
  <!-- Llamada y opciones para el GDPR Cookie Notice -->
  <script>
  gdprCookieNotice({
		  locale: 'es', // si lo cambias debes tener un archivo como el de arriba es.js
		  timeout: 1500, // tiempo de espera
		  expiration: 30, // días de duración de la cookie
		  domain: window.location.hostname, // dominio
		  implicit: false, // debe se false, porque de lo contrario no cumples
		  statement: '/condiciones', // url a la política de cookies / legal
		  analytics: ['ga'] // aquí el grupo analitica pero hay más en opciones
  });
  </script>
  
  </body>
</html>
````

Hay cosas interesantes en el código. Vayamos por líneas:

- Línea 9. Detección y carga selectiva de las cookies de analítica con Google Analytics. Es una adaptación necesaria para cumplir con la legislación. Si el visitante rechaza las cookies de analíticas, no carga ese código gracias al condicional (e.detail.analytics). Es importante ver las opciones que nos ofrece el código para agrupar por cookies de marketing, rendimiento o analítica. La cuestión es agrupar por finalidad y así que el usuario escoja. Por supuesto esto sirve para casos de sitios pequeños o medianos. Los grandes necesitarán configuraciones más avanzadas como las que ofrece Osano
- Línea 33. Aquí se carga las traducciones. Es fácil porque sólo tienes que copiar el original y traducir las cadenas al idiomas. El nombre este archivo debe coincidir con la etiqueta html lang.
- Línea 37. La llamada principal a la configuración personalizada del sitio web. Como se puede ver, aquí es bastante sencilla y se limita a diferenciar las cookies propias (la del propio aviso) y las de analítica. Con tiempos de caducidad, idioma, retardo en aparecer, dominio…etc.
  
Si has visitado el sitio web te habrás hecho una idea del funcioamento. Aparece un mensaje en la parte inferior donde hay un texto, un botón y un enlace a la configuración. El usuario puede aceptar y cargar la cookie de aviso, o puede optar por cargar también la de analítica web. Cumplimos por tanto con los requisitos de la legislación de cookies. Evitamos el consentimiento expreso permitiendo la selección de las cookies según propósito.

Por último le puedes dar un poco de estilo modificando el archivo style.css que cargas de la GDPR Cookie Notice, con los colores que más se ajustan al diseño.