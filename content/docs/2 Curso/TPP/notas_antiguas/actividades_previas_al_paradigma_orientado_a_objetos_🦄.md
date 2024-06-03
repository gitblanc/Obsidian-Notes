# TEMA 2 🙃
---

## Ensamblados
- Un **ensamblado** es una colección lógica de recursos de una aplicación (archivos .exe, .dll, .ini, ...).
- Cada proyecto genera un ensamblado.
- Los ensamblados poseen un **conjunto de módulos** (**código gestionado**, archivos .exe y .dll);

---
## Namespaces
- Son una agrupación lógica de tipos.
- Para incluír un namespace, se usa la declaración `using` lal principio de una clase o namespace.
- Los namespace se definen entre {} 
````c#
namespace TPP.OrientacionAObjetos{
		...
}
````

---
## Nivel de Ocultación de una Clase
- Una clase puede ser `public` o `internal`.
- Si es **interna**, sólo se podrá acceder a ella desde dentro de su ensamblado (desde su proyecto). Aquellas clases que se usan para implementar una funcionalidad deberíasn ser internal.

---
## Ocultación de la información y Clases
- **public**: accesible desde cualquier punto
- **private**: inaccesible desde fuera de la clase
- **protected**: accesible desde dentro de la clase y sus clases derivadas
- **internal**: accesible desde cualquier clase del ensamblado
- **protected internal**: accesible desde cualquier clase del ensamblado o sus derivadas

El nivel por omisión es **private**

---
## Punto de Entrada
- En un programa sólo puede haber un punto de entrada (Main), que ha de ser estático.
- Puede no retornar nada o un entero.
- Puede tener cualquier nivel de ocultación.
- Puede declararse con o sin parámetros.

Para especificar los argumentos seleccionar -> Proyecto | Propiedades | Depuración

---
## Tipos simples
![](img/tipos%20simples.png)

---
## Constantes y Consola
- Se declaran como `const double PI = 3.141592` y no se puede modificar su valor.
- La consola se controla con la clase `System.Console`.

---
## Enumeraciones
- Son un conjunto finito de posibles valores
- Definen un nuevo tipo con su propio grado de ocultación
- Es posible asignarles explícitamente valores enteros
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
![](img/operadores.png)

---
## Destructor
- Es un método que se ha de llamar -> ~nombreclase
- No tiene valor de retorno
- Se ejecuta previamente a la liberación de memoria de un objeto siempre
- El recolector de basura ejecutará el destructor de un objeto cuando éste se libere

````c#
class Clase{
	public Clase(){
		//Asignación de recursos
	}
	
	~Clase(){
		//Liberación de recursos
	}
}
````

---
## Objetos
- Se les accede a través de referencias
- La referencia `this` nos permite acceder al objeto implícito
- Los objetos se crean con el operador `new`

---
## Clases Parciales
- Una clase parcial se puede implementar en varios ficheros
- Hay que anteponer la palabra `partial`
![](img/partial%20class1.png)
![](img/partial%20class%202.png)

---
## Clases de utilidad
Una clase `static class` de C#:
- No permite definir atributos de instancia
- No permite definir propiedades de instancia
- No permite definir métodos de instancia
- No permite definir constructores de instancia

---
## Propiedades
- C# ofrece el concepto de propiedad para acceder al estado de los objetos como si de atributos se tratase, obteniendo los beneficios del **encapsulamiento**. Se oculta el estado interno del objeto, ofreciendo un acceso indirecto mediante las propiedades (**encapsulamiento**)
- Se puede cambiar la implementación de la propiedad sin modificar el acceso por parte del cliente
- Las propiedades pueden ser de lectura y /o escritura

Esto ayuda a la construcción de objetos, pues si una clase Persona posee un constructor sin parámetros y posee varias propiedades públicas de lectura y escritura como el nombre y el apellido, se puede construir un objeto Persona indicando los valores de sus propiedades (no necesariamente todas), en cualquier orden, evitando así la sobrecarga excesiva del constructor.
![](img/constructor%20alternatives.png)

---
## Strings
- El operador `+` concatena strings.
- Los objetos de tipo **string** son **inmutables**, no se puede modificar su estado.
- Si queremos modificar su estado, debe usarse la clase **StringBuilder**
- Los strings que comienzan por `@` permiten definir múltiples líneas
![](img/strings%201.png)
![](img/strings%202.png)

---
## Arrays
- Nos permite coleccionar referencias
- Son estructuras de datos con múltiples valores de un mismo tipo
- Un array es un objeto, porque para acceder a él necesitamos una referencia
````c#
int[] array1;
bool[] array2;
Angle[] array3;
````
- Un objeto array se crea con el operador `new`, indicando además el tamaño -> `new bool[2]`
- En el caso de los arrays de objetos, tenemos reservado espacio para referencias, no para objetos
![](img/arrays.png)
- E bucle **foreach** usa la sintaxis -> `foreach (int i in vector)`

