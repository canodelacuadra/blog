---
title: Core web vitals
description: Realizar métricas para medir la experiencia de un usuario web.
date: 2022-07-24
tags:
  - analítica web
layout: layouts/post.njk
---
## Core Web Vitals
Core Web Vitals como iniciativa de Google, nace de la necesidad de proporcionar un método unificado a los desarrolladores y webmasters, que les permitiera detectar de forma sencilla problemas de UX y WPO en una web.

En este sentido, Google ha señalado tres indicadores que considera esenciales para brindar una buena experiencia de usuario. Estas tres métricas, están enfocadas en
1. medir el tiempo que tarda en cargar una web, LCP
2.  la rapidez de interacción con el usuario 
3.  y la estabilidad visual de la misma

### Largest Contentful Paint (LCP)
La métrica Largest Contentful Paint, mide el tiempo que tarda en renderizarse en pantalla (above the fold) el contenido más grande.

Indica el momento en el que el usuario ve algo relevante en pantalla (sin hacer scroll)
El tiempo de respuesta del servidor está incluido en la medición
El LCP puede corresponder a una imagen, texto o video
largest contentful paint umbrales

Para ofrecer una buena experiencia de usuario, el LCP debe ocurrir a los 2,5 segundos o menos. Hasta los 4 segundos, Google considera que el resultado se puede mejorar y por encima de este umbral, lo considera lento. 

### First Input Delay (FID)
La métrica First Input Delay, mide el tiempo que transcurre desde la primera interacción del usuario, hasta que el navegador responde a la misma.

Para ofrecer una buena experiencia de usuario, el FID debe ocurrir en 100 milisegundos o menos. Hasta los 300 milisegundos, Google considera que el resultando se puede mejorar y por encima de este umbral, lo considera lento.

first input delay umbrales

Revela información de la primera impresión del usuario al hacer clic en la web
La métrica se verá alterada dependiendo del momento, navegador y elemento clicado por el usuario
Esta métrica no es posible simularla en laboratorio. Únicamente se puede medir sobre usuarios reales
El tiempo de bloqueo total (TBT) es una métrica de laboratorio para hacer pruebas sin ninguna interacción directa del usuario. También es recomendable tener en cuenta el tiempo de interacción (TTI). Estas dos métricas, pueden ayudar a realizar estimaciones sobre la percepción del usuario en diferentes tipos de red y dispositivo
### Cumulative Layout Shift (CLS)
La métrica Cumulative Layout Shift, es la responsable de evaluar la estabilidad visual de una web.

A menor desplazamiento de elementos durante la carga, menor será la probabilidad de que el usuario haga clic por error en alguno de ellos
La medición de los elementos de la página, se realiza a través de ventanas de sesión. Las ventanas de sesión, corresponden a diferentes partes de una página web a las que llega un usuario cuando hace scroll. La puntuación total para cada ventana de sesión, se denomina cambio de diseño acumulativo (CLS)
El CLS no mide tiempo, sino que realiza un cálculo de cambios en las posiciones
cumulative layout shift umbrales

Para ofrecer una buena experiencia de usuario, el CLS debe ser menor o igual a 0,1. Hasta 0,25 Google considera que el resultando se puede mejorar y por encima de este umbral, lo considera pobre.


## Web vitals

Web Vitals son señales de calidad clave para ofrecer una excelente UX en la web (https://web.dev/vitals). Esta extensión mide Core Web Vitals y brinda retroalimentación instantánea sobre las métricas de carga, interactividad y cambio de diseño. Es consistente con la forma en que Chrome mide estas métricas y las informa a otras herramientas de Google (p. ej., Informe de experiencia de usuario de Chrome, Información sobre la velocidad de la página, Consola de búsqueda).

La extensión captura:
Pintura con contenido más grande
Cambio de diseño acumulativo
Retraso de la primera entrada
Interacción con la siguiente pintura (experimental)

La extensión proporciona tres características principales:

1) Ambient Badge: esto ayuda a verificar si una página supera los umbrales de Core Web Vitals.

Una vez instalada, la extensión mostrará un ícono de insignia de estado deshabilitado hasta que navegue a una URL. En este punto, actualizará la insignia a verde o rojo dependiendo de si la URL supera los umbrales de métricas de Core Web Vitals.

La insignia tiene varios estados:

* Deshabilitado - gris
* Pasando - verde
* Una o más métricas fallan - rojo

Si una o más métricas fallan, la insignia animará los valores de estas métricas.

2) Desglose detallado en la ventana emergente

Al hacer clic en el ícono de la insignia Ambient, podrá profundizar en los valores de métricas individuales. En este modo, la extensión también dirá si un valor de métrica puede cambiar o requiere una acción del usuario.

Por ejemplo, First Input Delay requiere una interacción real (por ejemplo, hacer clic/tocar) con la página y estará en un estado de espera de entrada hasta que este sea el caso. Recomendamos consultar la documentación de web.dev para LCP, CLS y FID para comprender cuándo se asientan los valores de las métricas.

A partir de la versión 1.0.0, la ventana emergente combina sus experiencias locales de Core Web Vitals con datos de usuarios reales del campo a través de la API Chrome UX Report (CrUX). Esta integración le brinda información contextual para ayudarlo a comprender qué tan similares son sus experiencias individuales a las de otros usuarios de escritorio en la misma página. También hemos agregado una nueva opción para "Comparar experiencias locales con datos de campo del teléfono", si es necesario. Tenga en cuenta que es posible que los datos de CrUX no estén disponibles para algunas páginas, en cuyo caso intentamos cargar datos de campo para el origen en su conjunto.

3) Superposición de HUD

La superposición muestra una pantalla de visualización frontal (HUD) que se superpone a su página. Es útil si necesita una vista persistente de sus métricas de Core Web Vitals durante el desarrollo. Para habilitar la superposición:

Haga clic con el botón derecho en la insignia de Ambient y vaya a Opciones.
Verifique Mostrar superposición de HUD y haga clic en 'Guardar'
Vuelva a cargar la pestaña de la URL que desea probar. La superposición ahora debería estar presente.

