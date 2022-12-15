# 1. Modelo de objetos
---
- **Análisis**: pone énfasis en una investigación del problema y los requisitos, en vez de la solución
- **Diseño**: pone énfasis en una solución conceptual que satisface los requisitos
- **Diseño orientado a objetos** (DOO): definición de los objetos software y cómo colaboran para satisfacer los requisitos
- **Programación estructurada**: separa las estructuras de datos de los algoritmos que las manipulan

- Los objetos **colaboran** entre sí
- Cada objeto realiza unas **operaciones** que lo caracterizan
- No importa cómo las realice, sino **cuáles** realiza
- La implementación de esas operaciones son los **métodos**
- Un objeto lleva a cabo una **operación** cuando recibe una petición (o **mensaje**) de un cliente
- Las operaciones son el único modo de cambiar el estado interno del objeto
- Por ese motivo se dice que el estado interno del objeto está encapsulado

- **Interfaz de un objeto**: el conjunto de todas las signaturas públicas definidas por él, es decir, las peticiones que pueden hacérsele
- **Tipo**: nombre usado para denotar una determinada interfaz
- Un objeto puede tener muchos tipos, así como muchos objetos muy diferentes pueden compartir un mismo tipo
- **Enlace dinámico**: asociación en tiempo de ejecución que tiene lugar entre la petición a un objeto y una de sus operaciones, lo que permite el **polimorfismo**
	- **Polimorfismo**: cualquier objeto que implemente una interfaz concreta podrá ser reemplazado por otro que implemente esa misma interfaz
- **Polimorfismo**: capacidad de dos o más tipos de objetos de responder al mismo mensaje, cada uno a su manera. Nos permite tener una lista de figuras y dibujarlas todas sin conocerlas:
![[Pasted image 20221214170838.png]]
![[Pasted image 20221214170906.png]]
- La **clase** es una de las formas de crear tipos en Java
- Se dice que un objeto es una **instancia** de una clase
- El operador "**new**" crea un nuevo objeto y devuelve una referencia a él

- Síntomas de mala programación orientada a objetos:
	- Métodos largos (más de 10 líneas)
	- Abundancia de llamadas a métodos del mismo objeto

- El diseño de una clase **NO** se empieza por sus atributos, sino que se plantean primero las acciones que debe realizar el objeto (usando o bien atributos o bien delegación en otros objetos)

- **Operando**: objeto que el método necesita para operar. Permanecen estables
- **Opción**: forma de operar con los operandos. Pueden variar a medida que la clase evolucione

- Los parámetros de un método deben ser sólo operandos
![[Pasted image 20221214171825.png]]
![[Pasted image 20221214171840.png]]
![[Pasted image 20221214171859.png]]
![[Pasted image 20221214172008.png]]
![[Pasted image 20221214172019.png]]

- **Estado de un objeto**: combinación de los valores de los atributos de un objeto. Guardar el estado de un objeto supone guardar la suficiente información para que al recuperarla se obtengan exacmtamente las mismas respuestas ante la misma secuencia infinita de mensajes tanto del original como del objeto recuperado. Generalmente basta con guardar los atributos
- Normalmente no se debe dar acceso a los datos internos de un objeto (**encapsulación**), sino que se deben de usar **métodos de acceso**, es decir, getters y setters. Permite controlar las modificaciones del atributo.
- Ocultar los atributos permite modificar la implementación sin afectar a los clientes

- **Criterio de independencia**: cuanto menos se sepa de la implementación de un objeto, menos afectarán sus cambios. Por eso una clase no debe saber de otra. Lo único importante de un objeto son los mensajes que puede recibir

- **Estado concreto**: se define en función de los atributos, puede variar
- **Estado abstracto**: se define en función de las respuestas a los mensajes
- Cuando hablamos de estado siempre nos referimos al estado abstracto

### Como ***no*** diseñar clases
- Basarse en objetos reales
- Extraer nombres y verbos del lenguaje natural

## Guía para crear una clase
1. **Elegir una tarea a realizar: el qué**
	a) Decidir qué tipo de objeto lo hará
	b) ¿Puede hacerla alguna de las clases que ya tenemos?
2. **Decidida la clase y la responsabilidad, tocan los mensajes**
	- Dividir la responsabilidad en operaciones (atómicas para que se puedan combinar)
	- Parámetros con información imprescindible
	- Sacar partido de que los objetos recuerdan lo que se les ha mandado
3. **Implementación de las operaciones (métodos)**
	- No preocuparse por la eficiencia hasta el final

# 2 Interfaces y clases abstractas
---
![[Pasted image 20221214173858.png]]
![[Pasted image 20221214173933.png]]

## Interfaces
- Permiten comunicar objetos que ==no se conocen==
- Un objeto que quiera ser contratado debe cumplir con el contrato (es decir implementar la interfaz en cuestión)
![[Pasted image 20221214174122.png]]
- La revisión del contrato se hará de manera estática (se sabe en tiempo de compilación)
![[Pasted image 20221214174230.png]]

## Herencia
### Tipos
- **De interfaz**: declaramos el compromiso de implementar unos métodos (subtipos)
- **De implementación**: creación de una clase a partir de la implementación de otra (reutilización del código)

## ==Criterio de diseño==
- Cuando un objeto deba delegar ciertas operaciones en tro deberá exigírselas mediante una interfaz
	- Importan los mensajes que acepta el objeto
	- No de quién ha obtenido su implementación

## Clases abstractas
- Evitan la duplicación de código en clases que hacen prácticamente lo mismo
![[Pasted image 20221214174842.png]]
![[Pasted image 20221214174855.png]]
![[Pasted image 20221214174911.png]]

- Uno de sus usos es factorizar código propio
- AbstractAdepto se denomina clase base abstracta
	- Quedan mensajes sin implementar, luego no se puede instanciar
	- Se usa como implementación base para otras clases
- Una clase base puede dar implementación a todos los métodos de la interfaz
	- Entonces se denomina **clase base concreta**
	- Pueden instanciarse directamente
- Otro de sus usos es facilitar la extensión
![[Pasted image 20221214175323.png]]

### Uso práctico de las clases abstractas
- A la hora de implementar una interfaz, miraremos primero qué implementaciones nos vienen ya preparadas (escoger la más cercana)
![[Pasted image 20221214175540.png]]![[Pasted image 20221214175554.png]]

