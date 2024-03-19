*NOTA: Todo este contenido ha sido extraído de los apuntes proporcionados en la asignatura Tecnologías y Paradigmas de la Programación (TPP) de la Universidad de Oviedo, curso 2023-2024.*
# Primer Programa

```cs
using System;

namespace TPP.ObjectOrientation.Basic {
    /// <summary>
    /// First C# class
    /// </summary>
    class Hello {
        /// <summary>
        /// Main entry method
        /// </summary>
        public static void Main() {
            // * Shows "hello world" in the console
            System.Console.WriteLine("Hello world!");
        }
    }
}
```

# Ensamblados

- Un **assembly** es una colección lógica de recursos de una aplicación (archivos .exe, .dll, .ini, .jpg)
- Es un **componente**
- Cada proyecto en Visual Studio genera un ensamblado
- Los ensamblados poseen un conjunto de **módulos** (archivos .exe y .dll)

# Espacios de nombres

- Los **namespaces** son una agrupación lógica de tipos, al igual que en C++
	- Se pueden anidar
- Para incluir un namespace se usa la declaración `using` al principio antes de una clase o namespace
	- `using System;`
	- No es posible incluir un único tipo de un namespace

# Nivel de Ocultación de una Clase

- Una clase puede ser `public` o `internal`
	- Si es interna sólo se podrá acceder a ella desde dentro de su ensamblado (desde su proyecto)
	- Aquellas clases que se utilizan para implementar una funcionalidad, pero no forman parte de la fachada de un **assembly** deberían ser `internal`

# `C#` vs Java

![](Pasted%20image%2020240129124408.png)

![](Pasted%20image%2020240129124438.png)

- Los namespace se definen entre {}
```cs
namespace TPP.OrientacionObjetos.Basico {
…
}
```
- Para evitar poner siempre el nombre completo de un namespace cuando se haga uso de uno de sus tipos se emplea la palabra `using`
	- No se permite incluir un tipo suelto de un namespace
- Este mecanismo de control de acceso a tipos y miembros permite consiguir un **acoplamiento débil**

# Modularidad en `C#`

![](Pasted%20image%2020240129124736.png)

# Ocultación de la Información

- Niveles de ocultación de los miembros de una clase:
	- `public`: accesible (desde cualquier punto del programa)
	- `private`: inaccesible desde fuera de la clase
	- `protected`: accesible desde dentro de la clase y sus clases derivadas
	- `internal`: accesible desde cualquier clase del ensamblado
	- `protected internal`: accesible desde cualquier clase del ensamblado o sus derivadas (aunque no pertenezcan al ensamblado)
- El nivel de ocultación por omisión es `private`

# Punto de Entrada

- En un programa sólo puede haber un punto de entrada
- El punto de entrada deberá ser un método de clase (`static`) denominado `Main`
	- Puede retornar nada (`void`) o un `int`
	- Puede tener cualquier nivel de ocultación
	- Puede declararse:
		- Sin parámetros
		- O con un parámetro de tipo `String[]` (parámetros pasados por línea de comandos)

## Parámetros Línea de Comandos

- Configurar en: Proyecto >> Propiedades >> Depuración

# Tipos Simples

- Se ofrecen conversiones implícitas cuando no hay pérdida de información
- La conversión explícita se lleva a cabo mediante casts

![](Pasted%20image%2020240129130257.png)

# Constantes y Consola

- `C#` permite anteponer `const` a la declaración de variables y atributos, identificando así las variables cuyo valor no puede modificarse: `const double PI = 3.141592`
- Las constantes:
	- Las cadenas de caracteres se delimitan por `""`
	- Los carácteres se delimitan por `''`
- La consola se controla con la clase `System.Console`
- Los métodos `Write` y `WriteLine` permiten mostrar texto con formato `{índiceParámetro[,alineación][:formato]}`
- La salida está internacionalizada

```cs
using System;

namespace TPP.ObjectOrientation.Basic {
    
    class ConsoleDemo {
        static void Main(string[] args) {
            const double PI = 3.141592;
            const int integer = -34;
            Console.WriteLine("Number Formats:");
            Console.WriteLine(
                "(C) Currency: . . . . . . . . {0,20:C}\n" +
                "(D) Decimal:. . . . . . . . . {0,20:D}\n" +
                "(E) Scientific: . . . . . . . {1,20:E}\n" +
                "(F) Fixed point:. . . . . . . {1,20:F}\n" +
                "(G) General:. . . . . . . . . {0,20:G}\n" +
                "    (default):. . . . . . . . {0,20} (default = 'G')\n" +
                "(N) Number: . . . . . . . . . {0,20:N}\n" +
                "(P) Percent:. . . . . . . . . {1,20:P}\n" +
                "(R) Round-trip: . . . . . . . {1,20:R}\n" +
                "(X) Hexadecimal:. . . . . . . {0,20:X}\n",
                integer, PI);
        }
    }
}
```

# Enumeraciones

- Las enumeraciones son un conjunto finito de posibles valores
- Definen **un nuevo tipo** con su propio grado de ocultación
- Es posible asignarles explícitamente valores enteros:

```cs
enum Colores {
	azul, verde=3, rojo, amarillo
}
class Enumerados {
	static void Main(string[] args) {
		Colores color;
		color = Colores.azul;
		Console.WriteLine(color); // * azul
		color = (Colores)3;
		Console.WriteLine(color); // * verde
	}
}
```

# Operadores

- Resumen de los operadores de `C#`:
	- Aritméticos: `+` `-` `*` `/` `%`
	- Lógicos: `&&` `||` `!`
	- De comparación: `==` `!=` `>=` `<=` `>` `<`
	- Manipulación de bits: `&` `|` `^` `~` `>>` `<<`
	- Asignación: `=` `+=` `-=` `*=` `/=` `%=` `&=` `|=` `^=` `<<=` `>>=`
	- Incremento y Decremento: `++` `--` (prefijo y postfijo)
	- Operador ternario condicional: `?:`
- El operador `+` para cadenas implica concatenación
- El resto de operadores están en [Documentación Oficial](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/)

# If, While y DoWhile

