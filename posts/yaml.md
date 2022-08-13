---
title: YAML
description: Definición y conceptos básicos.
date: 2022-07-24
tags:
  - lenguajes
  - programación
  - serialización
layout: layouts/post.njk
---
YAML es un formato de serialización de datos legible por humanos inspirado en lenguajes como XML, C, Python, Perl, así como en el formato de los correos electrónicos (RFC 2822). YAML fue propuesto por Clark Evans en 2001, quien lo diseñó junto a Ingy döt Net y Oren Ben-Kiki.

YAML es un acrónimo recursivo que significa **Y**AML **A**in't **M**arkup **L**anguage (en castellano, ‘YAML no es un lenguaje de marcado’).​ A comienzos de su desarrollo, YAML significaba Yet Another Markup Language (‘otro lenguaje de marcado más’) para distinguir su propósito centrado en los datos en lugar del marcado de documentos. Sin embargo, dado que se usa frecuentemente XML para serializar datos y XML es un auténtico lenguaje de marcado de documentos, es razonable considerar YAML como un lenguaje de marcado ligero.

## Características
YAML fue creado bajo la creencia de que todos los datos pueden ser representados adecuadamente como combinaciones de listas, hashes (mapeos) y datos escalares (valores simples). 

La sintaxis es relativamente sencilla y fue diseñada teniendo en cuenta que fuera muy legible pero que a la vez fuese fácilmente mapeable a los tipos de datos más comunes en la mayoría de los lenguajes de alto nivel. Además, YAML utiliza una notación basada en la sangría y/o un conjunto de caracteres  distintos de los que se usan en XML, haciendo que sea fácil componer ambos lenguajes.

* Los contenidos en YAML se describen utilizando el conjunto de caracteres imprimibles de Unicode, bien en UTF-8 o UTF-16.
* La estructura del documento se denota indentando con espacios en blanco; sin embargo no se permite el uso de caracteres de tabulación para sangrar.
* Los miembros de las listas se denotan encabezados por un guion ( - ) con un miembro por cada línea, o bien entre corchetes ( [   ] ) y separados por coma espacio ( ,   ).
* Los vectores asociativos se representan usando los dos puntos seguidos por un espacio. en la forma "clave: valor", bien uno por línea o entre llaves ( {   } ) y separados por coma seguida de espacio ( ,   ).
* Un valor de un vector asociativo viene precedido por un signo de interrogación ( ? ), lo que permite que se construyan claves complejas sin ambigüedad.
* Los valores sencillos (o escalares) por lo general aparecen sin entrecomillar, pero pueden incluirse entre comillas dobles ( " ), o comillas simples ( ' ).
* En las comillas dobles, los caracteres especiales se pueden representar con secuencias de escape similares a las del lenguaje de programación C, que comienzan con una barra invertida ( \ ).
* Se pueden incluir múltiples documentos dentro de un único flujo, separándolos por tres guiones ( --- ); los tres puntos ( ... ) indican el fin de un documento dentro de un flujo.
* Los nodos repetidos se pueden denotar con un ampersand ( & ) y ser referidos posteriormente usando el asterisco ( * )
* Los comentarios vienen encabezados por la almohadilla ( # ) y continúan hasta el final de la línea.
* Los nodos pueden etiquetarse con un tipo o etiqueta utilizando el signo de exclamación( ! ) seguido de una cadena que puede ser expandida en una URL.
* Los documentos YAML pueden ser precedidos por directivas compuestas por un signo de porcentaje ( % ) seguidos de un nombre y parámetros delimitados por espacios.. Hay definidas dos directivas en YAML 1.1:
  * La directiva %YAML se utiliza para identificar la versión de YAML en un documento dado.
  * La directiva %TAG se utiliza como atajo para los prefijos de URIs. Estos atajos pueden ser usados en las etiquetas de tipos de nodos.
* YAML requiere que las comas y puntos y comas que se utilicen como separadores en las listas sean seguidos por un espacio, de forma que los valores escalares que contengan signos de puntuación (como 5,280 o http://www.wikipedia.org) se puedan representar sin necesidad de utilizar comillas.

Hay dos caracteres adicionales que están reservados en YAML para su posible estandarización en un futuro: la arroba ( @ ) y el acento grave ( ` ).

## Ejemplos
### Listas
````yaml
 --- # Películas favoritas, formato de bloque
 - BotijoAzul
 - BotijoVerde
 - Viridiana
 - Psicosis
 ...

 --- # Lista de la compra, formato en línea
 [leche, pan, huevos]
 [chorizo, morcilla, botijo, pollo]
 ````
### Vectores asociativos
````yaml
 --- # Bloque
 nombre: Pepe López
 edad: 33
 --- # En  línea
 {nombre: Pepe López, edad: 33}
 ````
### Literales de bloque

Preservando retornos de línea
 ````yaml
 --- |
  El texto mantiene su estructura,
  en el sentido que preserva los retornos de línea.
  
  Esto incluye también líneas en blanco.
   ````
Ignorando retornos de línea
 ````yaml
 --- >
  El texto rodeado 
  será formateado 
  como un único
  párrafo
   ````
  Las líneas en blanco
  denotan saltos de párrafo.

### Listas de vectores asociativos
 ````yaml
 - {nombre: Pepe López, edad: 33}
 - nombre: Maria Garcia
````
### Vectores asociativos de listas
 ````yaml
 hombres: [Pepe Lopez, Guillermo Garcia]
 mujeres:
  - María García
  - Susana Márquez
  ````