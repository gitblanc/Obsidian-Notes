---
title: Apuntes para Examen Teoría DS 👣
---
>[!Tip]
>Si quieres ir directamente al grano, te recomiendo que hagas `Ctrl + F` y busques ==Pregunta típica de examen==. Así sólo te estudias "lo más relevante"

# Tema 1. Introducción al diseño OO

## Diseño vs Análisis

- **Análisis**: pone énfasis en una investigación del problema y los requisitos, en vez de en la colución
- **Diseño**:  pone énfasis en una solución conceptual que satisface los requisitos
	- Es importante un buen diseño por el **cambio**

## Representación en UML

![](img/Pasted%20image%2020240602110840.png)

## Resultado del diseño OO

Se obtiene como resultado:
- Un sistema de objetos que satisfacen los requisitos
- Una descripción del comportamiento público de esos objetos
- Cómo se comunican esos objetos entre sí

![](img/Pasted%20image%2020240602111004.png)

## Orientación a objetos

- El diseño orientado a objetos construye las aplicaciones mediante una estructura de objetos que colaboran entre sí
- Cada objeto realiza unas operaciones que lo caracterizan
	- No importa cómo las realice, sino cuáles realiza
	- La implementación de esas operaciones son los **métodos**
- Un **objeto** lleva a cabo una **operación** cuando recibe una petición (o mensaje) de un cliente
	- Un mensaje es la única forma de decirle a un objeto que ejecute una operación
	- Las operaciones son el único modo de cambiar el estado interno del objeto
	- Por ese motivo, se dice que el estado interno del objeto está **encapsulado**
		- No se puede acceder a él directamente, y su representación es invisible desde el exterior del objeto

## Mensajes

- Una aplicación realiza sus operaciones mediante la combinación de las operaciones de uno o más objetos
- Cuando se desea que un objeto realice una operación se le envía un mensaje
- Para realizarla, podrá enviar a su vez mensajes a otros objetos

![](img/Pasted%20image%2020240602111618.png)

## Interfaz de un objeto

- **Signatura de la operación**: es lo que especifica cada operación declarada por un objeto (su nombre, los objetos que recibe como parámetros y el tipo de valor devuelto por la operación)
- **Interfaz de un objeto**: es el conjunto de todas las signaturas (públicas) definidas por él
	- Es decir, todas las peticiones que pueden hacérsele
- **Tipo**: es un nombre usado para denotar una determinada interfaz
	- Decimos que un objeto es del tipo `Window` si puede aceptar todas las peticiones para las operaciones definidas en la interfaz `Window`
	- Un **objeto puede tener muchos tipos**, así como objetos muy diferentes pueden compartir un mismo tipo
	- Un tipo es **subtipo** de otro si su interfaz contiene la interfaz de su **supertipo**

## Enlace dinámico

- **Enlace dinámico**: asociación en tiempo de ejecución que tiene lugar entre la petición a un objeto y una de sus operaciones. Permite:
	- Escribir programas que esperen un objeto con una interfaz determinada, sabiendo que cualquier objeto que tenga esa interfaz aceptará la petición
	- Sustituir en tiempo de ejecución un objeto por otro con la misma interfaz (**polimorfismo**)

## Polimorfismo

- **Polimorfismo**: es la capacidad de dos o más tipos de objetos de responder al mismo mensaje, cada uno a su manera
	- Un objeto no necesita saber a quién está enviando el mensaje

>[!Example]
>El polimorfismo nos permite tener una lista de figuras y poder dibujarlas todas sin conocerlas (sin saber de qué tipo concreto es cada una):

![](img/Pasted%20image%2020240602112614.png)

## Clase

- **Clase**: es una de las formas de crear tipos en Java

### Definición de las clases

1. Determinar el nombre que se quiere dar al conjunto de operaciones
2. Elección de las operaciones que realizarán los objetos del nuevo tipo (qué mensajes podrán recibir)
	- Las operaciones pueden ser de dos tipos:
		- **Acciones**: ordenan al objeto hacer algo
		- **Consultas**: piden al objeto alguna información
3. Implementación de los mensajes

## Creación de objetos

- Los objetos se crean instanciando clases
- Un objeto se dice que es una instancia de una clase

### Síntomas de programación estructurada encubierta

==Pregunta típica de examen==

- Métodos largos
	- Más de 10 líneas (no se está delegando)
- Abundancia de llamadas a métodos del mismo objeto
- Preguntarse cómo se calcula un factorial en un lenguaje OO
	- Lo importante es el quién, no el cómo
- Típica clase de `Utilidades`
	- No se encuentra un quién: no se han asignado bien las responsabilidades

## Atributos