![](Pasted%20image%2020240129132037.png)

# For

![](Pasted%20image%2020240129132101.png)

# Switch

![](Pasted%20image%2020240129132132.png)

# Clases 

- Una clase puede ser `internal` (por omisión) o `public`

# Constructores y destructores

- Un **constructor** define cómo se inicializa un objeto
	- Se llama de forma implícita justo **después de su construcción**
	- Por omisión existe un constructor sin parámetros
- Un **destructor** define la forma de liberar los recursos usados por un objeto
	- Se llama implícitamente **antes de su destrucción**
	- Se ha de llamar `~` seguido del nombre de la clase
	- No tiene valor de retorno
	- Se asegura su ejecución pero no de un modo determinista (no sabemos exactamente cuándo se ejecutará)
	- El recolector de basura ejecutará el destructor de un objeto cuando éste se libere

```cs
class Clase {
	public Clase(parámetros) {
		//asignación de recursos adicionales
	}
	~Clase() {
		//liberación de recursos adicionales
	}
}
```

# Objetos

- A los objetos se accede a través de referencias
- Dentro de un método de instancia (no `static`) la referencia `this` nos permite acceder al objeto implícito
- Los objetos se crean con el operador `new`
- A un objeto se le pueden pasar mensajes (miembros públicos) con el operador `.`

# Clases parciales

- En ocasiones, una clase ofrece un elevado número de miembros
	- Aunque todos tienen una cohesión, pueden estar a su vez clasificados
	- Puede ser interesante separarlos físicamente en distintos ficheros / directorios
- Para ello se crearon las clases parciales (`partial`)
	- Se puede implementar en varios ficheros
	- Es necesario anteponer la palabra reservada `partial`

# Static

- La identificación de miembros de la clase se realiza anteponiendo la palabra reservada `static`
- El acceso a éstos se hace mediante la utilización de la clase, seguida del operador `.` (`Marth.PI`)
	- No es posible usar un objeto como en Java
- `C#` ofrece el concepto de **constructor static**
	- Su código se ejecutará cuando se cargue la clase en memoria
- Para las clases de utilidad `C#` ofrece el concepto de `static class`

# Clases de utilidad

- Para las clases de utilidad `C#` ofrece el concepto de `static class`
- Una clase `static class` de `C#`:
	- No permite definir atributos de instancia
	- No permite definir propiedades de instancia
	- No permite definir métodos de instancia
	- No permite definir constructores de instancia

# Propiedades

- `C#` ofrece el concepto de **propiedad** para acceder al estado de los objetos como si de atributos se tratase, obteniendo los beneficios del encapsulamiento:
	- Se oculta el estado interno del objeto, ofreciendo un acceso indirecto mediante las propiedades (**encapsulamiento**)
- Se puede cambiar la implementación de la propiedad sin modificar el acceso por parte del cliente
- Las propiedades pueden ser de **lectura y/o escritura**
- Las propiedades en `C#` pueden:
	- Catalogarse con todos los niveles de ocultación
	- Ser de clase (`static`)
	- Ser abstractas
	- Sobreescribirse (enlace dinámico)

```cs
/// <summary>
    /// Properties demo
    /// </summary>
    public class Circumference {
        /// <summary>
        /// Private fields
        /// </summary>
        private int x;

        /// <summary>
        /// X readonly property
        /// </summary>
        public int X {
            get { return x; }
        }

        /// <summary>
        /// Radius read/write property
        /// With the following syntax, you do not need to define the corresponding private field
        /// </summary>
        public uint Radius  { get; set; }
        
        
        /// <summary>
        /// A new syntax to define a readonly property.
        /// The setter is declared private.
        /// No field is required.
        /// </summary>
        public int Y { get; private set; }
	}
```

```cs
class Persona {
	string Nombre { get; set; }
	string Apellido { get; set; }
	int Edad { get; set; }
	string DNI { get; set; }
	static void Main() {
		Persona maria = new Persona {
			FirstName = “Maria",
			Surname = “Herrero",
			Age = 43,
			IDNumber = "23746887-F"
		};
		Persona juan = new Persona {
				Surname = “Nadie", Age = 10, FirstName = “Juan" 
		};
} }
```

# Strings

- El tipo `string` forma parte del lenguaje `C#`
- Es un alias de la clase `System.String`
- Por tanto:
	- `string` y `String` son clases
	- sus instancias son objetos
	- las variables de este tipo, son referencias
- El operador `+` concatena strings
- Los objetos de tipo `string` son inmutables: no se puede cambiar o modificar su estado
- Si queremos modificar su estado, debe usarse la clase `StringBuilder`

```cs
using System;
using System.Text;

namespace TPP.ObjectOrientation.Encapsulation {

    /// <summary>
    /// String and StringBuilder demo
    /// </summary>
    class Program {

        static void Main(string[] args) {
            // * string
            string s1 = "hello";
            // * String
            System.String s2 = " world";
            // * s3 is a new string, concatenation of s1 and s2
            String s3 = s1 + s2;
            // * s1 and s2 are not modified (strings are immutable)
            Console.WriteLine("{0}\n{1}\n{2}\n", s1, s2, s3);

            // * Some methods and properties of String
            Console.WriteLine("Length: {0}", s3.Length);
            Console.WriteLine("Lowercase: {0}", s3.ToLower());
            Console.WriteLine("Substring from 2nd to 4th character: {0}", s3.Substring(2, 2));
            Console.WriteLine("Is is empty or null?: {0}", String.IsNullOrEmpty(s3));
            string s4 = String.Format("S1: \"{0}\" + S2: \"{1}\" = S3: \"{2}\"\n", s1, s2, s3);
            Console.WriteLine(s4);

            // * Strings starting with @ permit to define multiple line strings
            string paragraph = @"
        The W3C mission is to lead the World Wide Web to its 
        full potential by developing protocols and guidelines 
        that ensure the long-term growth of the Web. 
        Below we discuss important aspects of this mission, 
        all of which further W3C's vision of One Web.
        ";
            Console.WriteLine(paragraph);

            // * Mutable strings: StringBuilder
            StringBuilder sb = new StringBuilder();
            sb.Append(s1);
            sb.AppendFormat(" plus s2: {0}", s2);
            sb.AppendLine(s3);
            Console.WriteLine(sb);
        }
    }


}
```