Una clase abstracta puede:
- Dejar un método sin implementación para que lo implementen las clases derivadas
- Dar la implementación completa del mensaje

¿Cómo conseguimos que cambie solo parte de la implementación?
![[Pasted image 20221214175815.png]]
- Aquí es donde aparecen los métodos abstractos
- Se separa la parte común y la parte específica de la implementación
	- La clase base contendrá la parte obligatoria
	- Las clases derivadas aportarán la parte específica en nuevos mensajes
	- ¡Para esto sirve el **protected**!
	- Indica que hay que completar una implementación parcial
![[Pasted image 20221214180040.png]]

## Resumen

- La herencia de implementación (clases abstractas) se utiliza como soporte de las interfaces
	- Permiten colocar implementaciones comunes en clases base
- Una clase base puede ser:
	- **Abstracta** si sólo implementa parte de los mensajes (sólo puede ser usada para heredar de ella)
	- **Concreta** si implementa todos los mensajes (puede ser instanciada y usada directamente)
- Para cada operación, una clase abstracta puede:
	- Dar una implementación completa
	- Dar una implementación parcial delegando el resto en otros métodos
- Las clases que deriven de la clase base
	- Tendrán que implementar los mensajes que queden sin implementar completamente o parcialmente (**protected**)
	- Y podrán redefinir los ya implementados aprovechando o no dicha implementación (**super**)

## Extensión
- Las clases en una jerarquía lo normal es que sean implementaciones de una determinada interfaz
- Normalmente los clientes interactuarán con los objetos a través de dicha interfaz

## Jerarquías de interfaces
![[Pasted image 20221214180824.png]]
![[Pasted image 20221214180930.png]]

- ¡No hace falta tener jerarquías para que un diseño sea orientado a objetos!
- Las interfaces surgen por la necesidad de declarar unas responsabilidades
- Por tanto, ==nunca debe surgir una jerarquía como mera clasificación==
	- No hay que buscar un árbol equilibrado, tan sólo hay que comprobar que todas las interfaces tengan al menos un cliente que la use
![[Pasted image 20221214181225.png]]

## Jerarquías de clases abstractas
![[Pasted image 20221214181319.png]]

- ¿De dónde salen las clases abstractas?
	- Del implementador de la interfaz
	- Del implementador de las clases concretas mediante **refactoring**
![[Pasted image 20221214181445.png]]
![[Pasted image 20221214181508.png]]

- Una jerarquía de implementación de clases abstractas no es esencial que sea estable:
	- El cliente sólo conoce la interfaz
	- No le afectan las reorganizaciones que haya en sus implementaciones
- Las jerarquías de implementación son para compartir código común y puede reestructurarse cuantas veces se necesite
	- Si desaparece rombo fusionar FiguraPoligonal y Rectángulo
	- No hace falta pensar en el futuro lejano: reorganizar el árbol en función de las necesidades actuales

- En el análisis no importa el código ni tampoco el diseño, sino los métodos (pero no su implementación interna)

## Resumen Interfaces vs Clases abstractas

Repasemos sus diferencias atendiendo a:
- En qué momento se crea cada una
- Quién es su creador en el proceso de desarrollo (analista, diseñador,
programador)
- ¿Pueden ser raíz de una jerarquía?
- Importancia dentro del paradigma
	- ¿Qué consecuencias tendría para el lenguaje de programación quitar cada una de ellas?
- Qué hacen con respecto a las operaciones de sus ancestros
	- Añadir, redefinir, eliminar
- Impacto en el resto del diseño si cambiamos unas u otras
![[Pasted image 20221214182147.png]]
![[Pasted image 20221214182358.png]]

# 3 Principios de diseño
---
Síntomas de un diseño pobre:
- **Rigidez**: es difícil de cambiar. Un cambio produce una sucesión de cambios en cascada
- **Fragilidad**: es fácil que falle. Un cambio en una parte causa un fallo en otras partes no relacionadas
- **Inmovilidad**: es difícil de reutilizar
- **Viscosidad**: es difícil hacer lo correcto. Hay dos tipos de viscosidad:
	- **Del software**: si hacer cambios respetando el diseño original es más costoso que hacerlos mal
	- **Del entorno de desarrollo**: si es lento e ineficiente
- **Complejidad innecesaria**: sobrediseño
- **Repetición innecesaria**: copiar y pegar. Duplicación de código
- **Opacidad**: es complejo averiguar su intención

## Principios SOLID
- **SRP**: Single Responsibility Principle
- **OCP**: Open-Closed Principle
- **LSP**: Liskov Substitution Principle
- **DIP**: Dependency Inversion Principle
- **ISP**: Interface Segregationm Principle

## SRP: Principio de responsabilidad única
- **Una clase debería tener un único motivo para cambiar**
- Una responsabilidad es una razón para el cambio
	- Si podemos pensar en más de un motivo por el que la clase debería cambiar, dicha clase tiene más de una responsabilidad

![[Pasted image 20221214185841.png]]
No es un buen diseño, porque viola el principio de responsabilidad única:
- La clase Rectangle tiene dos responsabilidades
	- Si una de las dos aplicaciones requiriese un cambio en rectangle, afectaría a la otra

## OCP: Principio de abierto-cerrado
- **Las clases deberían estar abiertas para la extensión, pero cerradas para la modificación**
- La idea es que los cambios se hagan añadiendo código nuevo, no modificando el anterior que ya funcionaba
![[Pasted image 20221214190233.png]]
![[Pasted image 20221214190250.png]]

## LSP: Principio de sustitución de Liskov
- **Los subtipos deben poder sustituir a sus tipos base** / **Las funciones que usan referencias a una clase base deberían poder usar un objeto de cualquier clase derivada sin saberlo**
- Dicho de otra forma:
	- Los objetos de un programa deberían ser reemplazables por instancias de sus subtipos sin alterar el correcto funcionamiento de un programa
	- Debemos asegurarnos de que las clases derivadas extiendan la clase base sin alterar su comportamiento de manera que se viole el contrato

- No debemos usar `instanceof` ni downcasts

## DIP: Principio de inversión de dependencias
- **Los módulos de alto nivel no deben depender de los de bajo nivel, ambos deben depender de abstracciones**
- **Las abstracciones no deben depender de los detalles, sino éstos de las abstracciones**
![[Pasted image 20221214190912.png]]
La dependencia en un programa orientado a objetos bien diseñado suele ser a la inversa:
![[Pasted image 20221214191034.png]]

