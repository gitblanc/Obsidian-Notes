# Introducción

Abarca aquellas actividades que nos permiten conseguir un entendimiento más detallado y preciso de los requisitos:
- Analizar la información obtenida de los usuarios.  
- Detallar adecuadamente requisitos de alto nivel.  
- Estudio de los atributos de calidad.  
- Derivar requisitos funcionales a partir de otros requisitos.
- Definir prioridades.
- Identificar requisitos innecesarios o incompletos.

# Refinado de requisitos

El objetivo consiste en estudiar y detallar los requisitos de alto nivel producidos en la Obtención para elaborar requisitos de software.

- Requisito de alto nivel:  
	- El sistema generará una factura.
- Requisitos de software:
	- El sistema generará una factura por cada pedido realizado. 
	- El sistema realizará el proceso de generación de facturas cada hora.
	- Las facturas generadas por el sistema contendrán la siguiente información: (...)
	-  Por cada factura generada, el sistema cambiará el estado del pedido asociado a "Facturado".    
	- Por cada factura generada, el sistema creará un registro de cobro. 
		- El estado del nuevo registro de cobro será "Pendiente de pago".

# Modelado visual

![](./img/Pasted%20image%2020231003182947.png)

![](./img/Pasted%20image%2020231003183009.png)

![](./img/Pasted%20image%2020231003183110.png)

# Casos de uso

- **Caso de uso:** secuencia de interacciones entre un actor externo y un sistema que resulta en la obtención de un valor para dicho actor.

- Siempre siguen la estructura verbo + objeto.  
	- Comprar billete, elegir asientos, facturar equipaje...

- A partir de un caso de uso, se pueden extrapolar requisitos funcionales y sus correspondientes pruebas.

## Casos de uso. Actores

- No confundir usuarios y actores.
	- Un mismo usuario puede jugar el rol de distintos actores.
	- Recordad: un actor es una abstracción que define un participante en el caso de uso.

- Para identificar actores, tened presente:  
	-  ¿A quién se notifica un evento del sistema?  
	- ¿Quién provee servicios o información al sistema? 
	- ¿Quién ayuda al sistema a completar una tarea?

- Al igual que con los usuarios, no tienen por qué ser humanos.


## Diagramas de casos de uso

- Se emplean diagramas para representar los casos de uso.

- Hacemos uso de una notación basada en UML. * 
	- Una caja representa los límites del sistema.  
	- Los casos de uso se representan mediante óvalos.
	- Las flechas entre actores y casos de uso representan las interacciones. 
		- Actor -> caso de uso: actor primario del caso, lo inicia y obtiene valor.  
		- Caso de uso -> actor: actor secundario, interviene de algún modo.

![](./img/Pasted%20image%2020231003183753.png)

- Los diagramas de casos de uso pueden incluir las siguientes relaciones:
	- **Extensión**: un caso de uso añade pasos a otro caso de uso de primer nivel.
	- **Inclusión**: un caso de uso requiere a otro caso de uso que no puede existir por sí mismo y está duplicado en varios casos de uso.

![](./img/Pasted%20image%2020231003183924.png)

## Casos de uso de forma textual

- Un caso de uso ha de contener, como mínimo, la siguiente información: 
	- Identificador único y nombre descriptivo,  
	- Descripción textual.  
	- Condición que inicia el caso de uso.
	- Precondiciones a satisfacer para empezar el caso de uso (0+).  
	- Postcondiciones que describen el estado del sistema tras el caso de uso (1+). 
	- Flujo/s de eventos que tiene lugar durante el caso de uso.

- Otras recomendaciones:  
	- Fecha, autor, actores, prioridades, referencias, supuestos...

## Casos de uso: condiciones

- **Precondiciones**. Requisitos a cumplir por el sistema previa ejecución del caso de uso.
	- La condición de inicio (trigger) no es una precondición.  
	- El cajero automático debe disponer de efectivo para realizar una retirada de efectivo.
- **Postcondiciones**. Estado del sistema tras la ejecución del caso de uso. 
	- Cambios observables por el usuario.
	- Salidas físicas.  
	- Cambios internos en el sistema.  
	- El cajero automático debe actualizar su registro de efectivo tras una retirada.
- Es posible que las postcondiciones de un caso de uso sean las precondiciones de otro.
	- Combinando casos de uso para formar una macro.

## Casos de uso: flujos

