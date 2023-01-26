# 26 Enero 2022 🍿

## Servlets
- Pueden ser scripts de python, una página php..., es decir, cualquier tecnología que pueda ser ejecutada en el servidor
- ==Para poder ejecutar algo hay que desplegar ese algo dentro del servidor==

## Arquitectura web básica 
![[Pasted image 20230126151853.png|500]]
 ![[Pasted image 20230126152212.png|500]]

- Utilizaremos Java 17

## Especificación JEE (Java Enterprise Edition)

### Arquitectura J2EE
![[Pasted image 20230126152649.png|500]]

## ¿Qué es un Servlet?
- Es una clase Java wue acepta peticiones HTTPS y devuelve respuestas usando también HTTP.
- Se ejecuta dentro de un contenedor de Servlets que a su vez está dentro de un servidor de aplicaciones JEE

## Ciclo de vida de un Servlet 
![[Pasted image 20230126153428.png|500]]

## Tipos de peticiones HTTP
![[Pasted image 20230126153639.png|500]]

- ==Pregunta de examen== -> ¿Cuál es el método genérico desde el cual se invoca a los métodos do() genérico?: `service()`

## Registro de un Servlet
![[Pasted image 20230126154111.png|300]]

## Recogida de información de un usuario
- Usar `Object HttpServletRequest.getParameter(nombre)`

## Mantenimiento del estado de la sesión
![[Pasted image 20230126154355.png|300]]
- **Sesión**: variables que se almacenan (permanecen) en el servidor a instancias de una petición del cliente. Las sesiones suelen estar basadas en cookies.

### Seguimiento de la sesión
![[Pasted image 20230126154745.png|500]]
![[Pasted image 20230126154807.png|500]]

## JSP
![[Pasted image 20230126155427.png]]
==Pregunta examen==: los servlets resuelven los problemas de presentación

## Elementos de JSP
- Scripting
- Directivas
- Acciones
![[Pasted image 20230126155842.png||500]]

## Objetos predefinidos JSP
![[Pasted image 20230126155937.png||500]]

## Directivas
![[Pasted image 20230126160051.png||500]]

## Acciones
![[Pasted image 20230126160121.png||500]]