## Principio de Hollywood
- **Hay que depender de abstracciones, no de implementaciones concretas**, es decir, **programar para una interfaz, no para una implemenetación**

### ISP: Principio de segregación de interfaces
- Este principio trata con el problema de las interfaces gruesas (fat). Las clases que tienen este tipo de interfaz no son cohesivas, es decir, deberíamos separar sus métodos en distintos grupos, cada uno de los cuales serviría a un conjunto distinto de clientes.
- ISP sugiere: **los clientes no deberían tratar con la clase original, sino sólo con la interfaz correspondiente**
- Es mejor muchas interfaces específicas para cada cliente que una sóla interfaz de propósito general, es decir, los clientes no deberían depender de métodos que no usan.

![[Pasted image 20221214191652.png]]
![[Pasted image 20221214191707.png]]
![[Pasted image 20221214191721.png]]
![[Pasted image 20221214191740.png]]
![[Pasted image 20221214191751.png]]
![[Pasted image 20221214191805.png]]
![[Pasted image 20221214191817.png]]

## Patrones/Principios GRASP
- Principios generales para asignar responsabilidades
- GRASP (General Responsibility Assignment Software Patterns)
- Se refieren a las obligaciones (**responsabilidades**) de un objeto:
	- Conocer
		- Conocer los datos privados encapsulados
		- Conocer los objetos relacionados
		- Conocer las cosas que puede calcular o derivar
	- Hacer
		- Hacer algo él mismo
		- Iniciar una acción en otros objetos
		- Controlar y corrdinar actividades en otros objetos
- Los métodos se definen para llevar a cabo responsabilidades
- Las responsabilidades se implementan mediante métodos que o actúan sólos o colaboran con otros métodos u objetos
- Los diagramas de interacción reflejan las decisiones de diseño en la asignación de responsabilidades
![[Pasted image 20221214192353.png]]

## GRASP 1º: Experto en información
- Uno de los principios más generales para asignar responsabilidades a los objetos
- **Asignar una responsabilidad al experto (la clase que tiene la información necesaria para llevarla a cabo)**

## GRASP 2º: Creador
- ¿Quién debería ser el responsable de la creación de una nueva instancia de una clase?
![[Pasted image 20221214193005.png]]
- Si se asignan bien las responsabilidades, el diseño tendrá un bajo acoplamiento, mayor claridad, encapsulamiento y reutilización
- A veces la creación de objetos requiere una cierta complejidad
	- En esos casos es conveniente delegar la creación a una clase de fabricación auxiliar (MUCHO OJO CON ABUSAR DE LAS FACTORÍAS)

## GRASP 3º: Bajo acoplamiento
- ¿Cómo lograr que hay pocas dependencias, que los cambios tengan un bajo impacto e incrementar la reutilización?
- **Asignar una responsabilidad de manera que el acoplamiento permanezca bajo**
- **Acoplamiento**: medida de la fuerza con que un elemento está conectado a otros
	- Un elemento con bajo nivel de acoplamiento no depende de demasiados otros elementos
- Si una clase presenta un fuerte acoplamiento con otras:
	- Cambios en esas clases obligan a hacer cambios en ella
	- Es difícil de entender de manera aislada
	- Es difícil de reutilizar
- El alto acoplamiento en sí no es un problema
	- Es un problema entre elementos que no son estables, que pueden cambiar

## GRASP 4º: Alta cohesión
- ¿Cómo mantener la complejidad manejable?
- **Asignar una responsabilidad de manera que la cohesión permanezca alta**
- **Cohesión**: medida de la fuerza con que se relacionan las responsabilidades de un elemento
- Una clase con baja cohesión hace muchas cosas no relacionadas o hace demasiado trabajo

## Acomplamiento, cohesión y el cambio
![[Pasted image 20221214194344.png]]
![[Pasted image 20221214194428.png]]
![[Pasted image 20221214194444.png|500]]
![[Pasted image 20221214194456.png||500]]

## Suficiencia, completitud y ser primitivo
- **Suficiente**: el componente representa suficientes características de una abstracción como para permitir una asbtracción significativa con el componente
- **Completo**: la interfaz del componente representa todas las características de la abstracción
- **Primitivo**: si todas las operaciones que realiza un componente pueden implementarse fácil y eficientemente necesitando acceder a la representación interna del componente

![[Pasted image 20221214194827.png]]

## GRASP 5º: Controlador
- ¿Quién debe ser el responsable de gestionar un evento de entrada al sistema?
![[Pasted image 20221214194951.png]]

## GRASP 6º: Polimorfismo
- ¿Cómo manejar las alternativas basadas en el tipo?¿Cómo crear componentes software conectables?
![[Pasted image 20221214195115.png]]
- Hay que intentar huír de la lógica condicional con respecto al tipo (if, instanceof, switch)

## GRASP 7º: Fabricación pura
- ¿Qué objetos deberían tener la responsabilidad cuando no se quiere violar los principios de alta cohesión y bajo acoplamiento pero, sin embargo, las solouciones que ofrece el experto no son adecuadas?
![[Pasted image 20221214195326.png]]

## GRASP 8º: Indirección
- ¿Dónde asignar una responsabilidad, para evitar el acoplamiento directo entre dos o más elementos?
![[Pasted image 20221214195604.png]]

## GRASP 9º: Variaciones protegidas
- ¿Cómo diseñar objetos, subsistemas y sistemas de manera que las variaciones o inestabilidades en estos elementos no tengan un impacto no deseable en otros elementos?
![[Pasted image 20221214195725.png]]

## ¿Qué es un buen diseño?
- Un sistema está bien diseñado si:
	- Es fácil de comprender
	- Es fácil de cambiar
- Hay que diseñar para el cambio, pues todo programa sufrirá cambios
- El objetivo del diseño es facilitar esos cambios
- Un cambio será fácil de realizar si:
	- Sólo hay que hacerlo en un único sitio
	- Resulta fácil determinar dónde es dicho lugar
- Sólo habrá que cambiar en un lugar si:
	- Las clases y los métodos son cohesivos
		- Sólo tienen una responsabilidad
		- Si hacen varias cosas hanrá que modificarlas por distintos tipos de cambios
	- Se puede cambiar su implementación sin afectar al resto

## Resumen
- Clases con pocas responsabilidades
- Métodos con nombres que las indiquen claramente y el uso de patrones de diseño hacen que sea fácil saber cuál es la clase a modificar cuando aparezca algún cambio en los requisitos