# Arrays

- Los **arrays** son estructuras de datos con múltiples valores de un mismo tipo
- Un array es un objeto
- Para acceder a éste necesitamos una referencia
- Una referencia de un array se declara así:
	- `int[] arrayEnteros`
	- `bool[] arrayLogicos`
	- `Angulo[] arrayObjetoAngulo`
- Un array se crea con el operador `new`, indicando además el tamaño del array:
	- `arrayEnteros=new int[10];`
	- `vectorValoresLógicos=new bool[2];`
	- `vectorObjetosAngulo=new Angulo[91];`
- Los arrays se indexan desde 0 hasta longitud -1
- En el caso de los arrays de objetos, tenemos reservado espacio para referencias, no para los objetos:
```cs
for (int i=0;i<91;i++)
	vectorObjetosAngulo[i]=new Angulo(i);
```
- `C#` posee una sintaxis para crear arrays con una inicialización previa:
	- Los distintos valores de los elementos del array se enumeran dentro de `{}`, separados por comas:

```cs
char[] digitos = {'0', '1', '2', '3', '5', '6', '7', '8', '9'};
int[] enteros = { 2, 3, 234, -234, 43 };
bool[] lógica = { true, false };
Angulo[] angulos = { new Angulo(0), new Angulo(90), new Angulo(180) };
Angulo[] angulos2;
angulos2 = new Angulo[] { new Angulo(0), new Angulo(90), new Angulo(180) };
```

- Los arrays poseen una propiedad `Length` que devuelve el número de elementos de un array (bucle for y foreach)

```cs
for (int i = 0; i < vectorObjetosAngulo.Length; i++)
	Console.WriteLine(vectorObjetosAngulo[i]);

foreach (Angulo angulo in vectorObjetosAngulo)
	Console.WriteLine(angulo);
```

## Arrays Multidimensionales

- Existen dos alternativas para crear arrays de varias dimensiones:
	- **Arrays lineales**: memoria contigua lineal, de varias dimensiones
		- Más eficientes, menos versátiles
		- `Length` es el producto de los tamaños
		- El tamaño de cada dimensión se puede obtener con `GetLength`
	```cs
	string[,] vector=new string[3,4];
	for (int i = 0; i < vector.GetLength(0); i++)
		for (int j = 0; j < vector.GetLength(1); j++)
			vector[i,j]="("+(i+1)+","+(j+1)+")";
	```
	
	- Arrays de Arrays: permite la construcción de arrays irregulares

	```cs
	int[][] triangular=new int[10][];
	for (int i=0;i<triangular.Length;i++)
		triangular[i] = new int[triangular.Length-i];
	```

# Structs

- En `C#` un conjunto de campos públicos se puede representar como un Struct
	- Pueden tener constructores, propiedades, métodos, campos, operadores y miembros de clase (static)
	- Los structs no pueden heredar de otras clases o structs
		- Implícitamente derivan de `ValueType`
		- Sí pueden implementar interfaces
	- No pueden tener destructores
	- La ocultación de sus miembros es, por omisión, `public`
	- Aunque se creen con `new`, *¡siempre se almacenan en la pila!*
	- Se crearon para ser usados en la transferencia de datos y no sobrecargar el recolector de basura

```cs
using System;

namespace TPP.ObjectOrientation.Encapsulation {

    /// <summary>
    /// An example point struct
    /// </summary>
    struct PointStruct {

        public int X { get; set; }
        public int Y { get; set; }

        public override string ToString() {
            return String.Format("Point struct in ({0},{1}).", this.X, this.Y);
        }

    }

}
```

# Paso de Parámetros

- `C#` posee 3 tipos de paso de parámetros:
	- **Paso por valor**
		- El parámetro formal es una copia del parámetro real (argumento)
		- En el paso de objetos, lo que se copia es la referencia -> *¡El objeto es el original!*
		- *NOTA: no se modifica el valor*
	- **Paso por referencia de entrada y salida**:
		- El parámetro formal es un alias del parámetro real (argumento)
		- Se pasa con un valor (entrada) y se le puede asignar otro (salida), modificando el original
		- Se utiliza la palabra reservada `ref` tanto en el parámetro como en el argumento
		- *NOTA: se modifica el valor*
	- **Paso por referencia de salida**:
		- El parámetro formal es un alias del parámetro real (argumento)
		- Se pasa sin valor (entrada) y sirve para devolver más de un valor
		- Se usa la palabra reservada `out` tanto en el parámetro como en el argumento

```cs
static void Main() {
            int theBase = 2, theExponent = 3;
            Console.WriteLine("By value. Base: {0}, exponent: {1}, power: {2}.",
                theBase, theExponent, Power(theBase, theExponent));
            Console.WriteLine("After the invocation. Base: {0}, exponent: {1}.", theBase, theExponent);

            Console.WriteLine("By reference. Base: {0}, exponente: {1}, power: {2}.",
                theBase, theExponent, PowerRef(ref theBase, ref theExponent));
            Console.WriteLine("After the invocation. Base: {0}, exponente: {1}.", theBase, theExponent);

            string firstName, surname, idNumber;
            LeeDatos(out firstName, out surname, out idNumber);
            Console.WriteLine("First name: {0}, surname: {1}, id number: {2}.", firstName, surname, idNumber);
        }
```

Salida:
```shell
By value. Base: 2, exponent: 3, power: 8.
After the invocation. Base: 2, exponent: 3.
By reference. Base: 2, exponente: 3, power: 8.
After the invocation. Base: 0, exponente: 0.
First name: Edu
Surname: Blanco
Id number: 1234254
First name: Edu, surname: Blanco, id number: 1234254.
```

# Parámetros Opcionales

- Es posible asignar valores por omisión a los parámetros
	- **SIEMPRE tienen que ser los últimos** (más a la derecha)

```cs
public Persona[] GetPagina(int pagina = 1,
int elementosPorPagina = 10, bool soloMayoresEdad = true) {
…
}
```