---
## Structs 
- Pueden tener constructores, propiedades, métodos, campos, operadores y miembros de clase (static)
- No pueden heredar de otras clases o structs
- Derivan implícitamente de ValueType
- Pueden implementar interfaces
- No pueden tener destructores
- Por defecto, su nivel de ocultación es public
- Siempre se almacenan en la pila, por lo que no se modifican, ya que el parámetro pasado es una copia del argumento original
![](img/structs.png)

---
## Paso de parámetros
Hay tres tipos:
- **Por valor**: el parámetro formal es una copia del parámetro real (argumento). En el paso de objetos lo que se copia es la referencia (el objeto es el original).
- **Por referencia de entrada y salida**: el parámetro formal es un alias del parámetro real (argumento). Se pasa con un valor de entrada y se le puede pasar otro de salida, modificando el original. Se usa la palabra reservada `ref`.
- **Paso por referencia de salida**: el parámetro formal es un alias del parámetro real (argumento). Se pasa sin valor de entrada y sirve para devolver más de un valor. Se usa la palabra reservada `out`.
![](img/por%20valor.png)
![](img/por%20referencia.png)
![](img/por%20salida.png)
![](img/resultados%20parametros.png)

---
## Parámetros opcionales
- Valores por omisión a los parámetros que siempre han de ser los últimos (más a la derecha)
- Permite la invocación de una misma función con distinto número de argumentos
- Se puede cambiar el orden de los argumentos.
![](img/params%20opcionales%201.png)
![](img/params%20opcionales%202.png)

---
## Sobrecarga de operadores
- Emplea la palabra reservada `operator`
- Los operadores son siempre métodos de clase (`static`) -> no son polimórficos
- Permite sobrecargar la conversión explícita (cast) y la implícita
- Si sobrecargamos un operador `+` obtenemos automáticamente `+=`
![](img/sobrecarga%20operadores.png)

---
## Declaración implícita de variables
- Para las variables locales no se requiere especificar su tipo, en su lugar ponemos `var`
- Es útil cuando los tipos son muy largos, no es sencillo identificar el tipo (LINQ) o no existe un tipo explícito.

---
## Métodos extensores
Para crearlos hay que:
- Implementar un método de clase `static`
- En una clase de utilidad `static`
- El primer parámetro ha de ser del tipo que deseamos ampliar
- El primer parámetro ha de declararse anteponiendo la palabra `this`
````c#
static class StringExtension{
	static public uint CountWords (this string cad){
		...
	}
}
````
![](img/extensores.png)

---
## Herencia
- Mecanismo de reutilización de código
![](img/herencia.png)

---
## Invocación a constructores base
Se hace  con `base`:
````c#
public Circunference (int x, int y, int radius) : base(x,y){
	this.radius = radius;
}
````

---
## Polimorfismo
- Mecanismo de generalización que hace que la abstracción más general pueda representar abstracciones más específicas. El tipo general representa por tanto varias formas.
![](img/polimorfismo.png)

---
## Enlace dinámico
- Los métodos heredados se pueden especializar en las clases derivadas
- Si queremos que se llame al método real implementado por el objeto, debemos hacer uso del enlace dinámico (**dynamic binding**)
- Es un mecanismo por el que en tiempo de ejecución se invoca al método del tipo dinámico implementado por el objeto (no al estático declarado en su clase)
- Para que exista el enlace dinámico tenemos que:
	- Poner la palabra `virtual` al método que recibe el mensaje (referencia)
	- Sobreescribir su funcionalidad usando la palabra `override` en los métodos derivados
- Si no queremos que haya polimorfismo, pues es una coincidencia de nombres, ponemos la palabnra `new`
![](img/dynamic%20binding.png)
![](img/figure%201.png)
![](img/figure%202.png)

---
## Comparación de objetos
Podemos estar interesados en saber si:
- Dos objetos *son exactamente el mismo* -> Comparación por **identidad** -> usamos el operador `==`
- Dos objetos *representan la misma identidad* -> Comparación por **estado** -> redefinimos el método `Equals(Object o)`. Al redefinir el equals también será necesario redefinir el GetHashCode()

---
## Operadores is y as
- Cuando utilizamos colecciones polimórficas que hacen uso de Object, no siempre se puede hacer un **cast**, ya que no estamos seguros de que el objeto introducido sea del tipo que queremos. Para ello se introduce el operador **is**.
![](img/isas%201.png)
![](img/is%20as%202.png)
- Si después de usar el operador **is** vamos a realizar un cast, es mejor usar el operador **as**
![](./img/2%20CURSO/TPP/img/is%20as%203.png|500)
![](img/is%20as%204.png)

---
## Autoboxing
- Los tipos simples ¡no heredan de Object!
![](img/autoboxing%201.png)
![](img/autoboxing%202.png)

