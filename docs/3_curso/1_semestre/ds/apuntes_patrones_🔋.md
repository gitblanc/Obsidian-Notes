>[!Note]
>Estos apuntes están basados en el libro Patrones de Diseño de Erich Gamma junto con los apuntes de DS que nos proporciona la Universidad.
>
>En cada patrón, los apartados de Motivación y Estructura utiliza el segundo diagrama  (es decir, el que nos da César).
>
>Al final de cada patrón hay un ejemplo que nos da César para entender el patrón (que no deberías de estudiarlo como tal, sino más bien entenderlo)


## Strategy

### Propósito

Define una familia de algoritmos, encapsula cada uno de ellos y los hace intercambiables. Permite que un algoritmo varíe independientemente de los clientes que lo usan

### También conocido como

*Policy* (política)

### Motivación

Existen muchos algoritmos para dividir en líneas un flujo de texto. No resulta una buena práctica por varias razones:
- Los clientes que necesitan dividir el texto en líneas se vuelven más complejos si tienen que incluir dicho código, lo que los hace más grandes y más difíciles de mantener
- No tenemos por qué permitir múltiples algoritmos si no los vamos a usar todos
- Es difícil añadir nuevos algoritmos o modificar los existentes

Estos problemas pueden evitarse definiendo clases que encapsulen los diferentes algoritmos de división en líneas. Un algoritmo así encapsulado se denomina estrategia.

![](img/Pasted%20image%2020240603115339.png)

![](img/Pasted%20image%2020240603121408.png)

### Aplicabilidad

Usar el patrón Strategy cuando:
- Muchas clases relacionadas difieren sólo en su comportamiento
- Se necesitan distintas variantes de un algoritmo
- Un algoritmo usa datos que los clientes no deberían conocer
- Una clase define muchos comportamientos, y éstos se representan como múltiples sentencias condicionales en sus operaciones

### Estructura

![](img/Pasted%20image%2020240603115828.png)

![](img/Pasted%20image%2020240603121353.png)

### Participantes

- **Estrategia** (Componedor)
	- Declara una interfaz común a todos los algoritmos permitidos. El Contexto usa esta interfaz para llamar al algoritmo definido por una EstrategiaConcreta
- **EstrategiaConcreta** (ComponedorSimple, ComponedorTeX, ComponedorMatriz)
	- Implementa el algoritmo usando la interfaz Estrategia
- **Contexto** (Composicion)
	- Se configura con un objeto EstrategiaConcreta
	- Mantiene una referencia a un objeto Estrategia
	- Puede definir una interfaz que permita a la Estrategia acceder a sus datos

### Colaboraciones

- La estrategia y el contexto colaboran para implementar el algoritmo escogido
	- El contexto puede pasar todos los datos que necesita al llamar a la estrategia concreta
	- O se puede pasar a sí mismo como referencia para que ésta llame a los métodos que necesite
- Los clientes colaboran con el contexto
	- Pueden pasarle la estrategia concreta

### Consecuencias

- Define familias de algoritmos relacionados
- Es una alternativa a la herencia
	- Hace que el contexto sea más fácil de entender, modificar y mantener
	- Evita la duplicación de código
	- Evita la explosión de subclases
	- Se puede cambiar dinámicamente
- Elimina las múltiples sentencias condicionales
- El cliente puede elegir entre varias implementaciones (incluso dinámicamente)
- Los clientes deben conocer las diferentes estrategias
- Puede complicarse la comunicación entre el contexto y las estrategias
- Crece el número de objetos

### Posibles usos

- Validadores de campos de formularios
- Distintas modalidades de juego
	- En un juego de póquer, dominó, etc
	- Niveles de dificultad en el ajedrez o un simulador de coches

### Ejemplo que nos da César

![](img/Pasted%20image%2020240603120841.png)

*¿Cómo hacemos para que ahora vuelen?*

![](img/Pasted%20image%2020240603120946.png)