- **Atributos**: almacenan el estado interno del objeto, es decir, forma de guardar la información para su posterior uso por otros mensajes

![](img/Pasted%20image%2020240602113615.png)

>[!Tip]
>- No se debe empezar el diseño de una clase por sus atributos, ya que si la clase cambia, éstos también lo harán.
>- No hay que plantear la implementación como formas de modificar dichos atributos.
>- En vez de eso, se han de plantear las acciones que debe realizar el objeto
>- Nunca poner como atributo lo que debería ser una variable local de un método

## Parámetros

- **Parámetros**: son la forma de enviar información junto con el mensaje (en caso de que un objeto necesite información adicional para llevar a cabo una operación)

## Opciones y operandos

- **Opción**: representa una forma de operar con los operandos
- **Operando**: es un objeto que el método necesita para operar

>[!Tip]
>¿Cómo diferenciarlos?
>- Los **operandos** permanecen estables mientras que las opciones pueden variar a medida que la clase evolucione
>- Un parámetro es una **opción** si se puede encontrar un valor predeterminado adecuado

![](img/Pasted%20image%2020240602114424.png)

`document` es un operando y el resto son opciones (ya que pueden tener un valor predeterminado: A4, false, 1920x1080)

![](img/Pasted%20image%2020240602114554.png)

### Ventajas de separarlos

- Es más fácil de invocar al mensaje
- A medida que la clase evolucione se podrán añadir más opciones, pero los clientes de la clase no se verán afectados

![](img/Pasted%20image%2020240602114753.png)

![](img/Pasted%20image%2020240602114809.png)

![](img/Pasted%20image%2020240602114837.png)

>[!Note]
>- En la primera versión, el cliente debía conocer todas las opciones permitidas por la impresora ***aunque no las utilizase***
>- En la segunda forma al cliente se le pasa la impresora en el estado adecuado para que éste la utilice como se desea

*Mezclar estos conceptos significa no aplicar aún el concepto de **estado de un objeto***

## Estado de un objeto

- **Estado de un objeto**: es la combinación de los valores de los atributos de un objeto
	- Los valores de los atributos determinarán el comportamiento del objeto ante los distintos mensajes que reciba
	- El estado de un objeto determina la respuesta del objeto ante cada uno de los mensajes:
		- Determina qué mensajes no son permitidos
		- Determina el modo de actuar de los permitidos

- Guardar el estado de un objeto supone guardar la suficiente información para que al recuperarla se obtengan exactamente las mismas respuestas ante la misma secuencia de mensajes

## Encapsulación

- Normalmente no se debe dar acceso a los datos internos de un objeto

![](img/Pasted%20image%2020240602115449.png)

### Ventajas

- Permite controlar las modificaciones del atributo

![](img/Pasted%20image%2020240602115553.png)

- Ocultar los atributos permite modificar la implementación sin afectar a los clientes

![](img/Pasted%20image%2020240602115636.png)

## Criterio de independencia

- **Criterio de independencia**: cuanto menos se sepa de la implementación de un objeto menos afectarán sus cambios
	- Lo único importante de un objeto son los **mensajes** que puede recibir

## Estado concreto y estado abstracto

>[!Example]
>- Si en una clase `Temperatura` al pedir los datos en Celsius están en Fahrenheit... ¿se cambia el estado del objeto?
>	- No, porque no cambia sus respuestas, es decir, no cambia su comportamiento

- **Estado concreto**: se define en función de los atributos (podría variar en dependiendo de la implementación)
- **Estado abstracto**: se define en función de las respuestas a los mensajes

>[!Note]
>Cuando hablamos de estado siempre nos referimos al **estado abstracto**

## Diseño de clases

- Lo difícil es averiguar qué clases poner y con qué mensajes cada una

### Lo que no funciona

- Basarse en objetos reales
- No sirve extraer nombres y verbos del lenguaje natural
	- El **ascensor** tiene una **puerta** que se *abre* y se *cierra*
- Además puede expresarse de varias maneras
- Intentar sacar clases sin saber todavía qué tienen que hacer
- Centrarse en las tareas que realizar (el *qué*) y no separarlo jamás del *quién* (sino sería programación estructurada)

### Guía práctica

1. Elegir una tarea a realizar (el *qué*)
	- Decidir qué tipo de objeto lo hará
	- ¿Puede hacerla alguna de las clases que ya tenemos?
		- Si es así, añadir la nueva operación a dicha clase
2. Decidida la clase y la responsabilidad, tocan los mensajes
	- Dividir la responsabilidad en operaciones atómicas (para que se puedan combinar)
	- Parámetros con información imprescindible (el resto **opciones**)
	- Sacar partido de que los objetos "recuerdan" los que se les ha mandado (crear objetos inteligentes)
