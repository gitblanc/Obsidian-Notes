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