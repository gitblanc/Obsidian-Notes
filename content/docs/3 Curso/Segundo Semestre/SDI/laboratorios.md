---
title: Notas de Lab SDI 🌠
---
# Los servlets son multihilo

- Cada vez que el servidor accede al servlet, éste se ejecuta. Si se reciben varias peticiones, se ejecutarán de forma simultánea en hilos diferentes. No obstante, ambos hilos se ejecutan sobre la misma instancia del Servlet.
- Mediante **synchronized** bloqueamos un objeto y aseguramos que ese fragmento de código sea ejecutado por un único hilo a la vez.

## Manejo de sesión

- Si empleamos la clase HttpSession de la API de JEE podremos identificar de manera diferenciada las sesiones de usuarios y tener la posibilidad de guardar información (objetos) asociada a cada usuario de forma independiente.
![](img/Pasted%20image%2020230206163533.png|300)
- Para obtener un objeto en sesión usamos:
````java
HttpSession session = request.getSession();
PrintWriter out = response.getWriter(); //HttpServletResponse response
````
- Para comprobar que todas las peticiones van a la misma id:
![](img/Pasted%20image%2020230206164041.png)

# JSP - Java Server Pages

- Es prácticamente HTML
## Manejo de sesión

- Crear un fichero `login.jsp`
- Utilizando las etiquetas `<% %>` podemos introducir código Java en la JSP
- Para guardar una credencial en sesión:
````java
request.getSession().setAttribute("user", "admin")
response.setRedirect("admin.jsp") //se redirecciona a otra página web
````
![](img/Pasted%20image%2020230206165217.png|300)
- La variable application nos permite compartir datos en la aplicación con todos los usuarios.
- Application utiliza los métodos: `application.getAttribute(clave)` y `application.setAttribute(clave,valor)`

## JSP Beans

Los **Beans** son clases Java construidas en base a unas especificaciones:
-   Constructor por defecto sin argumentos.
-   Tienen “propiedades” (atributos) que pueden ser: leídas y/o escritas.
-   Se manejan a través de los métodos get y set de sus propiedades.
Un uso muy común de los Beans en JSP es la recuperación de datos de formularios, es decir, formar un objeto a partir de los parámetros recibidos.

- ==El producto(product) siempre va a contener un objeto != null ya que se crea automáticamente con el jsp:useBean. Por lo tanto, no vale con comprobar product != null, debemos comprobar el valor de sus propiedades.==

Si queremos hacer un contador común para todos los usuarios el ámbito del Bean sería “application”. Añadimos el atributo scope a la etiqueta useBean:
![](img/Pasted%20image%2020230206165914.png)
Ahora por cada instancia se incrementa el contador.

## Uso de tags JSTL Core

- Las etiquetas JSTL9 (JavaServer Pages Standard Tag Library) encapsulan gran parte de la funcionalidad común que se suele necesitar en las páginas web JSP. Usando estas etiquetas se evita incluir scripts de código Java propios.

- Para utilizar las etiquetas de JSTL debemos declarar el uso de JSTL, agregando la directiva al inicio de la página que se va a utilizar.
![](img/Pasted%20image%2020230206170048.png)
- `<c:forEach>` permite recorrer los elementos de una lista.
- Podemos acceder a sus atributos `#{product.<nombre_propiedad>}`. Para imprimir por pantalla el valor de la variable podemos utilizar `<c:out>`
![](img/Pasted%20image%2020230206170258.png)
- La directiva <c:if test=”exp”> permite ejecución condicional
![](img/Pasted%20image%2020230206170147.png)
- Utilizando Beans y JSTL podríamos llegar a prescindir de los scripts Java tradicionales.
![](img/Pasted%20image%2020230206170222.png)