3. Implementación de las operaciones (los métodos)
	- Cualquiera que no tenga errores
	- No preocuparse por la eficiencia hasta el final

## Interfaces vs Clases abstractas

- **Interfaces**: permiten comunicar objetos que no se conocen

![](img/Pasted%20image%2020240602121247.png)

![](img/Pasted%20image%2020240602121318.png)

![](img/Pasted%20image%2020240602121341.png)

![](img/Pasted%20image%2020240602121458.png)

La revisión del contrato se hará de manera estática:

![](img/Pasted%20image%2020240602121537.png)

### Tipos de herencia

- **De interfaz**: declaramos el compromiso de implementar unos métodos (*subtipos*)
- **De implementación**: creación de una clase a partir de la implementación de otra (*reutilización de código*)

>[!Tip]
>**Criterio de diseño**
>- Cuando un objeto deba delegar ciertas operaciones en otro deberá exigírselas mediante una interfaz
>	- Importan los mensajes que acepta el objeto, no de quién ha obtenido su implementación

## Reutilización con interfaces

![](img/Pasted%20image%2020240602121916.png)

![](img/Pasted%20image%2020240602121932.png)

Solución:

![](img/Pasted%20image%2020240602121948.png)

## Clases abstractas

- Usos:
	- Factorizar código propio
	- Facilitar la extensión

### Ejemplo de factorizar código propio

![](img/Pasted%20image%2020240602122909.png)

![](img/Pasted%20image%2020240602122924.png)

- El jubilado y el catedrático hacen prácticamente lo mismo. ¿Cómo lo evitamos?
	- Mediante clases abstractas

![](img/Pasted%20image%2020240602123025.png)

### Ejemplo de facilitar la extensión

![](img/Pasted%20image%2020240602123233.png)

![](img/Pasted%20image%2020240602123330.png)

Se puede aprovechar código ya implementado:

![](img/Pasted%20image%2020240602123446.png)

- Copiando y pegando código sería:

![](img/Pasted%20image%2020240602123522.png)

Aquí es donde nacen los métodos abstractos:

![](img/Pasted%20image%2020240602123555.png)

## Jerarquías de interfaces

![](img/Pasted%20image%2020240602123758.png)

En Orientado a Objetos:
- Se extraen las entidades
- Se buscan las relaciones entre ellos (herencia, agregación y asociación)
	- "Es un", "tiene un", "parece casi como un"...

>[!Tip]
>Nunca debe surgir una jerarquía como manera de clasificación
>- Hay que comprobar si toda interfaz tiene al menos un cliente que la use

![](img/Pasted%20image%2020240602124036.png)

>[!Tip]
>**Sin necesidad no hay interfaz**


## Jerarquías de clases abstractas

![](img/Pasted%20image%2020240602124249.png)

![](img/Pasted%20image%2020240602124329.png)

![](img/Pasted%20image%2020240602124346.png)

>[!Note]
>Una jerarquía de implementación (de clases abstractas) no es esencial que sea estable
>- El cliente sólo conoce la interfaz
>- No sabe si debajo de esa interfaz hay una jerarquía de clases abstractas para ahorrar código o clases que implementan directamente la interfaz (no trata directamente con ellas)
>- No le afectan las reorganizaciones que haya de sus implementaciones
>
>Las jerarquías de implementación son para compartir código común y puede reestructurarse cuantas veces se necesite
>- Hay que reorganizar el árbol en función de las necesidades actuales


>[!Example]
>Veamos qué ocurriría si tuviésemos dos o más interfaces, cada una con su correspondiente implementación base que quisiéramos aprovechar, en un lenguaje como Java que no tiene herencia múltiple.

![](img/Pasted%20image%2020240602124903.png)

Posible solución:

![](img/Pasted%20image%2020240602124920.png)

![](img/Pasted%20image%2020240602124935.png)

## Tabla Interfaz vs Clase abstracta

==Pregunta típica de examen==

|                                     | Interfaz                                                                              | Clase abstracta                                                                    |
| ----------------------------------- | ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **Situación en la que se originan** | Extracción de responsabilidades                                                       | Facilitar nuevas implementaciones. No repetir código                               |
| **Creador**                         | Analista/Diseñador                                                                    | Programador                                                                        |
| **¿Raíz?**                          | Sí                                                                                    | No                                                                                 |
| **Importancia**                     | Fundamental: es el enlace dinámico, lo que nos permite eliminar la lógica condicional | Comodidad (es un mero cortar y pegar)                                              |
| **Operaciones**                     | Añaden a las de sus ancestros                                                         | Implementan las de sus ancestros. Añaden operaciones de implementaciones parciales |
| **Impacto de los cambios**          | Alto; es un contrato que afecta a varios programadores                                | Bajo; la interfaz hace de cortafuegos                                              |