# 4. Introducción patrones de diseño
---
## Elementos de un patrón

- Cada patrón es una regla de 3 partes que expresa una relación entre un contexto determinado, un problema y una solución
- **Contexto**: describe las situaciones en las que se da el problema
- **Problema**: una descripción general que represente bien la esencia de éste
- **Solución**: cómo resolver el problema. Incluye dos aspectos:
	- La estructura estática del patrón (clases y sus relaciones)
	- Su comportamiento, los aspectos dinámicos
		- ¿Cómo colaboran los participantes?, ¿cómo se reparten el trabajo?, ¿cómo se comunican entre ellos?
- Los patrones son un esquema. 
- Un **patrón** es un bloque de construcción mental para ser implementado en un sinfín de aplicaciones y contextos diferentes

## Categorías de patrones
- Atendiendo a su nivel de abstracción
	- Arquitectónicos
	- De diseño
	- Centrados en el código
### Patrones arquitectónicos
- Situados en el nivel de abstracción más alto
- Describen la arquitectura, la estructura de un sistema en torno a subsistemas y las relaciones entre ellos

### Patrones de diseño
- Se sitúan en un nivel de abstracción medio, de diseño (independientes del lenguaje de programación)

### Modismos (idioms)
- Son patrones de muy bajo nivel (codificación)
- La mayoría son específicos de un lenguaje de programación determinado

## Propiedades de los patrones

1. Un patrón responde a un problema de diseño que se repite frecuentemente en determinadas situaciones y presenta una solución a dicho problema
2. Los patrones sirven para documentar la experiencia previa, los diseños que ya se probaron útiles
3. Identifican y especifican abstracciones que están por encima de clases y objetos o componentes individuales
4. Proporcionan un vocabulario de diseño común
5. Permiten documentar nuestros diseños
6. Ayudan a construír arquitecturas complejas y heterogéneas

## La curva de aprendizaje
- Un catálogo de patrones es un medio para comunicar la experiencia de forma efectiva, reduciendo lo que se conoce como "curva de aprendizaje" del diseño

## Secciones de un patrón de diseño
- Nombre del patrón (y clasificación)
- Propósito
- También conocido como
- Motivación
- Aplicabilidad
- Estructura
- Participantes
- Colaboraciones
- Consecuencias
- Implementación
- Código de ejemplo
- Patrones relacionados

==Hay un total de 23 patrones de diseño a estudiar==
![[Pasted image 20221214204207.png]]

## ¿Cómo seleccionar un patrón de diseño?
- Examinar la sección Intent (Propósito)
- Estudiar cómo se interrelacionan los patrones
- Estudiar los patrones de propósito similar
- Tener claras las causas de rediseño
- Considerar qué es lo más probable que cambie en nuestro diseño
	- Y encapsular el concepto que varía

## ¿Cómo usar un patrón de diseño?
- Leer el patrón entero por primera vez
- Estudiar en detalle las secciones de Estructura, Participantes y Colaboraciones
- Echar un vistazo al código de ejemplo
- Elegir los nombres correctos para los participantes en nuestro contexto
- Definir las clases (interfaces, atributos y relaciones)
- Definir nombres específicos de la aplicación para las operaciones del patrón
- Implementar las operaciones que lleven a cabo las responsabilidades del patrón

## Herencia de clases frente a herencia de interfaces
- Hay que distinguir entre la clase de un objeto y su tipo
- **Clase**: define la implementación del objeto
- **Tipo**: es su interfaz (el conjunto de peticiones a las que puede responder)
- Un objeto puede tener muchos tipos y objetops de distintas clases pueden tener el mismo tipo
- Especificar el nombre de la clase en el código al crear el objeto nos liga a una implementación particular en vez de a una interfaz
- **Es mejor crear los objetos indirectamente (Abstract Factory, Factory Method, Prototype)**
- **Evitando llamar directamente a un método determinado en el código se facilita cambiar la forma en que se responde a una petición (Chain of Responsibility, Command)**
- **Hay que limitar el software dependiente de plataforma, pues es difícil de llevar a otras (Abstract Factory, Bridge)**
- **Es preciso ocultar información a los clientes para prevenir los cambios en cascada (Abstract Factory, Bridge, Memento, Proxy)**
- **Los algoritmos que es probable que cambien a lo largo del tiempo deben estar aislados (Builder, Iterator, Strategy, Template Method, Visitor)**
- **Es difícil reutilizar clases que están fuertemente acopladas a otras. Esto conduce a sistemas monolíticos donde no se puede cambiar o eliminar una clase sin que afecte a muchas de las demás (Abstract Factory, Bridge, Chain of Responsibility, Command, Facade, Mediator, Observer)**
- **Extender funcionalidad mediante la herencia (Bridge, Chain of Responsibility, Composite, Decorator, Observer, Strategy)**
- **A veces es necesario modificar una clase de la que no se dispone del código fuente o que requeriría cambiar montones de subclases existentes (Adapter, Decorator, Visitor)**

## Bibliotecas de clases
- Son bibliotecas de clases predefinidas
	- Diseñadas para algúntipo de funcionalidad de propósito general
- Se basan en la reutilización de código (no nos imponen ningún diseño concreto)
- Es más importante aún evitar toda posible dependencia: no sabemos qué aplicaciones las van a utilizar

## Frameworks
- Conjunto de clases cooperantes que constituyen un diseño reutilizable para un determinado tipo de aplicaciones
- El framework debe ser adaptado a cada aplicación concreta
	- Creando subclases específicas de la aplicación a partir de las clases abstractas proporcionadas por aquel
- El framework dictamina cómo será la arquitectura de nuestra aplicación

## Bibliotecas de clases vs Frameworks
- Cuando reutilizamos una biblioteca de clases escribimos el código principal de la aplicación y llamamos al código que queremos reutilizar
- En el caso de los Frameworks, escribimos el código específico de la aplicación que será llamado por el framework

## Diferencias entre patrones de diseño y frameworks
- Los patrones de diseño son más abstractos que los frameworks
	- Los patrones sólo se codifican en los ejemplos de uso
	- El framework se escribe en un lenguaje de programación y se puede ejecutar directamente
- Los patrones de diseño son elementos arquitectónicos más pequeños
- Los patrones de diseño son generales; los frameworks, especializados

