---
title: Preguntas examen SEW 👹
---
1. ¿Qué compara `===`? ==Iguales en tipo y valor==
2. ¿MySQL es estándar de PHP? ==No==
3. ¿PHP de qué es estándar?        FALTA
4. ¿ECMAScript de qué es estándar? ==Estándar de los lenguajes de Script==
5. ¿XML de qué es estándar? ==Estándar de transferencia de datos==
6. ¿Año de la última versión de XML? ==2006==
7. ¿Última versión de PHP? ==8.0.26==
8. ¿Última versión de ECMAScript? ==13==
9. En JavaScript, si tu pulsas, ¿Qué eventos se lanzan? ==onclick==
10. mysqli::prepare, ¿para que es? ==(evitar inyección de código, mejorar la seguridad==
11. ¿MariaDB es compatible con MySQL? ¿Se usa en XAMPP? ==Si y si (se sustituye por MySQL a partir de la versión 5.5.30)==
12. ¿Qué es $_COOKIE? (superglobal, array, atributo predefinido, …) ==Variable superglobal, global, predefinida y array asociativo==
13. ¿Qué es $_SESSION? (superglobal, array, atributo predefinido, …) ==Variable superglobal, global predefinida y array asociativo==
14. Cascada de CSS ==Es uno de los principios fundamentales de las hojas de estilo y permite que varias hojas de estilo afecten a un mismo documento==
15. Prioridad y origen. Según si lo hizo el autor, el usuario o el agente de usuario. ==Primero declaraciones importante: agente usuario, usuario y autor; Luego declaraciones normales: autor, usuario y agente usuario==
16. ¿Cómo obtener el nombre del agente de usuario? ==navigator.userAgent==
17. ¿Qué versión de XML es la correcta? ¿La versión 1.1 se puede utilizar? ==1.0, si==
18. Saber cuál es la sintaxis correcta de la cabecera de un XML.   ==< ? xml... ? >== (todo junto)
19. Para poner encabezados de distintos niveles, ¿qué se usa? (hgroup, header o h1,
h2, h3, h4, h5 y h6) ==Todos los mencionados==
20. ¿Se basan todos los HTML en `<base>`? ==No. Permite establecer la url base==
21. Los servicios web, ¿son un estándar? ¿son un protocolo http? ¿se utilizan para
comunicar ordenadores? ==No son un estándar, usan habitualmente servicios http, permiten intercambio de información entre ordenadores, en XML y JSON==
22. TCP/IP ¿IP obtiene la IP del ordenador al que se le van a enviar los datos? ¿TCP/IP
son protocolos? ==Si y si==
23. ¿Qué es un array en JavaScript? ¿Es un objeto global? ¿Es …?  FALTA
24. ¿La funciones en JavaScript se ponen con function? ¿Pueden ser anónimas?
¿Puede no definirse el tipo de retorno? ==Pueden tener varios retornos, no pueden ser anónimas y son de tipo Function==
25. xs:length ¿Se puede aplicar a xs:string? ¿Se puede aplicar a xs:number? ¿Se
puede aplicar a xs:non negative number? ==Si en xs:string, no en xs:number ni xs:nonnegativenumber==
26. ¿Es JSON un estándar de JavaScript? ¿Tiene un árbol n-ario? ==Es un formato de texto (no árbol binario)== FALTA un poco
27. ¿XML es un árbol binario equilibrado? ¿Se pone por nodos de clave-valor? ¿Son
nodos que se van añadiendo a un árbol? FALTA
28. Árbol DOM ¿Un tabulador lo trata como un espacio? ¿Un salto de línea lo trata
como un espacio? ¿Dos espacios los trata como un espacio? ==Un tab lo trata como espacio, un salto de línea como un nuevo#text y varios espacios un solo#text== 
29. $(*document.palabraxquenomeacuerdo).each(function (){…}*) ¿Selecciona
todos los elementos del HTML? ¿Selecciona todos los elementos del body?
¿Recorre todos los elementos del HTML? ==Recorre todos los elementos dentro de document.loquesea y sólo esos elementos, no todo el DOM==
30. Especificidad abc. ¿La a para qué es? ¿para clases? ¿para ids? ¿para
pseudoelementos? ==a) para ids, b) para clases, atributos y pseudoclases, c) para elementos y pseudoelementos==
31. PHP ¿es un metalenguaje? ¿es un estándar? … ==Es un lenguaje multiplataforma==
32. XML ¿es un metalenguaje? ¿es un estándar? … ==Metalenguaje estándar del W3C==
33. La API de Geolocalización ¿es un estándar de ECMAScript? ¿es un estándar de
W3C? ¿es un estándar de API nombrequenomeacuerdo? ==Estándar HTML5 del W3C==
34. ¿Qué significan las siglas de XML? ==eXtensible Markup Language==
35. API de HTML5 ¿están contenidas en el estándar W3C? ==Si (si se habla de HTML5 como estándar)==
36. Math.sqrt(27).toPrecision(). Ponía tres valores con diferente número de
decimales. Saber cuántos decimales devuelve. 
````js
// Ejemplo:
let num = 13.3714
num.toPrecision(2) //13
num.toPrecision(3) //13.3
num.toPrecision(4) //13.37
num.toPrecision(5) //13.371
num.toPrecision(6) //13.3714
num.toPrecision(7) //13.37140
````
37. El objeto array ¿tiene la función forEach? ¿tiene la función unshift? ¿es un
elemento global? ==Tiene ambos métodos==
38. Objeto Object de JavaScript ¿heredan todos de él? ¿tiene un atributo string?
¿tiene un atributo number? FALTA
39. SVG ¿es un estándar de ECMAScript? ¿es un estándar de W3C? ==Estándar del W3C==
40. XML. La x del Microsoft Office (tipo docx) ¿se refiere a XML? ¿sólo se usa para
docx (para Excel, PowerPoint y eso no)? ==Se refiere a xml==