![](img/Pasted%20image%2020240602125450.png)

## ¿Qué quiere decir que las interfaces hacen de cortafuegos?

==Pregunta típica de examen==

En un buen diseño software, en **la raíz** de una jerarquía siempre debería situarse una interfaz ya que representan un contrato como resultado de las necesidades del cliente. A éste no le interesa el cómo (lo hace), sino el qué (deben poder hacer los objetos que implementan dicha interfaz).

Si no lo hiciéramos así y usásemos una clase base (abstracta o no) como raíz de la jerarquía, nos estaríamos atando a una determinada funcionalidad que ante un cambio en los requisitos lo que era común en las subclases ya no lo sea.

En definitiva, con una **interfaz** el cliente no se inmuta si cambia el cómo, mientras que con una **clase base**, se vería afectado ante un cambio.

## Síntomas de un diseño pobre

==Pregunta típica de examen==

- **Rigidez**: *es difícil de cambiar* 
	- Representa una resistencia al cambio
	- Un diseño es rígido si un simple cambio causa una sucesión de cambios en cascada en otros módulos dependientes
- **Fragilidad**: *es fácil que falle*
	- Un programa es frágil si un cambio en una parte del sistema causa un fallo en otras partes no relacionadas conceptualmente
	- Estos son los módulos que continuamente están siendo reparados
- **Inmovilidad**: *es difícil de reutilizar*
	- Es difícil separar el código en componentes que puedan ser reutilizados en otros sistemas (el esfuerzo de separarlo es demasiado grande)
- **Viscosidad**: *es difícil hacer lo correcto*
	- Se refiere a que es más fácil hacer las cosas mal en lugar de bien
	- Un proyecto viscoso es aquél en el que resulta difícil preservar el diseño original
	- **Viscosidad del software**: si hacer los cambios respetando el diseño original es más costoso que hacerlos mal
	- **Viscosidad del entorno de desarrollo**: si es lento e ineficiente (tiempo de compilación elevado...). Condiciona las decisiones de los desarrolladores
- **Complejidad innecesaria**: *sobrediseño*
	- Si el diseño contiene elementos que no resultan útiles (demasiada anticipación a los cambios en los requisitos)
	- Mucha de esa funcionalidad no se utilizará
	- Hace el software complejo y difícil de comprender
- **Repetición innecesaria**: *"copiar y pegar"*
	- Duplicación de código
	- El coste del cambio es cada vez mayor y es propenso a errores
- **Opacidad**: *es complejo averiguar su intención*
	- Dificultad de comprender un módulo o un programa
	- Debemos hacer un esfuerzo constante por mantener siempre el código tan claro y expresivo como sea posible
		- Que revele su intención
		- Debemos ponernos en el papel de quien va a leer nuestro código

## Principios SOLID

==Pregunta típica de examen==

- **SRP** (*Single Responsibility Principle*, Principio de Responsabilidad Única): Una clase debería tener un único motivo para cambiar
	- Definimos responsabilidad como una razón para el cambio
	- Si podemos pensar en más de un motivo por el que la clase debería cambiar, dicha clase tiene más de una responsabilidad

>[!Example]
>![](img/Pasted%20image%2020240602131818.png)
>
>![](img/Pasted%20image%2020240602131852.png)
>
>Este diseño viola el principio SRP, pues la clase `Rectangle` tiene dos responsabilidades

- **OCP** (*Open-Closed Principle*, Principio de abierto-cerrado): las clases deberían estar abiertas para la extensión, pero cerradas para la modificación
	- La idea es que **los cambios se hagan añadiendo código nuevo**, no modificando el anterior que funcionaba
	- Los principales mecanismos para lograr el principio de abierto-cerrado son la abstracción y el polimorfismo

>[!Example]
>![](img/Pasted%20image%2020240602132205.png)
>
>![](img/Pasted%20image%2020240602132237.png)

- **LSP** (*Liskov Substitution Principle*, Principio de sustitución de Liskov): los subtipos deben poder sustituir a sus tipos base
	- Los objetos de un programa deberían ser reemplazables por instancias de sus subtipos sin alterar el correcto funcionamiento de un programa
	- Debemos asegurarnos de que las clases derivadas extiendan la clase base sin alterar su comportamiento de manera que se viole el contrato

>[!Example]
>![](img/Pasted%20image%2020240602132538.png)
>
>![](img/Pasted%20image%2020240602132558.png)