# 5. Strategy
---
- Encapsular el concepto que varía
- Favorecer composición sobre la herencia
- Programar para una interfaz, no para una implementación

### Propósito
- Define una familia de algoritmos, encapsula cada uno y los hace intercambiables. Permite que el algoritmo varíe de forma independiente a los clientes que lo usan.

- Es un **patrón de comportamiento** también conocido como **Policy**
![[Pasted image 20221214222810.png]]

### Aplicabilidad
- Permite configurar una clase con un comportamiento determinado de entre varios
- Se necesitan distintas variantes de un algoritmo
- Los distintos comportamientos de una clase aparecen como múltiples sentencias condicionales.
	- El patrón Strategy permite mover cada rama de esos condicionales anidados a su propia clase

### Estructura
![[Pasted image 20221214222957.png]]

### Participantes
- **Strategy (Compositor)**: declara una interfaz común
- **ConcreteStrategy** **(SimpleCompositor, TeXCompositor, ArrayCompositor)**: implementa los distintos algoritmos
- **Context (Composition)**:
	- Se configura como una estrategia concreta
	- Mantiene una referencia a dicho objeto Strategy
	- Puede definir operaciones para permitir a la estrategia acceder a los datos que necesite

### Colaboraciones
- La Estrategia y el contexto colaboran para implementar el algoritmo escogido
	- El contexto puede pasar todos los datos que necesita al llamar a la estrategia concreta
	- O se puede pasar a sí mismo como referencia para que aquélla llame a los métodos que necesite
- Los clientes colaboran en el contexto
	- Pueden pasarle la estrategia concreta

Consecuencias
- Es una alternativa a la herencia
	- Evita la duplicación de código
	- Evita la explosión de subclases
	- Hace que el contexto sea más fácil de entender, modificar y mantener
	- Se puede cambiar dinámicamente
![[Pasted image 20221214223631.png]]
![[Pasted image 20221214223643.png]]
- Sin embargo, crece el número de objetos

### Posibles usos
- Validadores de campos de formularios
- Distintas modalidades de juego (niveles de dificultad, tipo de juego...) 

# 6. Factory Method y Abstract Factory 
---
- ¿Qué pasa con new()?
![[Pasted image 20221214224846.png]]
![[Pasted image 20221214224954.png]]
- Es decir, tenemos una serie de clases concretas que instancias, y la decisión de cuál debe ser sólo se puede tomar en tiempo de ejecución
- Cada vez que aparecen nuevas clases o se eliminan, hay que modificar el código
- Tenemos que identificar aquellos aspectos que varían y separarlos de lo que tiende a permanecer igual
![[Pasted image 20221214225257.png]]
![[Pasted image 20221214225322.png]]
![[Pasted image 20221214225404.png]]
![[Pasted image 20221214225427.png]]
¿Qué ocurre si añadimos o eliminamos algún tipo de pizza?
- Que tenemos que modificar el código
![[Pasted image 20221214225538.png]]
![[Pasted image 20221214225603.png]]
![[Pasted image 20221214225631.png]]
![[Pasted image 20221214225721.png]]
![[Pasted image 20221214225750.png]]
![[Pasted image 20221214225856.png]]

### Aclaración:
- Un método de creación es cualquier método (estático o no) que devuelve una instancia de un objeto
- Una clase es una factoría (**Factory**) si implementa uno o más métodos de creación


Ahora resulta que queremos añadir dos estilos de pizzerías (estilo New York y estilo Chicago)
- Tendremos que crear un framework para la pizzería:
![[Pasted image 20221214230908.png]]
![[Pasted image 20221214230227.png|500]]
![[Pasted image 20221214230339.png]]
![[Pasted image 20221214230355.png]]
 ¿Quién es el responsable de decidir qué objeto Pizza se crea?
 - Las subclases (usando el patrón **Factory Method**)

## Factory Method
- Es un patrón de creación

### Propósito
- Define una interfaz para crear un objeto, pero deja que sean las subclases quienes decidan la clase del objeto a crear
- También conocido como Constructor virtual

### Aplicabilidad
- Úsese cuando:
	- Una clase no puede anticipar la clase de objetos que debe crear
	- Una clase quiere que sus subclases especifiquen los objetos a crear
	- Hay clases que delegan responsabilidades en una o varias subclases y queremos localizar el conocimiento de qué subclase es el delegado

### Estructura
![[Pasted image 20221214230816.png]]
En Java:
- Podemos pasarle el nombre de la clase al método de fabricación y crear ésta mediante reflectividad
- Más común:
	- Guardar la clase en una variable de clase estática de Application
	- De esa manera no hay que heredar de ella sólo para cambiar el tipo de producto
	- 
## Abstract Factory
### Propósito
- Define una interfaz para crear familias de objetos relacionados sin especificar sus clases concretas
![[Pasted image 20221214233742.png]]
![[Pasted image 20221214233811.png]]

### Estructura
![[Pasted image 20221214233900.png]]

### Consecuencias
- Aísla las clases concretas
	- Los clientes manipulan los productos únicamente a través de sus interfaces abstractas, gracias a que las clases de productos concretos están encapsuladas en cada fábrica concreta, no aparecen en el código
	- Basta con cambiar una única clase, en un único sitio: la fábrica concreta
	- Dificulta añadir nuevos tipos de productos
		- Hay que cambiar la interfaz de la fábrica abstracta y por tanto implementar el nuevo método en todas sus subclases

### Implementación
- Las fábricas pueden ser **Singletons**
- Crear los productos:
	- Normalmente el **Abstract Factory** emplea a su vez un Factory Method para cada producto
	- Otra posibilidad es usar el patrón **Prototype**: una clase única para la fábrica abstracta y tener distintos tipos de objetos de la misma configurados mediante prototipos
- Fábricas extensibles:
	- Pretenden resolver el problema de poder añadir nuevos tipos de productos
	- Un único método de creación especificando el tipo de producto como parámetro
	- Es más flexible pero menos seguro:
		- Todos los productos deben compartir el mismo tipo base
		- Se pierde la comprobación estática de tipos

## Diferencias entre Factory, Factory Method y Abstract Factory
![[Pasted image 20221214234702.png]]

### Encapsular clases con Factory
- Hacer los constructores privados y dejar que los clientes creen objetos de ellas usando una factoría

# 7. Composite, State y Template Method
---
## Composite
### Propósito
- Permite componer objetos en estructuras arbóreas para representar jerarquías de todo-parte, de modo que los clientes puedan tratar a los objetos individuales y a los compuestos de manera uniforme

