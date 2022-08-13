---
title: Eleventy.
description: Desarrollo web  moderna pero con un enfoque artesanal y muy progresivo..
date: 2018-08-24
tags:
  - js
  - cms
layout: layouts/post.njk
---

Para algunas personas los generadores de sitios estáticos son la forma natural de crear un sitio web. La idea principal es la simplicidad y la escasez de mantenimiento. Si tienes un sitio web que va a cambiar poco o va a seguir una estructura muy básica en su contenido, son una solución ideal. Admitamos que muchos sitios web son carne de estático: 
- catálogos, 
- web corporativas, 
- páginas de aterrizaje 
- o incluso blogs. 
  
 Los CMS permiten aislar a los usuarios de las dificultades del código, pero también aportan su propia capa de complejidad y dependencias. No son una novedad, pero los generadores estáticos vuelven a molar 🆒 gracias a la integración de las brillantes herramientas de desarrollo web para el front-end y los servicios de despliegue de código.

## Eleventy es un generador de sitios web estáticos basado en JavaScript
El caso es que hay muchos generadores estáticos , así que muchas personas buscan un terreno conocido según su lenguaje favorito. Jekyll, basado en Ruby, ha sido la herramienta más conocida, pero otros como Hugo (en Go), han sido el referente más habitual entre los que buscaban mayor rendimiento.

 El imparable crecimiento de JavaScript de los últimos años, ha provocado también una explosión de generadores estáticos y completos frameworks para crear sitios web. Por su elegante simplicidad, quizás uno de los que destaca entre muchos es Eleventy (11ty). Creado por Zach Leatherman este ingenioso generador estático basado en JavaScript, es un gran ejemplo de que las cosas bien pensadas suelen ser las más sencillas.

Eleventy quiere que tengas siempre la sensación de control. No pretende complicarte la vida, pero si te la quieres complicar, ahí tienes la herramienta para extenderla como tú quieras (hay un modo debug que muestra paso a paso lo que ejecuta) Si quieres algo extremadamente sencillo, en pocas líneas lo tienes. Todo es progresivo y depende de tu proyecto. Vas añadiendo complejidad, según tu propio criterio. Si tu configuración de Eleventy se vuelve demasiado compleja, no culpes a la herramienta, porque es solo tu responsabilidad.

## Script inicial para instalar y ejecutar Eleventy
Sí, empezar con Eleventy es así de sencillo.
¿Pero qué tiene Eleventy para ser más que un generador estático?

En última instancia el objetivo de un generador estático es producir un código HTML listo para subir a un alojamiento web. Vieja escuela ¿verdad? La realidad es que un generador estático como Eleventy puede hacer, si tú quieres, muchas cosas para que ese proceso sea más óptimo. A continuación comentaré lo que me parece más destacable de Eleventy para que sea mi elección como generador estático. No quiero que esto sea un tutorial, porque los hay muy buenos y además la documentación oficial, aunque impone un poco, es bastante buena. Prefiero centrarme en destacar sus puntos más destacables en mi opinión:

## En cuestión de plantillas, Eleventy lo entiende casi todo.
Si tienes experiencia con algún lenguaje de plantillas va a ser complicado que no esté entre la lista de lenguajes, que Eleventy traduce a HTML. Sí, Eleventy viene de 11 plantillas (no caí en eso hasta tiempo después 🤯). Tus plantillas pueden estar escritas o mezclar hasta 11 tipos: HTML, Markdown, JavaScript, Liquid, Nunjucks, Handlebars, Mustache, EJS, Haml, Pug, o hasta plantillas literales de JavaScript. ¿Es necesario tanto soporte? En la práctica es normal que te termines por usar una o dos, pero el hecho de que puedas mezclar con total libertad esos lenguajes de plantillas, es una gran oportunidad para facilitar la migración de otros proyectos (por ejemplo si vienes de Jekyll con Liquid).


## Lo configuras como te de la gana.
Eleventy te deja absoluta libertad para configurar desde cero lo que necesites. En la práctica es más común partir de un «starter» que te ofrezca cierta configuración o hacerte tú, tus propias configuraciones. Hay un archivo de configuración clave .eleventy.js que se encarga de gestionar tu propia personalización, y luego todo es cuestión de organizar tus carpetas (si quieres, hay una forma por defecto) del proyecto. Eleventy es una herramienta en JavaScript y se gestiona vía npm, así que en tu archivo package.json es donde organizarás tus scripts (los starters y ejemplos ayudan) y las diferentes dependencias (si quieres librerías de CSS por ejemplo). En la documentación encuentras las diferentes opciones para configurar tu proyecto (directorios a copiar en producción, urls). Dejo un ejemplo de mi .eleventy.js (basado en este proyecto) en un sitio web reciente:
````js
const htmlmin = require("html-minifier");