- **DIP** (*Dependency Inversion Principle*, Principio de inversión de dependencias):
	- Los módulos de alto nivel no deben depender de los de bajo nivel; ambos deben depender de las abstracciones
	- Las abstracciones no deben depender de los detalles, sino éstos de las abstracciones
	- Se le conoce como el *Principio de Hollywood*
	- Simplificado: hay que depender de abstracciones, no de implementaciones concretas, es decir, programar para una interfaz, no para una implementación

>[!Example]
>![](img/Pasted%20image%2020240602132813.png)
>

- **ISP** (*Interface Segregation Principle*, Principio de segregación de interfaces):
	- Sugiere que los clientes no deberían tratar con la clase original, sino sólo con la interfaz correspondiente
	- Es mejor muchas interfaces específicas para cada cliente que una sola interfaz de propósito general
	- Dicho de otra forma: los clientes no deberían depender de los métodos que no usan

>[!Example]
>![](img/Pasted%20image%2020240602133216.png)
>
>![](img/Pasted%20image%2020240602133233.png)
>
>![](img/Pasted%20image%2020240602133250.png)
>
>![](img/Pasted%20image%2020240602133309.png)
>
>![](img/Pasted%20image%2020240602133327.png)
>
>![](img/Pasted%20image%2020240602133346.png)
>
>![](img/Pasted%20image%2020240602133409.png)

## Patrones GRASP

==Pregunta típica de examen==

- Son una serie de principios generales para asignar responsabilidades
- Mejor el término Principios que Patrones, ya que no son soluciones a problemas concretos de diseño, sino más bien principios que suelen ser aplicables siempre

- **GRASP 1** (*Experto en información*): asignar una responsabilidad al experto (la clase que tiene la información necesaria para llevarla a cabo)

>[!Example]
>![](img/Pasted%20image%2020240602134052.png)
>
>![](img/Pasted%20image%2020240602134128.png)
>
>![](img/Pasted%20image%2020240602134206.png)
>
>![](img/Pasted%20image%2020240602134238.png)
>
>![](img/Pasted%20image%2020240602134256.png)
>
>- **Contraindicaciones**:
>	- La clase `Sale` ahora deberá contener la lógica relacionada con la gestión de la base de datos
>		- Disminuye su cohesión, pues tiene una nueva responsabilidad
>		- Está acoplada, pues depende de servicios de otro subsistema
>		- Duplicación de código, pues es probable que la lógica de acceso a datos esté repetida
>- **Ventajas**:
>	- Se mantiene el encapsulamiento de la información (y hay un bajo acoplamiento)
>	- Se distribuye el comportamiento entre las clases que contienen la información requerida (alta cohesión)

- **GRASP 2** (*Creador*): ¿Quién debería ser el responsable de la creación de una nueva "instancia" de una clase?. Asignar a las clase B la responsabilidad de crear una instancia de la clase A si cumple alguna de las condiciones siguientes:
	- B agrega objetos de A
	- B contiene objetos de A
	- B registra objetos de A
	- B utiliza más estrechamente objetos de A
	- B tiene los datos de inicialización de un objeto de A

>[!Example]
>![](img/Pasted%20image%2020240602134943.png)
>
>- Contraindicaciones:
>	- A veces la creación de objetos requiere una cierta complejidad
>		- En esos casos es conveniente delegar la creación a una clase de fabricación auxiliar
>	- *Mucho ojo con las factorías*

- **GRASP 3** (*Bajo acoplamiento*): 
	- ¿Cómo lograr que haya pocas dependencias, que los cambios tengan un bajo impacto e incrementar la reutilización?
		- Asignar una responsabilidad de manera que el acoplamiento permanezca bajo
	- **Acoplamiento**: medida de la fuerza con que un elemento está conectado a otros
		- Si un elemento tiene un bajo acoplamiento no depende de demasiados otros elementos
		- Si una clase presenta un fuerte acoplamiento con otras, cambios en esas clases obligan a hacer cambios en ella

>[!Example]
>![](img/Pasted%20image%2020240602140327.png)
>
>Solución alternativa:
>
>![](img/Pasted%20image%2020240602140411.png)
>
>![](img/Pasted%20image%2020240602140435.png)
>
>Ventajas del bajo acoplamiento:
>- No afectan los cambios en otros componentes
>- Fácil de entender de manera aislada
>- Favorece la reutilización

- **GRASP 4** (*Alta cohesión*):
	- ¿Cómo mantener la complejidad manejable?
		- Asignar una responsabilidad de manera que la cohesión permanezca alta
	- **Cohesión**: es una medida de la fuerza con que se relacionan las responsabilidades de un elemento
	- Una clase con baja cohesión hace muchas cosas no relacionadas. Presentan los siguientes problemas:
		- Difíciles de entender
		- Difíciles de reutilizar
		- Difíciles de mantener
		- Delicadas, constantemente afectadas por los cambios