### Motivación
Un editor de dibujo permite realizar dibujos compuestos de elementos simples (líneas, rectángulos...) u otros dibujos.
- ¿Cómo evitamos que los clientes tengan que distinguir entre unos y otros?
![[Pasted image 20221215112521.png]]
![[Pasted image 20221215112540.png]]

### Estructura
![[Pasted image 20221215112613.png]]
![[Pasted image 20221215112649.png]]

### Participantes
- **Component**: 
	- Declara la interfaz común
	- Implementa el comportamiento predeterminado a todas las clases
	- Declara operaciones para acceder a los hijos
	- (opcional) Define una interfaz para acceder al padre
- **Leaf**: (linea, rectangulo, ...)
- **Composite**:
	- Almacena a sus componentes hijos
	- Implementa las operaciones relacionadas con los hijos
- **Client**: manipula los objetos de la composición a través de la interfaz de Component

### Consecuencias
- Permite jerarquías de objetos tan complejas como se quiera
	- El cliente podrá recibir un compuesto o un primitivo y no se dará cuenta
- Simplifica el cliente (evita tener que distinguir entre unos y otros)
- Se pueden añadir nuevos componentes fácilmente
- DESVENTAJA: puede hace el diseño demasiado general

### Implementación
- Maximizar la interfaz de Component
![[Pasted image 20221215113242.png]]


## State

### Propósito
- Permite a un objeto alterar su comportamiento cuando cambia su estado interno en tiempo de ejecución. Parecerá como si el objeto hubiera cambiado su clase.

### Motivación
![[Pasted image 20221215114813.png]]
![[Pasted image 20221215114835.png]]

### Aplicabilidad
Úsese cuando:
- El comportamiento de un objeto depende de su estado
	- Éste puede cambiar en tiempo de ejecución
- Las operaciones tienen sentencias condicionales anidadas que tratan con los estados
	- El patrón mueve cada rama de la lógica condicional a una clase aparte

### Estructura
![[Pasted image 20221215115047.png]]
![[Pasted image 20221215115101.png]]

### Participantes
- **Context**: 
	- Define la interfaz que interesa a los clientes
	- Mantiene una referencia a una subclase de estado concreto que representa el estado actual
- **State**:
	- Define la interfaz para encapsular el comportamiento asociado con el estado del contexto
- **Subclases ConcreteState**: 
	- Cada clase implementa las operaciones para ese estado concreto

### Colaboraciones
- El contexto podría pasarse a sí mismo como parámetro
	- Para que el estado acceda al contexto si es necesario
- Una vez que el contexto es inicializado en un determinado estado, los clientes no necesitan tratar directamente con los estados
- O bien el contexto o bien los estados concretos deciden cuándo se pasa de uno a otro estado

### Consecuencias
- Se pueden añadir nuevos estados y transiciones fácilmente simplemente definiendo nuevas subclases de State
- Uso de herencia dinámica
	- Este patrón no sería necesario en lenguajes que permiten cambiar la clase de un objeto en tiempo de ejecución
- Puede venir bien añadir métodos de entrada (entry) y de salida (exit) a la interfaz de State

![[Pasted image 20221215115954.png]]


### ¿En qué se diferencia del Strategy?

- Strategy es seleccionado por un agente externo o por el contexto. Strategy tiende a tener un único método de inicio que llama al resto. Hay **mucha cohesión** entre los métodos de Strategy
- State  normalmente cambia el estado de su contexto. Un state suele tener muchos métodos no relacionados (**baja cohesión**)
![[Pasted image 20221215120513.png]]


## Template Method

### Propósito
- Define el esqueleto de un algoritmo en una operación, difiriendo algunos pasos hasta las subclases. Permite que éstas redefinan ciertos pasos del algoritmo sin cambiar la estructura del algoritmo en sí

### Aplicabilidad
- Para implementar las partes de un algoritmo que no cambian y dejar que las subclases implementen aquéllas otras que pueden variar
- Como motivo de factorizar código, para evitar código duplicado
- Para controlar el modo en el que las subclases extienden de la clase base

### Estructura
![[Pasted image 20221215122415.png]]
![[Pasted image 20221215122458.png]]

### Participantes
- **AbstractClass**: 
	- Define las operaciones primitivas abstractas que redefinirán las subclases
	- Implementa un método de plantilla con el esqueleto del algoritmo
- **ConcreteClass**:
	- Implementa las operaciones primitivas

### Consecuencias
- Los Template Methods son una técnica fundamental para la reutilización de código
- Es la clase padre quien llama a operaciones en los hijos
- Los Template Methods pueden llamar a los siguientes tipos de operaciones
	- Operaciones concretas de otras clases (o métodos privados de la propia clase)
	- Operaciones concretas en la propia clase base abstracta (que pueden ser o no redefinidas)
	- Operaciones primitivas (abstractas), que deberán ser implementadas
	- Métodos de fabricación (Factory Method)
	- Operaciones de enganche (**hook**)
		- Normalmente protegidas, tienen una implementación vacía en la clase abstracta que las subclases podrán redefinir. Son como operaciones opcionales

### Operaciones de enganche
![[Pasted image 20221215123103.png]]
![[Pasted image 20221215123128.png]]

### Implementación
- Hacer a las operaciones primitivas llamadas por el método de plantilla **protected**
	- Y aquéllas que deban ser obligatoriamente redefinidas **abstractas**
- Minimizar el número de operaciones primitivas asbtractas
- Convenio de nombrado:
	- Que empiecen por **Do-**

### Patrones relacionados
- **Factory Method**
	- Los métodos de fabricación son llamados desde métodos plantilla
- **Strategy**
	- El Template Method usa la herencia para modificar parte de un algoritmo; el Strategy usa delegación para cambiar el algoritmo entero

# 8. Adapter y Command
---
## Adapter
- Es un patrón estructural
### Propósito
- Convierte la interfaz de una clase en otra que es la que esperan los clientes. Permite que trabajen juntas clases que de otro modo no podrían por tener interfaces incompatibles
![[Pasted image 20221215130354.png]]
- Muchas veces el adaptador tendrá que implementar funcionalidad que la clase adaptada no hace