>[!Error]
>Esto conlleva un problema
>- Ahora tenemos un montón de patos de goma volando por la pantalla
>- Al implementar `volar` en la superclase, hemos dado esa habilidad a todos los patos, incluyendo aquellos que no deberían

Una posibilidad sería que el `volar` en `PatoDeGoma` no hiciese nada (estuviese vacío)

**Solución:**

![](img/Pasted%20image%2020240603121214.png)

## Factory Method

### Propósito

Define una interfaz para crear un objeto, pero deja que sean las subclases quienes decidan qué clase instanciar. Permite que una clase delegue en sus subclases la creación de objetos

### También conocido como

*Virtual Constructor* (Constructor Virtual)

### Motivación

- Sea un framework para la construcción de editores de documentos de distintos tipos
	- Clases abstractas `Application` y `Document`
		- Los clientes deberán heredar de ellas para implementar los detalles de cada aplicación concreta
		- P. ej. `DrawingApplication` y `DrawingDocument`
	- ¿Cómo se implementa la opción `New` del menú?
	- ¿Cómo sabe la clase `Application` qué tipo concreto del documento debe crear?

Llamaremos a `CrearDocumento` un método de fabricación porque es el responsable de "fabricar" un objeto

![](img/Pasted%20image%2020240603123616.png)

![](img/Pasted%20image%2020240603123630.png)

### Aplicabilidad

Úsese el patrón Factory Method cuando:
- Una clase no puede anticipar la clase de objetos que debe crear
- Una clase quiere que sean sus subclases quienes especifiquen los objetos que ésta crea
- Las clases delegan la responsabilidad en una de entre varias subclases, y queremos localizar qué subclase concreta es en la que se delega

### Estructura

![](img/Pasted%20image%2020240603124130.png)

![](img/Pasted%20image%2020240603124302.png)

### Participantes

- **Producto** (Documento)
	- Define la interfaz de los objetos que crea el método de fabricación
- **ProductoConcreto** (MiDocumento)
	- implementa la interfaz del Producto
- **Creador** (Aplicacion)
	- Declara el método de fabricación, el cual devuelve un objeto de tipo Producto. 
	- Puede definir una implementación predeterminada del método de fabricación que devuelva un objeto ProductoConcreto
	- Puede llamar al método de fabricación para crear un objeto Producto
- **CreadorConcreto** (MiAplicacion)
	- Redefine el método de fabricación para devolver una instancia de un ProductoConcreto

### Colaboraciones

- El Creador se apoya en sus subclases para definir el método de fabricación que devuelve una instancia del ProductoConcreto apropiado

### Consecuencias

- Elimina la necesidad de enlazar clases específicas de la aplicación en el código
	- Sólo maneja la interfaz `Product`
		- Por lo que permite añadir cualquier clase `ConcreteProduct` definida por el usuario
- **Inconveniente**:
	- Tener que crear una subclase de `Creator` en los casos en los que ésta no fuera necesaria de no aplicar el patrón
- En los ejemplos anteriores, el método de fabricación era llamado únicamente por el creador y sus subclases. No tiene por qué ser siempre así: hay veces en que puede ser el cliente quien se encargue de ello
	- Por ejemplo en los casos de **jerarquías paralelas**

![](img/Pasted%20image%2020240603125322.png)

## Abstract Factory

### Propósito

Proporciona una interfaz para crear familias de objetos relacionados o que dependen entre sí, sin especificar sus clases concretas

### También conocido como

*Kit*

### Motivación

- Sea una biblioteca gráfica que permita generar interfaces para diferentes entornos de ventanas
	- Cada uno de ellos tendrá una clase distinta para representar una ventana, una barra de desplazamiento, un botón...
- Si queremos que una aplicación se aproveche de ello y sea portable, no podrá crear directamente objetos de esas clases específicas

![](img/Pasted%20image%2020240603125907.png)