- Permite:
	- Invocaciones a una función con distinto número de argumentos
	- Evitar el abuso de la sobrecarga
	- No es necesario pasar todos los parámetros con valor por omisión anteriores (se permite "saltar parámetros por omisión")
	- Puede usarse para mejorar la documentación del código, nombrando los parámetros en la invocación

# Sobrecarga de métodos

- Permite dar distintas implementaciones a un mismo identificador de método
- En `C#` para sobrecargar un método es necesario modificar:
	- O número de parámetros
	- O el tipo de alguno de sus parámetros
	- O el paso de alguno de sus parámetros (valor, `ref` o `out`)

# Sobrecarga de operadores

- Emplea la palabra reservada `operator`
- Los operadores son siempre métodos de clase (`static`) -> *No son polimórficos*
- Sobrecargando un operador (`+`), obtenemos automáticamente, si ha lugar, su asignación (`+=`)
- Sobrecargando `++` o `--` prefijo, obtenemos automáticamente su versión postfija
- Permite sobrecargar la **conversión explícita** (cast) y la **implícita** de tipos del lenguaje
- Puesto que la invocación a un método no es un lvalue, implementa el operador `[]` con un tipo de propiedad `ad hoc` -> *los **indexers*** 
	- *WTF esto es de DLP (asignatura de 3)*

# Declaración implícita de variables

- No se requiere especificar su tipo siempre que se asigne un valor en la declaración:

```cs
var vector = new[] { 0, 1, 2 }; // vector es int[]
foreach(var item in vector){ // item es int
	...
}
```

- Esto es útil cuando:
	- Los tipos poseen nombres largos (debido a la genericidad)
	- No es sencillo identificar el tipo de la expresión (LINQ)
	- No existe un tipo explícito (los tipos anónimos)

# Métodos extensores

- Posibilidad de añadir métodos a clases de las que no poseemos el código (String, Int32, IEnumerable...)
- Para ello:
	- Hay que implementar un método de clase (`static`)
	- En una clase de utilidad (`static`)
	- Su primer parámetro no tiene que ser del tipo que deseamos ampliar
	- El primer parámetro tiene que declararse anteponiendo la palabra reservada `this`

```cs
static class ExtensoraString {
	static public uint ContarPalabras(this string cadena) {
		...
	}
```

- Se creó para implementar LINQ, añadiendo métodos a `IEnumerable` e `IQueryable`

# Unit Testing, Refactoring & TDD