- **Normales**. Representan la secuencia de acciones más habitual que produce un resultado satisfactorio. (Escenario primario)
- **Alternativos**. Representan secuencias de acciones menos comunes o relevantes que también producen un resultado satisfactorio. (Esc. secundario)
- **Excepciones**. Representan condiciones que pueden impedir un resultado satisfactorio.
	- Pueden ser recuperables o no.
	- Si no se especifican en esta fase:  
		- El manejo de errores puede ser inconsistente.  
		- El sistema puede fallar en determinadas condiciones.
	- Excepciones comunes (errores de conexión, de BD...) deberían extraerse a sus propios RF.

- Para representar los flujos usamos diagramas de actividad:

![](./img/Pasted%20image%2020231003185448.png)

## Casos de uso: escenarios

- Un escenario es una descripción de una instancia concreta de uso del sistema.

- Un caso de uso consta de múltiples escenarios relacionados... 
	- ...y un escenario es una instancia específica de un caso de uso.

- De cara al análisis de requisitos, podemos:  
	- Extrapolar escenarios específicos a partir de un caso de uso general.  
	- Generalizar un escenario concreto para obtener un caso de uso general.

![](./img/Pasted%20image%2020231003185640.png)

## Casos de uso: ejemplo

![](./img/Pasted%20image%2020231003190811.png)

![](./img/Pasted%20image%2020231003191021.png)

![](./img/Pasted%20image%2020231003191441.png)

![](./img/Pasted%20image%2020231003191515.png)

![](./img/Pasted%20image%2020231003191531.png)

## Casos de uso: nivel de detalle

- El nivel de detalle depende de la relevancia de cada caso.  
- Podemos limitarnos a una descripción del objetivo del usuario y sus interacciones con el sistema, o sólo mencionar los flujos.
- Una especificación completa puede ser apropiada si:
	- Se trata de un sistema complejo cuyos fallos ocasionan gran riesgo.
	- Los casos de uso representan requisitos novedosos para los desarrolladores.
	- Los casos de uso son los requisitos más detallados que los desarrolladores dispondrán.
	- Existirá escasa interacción entre los usuarios y el equipo de desarrollo.
	- Se pretende elaborar casos de prueba basados en los requisitos de usuario.

## Casos de uso: identificación

![](./img/Pasted%20image%2020231003192015.png)

## Casos de uso: elaboración

Pasos propuestos para la elaboración de casos de uso:  
1. Identificar el actor primario.  
2. Elaborar la descripción.  
3. Definir precondiciones y postcondiciones. Límites del caso. 
4. Definir el flujo normal de pasos.
5. Definir el resto de flujos.

## Requisitos funcionales y casos de uso

- Requisitos funcionales != casos de uso.  
	- Los casos de uso cubren únicamente el comportamiento "externo" del sistema.
- Debemos especificar los requisitos funcionales necesarios para implementar cada caso de uso.
	- P.e.: ¿Qué hacer si una precondición no se satisface?  
- Mantener trazabilidad entre casos de uso y requisitos funcionales.

## Casos de uso: problemas

![](./img/Pasted%20image%2020231003192812.png)

# Diagramas de flujo de datos

- Adecuados para sistemas de procesamiento de transacciones.

- Describen el movimiento de datos en un sistema.  
	- Comunicaciones, transformaciones, colecciones...  
	- Ejemplo: ¿cuántos datos requiere la creación de un pedido?

- Útiles para extraer requisitos de datos. 
- A menudo usados en entrevistas.

![](./img/Pasted%20image%2020231003193029.png)

- Algunas convenciones a tener en cuenta:  
	- Los datos no pueden comunicarse directamente entre entidades del mismo tipo. 
	- El DFD no debería tratar de representar la secuencia del proceso.  
	- Los procesos se identifican de manera única y dependiendo del nivel de detalle. 
	- Los procesos se nombran de forma concisa.  
	- Evitar 10+ procesos; abstraer procesos de mayor nivel si es necesario.  
	- Los procesos deberían tener tanto entradas como salidas de datos.

# Diagrama swimlane

- Representan las operaciones a realizar para ejecutar un proceso del sistema.

- Similares a los diagramas de actividad, pero subdivididos en secciones que representan a los actores que realizan una serie de pasos.

![](./img/Pasted%20image%2020231003193834.png)

# Diagramas de estado

- Describen los cambios de estado de un sistema bajo unas condiciones determinadas.
- Uso típico en sistemas de tiempo real y en la gestión de pedidos, inventarios y similares.
- Los cambios de estado se representan mediante flechas entre estados; los eventos que ocasionan dichos cambios se indican mediante etiquetas.
- Se suele representar alternativamente mediante una tabla de estados.

![](./img/Pasted%20image%2020231003193929.png)

# Mapas de diálogo

![](./img/Pasted%20image%2020231003194028.png)