![](img/Pasted%20image%2020240603125958.png)

### Aplicabilidad

Úsese el patrón Abstract Factory cuando:
- Un sistema debe ser independiente de cómo se crean, componen y representan sus productos
- Un sistema debe ser configurado con un una familia de productos de entre varias
- Una familia de objetos producto relacionados está diseñada para ser usada conjuntamente, y es necesario hacer cumplir esta restricción
- Quiere proporcionar una biblioteca de clases de productos, y sólo quiere revelar sus interfaces, no sus implementaciones

### Estructura

![](img/Pasted%20image%2020240603130255.png)

### Participantes

- **FabricaAbstracta** (FabricaDeUtiles)
	- Declara una interfaz para operaciones que crean objetos producto abstractos
- **FabricaConcreta** (FabricaDeUtilesMotif, FabricaDeUtilesPM)
	- Implementa las operaciones para crear objetos producto concretos
- **ProductoAbstracto** (Ventana, BarraDeDesplazamiento)
	- Declara una interfaz para un tipo de objeto producto
- **Producto Concreto** (VentanaMotif, BarraDeDesplazamientoMotif)
	- Define un objeto producto para que sea creado por la fábrica correspondiente
	- Implementa la interfaz ProductoAbstracto
- **Cliente**
	- Sólo usa interfaces declaradas por las clases FabricaAbstracta y ProductoAbstracto

### Consecuencias

- Aísla las clases concretas
	- Los clientes manipulan los productos únicamente a través de sus interfaces abstractas, gracias a que las clases de productos concretos están encapsuladas en cada fábrica concreta, no aparecen en el código
- Permite intercambiar fácilmente familias de productos
	- Basta con cambiar una única clase, en un único sitio: la fábrica concreta
- Promueve la consistencia entre los productos
	- Sólo se pueden usar conjuntamente los objetos de cada familia
- Dificulta añadir nuevos tipos de productos
	- Hay que cambiar la interfaz de la fábrica abstracta y por tanto implementar el nuevo método en todas sus subclases

### Implementación

- Las fábricas pueden ser `Singletons`
- Crear los productos
	- Normalmente, el `Abstract factory` emplea a su vez un `Factory Method` para cada producto
		- Sencillo, pero requiere crear una subclase por cada familia
	- Otra posibilidad es emplear el patrón `Prototype`: una única clase para la fábrica abstracta y tener distintos objetos de la misma configurados mediante prototipos
- Fábricas extensibles
	- Pretenden resolver el problema de poder añadir nuevos tipos de productos
	- Un único método de creación especificando el tipo de producto como parámetro
	- Más flexible, pero menos seguro (se pierde la comprobación estática de tipos)

## Factory Method vs Abstract Factory

![](img/Pasted%20image%2020240603131608.png)

## Composite

### Propósito

Compone objetos en estructuras de árbol para representar jerarquías de parte/todo. Permite que los clientes traten de manera uniforme a los objetos individuales y a los compuestos

### Motivación

- Un editor de dibujo permite realizar dibujos compuestos de elementos simples (líneas, rectángulos...) u otros dibujos
	- ¿Cómo evitamos que los clientes tengan que distinguir entre unos y otros?

![](img/Pasted%20image%2020240603132417.png)

![](img/Pasted%20image%2020240603132441.png)

### Aplicabilidad

Usar el patrón Composite cuando:
- Quiera representar jerarquías de objetos parte-todo
- Quiera que los clientes traten por igual los objetos y los objetos individuales

### Estructura

![](img/Pasted%20image%2020240603132655.png)

![](img/Pasted%20image%2020240603132735.png)

![](img/Pasted%20image%2020240603132753.png)

### Participantes

- **Componente** (Grafico)
	- Declara la interfaz común
	- Implementa el comportamiento predeterminado de la interfaz que es común a todas las clases
	- Declara operaciones para acceder a sus hijos (aunque no necesariamente, pues pueden declararse en el compuesto)
	- (opcional) Define una interfaz para acceder al padre
