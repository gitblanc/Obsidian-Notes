# TEMA 2 馃檭
---

## Ensamblados
- Un **ensamblado** es una colecci贸n l贸gica de recursos de una aplicaci贸n (archivos .exe, .dll, .ini, ...).
- Cada proyecto genera un ensamblado.
- Los ensamblados poseen un **conjunto de m贸dulos** (**c贸digo gestionado**, archivos .exe y .dll);

---
## Namespaces
- Son una agrupaci贸n l贸gica de tipos.
- Para inclu铆r un namespace, se usa la declaraci贸n `using` lal principio de una clase o namespace.
- Los namespace se definen entre {} 
````c#
namespace TPP.OrientacionAObjetos{
		...
}
````

---
## Nivel de Ocultaci贸n de una Clase
- Una clase puede ser `public` o `internal`.
- Si es **interna**, s贸lo se podr谩 acceder a ella desde dentro de su ensamblado (desde su proyecto). Aquellas clases que se usan para implementar una funcionalidad deber铆asn ser internal.

---
## Ocultaci贸n de la informaci贸n y Clases
- **public**: accesible desde cualquier punto
- **private**: inaccesible desde fuera de la clase
- **protected**: accesible desde dentro de la clase y sus clases derivadas
- **internal**: accesible desde cualquier clase del ensamblado
- **protected internal**: accesible desde cualquier clase del ensamblado o sus derivadas

El nivel por omisi贸n es **private**

---
## Punto de Entrada
- En un programa s贸lo puede haber un punto de entrada (Main), que ha de ser est谩tico.
- Puede no retornar nada o un entero.
- Puede tener cualquier nivel de ocultaci贸n.
- Puede declararse con o sin par谩metros.

Para especificar los argumentos seleccionar -> Proyecto | Propiedades | Depuraci贸n

---
## Tipos simples
![[tipos simples.png]]

---
## Constantes y Consola
- Se declaran como `const double PI = 3.141592` y no se puede modificar su valor.
- La consola se controla con la clase `System.Console`.

---
## Enumeraciones
- Son un conjunto finito de posibles valores
- Definen un nuevo tipo con su propio grado de ocultaci贸n
- Es posible asignarles expl铆citamente valores enteros
````c#
enum Colores{
	azul, verde=3, rojo, amarillo
}

class Enumerados {
	static void Main(string[] args){
		Colores color;
		color = Colores.azul;
		Console.WriteLine(color);//azul
		colores = (Colores)3;
		Console.WriteLine(color);//verde
	}
}
````

---
## Operadores
![[operadores.png]]

---
## Destructor
- Es un m茅todo que se ha de llamar -> ~nombreclase
- No tiene valor de retorno
- Se ejecuta previamente a la liberaci贸n de memoria de un objeto siempre
- El recolector de basura ejecutar谩 el destructor de un objeto cuando 茅ste se libere

````c#
class Clase{
	public Clase(){
		//Asignaci贸n de recursos
	}
	
	~Clase(){
		//Liberaci贸n de recursos
	}
}
````

---
## Objetos
- Se les accede a trav茅s de referencias
- La referencia `this` nos permite acceder al objeto impl铆cito
- Los objetos se crean con el operador `new`

---
## Clases Parciales
- Una clase parcial se puede implementar en varios ficheros
- Hay que anteponer la palabra `partial`
![[partial class1.png]]
![[partial class 2.png]]

---
## Clases de utilidad
Una clase `static class` de C#:
- No permite definir atributos de instancia
- No permite definir propiedades de instancia
- No permite definir m茅todos de instancia
- No permite definir constructores de instancia

---
## Propiedades
- C# ofrece el concepto de propiedad para acceder al estado de los objetos como si de atributos se tratase, obteniendo los beneficios del **encapsulamiento**. Se oculta el estado interno del objeto, ofreciendo un acceso indirecto mediante las propiedades (**encapsulamiento**)
- Se puede cambiar la implementaci贸n de la propiedad sin modificar el acceso por parte del cliente
- Las propiedades pueden ser de lectura y /o escritura