- [Unit Testing](http://en.wikipedia.org/wiki/Unit_testing)
- [refactoring](http://en.wikipedia.org/wiki/Code_refactoring)
- [TDD](http://www.agiledata.org/essays/tdd.html)
- [tutorial](https://docs.microsoft.com/en-us/previous-versions/gg454256(v=msdn.10)?redirectedfrom=MSDN)

# Herencia

- Es un mecanismo de **reutilización de código**
- El **estado** de una instancia derivada está definido por la unión (herencia) de las estructuras de las clases base y derivada
- El conjunto de mensajes (**interfaz**) que puede aceptar un objeto derivado es la unión (herencia) de los mensajes de su clase base y derivada

![](Pasted%20image%2020240129172701.png)

## Sintaxis

![](Pasted%20image%2020240129172815.png)

## Invocación a Constructores Base

- En `C#` se hace con `base` (en Java es con `super`)

```cs
public Circunferencia(int x, int y, int radio):base(x,y) {
	this.radio=radio;
}
```

# Polimorfismo

- Mecanismo de **generalización**, que hace que la abstracción más general pueda representar abstracciones más específicas
	- El tipo general representa, por tanto, varias formas
- Por ello, la conversión ascendente en la jerarquía es automática
	- **Las referencias derivadas promocionan a referencias base** (subtipado)

![](Pasted%20image%2020240129173148.png)

![](Pasted%20image%2020240129173215.png)

- Para conocer el tipado dinámico se ofrecen los operadores `is` y `as`

# Enlace Dinámico

- Los métodos heredados se pueden especializar en las clases derivadas
- Si queremos hacer que se llame al método real implementado por el objeto, debemos hacer uso del **enlace dinámico** (*dynamic binding*)
	- Mecanismo por el cual, en tiempo de ejecución, se invoca al método del tipo dinámico implementado por el objeto (no al estático declarado en su clase)
- `C#` no tiene enlace dinámico por defecto
	- Para que exista enlace dinámico en `C#` tenemos que:
		- Poner la palabra reservada `virtual` al método que reciba el mensaje (referencia)
		- Redefinir su funcionalidad usando la palabra reservada `override` en los métodos derivados

![](Pasted%20image%2020240129173942.png)

# Comparación de objetos

- Dos objetos son exactamente el mismo -> comparación por **identidad**
	- Usar el operador `==`
- Dos objetos representan la misma entidad -> comparación por **estado**
	- Redefinición (override) del método: `bool Object::Equals(Object o)`

# GetHashCode

- Al usar el Equals, se ha de implementar `int Object::GetHashCode()`
- Deberá implementarse siguiendo los siguientes criterios:
	- Es necesario que dos objetos iguales (`Equals`) devuelvan el mismo código hash
	- Dos objetos que devuelvan un mismo código hash no necesariamente serán iguales (`Equals`)
	- Debe retornar un entero de forma rápida

# Operadores `is` `as` 

- `Object` es más general que `String`
- En ocasiones queremos llamar a un mensaje específico de la clase hija y no es posible
- Esto es común cuando utilizamos colecciones polimórficas que hacen uso de `Object`

```cs
ArrayList lista = new ArrayList();
lista.Add(new Persona("Pepe", "Pérez", "Martínez", 57));
// * Error de compilación
Persona pepe = lista[0];
```

- El problema de hacer un cast es que podría lanzar un `InvalidCastException`
	- No estamos seguros de que el objeto introducido sea una Persona (podría ser un String)
- Para evitarlo se introduce el operador `is`

```cs
if (lista[0] is Persona)
	((Persona)lista[0]).CumplirAños();
```

- Si después de usar el operador `is` vamos a realizar un cast, es mejor usar `as`
	- Se obtiene el tipo del objeto con un mejor rendimiento dinámico

```cs
Persona persona = lista[0] as Persona;
if (persona != null)
	persona.CumplirAños();
```

# Autoboxing

- Los tipos simples (int, char, float, double...) ¡no heredan de `Object`!
- Se ha añadido una conversión implícita de los tipos simples a `ValueTypes` (derivados de `Object`)
- Ejemplo: `int` promociona a `Int32` y un `Int32` se convierte automáticamente en un `int`

```cs
private static int Autoboxing(Int32 objeto) {
return objeto;
}
static void Main(string[] args) {
	// * Boxing
	int i=3; Int32 oi=i; Object o=i;
	Console.WriteLine(o);
	// * Unboxing
	i=oi; i=(int)o; Console.WriteLine(i);
	// * Autoboxing mediante paso de parámetros
	Console.WriteLine( Autoboxing(i) );
}
```

# Clases y Métodos Abstractos

- En `C#` se emplea la palabra reservada `abstract`
- Todo método abstracto ofrece enlace dinámico
	- No hay que especificar que es `virtual`
- Toda clase que posea un método o más abtracto, será una **clase abstracta**

# Interfaces

## Sintaxis

```cs
[public|internal] interface Nombre[:interfaces-base]{
	...
}
```

- Es común iniciar los identificadores de las interfaces con la letra `I`
- Todos los mensajes son públicos, virtuales y abstractos (no se pone `public` ni `virtual` ni `abstract`)
- Una interfaz puede heredar de cualquier número de interfaces
- No pueden tener miembros `static`

# IDisposable

- Del namespace `System`
- Libera los recursos adicionales gestionados por el objeto
- Método `void Dispose()`

## IDisposable y Destructores

- Una clase que defina un destructor, comúnmente implementará IDisposable

```cs
classFichero: IDisposable{
	privatestringnombreFichero;
	privateboolestaAbierto;
	publicFichero(stringnombreFichero) {
		this.nombreFichero= nombreFichero;
		this.estaAbierto= true;
		Console.WriteLine("Abriendo el fichero {0}.", nombreFichero);
	}
	publicvoidDispose() {
		if(this.estaAbierto) {
			this.estaAbierto= false;
			Console.WriteLine("Cerrando el fichero {0}.", nombreFichero);
		}
	}
	~Fichero() { this.Dispose(); }
	...
```

## IDisposable y using

- El invocar explícitamente a un método para liberar recursos es susceptible de ser olvidado
- Puede ser muy tedioso debido al uso de **excepciones**
- Por ello, `C#` usa la palabra reservada `using` para asegurar la liberación de los recursos adicionales de un objeto `IDisposable`
	- Incluso si se lanza una excepción y no se maneja

```cs
using(Ficherofichero= newFichero("entrada.txt")) {
	stringlínea = fichero.LeerLínea();
	// Lanza una excepción DivideByZeroException
	fichero.EscribirLínea(línea + línea.Length/"".Length);
} // Se cierra el fichero
```

## Ejemplo completo

```cs
static void Main() {
    string line;

    using (File file1 = new File("input1.txt")) { // Shows "opening input1.txt"
        line = file1.ReadLine();   // Shows "reading line"
        file1.WriteLine(line);  // Shows "writing line"
    } // * Shows "closing file"
    Console.WriteLine();

    File file2 = new File("input2.txt"); // Shows "opening input2.txt"
    line = file2.ReadLine();      // Shows "reading line"
    file2.WriteLine(line);     // Shows "writing line"
    // If the application does not end abnormally (exception or assert),
    // it will eventually show "closing input2.txt", but we don't know when

    // If we want explicitly close the file, we can call Dispose
    file2.Dispose();
    Console.WriteLine();

    using (File file3 = new File("input3.txt")) { // Shows "opening input3.txt"
        line = file3.ReadLine(); // Shows "reading line"
        file3.WriteLine(line + line.Length/"".Length);  // Throws a DiviceByZero exception
    } // * Shows "closing input3.txt" (aún incluso se haya lanzado la excepción)

    Console.WriteLine("This is not shown in the console."); // Because an exception was thrown
}
```

# Implementación explícita de interfaces

![](Pasted%20image%2020240214230353.png)

# Composición vs Herencia

- [Leer el siguiente artículo de artima.com](https://www.artima.com/articles/composition-versus-inheritance)

# Excepciones

- En `C#` sólo se pueden lanzar excepciones del tipo `System.Exception`
	- No se pueden lanzar excepciones *Value Types* (objetos en pila)
- La clase `System.ApplicationException` supone un medio para crear excepciones definidas por aplicaciones
	- No deben representar un error grave
- La clase `System.SystemException` proporciona un medio para separar las excepciones del sistema de las excepciones definidas por aplicaciones

## Lanzando excepciones en `C#`

- Se usa la palabra reservada `throw`
	- Tiene que ir seguida de un objeto del tipo `Exception`
- En `C#` no es obligatorio manejar ninguna excepción

## Capturando excepciones

- Utilizar `try` y `catch`
- Si queremos que, en cualquier caso, se ejecute un código, éste podrá ubicarse en un bloque `finally`

```cs
class ExceptionsDemo {

    /// <summary>
    /// A method that can throw 3 different exceptions
    /// </summary>
    /// <param name="n">A parameter used to select the exception to be thrown</param>
    static void ThrowException(int n) {
        switch (n) {
            case 1:
                int a = 0;
                Console.WriteLine(n / a); // * DivideByZeroException 
                break;
            case 2:
                String s=null;
                s.Clone(); // *  NullReferenceException
                break;
            default:
                throw new ApplicationException("Another exception");
        }
    }


    static void Main(string[] args) {
        // * Here, the IndexOutOfRange exception could be thrown
        // * if no parameters have been passed to the Main method
        int option = Int32.Parse(args[0]);

        // * We execute code that can throw exceptions
        try {
            ThrowException(option);
        } catch (NullReferenceException e) {
            Console.Error.WriteLine(e.Message);
            // * The finally block is executed
        } catch (Exception e) {
            // * The two other exceptions are handled here, due to polymorphism.
            Console.Error.WriteLine(e.Message+"\n"+e.Source+"\n"+e.StackTrace);
            // * The finally block is executed
        } finally {
            Console.WriteLine("This setence is always executed.");
        }
        Console.WriteLine("The application has handled its exceptions and it keeps running.");
    }
}
```

## Manejando cualquier excepción

- Poner un `catch` sin parámetros
- También se puede poner un `throw` sin parámetros

```cs
public static void m(strings) {
	switch(s) {
	case"1": throw new Exception(s);
	case"2": throw new ApplicationException(s);
	case"3": throw new SystemException(s);
	} 
}
public static void Main(string[] args) {
try{m(args[0]); }
catch{
	Console.Error.WriteLine("La manejamos y la volvemos a lanzar.");
throw; }}
```

## Excepciones no manejadas

- Su salida es el tipo de excepción + su propiedad `Message` + su propiedad `StackTrace`

# Gestión de recursos en `C#`

![](Pasted%20image%2020240214232345.png)

![](Pasted%20image%2020240214232405.png)

![](Pasted%20image%2020240214232422.png)

- Los destructores en `C#` son invocados cuando se liberan los objetos por el recolector de basura
- Es posible que los destructores de `C#` sean válidos para liberar determinados recursos
	- Sin embargo en ocasiones es necesario una liberación determinista: especificar el momento exacto en el que queremos liberar el recurso
		- Por ejemplo, si ese recurso se va a usar en una rutina posterior

# Asertos en `C#`

- **Aserto** (aserción): construcción del lenguaje de programación para asegurar que una condición deba ser siempre cierta
	- Si ésta fuese falsa, se trataría de un error de programación (parando la ejecución
	- Están orientados al proceso de desarrollo
	- Se pueden desactivar para la entrega (Release)
- La técnica más usada para implementar asertos está basada en **compilación condicional**

![](Pasted%20image%2020240214232850.png)

# Precondiciones en `C#`

- Pueden ser de dos tipos:
	1. El método invocado **no se puede ejecutar para determinados valores de los parámetros** (ej: factorial de un número negativo)
	2. El método invocado **no se puede ejecutar para un determinado estado del objeto implícito** (ej: sacar un elemento de una pila vacía)
- Para ambos casos, existen las siguientes excepciones dentro del namespace `System`
	- `ArgumentException` para los argumentos
	- `InvalidOperationException` para los estados de los objetos

## Programación por contrato. Pre/Postcondiciones e invariantes

```cs
public void AddUser(string userName, string plainPassword, UserData data) //no throws clause!!{
	//INVARIANT : Always at the beginning of a method (except constructors). Is object consistent?
	Invariant();
	int previousUserCount = GetUserCount();
	//PRECONDITIONS are not always wrong parameters: object can be in an invalid state. InvalidOperationException is used
	if (UserFileIsLocked())
		throw new InvalidOperationException("The file is temporally inaccessible");
	//If arguments have an incorrect value, ArgumentException is used.
	if (!ValidUserName(userName))
		throw new ArgumentException("User name is invalid: please use a non-existing, non-null user name");
	if (plainPassword.Length < 10)
		throw new ArgumentException("The password size must be at least 10");
	if (!PasswordWithEnoughComplexity(plainPassword))
		throw new ArgumentException("Password must have at least one upper and lowercase char, number and symbol");
	if (data == null)
		throw new ArgumentException(("Extra user data cannot be null");
	...
	//TIP: We can create our own exceptions (inheriting from the Exception class) for this, but normally
	//ArgumentException and InvalidOperationException are enough for most cases
	//Do the work: add user name and data, encrypting the password
	_AddUser(userName, plainPassword, data);
	//POSTCONDITION of this method (invariants are object-scoped, postconditions are method-scoped)
	Debug.Assert(GetUserCount() == previousUserCount + 1);
	//INVARIANT check: Also, always end of a method (leave object consistent)
	Invariant();
}
private void Invariant(){
	//User file cannot get corrupt during the whole execution
	Debug.Assert(CheckUserFileIntegrity());
}
```

# Genericidad

- Propiedad que permite construiir abstracciones modelo para otras abstracciones
- Beneficios:
	- Mayor **robustez** (detección de errores en tiempo de compilación)
	- Mayor **rendimiento**

## `default(T)`

- En `C#`, un tipo genérico puede ser cualquier tipo del lenguaje, incluyendo los tipos simples
- En ocasiones queremos asignar o retornar el valor por omisión de un tipo `T`
	- La asignación `variable = null` no sería válida, porque `T` también podría ser un *Value Type* (**int**, **char**...)
		- *Literalmente DLP* :^ wtf
- Para ello se utiliza la palabra reservada `default`
- La expresión `default(T)` devuelve
	- `null` si `T` es de tipo objeto
	- `0`, `'\0'` o `false`, si `T` es de tipo simple

## Métodos Genéricos

- Un ejemplo de código:

```cs
class Generics {

    /// <summary>
    /// Generic method that returns a reference with the appropriate type
    /// or null if the cast is not valid
    /// </summary>
    /// <typeparam name="T">The type we want to cast the parameter</typeparam>
    /// <param name="reference">The expression to be cast</param>
    /// <returns>The expression with the new type, or null if the cast was not valid</returns>
    public static T ConvertReference<T>(Object reference) {
        if (!(reference is T))
            return default(T); // default value of T type (e.g., 0 for int, double, short...; null for references; false for bool...)
        return (T)reference;
    }

    public static void Main() {
        Object myString = "hello", myInteger = 3;
        // Correct conversions
        Console.WriteLine(ConvertReference<String>(myString));
        Console.WriteLine(ConvertReference<int>(myInteger));
        // Wrong conversions
        Console.WriteLine(ConvertReference<int>(myString));
        Console.WriteLine(ConvertReference<String>(myInteger));
    }
}
```

## Clases Genéricas

- Un ejemplo de código:

```cs
/// <summary>
/// Generic wrapper class
/// </summary>
/// <typeparam name="T">The type of the object to be wrapped</typeparam>
class GenericClass<T> {
	private T field;

	public GenericClass(T field) {
		this.field = field;
	}

	public T get() {
		return field;
	}

	public void set(T field) {
		this.field = field;
	}

}

class Run {
	public static void Main() {
		GenericClass<int> myInteger = new GenericClass<int>(3);
		Console.WriteLine(myInteger.get());
		GenericClass<string> myString = new GenericClass<string>("hello");
		Console.WriteLine(myString.get());
	}
}
```

# Genericidad Acotada

- Realmente los elementos genéricos son `Objects`
- La **genericidad acotada** (*bounded*) permite hacer más específico estos tipos
	- Ejemplo: *se puede hacer un método de ordenación donde se puedan ordenar objetos `IComparable<T>`*

![](Pasted%20image%2020240221101732.png)

- *NOTA*: La **genericidad acotada** se indica con el `where T: IComparable<T>`

```cs
public static class Algorithms {
	// La genericidad acotada se indica con el "where T: IComparable<T>"
    static public void Sort<T>(T[] vector) where T: IComparable<T> {
        for (int i=0; i<vector.Length; i++)
            for (int j = vector.Length-1; j > i; j--)
                if (vector[i].CompareTo(vector[j]) >0) {
                    T aux = vector[i];
                    vector[i] = vector[j];
                    vector[j] = aux;
                }
    }

}

 class Program {

     static void Main() {
         // Creates a vector
         const uint NUMBER_ELEMENTS = 50;
         int[] vector = new int[NUMBER_ELEMENTS];

         // Random values are assigned
         Random random = new Random();
         for (int i = 0; i < vector.Length; i++)
             vector[i] = random.Next(Int32.MinValue, Int32.MaxValue);

         // We sort it (Int32 implements Comparable<Int32>)
         Algorithms.Sort(vector);

         // We check that the vector is sorted
         for (int i = 0; i < vector.Length - 1; i++)
             Debug.Assert(vector[i] <= vector[i + 1]);
     }

 }
```

# `IEnumerable<T>`

- Esta interfaz representa una colección de elementos (genérica)
	- No tiene por qué ser un contenedor (ejemplo: *la generación de la serie Fibonacci*)
- Deriva del interfaz polimórfico (no genérico) `IEnumerable`
- Un objeto que implemente `IEnumerable` se puede recorrer con un `foreach`
- Los arrays derivan de `Array` e implementan `IEnumerable<T>`

```cs
int[] arrayEnteros = new int[] { 10, 99, 50 }; 
Array a = arrayEnteros; 
IEnumerable enumerable = arrayEnteros; 
IEnumerable enumerablei = arrayEnteros;
```

- La interfaz `IEnumerable<T>` sólo posee un método `GetEnumerator` (también `IEnumerable`)
- El método `GetEnumerator` es un *factory method* (patrón de diseño) encargado de construir un iterador
	- El `IEnumerator` es un *bridge* (patrón de diseño) para ser independiente de la implementación del iterador
	- El iterador suele implementarse como una clase anidada de la colección

![](Pasted%20image%2020240221102502.png)

- Ejemplo de código:

```cs
class Fibonacci: IEnumerable<int> {

    /// <summary>
    /// Number of elements in the sequence
    /// </summary>
    private int numberOfElements;

    public Fibonacci(int numberOfElements) {
        this.numberOfElements = numberOfElements;
    }

    /// <summary>
    /// Explicit implementation of the generic interface.
    /// Notice that IEnumerable<int>.GetEnumerator is used instead of IEnumerable.GetEnumerator,
    /// because there are two versions of GetEnumerator (the one in IEnumerable<T> and the one in IEnumerable)
    /// </summary>
    IEnumerator<int> IEnumerable<int>.GetEnumerator() {
        return new FibonacciEnumerator(numberOfElements);
    }

    /// <summary>
    /// Explicit implementation of the polymorphic interface.
    /// Notice that IEnumerable.GetEnumerator is used instead of IEnumerable<T>.GetEnumerator,
    /// because there are two versions of GetEnumerator (the one in IEnumerable<T> and the one in IEnumerable)
    /// </summary>
    IEnumerator IEnumerable.GetEnumerator() {
        return new FibonacciEnumerator(numberOfElements);
    }

} //  Fibonacci class

internal class FibonacciEnumerator : IEnumerator<int> {
    /// <summary>
    /// Index is the position of the term in the sequence.
    /// FirstTerm and secondTerm store the two last terms.
    /// SecondTerm is the current term.
    /// </summary>
    int index, firstTerm, secondTerm;

    /// <summary>
    /// Maximum number of elements in this enumerator (iterator).
    /// </summary>
    int elements;

    public FibonacciEnumerator(int elements) {
        this.elements = elements;
        Reset();
    }

    /// <summary>
    /// The current term (generic version)
    /// </summary>
    int IEnumerator<int>.Current {
        get { return secondTerm; }
    }

    /// <summary>
    /// The current term (polymorphic method)
    /// </summary>
    object IEnumerator.Current {
        get { return secondTerm; }
    }

    /// <summary>
    /// Increments the enumerator (iterator) going to the following term
    /// </summary>
    /// <returns>True if the increment was successful; false if the end was reached</returns>
    public bool MoveNext() {
        if (index >= this.elements)
            return false;
        if (++index > 2) {
            int temp = secondTerm;
            secondTerm += firstTerm;
            firstTerm = temp;
        }
        return true;
    }

    /// <summary>
    /// Resets the enumerator (iterator), setting it to the begining of the sequence
    /// </summary>
    public void Reset() {
        index = 0;
        firstTerm = secondTerm = 1;
    }

    /// <summary>
    /// This method is called when the object is destroyed.
    /// It is used to free its resources (nothing in this case).
    /// It must be implemented, though, because it is part of the IEnumerator.
    /// </summary>
    public void Dispose() {
    }

} // FibonacciEnumerator

class Program {

    static public void ShowWithForEach<T>(IEnumerable<T> enumerable,TextWriter output) {
        output.Write("[ ");
        foreach (T item in enumerable)
            output.Write("{0} ",item);
        output.WriteLine("]");
    }

    static public void ShowWithEnumerator<T>(IEnumerable<T> enumerable, TextWriter output) {
        IEnumerator<T> iterador = enumerable.GetEnumerator();
        output.Write("[ ");
        while (iterador.MoveNext())
            output.Write("{0} ", iterador.Current);
        output.WriteLine("]");
    }

    static public void Main() {
        string[] array = { "How", "are", "you", "doing", "?" };
        ShowWithForEach(array, Console.Out);
        ShowWithEnumerator(array, Console.Out);

        Fibonacci fibonacci = new Fibonacci(10);
        ShowWithForEach(fibonacci, Console.Out);
        ShowWithEnumerator(fibonacci, Console.Out);
    }
}
```

# Tipos anulables

- En ocasiones, se quiere representar que un tipo simple pueda no poseer valor (**null**)
- El mejor ejemplo es una base de datos con un campo de tipo simple anulable
- En `C#` estos tipos se representan añadiendo el sufijo `?` al tipo simple: `int?`. `double?`, `bool?`...
- Estos tipos derivan del struct `Nullable<T>`
- Sus principales miembros son las propiedades:
	- `HasValue:bool` (sólo lectura), nos indica si el valor no es nulo
	- `Value:T` (lectura y escritura) en el caso de que no sea nulo nos devuelve su valor, sino `default(T)`
- También se ha añadido el operador `??`

- Ejemplo de código:

```cs
 public class Person {
     public string FirstName { get; set; }
     public string Surname { get; set; }

     /// <summary>
     /// Age of the person.
     /// Let's suppose it is taken from a database, and that it can be nullable (in the DB).
     /// </summary>
     public int? Age { get; set; }

     public string IDNumber { get; set; }

     public override string ToString() {
         if (this.Age.HasValue)
             // * We show the age because it is defined
             return string.Format("{0} {1}, {2} years old and IDNumber {3}.",
                 this.FirstName, this.Surname, this.Age.Value, this.IDNumber);
         else
             // * No age is defined
             return string.Format("{0} {1}, IDNumber {2}.", this.FirstName, this.Surname, this.IDNumber);
     }
 }

/// <summary>
/// Printout of person, using nullable types
/// </summary>
public class PersonPrintout {

    // * To generate random people
    private static string[] names = { "María", "Juan", "Pepe", "Luis", "Carlos", "Miguel", "Cristina" };
    private static string[] surnames = { "Díaz", "Pérez", "Hevia", "García", "Rodríguez", "Pérez", "Sánchez" };
    private static int numberPeople = 100;

    /// <summary>
    /// Person printout
    /// </summary>
    private Person[] printout;

    public PersonPrintout() {
        printout = new Person[numberPeople];
        Random random = new Random();
        for (int i = 0; i < numberPeople; i++)
            printout[i] = new Person {
                FirstName = names[random.Next(0, names.Length)],
                Surname = surnames[random.Next(0, surnames.Length)],
                // * The random age can also be null
                Age = random.Next() % 2 == 0 ? null : (int?)random.Next(2, 30),
                IDNumber = "" + random.Next(9000000, 90000000) + "-" + (char)random.Next('A', 'Z'),
            };
    }

    /// <summary>
    /// A filter of people by age
    /// <param name="ageGreaterOrEqualThan">The minimum age required to a person to not be filtered.
    /// null means no filter.</param>
    /// </summary>
    public Person[] Filter(int? ageGreaterOrEqualThan) {
        // * Is there any filter?
        if (!ageGreaterOrEqualThan.HasValue)
            return printout;
        Person[] toReturn = new Person[printout.Length];
        int numberOfFilteredPeople = 0;
        foreach (Person person in printout)
            // * Value obtains the age (if any)
            if (person.Age.HasValue && person.Age.Value >= ageGreaterOrEqualThan.Value)
                toReturn[numberOfFilteredPeople++] = person;
        Array.Resize(ref toReturn, numberOfFilteredPeople);
        return toReturn;
    }

class Program {
    static void Show(IEnumerable<Person> people) {
        foreach (Person person in people) {
            Console.WriteLine(person);
        }
        Console.WriteLine();
    }

    static void Main() {
        PersonPrintout printout = new PersonPrintout();
        // * Shows all the people
        Console.WriteLine("All the people:");
        Show(printout.Filter(null));
        // * Only those 18 or beyond
        Console.WriteLine("\n18 or beyond:");
        Show(printout.Filter(18));
        // * Shows the summation of all the ages (including people without
        //   a value in their age)
        Console.WriteLine("\nSumatorio de las edades: {0}.", printout.AgeSummation());
    }
}
```

# Colecciones

- En la mayoría de las aplicaciones es necesario tener una abstracción que facilita el acceso de varios objetos (vectores, pilas, colas, diccionarios...)
- Este tipo de abstracciones se suele denominar **contenedores**
- `C#`ofrece:
	- Objetos de tipo *array* (vector)
	- Colecciones (`System.Collections`)
	- Hay 2 tipos de colecciones:
		- Polimórficos (versión 1): usan polimorfismo (`object`) para coleccionar elementos: `System.Collections`
		- Genéricos (versión 2): coleccionan elementos mediante genericidad: `System.Collections.Generic`
- Cuando sea posible, mejor usar los genéricos porque:
	- El código es más eficiente
	- Se producen menos errores en tiempo de ejecución
	- El código es más legible y se evitan numerosos casts

## `System.Collections.Generic`

- Las clases más importantes son:
	- `List<T>`: vector cuyo tamaño es variable dinámicamente
	- `Dictionary<Key,Value>`: colección de pares clave/contenido organizados mediante *hashing* de la clave
	- `HashSet<T>`: colección en la que los elementos no pueden estar repetidos (conjuntos)
	- `LinkedList<T>`: lista doblemente enlazada
	- `Queue<T>`: colección con política FIFO (cola)
	- `Stack<T>`: colección con política LIFO (pila)
	- `SortedDictionary<T>`: colección de pares clave/contenido ordenados por clave
- [Documentación oficial](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic)