### Aplicabilidad
- Queremos usar una clase existente y ésta no tiene la interfaz (tipo) que necesitamos
- Queremos crear una clase reutilizable que coopere con clases con las que no está relacionada (interfaces incompatibles)
- (Sólo la versión de objetos) Necesitamos usar varias subclases existentes pero sin tener que adaptar su interfaz creando una nueva subclase de cada una
	- Un adaptador de objetos puede adaptar la interfaz de su clase padre

### Estructura
![[Pasted image 20221215130806.png]]
![[Pasted image 20221215130843.png]]
![[Pasted image 20221215130911.png]]
![[Pasted image 20221215130933.png]]

### Participantes
- **Target**: define la interfaz específica del dominio (usada por los clientes)
- **Client**: colabora con objetos de tipo Target
- **Adaptee**: la clase existente cuya interfaz necesita ser adaptada
- **Adapter**: adapta la interfaz de Adaptee a la de Target

### Consecuencias
- Un adaptador de clases:
	- Adapta una clase concreta a una interfaz (no se puede usar cuando queremos adaptar una clase y todas sus subclases)
	- Permite que el adaptador redefina parte del comportamiento de la clase adaptada
	- Introduce un sólo objeto adicional, sin indirección
- Un adaptador de objetos:
	- Permite que un único adaptador funcione para un objeto de la clase adaptada y todas sus subclases
	- Permite adaptar objetos existentes
	- No es del tipo del objeto adaptado

## Command
- Patrón de comportamiento

### Propósito
- Encapsula una petición dentro de un objeto, permitiendo parametrizar a los clientes con distintas peticiones, encolarlas, guardarlas en un registro de sucesos o implementar un mecanismo de deshacer/repetir

### Motivación
- La clave de este patrón es una interfaz **Command** que define una operación **execute**
- Son las subclases concretas quienes implementan la operación y especifican el receptor de la orden
![[Pasted image 20221215133007.png]]
![[Pasted image 20221215133020.png]]
- Lo que permite el patrón Command es desacoplar el objeto que invoca a la operación de aquél que tiene el conocimiento necesario para realizarla

### Aplicabilidad
- Úsese el patrón Command cuando se quiera:
	- Parametrizar objetos con una determinada acción
	- Especificar, guardar y ejecutar una petición en distintos momentos (desacoplamiento atemporal)
	- Permitir deshace/repetir
		- En este caso, **execute** deberá guardar el estado para poder revertir los efectos de ejecutar la operación
		- Y hará falta una operación añadida, **unexecute**
	- Guardar todas las operaciones ejecutadas en un registro (log)
		- Proporcionando un par de operaciones **store** y **load**
	- Usar transacciones (como en RI)

### Estructura
![[Pasted image 20221215133428.png]]
![[Pasted image 20221215133450.png]]

### Participantes
- **Command**: define una interfaz para ejecutar una operación
- **ConcreteCommand**: 
	- Asocia un objeto Receiver con una acción
	- Implementa execute llamando a las operaciones de dicho objeto receptor
- **Client**: crea un objeto ConcreteCommand y establece su receptor
- **Invoker**: le pide al Command que se ejecute
- **Receiver**: quien realmente lleva a cabo la acción

### Colaboraciones
- El cliente crea un objeto **ConcreteCommand** y especifica su receptor
- Un objeto **Invoker** guarda el objeto **ConcreteCommand**
- Aquél llama a la operación de este último
- El objeto **ConcreteCommand** se vale de las operaciones de su receptor para llevar a cabo la acción
![[Pasted image 20221215134101.png]]

### Consecuencias
- Resulta sencillo añadir nuevas acciones, al no tener que tocar las clases existentes
![[Pasted image 20221215134157.png]]
![[Pasted image 20221215134241.png]]

# 9. Decorator y Observer
---

## Decorator

### Propósito
- Permite añadir responsabilidades a un objeto dinámicamente. Los decoradores proporcionan una alternativa flexible a la herencia para extender la funcionalidad
- También conocido como Wrapper

### Estructura
![[Pasted image 20221215145648.png]]
![[Pasted image 20221215145818.png]]
![[Pasted image 20221215145834.png]]

### Aspectos clave
- Los decoradores tienen el mismo tipo que los objetos que decoran
	- Por tanto podemos usar un decorador en vez del objeto original
- Se puede usar uno o más decoradores para envolver un objeto
- El decorador añade su propio comportamiento antes o después de delegar al objeto decorado el resto del trabajo
- Los objetos pueden ser decorados en cualquier momento (en tiempo de ejecución y en cualquier orden)

### Motivación 
- A veces se quiere añadir responsabilidades a objetos individuales, no a toda una clase
- Una solución más flexible que la herencia sería envolver el componente en otro objeto envoltorio que realice una operación (el decorador)
- La presencia del decorador es transparente para los clientes del componente
- El decorador puede llevar a cabo acciones adicionales
![[Pasted image 20221215150356.png]]

### Aplicabilidad
- Para añadir responsabilidades a otros objetos dinámicamente y de forma transparente
- Cuando no se puede heredar o no resulta práctico

### Estructura
![[Pasted image 20221215150513.png]]

### Participantes
- **Component**: define la interfaz de los objetos a los que se les puede añadir responsabilidades dinámicamente
- **ConcreteComponent**
- **Decorator**: mantiene una referencia a un objeto Component y tiene su misma interfaz
- **ConcreteDecorator**: añade responsabilidades al componente

### Consecuencias
- **Ventajas**:
	- Más flexibilidad que la herencia estática
	- Evita que las clases de arriba de la jerarquía estén repletas de funcionalidad
		- En vez de definir una clase compleja para tratar de dar cabida a todas ellas, la funcionalidad se logra añadiendo decoradores a una clase simple
- **Inconvenientes**: 
	- Un decorador y sus componentes no son idénticos
	- Muchos objetos pequeños

![[Pasted image 20221215151101.png]]

### Patrones relacionados
- **Adapter**
	- El decorador sólo cambia las responsabilidades del objeto, no su interfaz
- **Composite**
	- Un decorator puede verse como un Composite de sólo un componente
	- Pero el decorador añade responsabilidades adicionales (no está pensado para la agregación de objetos)
- **Strategy**
	- Un decorator cambia la piel del objeto, un Strategy sus tripas

![[Pasted image 20221215151445.png]]
![[Pasted image 20221215151456.png]]

## Observer
- Patrón de comportamiento de objetos