module.exports = function(eleventyConfig){
  
   eleventyConfig.setUseGitIgnore(false);
    
   eleventyConfig.addWatchTarget("./_tmp/style.css");
  
   eleventyConfig.addPassthroughCopy( { "./_tmp/style.css": "./style.css" });
    
   eleventyConfig.addPassthroughCopy("images");
    
   eleventyConfig.addShortcode("version", function () {
      return String(Date.now());
    });
  
   eleventyConfig.addShortcode("year", function(){
     return  String(new Date().getFullYear());
    });

   eleventyConfig.addTransform("htmlmin", function (content, outputPath) {
       
     if (
          process.env.ELEVENTY_PRODUCTION &&
          outputPath &&
          outputPath.endsWith(".html")
       ) {
          let minified = htmlmin.minify(content, {
            useShortDoctype: true,
            removeComments: true,
            collapseWhitespace: true,
        });
          return minified;
        }
    
        return content;
    });

    
    return {
        dir: {
            input: "src",
            output: "public"
        }
    }

}
````

## Una cascada de datos completísima.
Al igual que con las extensiones de plantillas, un aspecto sobresaliente de Eleventy es su espectacular forma de gestionar los datos. Puedes añadir datos a los plantillas, literalmente de casi todas partes. En local, a través de archivos de configuración global, archivos .json o hasta la posibilidad de que incorporar datos dinámicos según llamadas a través de API. Todo esto supone una cascada de datos para ser fusionada en tiempo de ejecución. Pero no hace falta complicarse demasiado, ya que tus datos pueden ser tan obvios como texto en la cabecera de la plantilla. Volvemos a la sencillez inicial y a la progresividad en ofrecer alternativas. No obstante, la cascada de datos puede volverse algo difícil de manejar. Personalmente no he tenido experiencia en resolver casos complejos y es posible que sea uno de los campos con mejoras en el futuro.

## Configuración adicional con shortcodes y transformaciones
Como verás en el archivo .eleventy.js de arriba, otro aspecto que puedes configurar es la posibilidad de añadir «shortcodes» que te faciliten incorporar contenido dinámico en tu plantilla (fechas o extractos dinámicos basados en variables). Las transformaciones permiten, al igual que un gestor de tareas, incorporar a tu flujo de trabajo transformaciones del código como minificar el HTML, que optimizan la entrega de tu contenido y consiguen más velocidad en la carga de la página. También es posible agregar tus propios filtros personalizados según el lenguaje de plantilla que uses. Como digo la documentación es bastante completa y todo depende de tus necesidades.

## Orientado al rendimiento y a la velocidad.
Aunque muchos generadores tienen como objetivo simplificar la entrega de contenido, es innegable que el enfoque de Eleventy está muy orientado a crear sitios absurdamente rápidos. Si estás preocupado por la velocidad y desempeño de tu sitio web, Eleventy ofrece unas configuraciones y extensiones orientadas crear sitios web con valores de Core Web Vitals y Lighthouse casi imposibles de conseguir con otras herramientas. 


## Una gran comunidad y con muchos complementos adicionales.
Como en otros proyectos, un gran activo de Eleventy consiste en una entusiasta comunidad activa que pone a disposición plugins y extensiones que ayudan a solucionar diferentes necesidades. Existen plugins oficiales que ayudan a gestionar imágenes, caché y otros usos necesarios para cuando necesitas máximo desempeño. La comunidad ofrece recursos y también ideas ingeniosas de conseguir soluciones a cuestiones que un generador estático convencional no se plantearía. Además, como comentaba anteriormente los sitios web reaizados con Eleventy ofrecen unos valores altísimos en velocidad.

Creo que Eleventy ofrece una excelente solución a la necesidad de crear sitios web sencillos, pero con toda la configuración avanzada que exige un sitio web moderno.

## Conclusión sobre Eleventy
En lo personal sólo he empezado a trastear con Eleventy y tengo que admitir que la experiencia es fantástica, aunque no exenta de cierta dificultad para comprender la herramienta (en especial, si no has usado otros generadores estáticos anteriormente). Hay muy buenos recursos y la comunidad está produciendo soluciones increíbles. Creo que Eleventy ofrece una excelente solución a la necesidad de crear sitios web sencillos, pero con toda la configuración avanzada que exige un sitio web moderno. Si eres desarrollador no vas a echar nada en falta para realizar tus proyectos. Otro punto positivo que le encuentro es que, a pesar de su enfoque en JavaScript, es una herramienta ideal para el aprendizaje de tecnologías web. Conforme aprendes cosas las vas incorporando al proyecto y todo es muy artesano, lo que favorece que tengas la sensación de control sobre lo que haces. No necesitas librerías si no quieres. Con Markdown y algo de CSS, puedes crear tu primer sitio y a partir de ahí, complicarte lo que quieras. En definitiva, Eleventy es una herramienta ideal para generar sitios web de forma moderna pero con un enfoque artesanal y muy progresivo.