---
## Clases y Métodos Abstractos
- Cuando en una abstracción necesitamos que un mensaje forme parte de su interfaz, pero no podemos implementarlo, este mensaje se declara como método abstracto.
- Se usa la palabra `abstract`
- Este método no se implementa
- Todo método abstracto ofrece enlace dinámico (no hay que especificar que es virtual)
- En su redefinición hay que usar `override`
- Toda clase que posea al menos un método abstracto será una clase abstracta

---
## Interfaces
- **Interfaz**: Conjunto de métodos y/o propiedades públicos que ofrecen un conjunto de clases
- Son métodos comunes a las distintas abstracciones
![](./img/interfaces.png|300)
- No pueden tener miembros `static`
![](img/interfaces%202.png)
![](img/interfaces%203.png)
![](img/interfaces%204.png)
![](img/interfaces%205.png)
![](img/interfaces%206.png)
![](img/interfaces%207.png)

---
## IDisposable y using
- Es una interfaz del namespace System con un único método -> `void Dispose()`
- Se encarga de liberar los recursos adicionales gestionados por el objeto
- Toda clase que asigna recursos adicionales debe implementar esta interfaz
- Las clases que definan un destructor, probablemente implementarásn IDisposable
![](img/idisposable.png)
- Se usa la palabra reservada `using` para asegurar la liberación de los recursos adicionales de un objeto IDisposable
![](img/idisposable%202.png)
---
## Implementación explícita de interfaces
![](img/ieinterf.png)

---
## Composición vs herencia
- **Herencia**: un objeto o clase se basa en otro obnjeto o clase, usando la misma implementación o comportamiento
![](img/hervscomp.png)
- **Composición**: quiere decir que tenemos una instancia de una clase que contiene instancias de otras clases que implementan las funciones deseadas
![](img/composicion-esquema.png)
Comparativa:
![](img/comparativa.png)

---
## Excepciones
- Una **excepción** es un objeto que encapsula información acerca de un evento irregular ocurrido en tiempo de ejecución
- En C# solo se pueden lanzar excepciones del tipo `System.Exception`
![](img/excepciones.png)
- Se usa la palabra `throw`
- No es obligatorio manejar ninguna excepción
- Para manejarlas se usa `try` y `catch`. También podremos poner `finally` si queremos que se ejecute un código en concreto
![](img/excp1.png)
![](img/excp2.png)

---
## Asertos en C#
- **Aserto**: construcción del lenguaje para asegurar que una condición deba ser siempre cierta. Si no lo fuese, se pararía la ejecución. Están orientadas al proceso de desarrollo
- La técnica más usada está basada en **compilación condicional**
![](./img/2%20CURSO/TPP/img/asertos.png)
![](img/asertos2.png)

---
## Precondiciones
Pueden ser de dos tipos:
- El método no se puede ejecutar para determinados **valores de los parámetros** (factorial de u número negativo)
- El método no se puede ejecutar para un determinado estado del objeto implícito () ssacar un elemento de la pila vacía
-> Consultar [[Invariants, preconditions, postconditions 🦠]]

- **Invariantes**: siempre al principio de los métodos (excepto constructores). También han de mirarse al final de cada método
- **Precondiciones**: comprueba si el objeto está en un estado válido
- **Postcondidiones**: han de comprobarse después de ejecutar un método

---
## Genericidad
- Permite construir abstracciones modelo para otras abstracciones
- Ofrece una mayor robustez (detección de errores en tiempo de compilación) y un mayor rendimiento

---
## default(T)
- Un tipo genérico puede ser cualquier tipo del lenguaje, incluyendo los tipos simples
- En ocasiones queremos asignar o retornar el valor por omisión de un tipo T:
	- La asignación `variable = null` no sería válida, porque T también podría ser un Value Type (int , char)
- Para ello  se usa la palabra `default`
![](img/default.png)

---
## Genericidad acotada
- Permite hacer más específicos los tipos genéricos.
- Por ejemplo un método de ordenación donde se puedan ordenar objetos `IComparable<T>`
![](img/icomparable.png)

---
# `IEnumerable<T>`
- Interfaz que representa una colección de elementos genérica
- Deriva de IEnumerable
- Un objeto que implemente un **IEnumerable** se puede recorrer con un **foreach**
- Los arrays derivan de Array e implementan `IEnumerable<T>`
![](img/ienumerable.png)
- IEnumerable(T) sólo posee un método -> `GetEnumerator()`
- Este es un *factory method* (patrón de diseño) encargado de construír un iterador
- El IEnumerator es un *bridge* (patrón de diseño) para ser independiente de la implementación del iterador
- El iterador suele implementarse como una clase anidada de la colección
![](img/ienumerable2.png)
![](img/ienumerable%204.png)
![](img/ienumerable%203.png)
![](img/ienumerable%205.png)

---
## Tipos anulables
- En ocasiones se quiere representar que un tipo simple pueda no poseer valor null
- Estos tipos derivan del struct `Nullable<int>`
- También se usa el operador `??`

## System.Collections.Generic
![](img/colectionsgeneric.png)

---

Siguiente lección -> [[Paradigma Orientado a Objetos 🐤]]