Esto ayuda a la construcci贸n de objetos, pues si una clase Persona posee un constructor sin par谩metros y posee varias propiedades p煤blicas de lectura y escritura como el nombre y el apellido, se puede construir un objeto Persona indicando los valores de sus propiedades (no necesariamente todas), en cualquier orden, evitando as铆 la sobrecarga excesiva del constructor.
![[constructor alternatives.png]]

---
## Strings
- El operador `+` concatena strings.
- Los objetos de tipo **string** son **inmutables**, no se puede modificar su estado.
- Si queremos modificar su estado, debe usarse la clase **StringBuilder**
- Los strings que comienzan por `@` permiten definir m煤ltiples l铆neas
![[strings 1.png]]
![[strings 2.png]]

---
## Arrays
- Nos permite coleccionar referencias
- Son estructuras de datos con m煤ltiples valores de un mismo tipo
- Un array es un objeto, porque para acceder a 茅l necesitamos una referencia
````c#
int[] array1;
bool[] array2;
Angle[] array3;
````
- Un objeto array se crea con el operador `new`, indicando adem谩s el tama帽o -> `new bool[2]`
- En el caso de los arrays de objetos, tenemos reservado espacio para referencias, no para objetos
![[arrays.png]]
- E bucle **foreach** usa la sintaxis -> `foreach (int i in vector)`

---
## Structs 
- Pueden tener constructores, propiedades, m茅todos, campos, operadores y miembros de clase (static)
- No pueden heredar de otras clases o structs
- Derivan impl铆citamente de ValueType
- Pueden implementar interfaces
- No pueden tener destructores
- Por defecto, su nivel de ocultaci贸n es public
- Siempre se almacenan en la pila, por lo que no se modifican, ya que el par谩metro pasado es una copia del argumento original
![[structs.png]]

---
## Paso de par谩metros
Hay tres tipos:
- **Por valor**: el par谩metro formal es una copia del par谩metro real (argumento). En el paso de objetos lo que se copia es la referencia (el objeto es el original).
- **Por referencia de entrada y salida**: el par谩metro formal es un alias del par谩metro real (argumento). Se pasa con un valor de entrada y se le puede pasar otro de salida, modificando el original. Se usa la palabra reservada `ref`.
- **Paso por referencia de salida**: el par谩metro formal es un alias del par谩metro real (argumento). Se pasa sin valor de entrada y sirve para devolver m谩s de un valor. Se usa la palabra reservada `out`.
![[por valor.png]]
![[por referencia.png]]
![[por salida.png]]
![[resultados parametros.png]]

---
## Par谩metros opcionales
- Valores por omisi贸n a los par谩metros que siempre han de ser los 煤ltimos (m谩s a la derecha)
- Permite la invocaci贸n de una misma funci贸n con distinto n煤mero de argumentos
- Se puede cambiar el orden de los argumentos.
![[params opcionales 1.png]]
![[params opcionales 2.png]]

---
## Sobrecarga de operadores
- Emplea la palabra reservada `operator`
- Los operadores son siempre m茅todos de clase (`static`) -> no son polim贸rficos
- Permite sobrecargar la conversi贸n expl铆cita (cast) y la impl铆cita
- Si sobrecargamos un operador `+` obtenemos autom谩ticamente `+=`
![[sobrecarga operadores.png]]

---
## Declaraci贸n impl铆cita de variables
- Para las variables locales no se requiere especificar su tipo, en su lugar ponemos `var`
- Es 煤til cuando los tipos son muy largos, no es sencillo identificar el tipo (LINQ) o no existe un tipo expl铆cito.

---
## M茅todos extensores
Para crearlos hay que:
- Implementar un m茅todo de clase `static`
- En una clase de utilidad `static`
- El primer par谩metro ha de ser del tipo que deseamos ampliar
- El primer par谩metro ha de declararse anteponiendo la palabra `this`
````c#
static class StringExtension{
	static public uint CountWords (this string cad){
		...
	}
}
````
![[extensores.png]]

---
## Herencia
- Mecanismo de reutilizaci贸n de c贸digo
![[herencia.png]]

