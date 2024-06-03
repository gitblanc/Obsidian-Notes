---
title: Preguntas Examen Teoría NodeJS 🚁
---
1. Nodejs mejora la concurrencia porque su arquitectura se basa:
- ==Un solo hilo de ejecución con un bucle de eventos==
2. Son características de una comunicación asíncrona:
- ==Las operaciones no son bloqueantes==
- ==Se realizan mediante el sistema de callback(retrollamadas) y/o promesas==
3. ¿Qué es Nodejs?
- ==Una plataforma de software que permite ejecutar JS del lado del servidor==
4. ¿Qué tipo de escalabilidad usa Nodejs para las aplicaciones?
- ==Horizontal==
5. En una aplicación Nodejs, el fichero package.json contiene:
- ==La configuración y los metadatos de la aplicación==
- ==Las dependencias==
6. Es un framework de desarrollo de aplicaciones web minimalista y flexible para Nodejs
- ==Express==
7. En Nodejs la función require se utiliza para:
- ==Importar módulos==
8. ¿Cómo se denominan las funciones que se ejecutan cuando se recibe la petición en una app Nodejs?
- ==Handler (manejadores)==
9. Forma de incluír un módulo en Nodejs:
- `require(./routes/users.js)(app);`
- `let express = require('express');`
10. Una plantilla Twig recibe un atributo con clave "nombre". ¿Cómo se insertaría el valor de ese atributo en un elemento h1?
`<h1>{{ nombre }}</h1>`
11. Para obtener los valores de los parámetros enviados en una petición GET en Nodejs se utiliza:
- `req.params.<clave_parametro>`
- `req.query.<clave_parametro>`
12. ¿Cuál es el objetivo principal de los servicios web?
- ==Permitir la interoperabilidad entre aplicaciones==
13. ¿Por qué los servicios web son adecuados para entornos Web?
- ==Emplean tecnologías estándares como HTTP, SOAP, XML, JSON...==
14. ¿En qué consiste el principio HATEOAS de una API REST?
- ==Los mensajes deben contener enlaces a otros recursos de la API==
15. ¿En qué filosofía se basa REST?
- ==Se basa en una filosofía orientada a recursos==
16. Una petición web a un recurso REST
- ==Debe retornar un código de respuesta estándar==
- ==Debe retornar una respuesta en formato estándar==
17. &nbsp; ¿Cómo gestiona Nodejs las operaciones de I/O?
- ==De forma asíncrona y sin bloqueo==
18. Para obtener los valores de los parámetros enviados en una petición POST en Nodejs se utiliza:
- `req.body.<clave_parametro>`
19. ¿Qué función de Nodejs se utiliza para leer datos de un formulario HTML enviado a un servidor?
- ==body-parser==
20. ¿Cuál de los siguientes módulos se utiliza para crear un servidor web en Nodejs?
- ==http==
21. Es una forma de declarar un módulo en Nodejs
- `module.exports = function() {...}`
22. Se utiliza para describir la funcionalidad que proporciona un servicio web SOAP
- ==WSDL==
23. Es un estándar basado en XML para el intercambio de información entre aplicaciones en entornos descentralizados y distribuidos:
- ==SOAP==
24. Es un mecanismo que le permite a una aplicación realizar transferencias seguras de datos en dominios cruzados entre navegadores y servidores web
- ==CORS==
25. Lenguaje de dominio específico de JHipster que sirve para describir las entidades y sus relaciones de una aplicación web
- ==JDL==
26. En MongoDB, una colección:
- ==Almacena documentos que pueden tener estructuras diferentes==
27. ¿Cuál es la principal diferencia al definir un módulo como un objeto y no como una clase o función en una aplicación Nodejs?
- ==Al incluir el módulo varias veces, todos retornan la referencia al mismo objeto==
28. ¿Cuál sería la mejor alternativa para utilizar un módulo desde otros módulos en una aplicación Nodejs?
- ==Obtener el objeto/función una vez y enviarlo como parámetros a otros módulos==
29. Es una de las principales ventajas de MongoDb
- ==No necesita definir un esquema previo==
30. Los servicios web SOAP permiten el intercambio de información en formato:
- ==XML==
31. En una aplicación Nodejs, el fichero package.json contiene:
- ==La configuración, las dependencias y los metadatos de la aplicación==
32. En MongoDB, la información se almacena en formato:
- ==BSON==
33. Un documento contiene:
- ==Un objeto BSON con atributos que pueden tomar diferentes valores==
34. Desventajas de MongoDB:
- ==No es adecuada para aplicaciones con transacciones==
- ==No soporta transacciones ACID==
- ==Sin garantía de integridad de datos==
- ==Menos soporte para consultas complejas==
- ==Uso intensivo de recursos==
35. En MongoDB:
- ==Los documentos se almacenan en colecciones==
- ==Una colección es la carpeta donde se almacenan los documentos==
- ==La colección no define la estructura de documentos (no es una tabla)==
- ==Cada documento puede seguir una estructura diferente==
- ==La estructura de un documento puede ser modificada dinámicamente==
36. La función del enrutador puede:
- ==Ejecutar cualquier lógica de negocio==
- ==Dejar correr la petición==
- ==Cortar la petición==