- **Hoja** (Rectangulo, Linea, Texto...)
	- Representa objetos hoja en la composición
	- Una hoja no tiene hijos
- **Compuesto** (Dibujo)
	- Almacena sus componentes hijos
	- Implementa las operaciones relacionadas con los hijos
- **Cliente**
	- Manipula los objetos de la composición a través de la interfaz de Componente

### Consecuencias

- Permite jerarquías de objetos tan complejas como se quiera
	- Allá donde el cliente espere un objeto primitivo, podrá recibir un compuesto y no se dará cuenta
- Simplifica el cliente
	- Al eliminar el código para distinguir entre unos y otros
- Se pueden añadir nuevos componentes fácilmente
- Como desventaja, podría hacer el diseño demasiado general

### Implementación

- Referencias explícitas al padre
- Maximizar la interfaz de *Component*
	- El componente puede proporcionar implementaciones predeterminadas que luego las clases hoja y las compuestas redefinan
	- Problema: puede haber operaciones que tengan sentido en unas pero no en otras
		- Ejemplo: las operaciones de gestión de los hijos
- Orden de los hijos
	- Si es significativo, hay que diseñar las interfaces de acceso y gestión de los hijos cuidadosamente

## State

### Propósito

Permite que un objeto modifique su comportamiento cada vez que cambie su estado interno. Parecerá que cambia la clase del objeto

### También conocido como

*Objects for States* (Estados como Objetos)

### Motivación

- Una conexión de red es representada en una implementación TCP como TCPConnection
- La conexión puede estar en uno de los siguientes estados:
	- Abierta
	- Escuchando
	- Cerrada

![](img/Pasted%20image%2020240603144016.png)

### Aplicabilidad

Úsese el patrón State en cualquiera de los siguientes casos:
- El comportamiento de un objeto depende de su estado, y éste puede cambiar en tiempo de ejecución
- Las operaciones tienen largas sentencias condicionales anidadas que tratan con los estados
	- Siendo el estado normalmente una constante
	- Muy frecuentemente, son varias las operaciones en las que se repite esa misma estructura condicional
	- Este patrón mueve cada rama de la lógica condicional a una clase aparte
		- Lo que nos permite tratar al estado del objeto como un objeto de pleno derecho, que puede variar independientemente de otros objetos

### Estructura

![](img/Pasted%20image%2020240603144412.png)

![](img/Pasted%20image%2020240603144426.png)

### Participantes

- **Contexto** (ConexionTCP)
	- Define la interfaz de interés para los clientes
	- Mantiene una instancia de una subclase de EstadoConcreto que define el estado actual
- **Estado** (EstadoTCP)
	- Define una interfaz para encapsular el comportamiento asociado con el estado del Contexto
- **subclases del EstadoConcreto** (TCPEstablecida, TCPEscuchando, TCPCerrada)
	- Cada subclase implementa un comportamiento asociado con un estado del Contexto

### Colaboraciones

- El Contexto delega las operaciones dependientes del estado al objeto que representa el estado actual
- El contexto podría pasarse a sí mismo como parámetro
	- Para que el estado acceda al contexto si es necesario
- una vez que el Contexto es inicializado en un determinado estado, los clientes no necesitan tratar directamente con los estados
- O bien el Contexto o bien los EstadosConcretos deciden cuándo se pasa de un estado a otro

### Consecuencias

- Localiza el comportamiento específico del estado y lo aísla en un objeto
	- Se pueden añadir nuevos estados y transiciones fácilmente simplemente definiendo nuevas subclases de `State`
- Hace explícitas las transiciones entre estados

### Implementación