---
## Invocaci贸n a constructores base
Se hace  con `base`:
````c#
public Circunference (int x, int y, int radius) : base(x,y){
	this.radius = radius;
}
````

---
## Polimorfismo
- Mecanismo de generalizaci贸n que hace que la abstracci贸n m谩s general pueda representar abstracciones m谩s espec铆ficas. El tipo general representa por tanto varias formas.
![[polimorfismo.png]]

---
## Enlace din谩mico
- Los m茅todos heredados se pueden especializar en las clases derivadas
- Si queremos que se llame al m茅todo real implementado por el objeto, debemos hacer uso del enlace din谩mico (**dynamic binding**)
- Es un mecanismo por el que en tiempo de ejecuci贸n se invoca al m茅todo del tipo din谩mico implementado por el objeto (no al est谩tico declarado en su clase)
- Para que exista el enlace din谩mico tenemos que:
	- Poner la palabra `virtual` al m茅todo que recibe el mensaje (referencia)
	- Sobreescribir su funcionalidad usando la palabra `override` en los m茅todos derivados
- Si no queremos que haya polimorfismo, pues es una coincidencia de nombres, ponemos la palabnra `new`
![[dynamic binding.png]]
![[figure 1.png]]
![[figure 2.png]]

---
## Comparaci贸n de objetos
Podemos estar interesados en saber si:
- Dos objetos *son exactamente el mismo* -> Comparaci贸n por **identidad** -> usamos el operador `==`
- Dos objetos *representan la misma identidad* -> Comparaci贸n por **estado** -> redefinimos el m茅todo `Equals(Object o)`. Al redefinir el equals tambi茅n ser谩 necesario redefinir el GetHashCode()

---
## Operadores is y as
- Cuando utilizamos colecciones polim贸rficas que hacen uso de Object, no siempre se puede hacer un **cast**, ya que no estamos seguros de que el objeto introducido sea del tipo que queremos. Para ello se introduce el operador **is**.
![[isas 1.png]]
![[is as 2.png]]
- Si despu茅s de usar el operador **is** vamos a realizar un cast, es mejor usar el operador **as**
![[2 CURSO/TPP/img/is as 3.png|500]]
![[is as 4.png]]

---
## Autoboxing
- Los tipos simples 隆no heredan de Object!
![[autoboxing 1.png]]
![[autoboxing 2.png]]

---
## Clases y M茅todos Abstractos
- Cuando en una abstracci贸n necesitamos que un mensaje forme parte de su interfaz, pero no podemos implementarlo, este mensaje se declara como m茅todo abstracto.
- Se usa la palabra `abstract`
- Este m茅todo no se implementa
- Todo m茅todo abstracto ofrece enlace din谩mico (no hay que especificar que es virtual)
- En su redefinici贸n hay que usar `override`
- Toda clase que posea al menos un m茅todo abstracto ser谩 una clase abstracta

---
## Interfaces
- **Interfaz**: Conjunto de m茅todos y/o propiedades p煤blicos que ofrecen un conjunto de clases
- Son m茅todos comunes a las distintas abstracciones
![[interfaces.png|300]]
- No pueden tener miembros `static`
![[interfaces 2.png]]
![[interfaces 3.png]]
![[interfaces 4.png]]
![[interfaces 5.png]]
![[interfaces 6.png]]
![[interfaces 7.png]]

---
## IDisposable y using
- Es una interfaz del namespace System con un 煤nico m茅todo -> `void Dispose()`
- Se encarga de liberar los recursos adicionales gestionados por el objeto
- Toda clase que asigna recursos adicionales debe implementar esta interfaz
- Las clases que definan un destructor, probablemente implementar谩sn IDisposable
![[idisposable.png]]
- Se usa la palabra reservada `using` para asegurar la liberaci贸n de los recursos adicionales de un objeto IDisposable
![[idisposable 2.png]]
---
## Implementaci贸n expl铆cita de interfaces
![[ieinterf.png]]