>[!Example]
>![](img/Pasted%20image%2020240602140913.png)
>
>![](img/Pasted%20image%2020240602140931.png)
>
>![](img/Pasted%20image%2020240602140952.png)
>
>![](img/Pasted%20image%2020240602141018.png)

- **GRASP 5** (*Controlador*): 
	- ¿Quién debe ser responsable de gestionar un evento de entrada al sistema?
		- Asignar la responsabilidad de recibir o manejar un evento a una clase que representa las siguientes opciones:
			- Representa el sistema global, un dispositivo o un subsistema
			- Representa un escenario de caso de uso en el que tiene lugar el evento

>[!Example]
>![](img/Pasted%20image%2020240602142456.png)
>
>![](img/Pasted%20image%2020240602142523.png)
>
>![](img/Pasted%20image%2020240602142541.png)

- **GRASP 6** (*Polimorfismo*): 
	- ¿Cómo manejar las alternativas basadas en el tipo? ¿Cómo crear componentes software conectables?
		- Cuando las alternativas o comportamientos relacionados varían según el tipo de objeto, se asignará la responsabilidad a los tipos para los que varía el comportamiento, empleando operaciones polimórficas
		- Es decir, hay que intentar huir de la lógica condicional con respecto al tipo (`if`, `switch`, `instanceof`...)

>[!Example]
>![](img/Pasted%20image%2020240602142850.png)
>
>![](img/Pasted%20image%2020240602142909.png)
>
>![](img/Pasted%20image%2020240602142930.png)

- **GRASP 7** (*Fabricación pura*):
	- ¿Qué objetos deberían tener la responsabilidad cuando no se quiere violar los principios de alta cohesión y bajo acoplamiento pero, sin embargo, las soluciones que ofrece el experto no son adecuadas?
		- Se asignará un conjunto de responsabilidades altamente cohesivo a una clase artificial, de conveniencia, que no representa un concepto del dominio del problema, sino que se ha inventado para permitir esa alta cohesión, bajo acoplamiento y la reutilización de código.

>[!Example]
>![](img/Pasted%20image%2020240602143208.png)

- **GRASP 8** (*Indirección*): 
	- ¿Dónde asignar una responsabilidad, para evitar el acoplamiento directo entre dos o más elementos?
		- Se asignará la responsabilidad a un objeto intermedio que medie entre otros componentes o servicios de manera que no se acoplen directamente
- **GRASP 9** (*Variaciones protegidas*): 
	- ¿Cómo diseñar objetos, subsistemas y sistemas de manera que las variaciones o inestabilidades en estos elementos no tengan un impacto no deseable en otros elementos?
		- Identifique los puntos de variaciones previstas o de inestabilidad; asigne responsabilidades para crear una interfaz estable alrededor de ellos.
		- Es decir, identificar aquellos aspectos que varían y separarlos de lo que tiende a permanecer igual (encapsular y aislar el concepto que no varía)
	- Mecanismos de Variaciones protegidas:
		- Principio de abierto-cerrado
		- Principio de sustitución de Liskov
		- Principio de inversión de dependencias
		- Principio de segregación de interfaces
## Diseño modular

- **Modularidad**: es la propiedad de un sistema que se ha descompuesto en un conjunto de módulos cohesivos y débilmente acoplados
	- La modularidad se alcanza diseñando cada método con un único y claro objetivo, y agrupando un conjunto de aspectos relacionados en una clase

## Acoplamiento, cohesión y el cambio

==Pregunta típica de examen==

### Acoplamiento

![](img/Pasted%20image%2020240602141430.png)

### Acoplamiento y cohesión (Beck)

- **Cohesión**: mide el grado de conectividad entre las funciones y elementos de un mismo módulo
	- Beck dice lo siguiente:
		- Un elemento es cohesivo en la medida en que el elemento entero cambia cuando el sistema necesita hacer un cambio en una funcionalidad determinada
		- Y lo relaciona también con el tamaño: un elemento puede perder cohesión si es demasiado grande o demasiado pequeño

![](img/Pasted%20image%2020240602141535.png)

![](img/Pasted%20image%2020240602141711.png)

![](img/Pasted%20image%2020240602141723.png)

### Suficiencia, completitud y ser primitivo

- **Suficiente**: el componente representa suficientes características de una abstracción como para permitir una abstracción significativa con el componente
	- *Si estamos diseñando una clase Conjunto, está muy bien tener una operación para eliminar un elemento dado, pero servirá de muy poco si no tenemos otra para añadir elementos al conjunto.*