### Propósito
- Define una dependencia de uno a muchos entre objetos, de modo que cuando un objeto cambia su estado, todos los demás objetos dependientes se modifican y actualizan su estado automáticamente
- También conocido como Publicar-Suscribir
![[Pasted image 20221215153322.png]]

### Aplicabilidad
- Una abstracción tiene dos aspectos, uno de los cuales depende del otro
- Un cambio en un objeto requiere que cambien otros
	- Y no sabemos a priori cuáles ni cuántos
- Un objeto necesita notificar a otros cambios en su estado sin hacer presunciones sobre quiénes son dichos objetos (cuando no queremos que estén fuertemente acoplados)

### Estructura
![[Pasted image 20221215153542.png]]
![[Pasted image 20221215153616.png]]
![[Pasted image 20221215153649.png]]

### Participantes 
- **Subject**:
	- Conoce a sus observadores
	- Proporciona una interfaz para que se suscriban los objetos Observer (o que se borren)
- **Observer**:
	- Define una interfaz para actualizar los objetos que deben ser notificados de cambios en el objeto Subject
- **ConcreteSubject**:
	- Guarda el estado de interés para los objetos ConcreteObserver
	- Envía una notificación a sus observadores cuando cambia su estado
- **ConcreteObserver**:
	- Mantiene una referencia al objeto ConcreteSubject
	- Guarda el estado que debería permanecer sincronizado con el objeto observado
	- Implementa la interfaz Observer para mantener su estado consistente con el objeto observado

![[Pasted image 20221215154200.png]]

### Consecuencias
- No se especifica el receptor de una actualización, se envía a todos los interesados
- Se podrían producir actualizaciones inesperadas en cascada muy ineficientes 
- La actualización es lanzada por el objeto observado

### Protocolos de actualización
- Push
	- El objeto observado envía información detallada a sus observadores sobre el cambio producido (la necesiten o no)
- Pull
	- Tan sólo avisa de que cambió (los observadores solicitan la información que necesiten)

Un buen ejemplo serían los Eventos de Java y los Listener

# 10. Prototype y Visitor
---
## Prototype
- Supongamos un editor de dibujo
- Tenemos las figuras de siempre: cuadrado, circulo ,rectángulo y triángulo
- Pero queremos añadir stencils, es decir, elementos de uml, widgets, o cualquier otra figura compleja
- El programa obviamente no puede conocer todos los tipos de figura, pues son infinitos y se crean dinámicamente

- El patrón Prototype consiste en que los objetos sepan **cómo clonarse a sí mismos**

### Propósito
- Especifica los tipos de objetos a crear usando una instancia prototípica y crea nuevos objetos copiando dicho prototipo

![[Pasted image 20221215203949.png]]

### Aplicabilidad 
- Usese el patrón Prototype cuando un sistema no pueda (o no deba) conocer cómo se crean, componen y representan los productos, y si además se da alguna de estas circunstancias:
	- las clases a instanciar son definidas en tiempo de ejecución
	- para evitar construir una jerarquía paralela de factorías de productos
	- cuando las instancias de una clase puedan tener sólo unos pocos posibles estados, y pueda resultar más convincente crear los objetos correspondientes como prototipos y clonarlos, en vez de instanciar manualmente la clase, cada vez con el estado necesario

### Estructura
![[Pasted image 20221215204259.png]]
![[Pasted image 20221215204327.png]]

### Participantes
- **Prototype**: declara la interfaz para clonarse (suele ser una única operación)
- **ConcretePrototype**: implementa la operación de clonación
- **Client**: crea un nuevo objeto diciéndole al prototipo que se clone

- Un cliente le pide al prototipo que se clone

### Consecuencias
- Como el **Abstract Factory** oculta las clases concretas de producto al cliente
- También permite:
	- Añadir y eliminar productos dinámicamente (en tiempo de ejecución)
	- Especificar nuevos objetos modificando valores de sus propiedades
		- Mediante composición 
	- Especificar nuevos objetos variando su clase (como en el **Composite**)
	- Reduce las subclases (a diferencia del **Factory Method**)

Inconvenientes:
- La implementación de la operación de clonación puede no ser fácil

## Visitor

### Propósito
- Representa una operación a realizar sobre una estructura de objetos. Permite definir nuevas operaciones sin modificar las clases de los elementos sobre los que opera
![[Pasted image 20221215205904.png]]
![[Pasted image 20221215205954.png]]
![[Pasted image 20221215210008.png]]
![[Pasted image 20221215210045.png]]

- En Java, el enlace dinámico no se aplica a los parámetros, sino sólo al receptor del mensaje

### Aplicabilidad
Debería aplicarse cuando:
- Una estructura de objetos contiene muchas clases de objetos con diferentes interfaces, y queremos realizar operaciones sobre esos elementos que dependen de su clase concreta
- Se necesitan realizar muchas operaciones distintas y no relacionadas sobre objetos de una estructura de objetos, y queremos evitar contaminar sus clases con dichas operaciones
	- El **Visitor**  permite mantener juntas operaciones relacionadas definiéndolas en una clase

### Estructura
![[Pasted image 20221215211855.png]]
![[Pasted image 20221215211917.png]]

### Participantes
- **Visitor**:
	- Declara una operación **visit** para  cada clase de operación **ConcreteElement**
	- El nombre y signatura identifican a la clase que envía la petición visit al visitante
- **ConcreteVisitor**:
	- Implementa cada operación declarada por **Visitor**
	- Cada operación implementa un fragmento del algoritmo definido por la clase correspondiente de la estructura
	- **ConcreteVisitor** proporciona el contexto para el algoritmo y guarda su estado local
- **Element**: define una operación **accept** que recibe un visitante como argumento
- **ObjectStructure**: 
	- Permite enumerar sus elementos
	- Puede proporcionar una interfaz de alto nivel para permitir al visitante visitar sus elementos
	- Puede ser un **Composite** o una colección, como una lista o un conjunto

### Colaboraciones
- Un cliente debe crear un objeto ConcreteVisitor y a continuación recorrer la estructura visitando cada objeto con el **Visitante**
- Cada vez que se visita un elemento, éste llama a la operación del Visitor que se corresponde con su clase
	- El elemento se pasa a sí mismo como argumento de la operación, en caso de que sea necesario

### Consecuencias
- El visitante facilita añadir nuevas operaciones
- Un visitante agrupa operaciones que están relacionadas y separa las que no lo están
- Es difícil añadir nuevas clases de elementos concretos

---