---

## Examen extraordinaria Mayo 2021

1. Sobre el evento "onchange" en JavaScript se puede decir: ==Está definido para los elementos HTML: < input >, < select > y < textarea >==
2. Sobre ActiveX se puede decir: ==No se debe usar nunca por problemas de seguridad==
3. Sobre PHP se puede decir: ==Es un lenguaje dinámico con inferencia de tipos==
4. Sobre prototype en JavaScript se puede decir: ==Permite modificar objetos añadiendo métodos y propiedades en tiempo de ejecución==
5. Sobre el evento "onsubmit" en JavaScript se puede decir: ==Está definido para el elemento HTML: < form >==
6. Para incorporar en un documento HTML5 válido un recurso multimedia de tipo video (video.mp4) se debe escribir: ==< video src="video.mp4" loop >< /video >==
7. Sobre PHP se puede decir: ==Es un lenguaje que soporta SGBD relacionales==
8. Sobre MariaDB se puede decir: ==Es usada por XAMPP==
9. Sobre las API de HTML5 se puede decir: ==Están dentro del estándar HTML5 del W3C==
10. Sobre `$_FILES` en PHP se puede decir: ==Es un array asociativo== 
11. Sobre el uso de la secuencia de elementos complejos no ordenados con < xs:all > en XML se puede decir: ==Los elementos aparecen en cualquier orden==
12. La cascada en CSS: ==Es uno de los principios fundamentales de las hojas de estilo y permite que varias hojas de estilo afecten a un mismo documento==
13. Sobre el método mysqli::prepare de PHP, cuando hay código SQL procedente de orígenes externos, se puede decir: ==Es necesario para evitar la inyección directa de SQL==
14. Sobre el evento "onload" en JavaScript se puede decir: ==Está definido para el elemento HTML < body >==
15. Sobre el uso de secciones CDATA en XML se puede decir: ==Permite especificar datos, utilizando cualquier carácter, especial o no, sin que se interprete como marcado XML==
16. Sobre jQuery se puede decir: ==Es una biblioteca externa==
17. Sobre HTTPS se puede decir: ==El nivel de cifrado depende del servidor remoto y del navegador utilizado por el cliente==
18. Sobre el evento "onclick" en JavaScript se puede decir: ==Está definido para todos los elementos HTML==
19. Sobre el lenguaje derivado de XML denominado XML Signature se puede decir: ==Es utilizado para información de firma electrónica==
20. Sobre el uso de espacios de nombres en XML se puede decir: ==Evita el problema de la homonimia en las etiquetas==
21. Sobre PHP se puede decir: ==Es un lenguaje interpretado y ejecutado en el servidor==
22. Sobre CSS se puede decir que: ==Es un lenguaje para describir la presentación de documentos estructurados (como HTML y XML) en diferentes medios==
23. Sobre mysqli de PHP se puede decir: ==Es una clase==
24. Sobre el evento "onmousedown" en JavaScript se puede decir: ==Está definido para todos los elementos HTML==
25. En cuanto a los selectores en CSS: ==El selector "body>p" selecciona los párrafos que son hijos de los elementos del body==
26. Sobre XSLT se puede decir: ==Tiene sintaxis XML, No lo soportan los navegadores y es un estándar del W3C==
27. Sobre JSON se puede decir: ==Es un formato de texto==
28. Sobre el API Geolocation de HTML5 se puede decir: ==Está dentro del estándar del W3C==
29. Sobre el lenguaje TypeScript se puede decir: ==Es un lenguaje que tiene comprobación de tipos==
30. Para establecer la información referida a las palabras clave de un documento HTML5 válido se debe añadir < head >: `<meta name="keywords" content="british,type,face,font"> />`
31. Del árbol DOM (Document Object Model) construido a partir de un documento HTML5 válido se puede decir: ==Los elementos se representan como objetos que pueden ser manipulados con una API==
32. Que elementos se deben de utilizar para crear (marcar) secciones dentro de un documento HTML5 válido: ==< article >, < section >, < nav >, < aside >, < header >, < footer >, < address >==
33. Sobre el uso de tipos abstractos en XML se puede decir: ==Los tipos derivados NO pueden usarse en los mismos sitios que el tipo base==
34. En cuanto a la especificidad en CSS: ==El selector ".contenedor" tiene una especificidad de 010==
35. El elemento < link > de HTML5 sirve para: ==Vincular otros recursos==
36. Sobre el lenguaje derivado de XML denominado XAML se puede decir: ==Es utilizado por interfaces y tecnología .NET==
37. Sobre el evento "onunload" de Javascript se puede decir: ==Está definido para el elemento de HTML < body >==
38. Sobre `$_GET` en PHP se puede decir: ==Es superglobal==
39. Sobre los servicios Web se puede decir: ==Permiten la interración entre ordenadores==
40. Sobre el servicio "onblur" en JavaScript se puede decir: ==Está definido para los elementos HTML: < button >, < input >, < label >, < select >, < textarea > y < body >==
41. Sobre XAMPP se puede decir: ==Es un entorno de desarrollo local que permite trabajar con Apache, PHP, y MariaDB==
42. Sobre mysqli::query de PHP se puede decir: ==Que devuelve un objeto==
43. Sobre el lenguaje WebAssembly se puede decir: ==Su objetivo es incrementar la velocidad de ejecución==, y ==Es un formato binario basado en una máquina de pila==
44. Sobre ajax se puede decir: ==Utiliza el objeto predefinido XMLHttpRequest==
45. Sobre el objeto "Date" en JavaScript se puede decir: ==Es un objeto predefinido==
46. Sobre el uso del tipo duración (xs:duration) en XML se puede decir: ==< duracionRuta >P1Y7M29DT10H< /duracionRuta > indica una duración de 1 año 7 meses 29 días y 10 horas==
47. El modelo de caja CSS generado para un elemento < article > de HTML5: ==Se puede modificar mediante las propiedades margin, padding y border==
48. Sobre el lenguaje derivado de XML denominado XMI se puede decir: ==Es utilizado en el intercambio de metadatos de diseños de software en UML==
49. Sobre "const" en JavaScript se puede decir: ==Especifica que las constantes tienen ámbito local a un bloque==
50. Sobre XPath se puede decir: ==Permite acceder al árbol DOM de un documento XML==
51. Sobre `$_SERVER` en PHP se puede decir: ==Es un array asociativo==
52. El puerto que utiliza HTTPS es: ==443==
53. El puerto que utiliza HTTP es: ==80==
54. Sobre `$_POST` se puede decir: ==Es una variable superglobal==
55. Sobre PHP se puede decir: ==Es el lenguaje de script más utilizado en servidores==
56. Para establecer la información referida al autor de un documento HTML5 válido se debe
añadir al < head >: ==< meta name="author" content="pepito grillo" />==
57. Sobre jQuery se puede decir: ==Permite recorrer el árbol DOM y seleccionar los elementos HTML==
58. Sobre Window en JavaScript se puede decir: ==Es un objeto predefinido==
59. En cuanto a especificidad en CSS:

````css
#contenedor /*Especificidad 100*/

.contenedor /*Especificidad 010*/

body>p /*Especificidad 002*/

a[accesskey] /*Especificidad 011*/

* /*Especificidad 000 (selector universal)*/
````

---
# Datos que Cueva dice "importantes" en clase

- Primer navegador: ==Lynx==
- Primer navegador gráfico: ==ViolaWWW==
- HTML inicialmente sólo tenía **==22 etiquetas==**
- En un árbol DOM ==no podemos usar el elemento BASE==, en su lugar usamos los path relativos
- Metalenguaje: ==lenguaje para crear lenguajes==
- Última  norma de XML: ==Septiembre de 2006==
- $ es lo mismo que JQuery: ==$ es la abreviatura del constructor de jQuery==
- ¿Cómo se hace un bucle en jQuery?: ==$(this) recorro "cada" elemento==
- El padre de una celda es: ==la fila==
- AJAX: ==JavaScript Asíncrono y XML==
- El objeto XMLHttpRequest: ==es un objeto de JavaScript que permite usar la comunicación asíncrona==
- JSON: ==JavaScript Object Notation==
- ==Todo objeto JavaScript vive en el navegador==
- Inconveniente del uso de Ajax: ==no es accesible==
- Google Maps: ==no es accesible==
- $FILES: ==es la forma de acceder a un archivo del cliente, es un objeto predefinido, no hay que instanciarlo==
- mysql: ==es una clase==
- ==No se debe ejecutar instrucciones SQL directamente desde orígenes externos por la inyección de código==
- Uso de variables locales y globales en JavaScript
	- **==var y let==** en el interior de una función hace que la variable sea **local**, mientras que en el exterior de una función es **global**
- Lenguajes derivados de XML:

![](img/Pasted%20image%2020221217153849.png)
---