- **Completo**: la interfaz del componente representa todas las características de la abstracción
	- *Diferente de la suficiencia: allí íbamos a mínimos; la completitud hace referencia a que ofrezca una interfaz lo suficientemente general como para que pueda ser utilizado por cualquier cliente. Es una cualidad subjetiva (y peligrosa).*
- **Primitivo**: si todas las operaciones que realiza un componente pueden implementarse fácil y eficientemente, necesitando acceder a la representación interna del componente
	- *Matiza lo anterior: la operación «añadir» del conjunto es primitiva; una para añadir varios elementos a la vez no (puede lograrse con la anterior, sin requerir acceso a la representación interna). De nuevo, es algo subjetivo.*

### Cohesión

![](img/Pasted%20image%2020240602142154.png)

## ¿Qué es un buen diseño?

==Pregunta típica de examen==

- Un sistema está bien diseñado si:
	- Es fácil de comprender
		- Si la responsabilidad se indica claramente (nombres adecuados, se usan patrones de diseño) 
	- Es fácil de cambiar
		- Hay que tener en cuenta que todo programa sufrirá cambios, y el objetivo del diseño es facilitarlos. De esta forma, *diseñar para el cambio* significa:
			- Sólo hay que cambiar en un único sitio (o añadiendo código nuevo -> Principio Abierto-Cerrado)
			- Es fácil determinar el lugar de dicho cambio
			- Debemos centrarnos en clases y métodos cohesivos (una única responsabilidad)

>[!Tip]
>¡Hay que diseñar para el cambio!
>- Todo programa sufrirá cambios
>- El objetivo es facilitarlos
>- Un cambio será fácil de realizar si:
>	- Sólo hay que hacerlo en un único sitio
>	- Resulta fácil determinar dicho sitio

# Tema 2. Patrones de Diseño

## Herencia de clases vs Herencia de interfaces

- **Herencia de clases**: es un mecanismo para reutilizar código
- **Herencia de interfaces**: describe cuándo se puede utilizar un objeto en lugar de otro (subtipos)

>[!Tip]
>Hay que programar para una interfaz, no para una implementación


## Herencia frente a composición

==Pregunta típica de examen==

- **Herencia de clases**: permite definir la implementación de una clase en términos de la de otra
	- Se define estáticamente, en tiempo de compilación
	- Es fácil de usar
	- La subclase es muy dependiente de la implementación de la clase padre (hace muy difícil la reutilización en otros dominios)
- **Composición de objetos**: es una alternativa a la herencia, donde la nueva funcionalidad se obtiene ensamblando o componiendo nuevos objetos
	- Se define dinámicamente en tiempo de ejecución a través de objetos que guardan referencias a otros objetos
	- A estos objetos sólo se accede a través de sus interfaces
	- Se puede cambiar cualquier objeto por otro de su mismo tipo en tiempo de ejecución
	- Ayuda a que la clase se centre en una única tarea

## Elementos de un patrón

- **Contexto**: describe las situaciones en las que se da el problema
- **Problema**: descripción general que represente bien la esencia de éste
- **Solución**: cómo resolver el problema

## Categorías de Patrones

- **Arquitectónicos**: situados a un nivel de abstracción más alto, describen la arquitectura, la estructura de un sistema en torno a subsistemas y las relaciones entre ellos (ej: Modelo Vista Controlador)
- **De diseño**: se sitúan en el nivel de abstracción medio, de diseño (independientes del lenguaje de programación, ej: Observer)
- **Centrados en el código**: o Modismos, que suelen ser específicos de un lenguaje de programación determinado.
	- Revelan su intención

## Elementos de un patrón

![](img/Pasted%20image%2020240602175226.png)

## Secciones de un patrón de diseño

![](img/Pasted%20image%2020240602175311.png)

![](img/Pasted%20image%2020240602175325.png)

![](img/Pasted%20image%2020240602175338.png)
## Organización del catálogo de patrones

![](img/Pasted%20image%2020240602175419.png)

## Causas de rediseño

>[!Note]
>Aquí incluyo cuándo se debe usar cada patrón

>[!Tip]
>**TIP 1**: *crear un objeto especificando explícitamente su clase*
>
>Si se especifica el nombre de la clase en el código al crear el objeto nos liga a una implementación particular en vez de a una interfaz.
>
>Es mejor crear los objetos directamente.
>
>Se usan los patrones: *Abstract Factory*, *Factory Method* y *Prototype*


>[!Tip]
>**TIP 2**: *depender de operaciones concretas*
>
>Evitando llamar directamente a un método determinado en el código se facilita cambiar la forma en que se responde a una petición
>
>Se usan los patrones: *Chain of Responsibility* y *Command*