---
## Composici贸n vs herencia
- **Herencia**: un objeto o clase se basa en otro obnjeto o clase, usando la misma implementaci贸n o comportamiento
![[hervscomp.png]]
- **Composici贸n**: quiere decir que tenemos una instancia de una clase que contiene instancias de otras clases que implementan las funciones deseadas
![[composicion-esquema.png]]
Comparativa:
![[comparativa.png]]

---
## Excepciones
- Una **excepci贸n** es un objeto que encapsula informaci贸n acerca de un evento irregular ocurrido en tiempo de ejecuci贸n
- En C# solo se pueden lanzar excepciones del tipo `System.Exception`
![[excepciones.png]]
- Se usa la palabra `throw`
- No es obligatorio manejar ninguna excepci贸n
- Para manejarlas se usa `try` y `catch`. Tambi茅n podremos poner `finally` si queremos que se ejecute un c贸digo en concreto
![[excp1.png]]
![[excp2.png]]

---
## Asertos en C#
- **Aserto**: construcci贸n del lenguaje para asegurar que una condici贸n deba ser siempre cierta. Si no lo fuese, se parar铆a la ejecuci贸n. Est谩n orientadas al proceso de desarrollo
- La t茅cnica m谩s usada est谩 basada en **compilaci贸n condicional**
![[2 CURSO/TPP/img/asertos.png]]
![[asertos2.png]]

---
## Precondiciones
Pueden ser de dos tipos:
- El m茅todo no se puede ejecutar para determinados **valores de los par谩metros** (factorial de u n煤mero negativo)
- El m茅todo no se puede ejecutar para un determinado estado del objeto impl铆cito () ssacar un elemento de la pila vac铆a
-> Consultar [[Invariants, preconditions, postconditions 馃]]

- **Invariantes**: siempre al principio de los m茅todos (excepto constructores). Tambi茅n han de mirarse al final de cada m茅todo
- **Precondiciones**: comprueba si el objeto est谩 en un estado v谩lido
- **Postcondidiones**: han de comprobarse despu茅s de ejecutar un m茅todo

---
## Genericidad
- Permite construir abstracciones modelo para otras abstracciones
- Ofrece una mayor robustez (detecci贸n de errores en tiempo de compilaci贸n) y un mayor rendimiento

---
## default(T)
- Un tipo gen茅rico puede ser cualquier tipo del lenguaje, incluyendo los tipos simples
- En ocasiones queremos asignar o retornar el valor por omisi贸n de un tipo T:
	- La asignaci贸n `variable = null` no ser铆a v谩lida, porque T tambi茅n podr铆a ser un Value Type (int , char)
- Para ello  se usa la palabra `default`
![[default.png]]

---
## Genericidad acotada
- Permite hacer m谩s espec铆ficos los tipos gen茅ricos.
- Por ejemplo un m茅todo de ordenaci贸n donde se puedan ordenar objetos `IComparable<T>`
![[icomparable.png]]

---
# `IEnumerable<T>`
- Interfaz que representa una colecci贸n de elementos gen茅rica
- Deriva de IEnumerable
- Un objeto que implemente un **IEnumerable** se puede recorrer con un **foreach**
- Los arrays derivan de Array e implementan `IEnumerable<T>`
![[ienumerable.png]]
- IEnumerable(T) s贸lo posee un m茅todo -> `GetEnumerator()`
- Este es un *factory method* (patr贸n de dise帽o) encargado de constru铆r un iterador
- El IEnumerator es un *bridge* (patr贸n de dise帽o) para ser independiente de la implementaci贸n del iterador
- El iterador suele implementarse como una clase anidada de la colecci贸n
![[ienumerable2.png]]
![[ienumerable 4.png]]
![[ienumerable 3.png]]
![[ienumerable 5.png]]

---
## Tipos anulables
- En ocasiones se quiere representar que un tipo simple pueda no poseer valor null
- Estos tipos derivan del struct `Nullable<int>`
- Tambi茅n se usa el operador `??`

## System.Collections.Generic
![[colectionsgeneric.png]]

---

Siguiente lecci贸n -> [[Paradigma Orientado a Objetos 馃悿]]