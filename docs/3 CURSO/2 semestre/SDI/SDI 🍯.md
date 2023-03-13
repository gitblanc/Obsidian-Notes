# 26 Enero 2023 🍿

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

---
# 30 Enero 2023 🪀

## Spring vs SpringBoot
- **Spring**: framework basado en JEE que usa el patrón MVC (modelo vista controlador) para desarrollo de aplicaciones web cuya principal caracteróstica es el uso de un modelo POJO
- **SpringBoot**: no es un framework, es una forma fácil de desarrollar aplicaciones Spring pero facilitando los aspectos duros de Spring

## SpringBoot
- Aumenta la agilidad del desarrollo de aplicaciones en Spring
	- Provee de configuraciones por defecto
	- Uso opcional de POMs
	- Evita la generación de código y configuraciones XML
	- Permite crear aplicaciones stand-alone

## Spring
- Aplicaciones basadas en el patrón MVC
- Soporte completo al desarrollo de aplicaciones  POJO
- Sistema de inyección de dependencias basado en el IoC (**Inversion of control**: el responsable de instanciar es el framework)
- Gran cantidad de módulos con funcionalidad reutilizable
- Traducción de excepciones específicas a genéricas

## Standalone
![[Pasted image 20230130112326.png|500]]

## Entorno de desarrollo
- IntelliJ

## Main: condiciones
![[Pasted image 20230130112643.png|500]]
![[Pasted image 20230130112706.png|500]]

## @SpringBootApplication
- Tiene 3 anotaciones:
	- @Configuration
	- @EnableAutoConfiguration
	- @ComponentScan: se debe escanear la aplicación en busca de componentes implementados

## Elementos principales
![[Pasted image 20230130113352.png]]

- Todos son componentes
- Algunos añaden funcionalidad al componente
- Todos los componentes se procesan internamente como Beans (clase Java POJO con constructor por defecto y con getters y setters)
	- Los beans registrados contienen una instancia de un objeto
- Los componentes son instanciados y registrados como beans

## Elementos escaneables
![[Pasted image 20230130113906.png|500]]

## Controladores
- Componentes que procesan peticiones realizadas por los clientes
- El retorno es el nombre de una vista
![[Pasted image 20230130114240.png|500]]
- Suelen invocar la lógica de negocio definida en los servicios
- Las vistas pueden recibir un Modelo de datos con atributos
![[Pasted image 20230130114435.png|600]]
![[Pasted image 20230130114554.png|600]]

## Procesamiento en Spring
![[Pasted image 20230130114748.png|600]]

### @RequestParam
![[Pasted image 20230130115029.png|600]]
- Si no lo pasas uno de los parámetros casca

### Petición y parámetros
![[Pasted image 20230130115314.png|600]]

## Thymeleaf
- Es la plantilla de acceso a los atributos del modelo
![[Pasted image 20230130120115.png|600]]
- El modelo contiene atributos
![[Pasted image 20230130121508.png|600]]
![[Pasted image 20230130121619.png|600]]
![[Pasted image 20230130121724.png|600]]
![[Pasted image 20230130121743.png|600]]

## Servicios
- Componentes que contienen lógica de negocio
- Suelen ser utilizados desde los controladores o desde otros servicios

## Repositorios
- Son los componentes que acceden a la base de datos
- Suelen ser utilizados desde la capa de servicios
- El repositorio puede usar multitud de APIs para acceder a la base de datos

---
# 6 Febrero 2023 🪬
- Un interceptor en un Servlet personalizado.
- LocaleChangeInterceptor: interceptor que permite definir un parámetro para realizar cambios de localización:
![[Pasted image 20230206114901.png]]
- ISO 639 -> especificación del código de idiomas (es, en, it...)
- Se suelen usar varios ficheros de propiedades, uno por cada localización:
![[Pasted image 20230206115504.png]]
- **antmatcher**: especificación url en los cuales pueden aparecer comodines (un sólo asterisco es un único nivel, dos son todos los niveles que queramos)
![[Pasted image 20230206121920.png]]

---
# 13 Febrero 2022 🍎

- Una sesión se destruye automáticamente tras un tiempo de inactividad
- El Bean **HttpSession** permite acceder a la sesión (funciona como un hashmap)
- Formas de tratar la sesión en Spring:
	- Las plantillas **Thymeleaft** pueden acceder a la sesión:
		- **Indirectamente**: atributos del modelo eviados desde el controlador a la plantilla
		- **Directamente**: usando el objeto {session}
	- Anotación @SessionScope
		- ==Conseguir que todos los Beans se gestionen como singleton (que todos los accesos se traten como una instancia)==
- Las URLs con **datos/acciones sensibles** dolo pueden ser usadas por ciertos usuarios (ej: no todos los alumnos pueden ver todas las asignaturas, sólo aquellas a las que estén matriculados)
- Usar **AccessDecisionVoter**
- No se deben manejar coleciones con muchos recursos/entidades. Se debe usar **paginación**:
	- Clase `Page<E>`
- La siguiente a la actual (page=getNumber+1) si es que existe (<=getTotalPages)
- La ultima (page=getTotalPages - 1) siempre
- Todas las excepciones producen rollback

---
# 20 Febrero 2023 🍓
- Están **==prohibidas==** las **esperas incondicionales** -> `Thread.sleep()`

---
# 6 Marzo 2023 🌏

## Node.js
- Es una plataforma de software que nos permite ejeutar JavaScript del lado del servidor
- No es un framework
- Características:
	- Basado en un **diseño modular**:
		- Cada funcionalidad es dividida en módulos o paquetes separados
		- Por defecto cuando se instala Node, se incluye un conjunto de módulos
		- La gestión de dependencias o paquetes se realiza con **NPM**
	- **Modelo de operaciones I/O asíncrona o sin bloqueo**:
		- Se usa para leer o escribir en el sistema de archivos, lmacenar información en bases de datos y establecer comunicación de red o comunicarse con otros componentes
		- Las operaciones son bloqueantes
		- Las operaciones se ejecutan de forma secuencial
		- El programa permanece bloqueado hasta que termine la operación
		- El cliente espera la respuesta del servidor para continuar con el flujo del programa

---
# 13 Marzo 2023 🐚

- **express-generator**: herramienta que permite crear rápidamente un esqueleto de aplicación Node.js
	- Instalar con `npm install express-generator`
	- Crear el esqueleto: `express --view=pug myapp`
	- `cd myapp` 
	- `npm install`
	- `npm start`
- Estructura de directorios de una aplicación con express:
![[Pasted image 20230313113333.png|200]]
- El app.js es el primer fichero que se ejecuta

---