>[!Tip]
>**TIP 3**: *dependencia de plataformas de hardware o software*
>
>Las interfaces de los sistemas operativos y las APIs de muchas aplicaciones son dependientes de la plataforma
>
>Hay que limitar dichas dependencias
>
>Se usan los patrones: *Abstract Factory* y *Bridge*

>[!Tip]
>**TIP 4**: *depender de implementaciones o representaciones de objetos*
>
>Los clientes que conocen cómo se representa internamente cómo se almacena, dónde se localiza o cómo se implementa tendrán que cambiar cuando cambie aquél
>
>Se usan los patrones: *Abstract Factory*, *Bridge*, *Memento* y *Proxy*

>[!Tip]
>**TIP 5**: *dependencias de algoritmos*
>
>Los algoritmos que es probable que cambien a lo largo del tiempo (para optimizarlos o porque se sustituyan por otro distinto) deben estar aislados
>
>Se usan los patrones: *Builder*, *Iterator*, *Strategy*, *Template Method* y *Visitor*

>[!Tip]
>**TIP 6**: *fuerte acoplamiento*
>
>Es difícil reutilizar clases que están fuertemente acopladas a otras
>
>Se usan los patrones: *Abstract Factory*, *Bridge*, *Chain of Responsibility*, *Command*, *Facade*, *Mediator* y *Observer*

>[!Tip]
>**TIP 7**: *extender funcionalidad mediante la herencia*
>
>Definir una subclase requiere un profundo conocimiento de la clase padre
>
>Se usan los patrones: *Bridge*, *Chain of Responsibility*, *Composite*, *Decorator*, *Observer* y *Strategy*

>[!Tip]
>**TIP 8**: *no se puede modificar las clases*
>
>A veces hay que modificar una clase de la que no disponemos del código fuente o que requeriría cambiar montones de subclases existentes
>
>Se usan los patrones: *Adapter*, *Decorator* y *Visitor*

# Diferencias entre patrones

==Pregunta típica de examen==

## Decorator vs Strategy

- *En cuanto a su propósito*, mientras que el **Strategy** permite cambiar parte del comportamiento interno de un objeto (el contexto), delegando en otro (la estrategia, que puede ser sustituido por otra estrategia), el **Decorator** añade responsabilidades a uno o varios métodos de un objeto en tiempo de ejecución, llevando a cabo tareas adicionales antes o después de llamar al método correspondiente del objeto que decora.
- *En cuanto a la forma de implementarlos*, un objeto sabe que internamente tiene una **estrategia** que lo completa sin la cual no puede funcionar, mientras que la presencia de un **decorador** es totalmente transparente al objeto que decora, envolviéndolo desde fuera.

### Decorador vs lista de Estrategias

![](img/Pasted%20image%2020241212154129.png)

![](img/Pasted%20image%2020241212154143.png)

### Ejemplo: tickets (sistema de ficheros)

Con un **Decorator**:

![](img/Pasted%20image%2020241212154222.png)

![](img/Pasted%20image%2020241212154337.png)

Con una lista de Estrategias (**Strategy**):

![](img/Pasted%20image%2020241212154301.png)

![](img/Pasted%20image%2020241212154348.png)

## Decorator vs Composite

Un **Decorator** es como un **Composite** pero sólo tiene un componente hijo. Además, el **Decorator** añade responsabilidades adicionales al objeto envuelto, mientras que el **Composite** se limita a "recapitular" los resultados de sus hijos
## State vs Strategy

- **Strategy**: es seleccionada por un agente externo o por el contexto. Una estrategia tiende a tener un único método de "*inicio*" que llama a todos los demás. Hay mucha cohesión entre los métodos de un Strategy
- **State**: un State generalmente selecciona el siguiente estado de su contexto. Un estado tiende a tener muchos métodos no relacionados, por lo que hay poca cohesión entre los métodos de un State.
	- Los métodos del State suelen llamarse igual y tener la misma signatura que las que tenían dicho subconjunto de operaciones en el contexto

## Factory Method vs Abstract Factory

![](img/Pasted%20image%2020240603131608.png)

## Prototype vs Abstract Factory vs Factory Method

- El objeto fábrica de **Abstract Factory** produce varios objetos de varias clases, mientras que el **Prototype** hace que el objeto fábrica construya un producto copiando un objeto prototípico. 
	- En este caso, el objeto fábrica y el prototipo son el mismo objeto, ya que el prototipo es el responsable de devolver el producto
- El **Factory Method** puede requerir crear una nueva subclase simplemente para cambiar la clase del producto (dichos cambios pueden tener lugar en cascada), mientras que el **Prototype** hace que el objeto fábrica construya un producto copiando un objeto prototípico.
	- En este caso, el objeto fábrica y el prototipo son el mismo objeto, ya que el prototipo es el responsable de devolver el producto