- ¿Quién define las transiciones entre estados?
	- Si el criterio es siempre el mismo, puede ser el propio contexto
	- Normalmente es más flexible y apropiado que sean las subclases de los estados
		- Esto requiere añadir una operación al contexto para cambiar su estado de forma explícita
		- **Ventaja**: flexibilidad
		- **Inconveniente**: dependencias de implementación (acoplamiento) entre las subclases que representan los estados concretos
- Uso de la herencia dinámica
	- Este patrón no sería necesario en lenguajes que permiten cambiar la clase de un objeto en tiempo de ejecución o que proveen mecanismos para delegar peticiones automáticamente en otros objetos
- Acciones de entrada/salida
	- Cuando hay que realizar alguna acción al entrar o salir de un estado puede venir bien añadir un método `entry`, `exit` o ambos a la interfaz `State`

### Posibles usos

![](img/Pasted%20image%2020240603145625.png)

## State vs Strategy

- **Strategy**: es seleccionada por un agente externo o por el contexto. Una estrategia tiende a tener un método único de "inicio" que llama a todos los demás. Hay mucha cohesión entre los métodos de un Strategy
- **State**: un State generalmente selecciona el siguiente estado de su contexto. Un estado tiende a tener muchos métodos no relacionados, por lo que hay poca cohesión entre los métodos de un State
	- Los métodos del State suelen llamarse igual y tener la misma signatura que las que tenían dicho subconjunto de operaciones en el contexto

## Template Method

### Propósito

Define en una operación el esqueleto de un algoritmo, delegando en las subclases algunos de sus pasos. Permite que las subclases redefinan ciertos pasos de un algoritmo sin cambiar su estructura

### Motivación

- Sea un framework de aplicaciones que proporciona unas clases `Application` y `Document`
	- La primera es la responsable de abrir los documentos almacenados en ficheros
	- La segunda representa la información en sí del documento, una vez que ya ha sido leído del fichero
- Las aplicaciones construidas con el framework redefinirán ambas clases para adaptarlas a sus necesidades concretas
- ¿Cómo implementar, de manera genérica, el método `openDocuiment` de la clase `Application`?

![](img/Pasted%20image%2020240603151045.png)

- El método abstracto anterior define todos los pasos necesarios para abrir un documento
	- Comprueba si se puede abrir, crea un objeto `Document`, lo añade al conjunto de documentos y finalmente lo lee
	- Lo hace en términos de operaciones abstractas

![](img/Pasted%20image%2020240603151215.png)

### Aplicabilidad

El patrón Template Method debería usarse:
- Para implementar las partes de un algoritmo que no cambian y dejar que sean las subclases quienes implementen el comportamiento que puede variar
- Como motivo de factorizar código, cuando movemos cierto código a una clase base común para evitar código duplicado
- Para controlar el modo en que las subclases extienden la clase base
	- Dejando que sea sólo a través de unos métodos plantilla dados

### Estructura

![](img/Pasted%20image%2020240603151421.png)

![](img/Pasted%20image%2020240603151434.png)

### Participantes

- **ClaseAbstracta** (Application)
	- Define las operaciones primitivas abstractas que redefinirán las subclases
	- Implementa un método de plantilla con el esqueleto del algoritmo
- **ClaseConcreta** (MiApplication)
	- Implementa las operaciones primitivas para realizar los pasos del algoritmo específicos de las subclases

### Consecuencias

- Los métodos de plantilla son una técnica fundamental para la reutilización de código
- Inversión de control
	- Es la clase padre quien llama a operaciones en los hijos
- Los métodos de plantilla pueden llamar a los siguientes tipos de operaciones:
	- Operaciones concretas de otras clases
	- Operaciones concretas en la propia clase base abstracta
		- Proporcionan comportamiento predeterminado que las subclases pueden redefinir si es necesario
	- Operaciones primitivas (es decir, abstractas)
		- Que las subclases deberán implementar
	- Métodos de fabricación
	- Operaciones de enganche (*hook*)
		- Normalmente protegidas, tienen una implementación vacía en la clase abstracta, que las subclases podrán redefinir. Son como operaciones opcionales

