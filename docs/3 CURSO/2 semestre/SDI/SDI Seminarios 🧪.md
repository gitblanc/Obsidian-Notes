# 3 Febrero 2023 💊

## Protocolo HTTP
- El cliente suele ser el navegador
- GET: sirve para recuperar información
- POST: sirve para crear nueva información
	- PATCH: envía exclusivamente los datos a modificar del recurso
- PUT: sirve para modificar completamente un recurso

## ¿Cómo funcionan los formularios?
Responden a tres preguntas:
- ¿cómo (método get,post,...), a quién(action) y el qué (los datos)?

---
# 17 Febrero 2023 🥑
## REPASO EXAMEN
### Estas preguntas no están subidas ni en ninguna diapositiva
1. ¿Qué elemento de una aplicación JEE se encarga de :
	- Recibir las peticiones HTTP
	- Redireccionarlas a servlets específicos
			==Contenedor de Servlets==
	
2. Nombra dos métodos incluidos en la interfaz Servlet, explica muy bien para qué sirven
init y destroy, doGet, doPost

3. En un ciclo de vida de un servlet cuantas veces se podría ejecutar la función init() y doGetO
	- Especificar cuantas como mínimo y como máximo
		- ==Init: mínimo 1 máximo 1
		- ==doGet(): mínimo 0, máximo infinito==

4. Desde un servlet, explica la diferencia funcional entre obtener un valor "nombre" con:
 A) request. getParameter("nombre")
 B) request. getSession.getAttribute("nombre")
==El ámbito es diferente
 A) obtener el parámetro nombre de la petición actual
 B) obtener el atributo nombre de la sesión del cliente==

5. ¿Sobre qué elemento básico de JEE se contruye una JSP?
- ==Cada JSP se transforma en un Servlet==

6. ¿Principal ventaja de las JSP sobre las tecnologías anteriores?
==Mayor separación entre presentación y lógica de negocio
- ==Generar HTML por código dificultaba:
- ==Separación de tareas: lógica y diseño==

7. ¿Qué tres tipos de elementos puede contener una JSP?
- ==Directivas, acciones y scripting (elementos de secuencia)==

8. ¿En la siguiente directiva JSP que es "gestorCanciones"?
`«jspisetProperty name= "gestorCanciones" property= "canciones "value= "27>`
- ==Un Bean / el identificador / nombre de un Bean==

9. ¿En una arquitectura MVC en JE que elemento se utilizaría para implementar el modelo (lógica de negocio y datos)?-> Servlets, Beans y JSPs
- ==Los Beans (clases Java) son los que se encargan de la lógica de negocio==

10. ¿En qué consiste el patrón Fachada?¿Cuál es su principal ventaja?
- ==Interfaz único simplificado con los servicios más generales del sistema
- ==Interfaz simple para un subsistema capa / compleja
- ==Reducir el acoplamiento==

11. ![[Pasted image 20230217163822.png|600]]
- ==Fachada==

12. ![[Pasted image 20230217164056.png|600]]
- ==Presentación y persistencia no pueden comunicarse entre ellas==

13. ![[Pasted image 20230217164159.png|600]]
14. ¿Quién recibe antes una petición, un controlador o un interceptor?
	- ==El interceptor recibirá antes la petición==
- ¿Cuál es la función del LocaleChangeInterceptor en los sistemas de internacionalización?
	- ==Se utiliza para detectar si las peticiones incluyen el parámetro que indica el idioma, ej Lang=es==
15. ![[Pasted image 20230217164639.png|600]]
16. ¿Según la siguiente configuración que se requiere para que una petición pueda acceder a la URL /barco/eliminar?, razona la respuesta.
http .authorizeRequests ()
==.antMatchers ("/barco/add") .authenticated ()==
vantMatchera ("/barco") .hasAuthority ("ROLE USUARIO")
.antMatchers (*/barco/as*) .hasAuthority ("ROLE ADMIN")
anyRequest () . permitAlI ()

17. ![[Pasted image 20230217164834.png|600]]
18. ¿Qué dos tipos de validaciones de datos de entrada podríamos aplicar? Nombralos y explícalos brevemente. ¿Cuáles son más seguras?
- ==cliente: utilizan código de script que valida los datos de entrada en el propio navegador del diente antes de enviar los datos al servidor
- ==servidor: son comprobaciones en el servidor sobre los datos enviados por el cliente.
- ==Las validaciones en el servidor son más seguras.==

19. ![[Pasted image 20230217165205.png]]

20. 1) ¿Qué es el objeto sesión? 2) Pon un ejemplo de uso común.
- ==Es un objeto propio de cada cliente / usuario
	- ==Se identifica con una ID única que viaja en cada petición realizada por el navegador.
	- ==En el objeto sesión se pueden almacenar/recuperar datos por claves
- ==Almacenar productos temporalmente en el carrito de la compra==

21. Completa el siguiente código, se debe utiliza HttpSession para guardar la fecha del último inicio de cada usuario:
![[Pasted image 20230217165522.png]]
22. ¿Cómo afectaría a los formularios de la aplicación incluir protección contra ataques CSRF
- ==deberían incluir un parámetro nuevo con el token CSRF
- ==El token es generado por la aplicación==

23. ![[Pasted image 20230217165803.png]]
- ==asignaturasRepository.findOne solo recibe el ID de la nota
- ==El repositorio debería recibir también una referencia al usuario==

24. ![[Pasted image 20230217165938.png]]
26. ![[Pasted image 20230217170015.png]]
- ==De esta no tengo la solución==

---