Operaciones de enganche:

![](img/Pasted%20image%2020240603152121.png)

![](img/Pasted%20image%2020240603152142.png)

### Implementación

- Hacer las operaciones primitivas llamadas por el método de plantilla `protected`
	- Y, a aquéllas que deban ser obligatoriamente redefinidas, abstractas
- Minimizar el número de operaciones primitivas abstractas
- Convenios de nombrado
	- Es conveniente identificar las operaciones que deben ser redefinidas anteponiendo un prefijo al nombre (ej: `Do-`)

### Patrones relacionados

- *Factory Method*
	- Muchas veces los métodos de fabricación son llamados desde métodos plantilla
- *Strategy*
	- El *Template Method* usa la herencia para modificar parte de un algoritmo; *Strategy* usa delegación para cambiar el algoritmo entero

## Adapter

### Propósito

Convierte la interfaz de una clase en otra interfaz que es la que esperan los clientes. Permite que cooperen clases que de otra forma no podrían tener interfaces compatibles

### También conocido como

*Wrapper* (Envoltorio)

### Motivación

- Supongamos que estamos haciendo un editor de dibujo
	- La abstracción fundamental es el objeto gráfico (`Shape`), que puede dibujarse a sí mismo
	- Define una subclase por cada tipo de objeto gráfico: `LineShape`, `PolygonShape`...
- Supongamos que, para implementar una subclase `TextShape` (bastante más compleja que las anteriores) queremos echar mano de una clase `TextView` que nos proporciona la biblioteca gráfica
- La interfaz de `TextView` no tendrá nada que ver con la de `Shape`
	- Le faltarán algunas operaciones, otras las tendrá con otro nombre, o bien recibirán parámetros de otro tipo...
- Crearemos una clase `TextShape` que adapte la interfaz `TextView` a la de `Shape`
- Dos opciones:
	- Heredando la interfaz de `Shape` y la implementación de `TextView` (versión de dos clases)
	- Mediante composición de objetos, haciendo que `TextShape` delegue en una instancia de `TextView` (versión de objetos)

![](img/Pasted%20image%2020240603153138.png)

### Aplicabilidad

Debería usarse el patrón Adapter cuando:
- Se quiere usar una clase existente y su interfaz no concuerda con la que necesita
- Se quiere crear una clase reutilizable que coopere con clases con las que no está relacionada (que no tendrán interfaces compatibles)
- (Sólo la versión de objetos) Necesitamos usar varias subclases existentes pero sin tener que adaptar su interfaz creando una nueva subclase de cada una

### Estructura

![](img/Pasted%20image%2020240603153436.png)

![](img/Pasted%20image%2020240603153455.png)

![](img/Pasted%20image%2020240603153527.png)

![](img/Pasted%20image%2020240603153545.png)

### Participantes

- **Objetivo** (Forma)
	- Define la interfaz específica del dominio que usa el Cliente
- **Cliente** (EditorDeDibujo)
	- Colabora con objetos que se ajustan a la interfaz Objetivo
- **Adaptable** (VistaTexto)
	- Define una interfaz existente que necesita ser adaptada
- **Adaptador** (FormaTexto)
	- Adapta la interfaz de Adaptable a la interfaz Objetivo

### Consecuencias

Las versiones de clases y de objetos de este patrón tienen diferentes ventajas e inconvenientes:
- **Un adaptador de clases**:
	- Adapta una clase concreta a una interfaz (no se puede usar cuando queremos adaptar una clase y todas sus subclases)
	- Permite que el adaptador redefina parte del comportamiento de la clase adaptada (es una subclase de aquélla)
	- Introduce un solo objeto adicional, sin indirección
- **Un adaptador de objetos**
	- Permite que un único adaptador funcione no sólo con un objeto de la clase adaptada, sino de cualquiera de sus subclases
	- Permite adaptar objetos existentes
	- No es del tipo de objeto adaptado

## Command

### Propósito

Encapsula una petición en un objeto, permitiendo así parametrizar a los clientes con diferentes peticiones, hacer cola o llevar un registro de las peticiones, y poder deshacer las operaciones

### También conocido como

*Action* (Acción), *Transaction* (Transacción)

### Motivación

- Una biblioteca de clases para interfaces de usuario tendrá objetos como botones y elementos de menú responsables de realizar alguna operación en respuesta a una entrada del usuario
- La biblioteca no puede implementar dichas operaciones directamente en el botón o el menú
	- Sólo las aplicaciones que usan la biblioteca saben qué hay que hacer y a qué operaciones de otros objetos hay que llamar

![](img/Pasted%20image%2020240603161258.png)

- La clave de este patrón es una interfaz `Command` que define una operación `execute`
- Son las subclases concretas quienes implementan la operación y especifican el receptor de la orden
- Podemos configurar cada elemento del menú, `MenuItem`, con un objeto `Command`
- Los elementos del menú no saben qué objeto concreto están usando (simplemente llaman a su método `execute`)

![](img/Pasted%20image%2020240603161523.png)

![](img/Pasted%20image%2020240603161537.png)

### Aplicabilidad

Úsese el patrón Command cuando se quiera:
- Parametrizar objetos con una acción a realizar
- Especificar, guardar y ejecutar peticiones en distintos momentos
	- Es decir, que la acción a realizar y el objeto que la crea tengan ciclos de vida distintos (desacoplamiento temporal)
- Permitir deshacer/repetir (undo/redo)
	- En ese caso, `execute` deberá guardar el estado para poder revertir los efectos de ejecutar la operación
	- Y hará falta una operación añadida, `unexecute`
- Guardar todas las operaciones ejecutadas en un registro (log)
	- Proporcionando un par de operaciones `store` y `load`
- Usar transacciones

### Estructura

![](img/Pasted%20image%2020240603161915.png)

![](img/Pasted%20image%2020240603161931.png)

### Participantes

- **Orden** (Command)
	- Define una interfaz para ejecutar una operación
- **OrdenConcreta** (ConcreteCommand, OpenCommand...)
	- Define un enlace entre un objeto receptor y una acción
	- Implementa `execute` llamando a las operaciones de dicho receptor
- **Cliente** (Aplicación)
	- Crea un objeto OrdenConcreta (ConcreteCommand) y establece su receptor
- **Invocador** (ElementoDeMenu)
	- Le pide a la orden que ejecute la petición
- **Receptor** (Documento, Aplicacion)
	- Quien realmente lleva a cabo la acción.

### Colaboraciones

- El cliente crea un objeto `ConcreteCommand` y especifica su receptor
- Un objeto `Invoker` guarda el objeto `ConcreteCommand`
- Aquél llama a la operación de este último
	- Quien antes guarda el estado par luego poder deshacer la operación (si son operaciones que se pueden deshacer)
- El objeto `ConcreteCommand` se vale de las operaciones de su receptor para llevar a cabo la acción

![](img/Pasted%20image%2020240603162626.png)

### Consecuencias

- Desacopla el objeto que llama a la operación del que sabe cómo llevarla a cabo
- Son ciudadanos de primera clase (objetos)
- Se pueden ensamblar (Composite)
- Resulta sencillo añadir nuevas acciones, al no tener que tocar las clases existentes

### Implementación

- ¿Cómo de inteligente debería ser?
	- Desde un mero enlace entre el receptor y las operaciones a realizar en él hasta implementarlo todo él solo sin especificar un receptor
- Diferentes niveles de deshacer/repetir
	- A veces será necesario crear una copia del objeto antes de guardarlo en el historial
		- En este caso, los Command serían también Prototype

### Ejemplo de César

![](img/Pasted%20image%2020240603163102.png)

![](img/Pasted%20image%2020240603163117.png)