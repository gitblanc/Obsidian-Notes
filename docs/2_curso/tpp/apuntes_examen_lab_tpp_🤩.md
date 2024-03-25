*Nota: en este documento voy a almacenar las cosas que considero más críticas para el examen*

## Clases de utilidad (static)

- Las clases de utilidad han de llevar `static`, es decir: `public static class EjemploAyuda`

## Propiedades

- Permiten acceder al estado de los objetos como si de atributos se tratase
	- Se oculta el estado interno del objeto, ofreciendo un acceso indirecto mediante las propiedades (encapsulamiento)

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

## Arrays Multidimensionales

- Existen dos tipos:
	- **Arrays Lineales**: memoria contigua lineal, de varias dimensiones

	```cs
	string[,] vector=new string[3,4];
	for (int i = 0; i < vector.GetLength(0); i++)
		for (int j = 0; j < vector.GetLength(1); j++)
			vector[i,j]="("+(i+1)+","+(j+1)+")";
	```

	- **Arrays de Arrays**: permite la construcción de arrays irregulares

	```cs
	int[][] triangular=new int[10][];
	for (int i=0;i<triangular.Length;i++)
		triangular[i] = new int[triangular.Length-i];
	```

## Paso de parámetros

- **Paso por valor**
	- El parámetro formal es una *copia* del parámetro real
	- *NO SE MODIFICA EL VALOR*
- **Paso por referencia de entrada y salida** (`ref`)
	- Se pasa con un valor (entrada) y se le puede asignar otro (salida), modificando el original
	- SE MODIFICA EL VALOR
- **Paso por referencia de salida** (`out`)
	- Se pasa sin valor (entrada) y sirve para devolver más de un valor

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

```cs
By value. Base: 2, exponent: 3, power: 8.
After the invocation. Base: 2, exponent: 3.
By reference. Base: 2, exponente: 3, power: 8.
After the invocation. Base: 0, exponente: 0.
First name: Edu
Surname: Blanco
Id number: 1234254
First name: Edu, surname: Blanco, id number: 1234254.
```

## Parámetros Opcionales

- Siempre tienen que ser los últimos (más a la derecha)

```cs
public Persona[] GetPagina(int pagina = 1,
int elementosPorPagina = 10, bool soloMayoresEdad = true) {
…
}
```

## Declaración implícita de variables

- No se requiere especificar su tipo siempre que se asigne un valor en la declaración

```cs
var vector = new[] { 0, 1, 2 }; // vector es int[]
foreach(var item in vector){ // item es int
	...
}
```

## Métodos extensores

- Hay que crear una clase de utilidad (`static)
- Hay que implementar un método de clase `static` en dicha clase de utilidad
- El primer parámetro tiene que declararse anteponiendo la palabra reservada `this`

```cs
static class ExtensoraString {
	static public uint ContarPalabras(this string cadena) {
		...
	}
```

## Herencia

- Mecanismo de **reutilización** de código

```cs
public class Derivada : Base
{
	...
}
```

## Polimorfismo

- Mecanismo de **generalización**, que hace que la abstracción más general pueda representar abstracciones más específicas
- Si se implementa, el tipo ha de ser `object`, **NO** `T` (`T` es genericidad)

## Enlace dinámico

- Los métodos heredados se pueden especializar en las clases derivadas
- En las clase base hay que poner `virtual` al método
- En las clases derivadas hay que poner `override` al método

![](img/Pasted%20image%2020240325150234.png)

## Operadores `is` `as`

- El operador `is` nos permite comprobar si un objeto es de tipo X

```cs
if (lista[0] is Persona)
	((Persona)lista[0]).CumplirAños();
```

- El problema es que si después de usar el operador `is` vamos a realizar un cast (como e muestra arriba), es mejor usar directamente `as`

```cs
Persona persona = lista[0] as Persona;
if (persona != null)
	persona.CumplirAños();
```

## Autoboxing (boxing y unboxing)

- Los tipos simples (int, char, float, double...) ¡no heredan de `Object`!
- Ejemplo: `int` promociona a `Int32` y un `Int32` se convierte automáticamente en `int`

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

## IDisposable y Destructores

- Una clase que defina un constructor, comúnmente implementará `IDisposable`:

```cs
classFichero: IDisposable{
	private string nombreFichero;
	private bool estaAbierto;
	public Fichero(string nombreFichero) {
		this.nombreFichero = nombreFichero;
		this.estaAbierto = true;
		Console.WriteLine("Abriendo el fichero {0}.", nombreFichero);
	}
	public void Dispose() {
		if(this.estaAbierto) {
			this.estaAbierto= false;
			Console.WriteLine("Cerrando el fichero {0}.", nombreFichero);
		}
	}
	~Fichero() { this.Dispose(); }
	...
```

- Esto es susceptible de ser olvidado.
	- Por ello se usa la palabra `using` para **asegurar** la liberación de los recursos adicionales de un objeto `IDisposable`
		- incluso si se lanza una excepción y no se maneja

```cs
using(Ficherofichero= newFichero("entrada.txt")) {
	stringlínea = fichero.LeerLínea();
	// Lanza una excepción DivideByZeroException
	fichero.EscribirLínea(línea + línea.Length/"".Length);
} // Se cierra el fichero
```

- Un ejemplo completo:

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

## Programación por contrato (precondiciones, postcondiciones, invariante)

- Siguen esta estructura:

![](img/Pasted%20image%2020240325151346.png)

- **Precondiciones**: se ponen antes de la sección crítica
- **Postcondiciones**: se ponen justo después de la sección crítica
- **Invariante**: se llama lo primero en un método y lo último (es lo que a narices no puede estar mal o ser de otra forma, por ejemplo que una lista tenga -2837456 elementos), y en los constructores se llama lo último

```cs
// Constructor de una pila
        public MyStack(uint elems)
        {
            if (elems < 1)
                throw new ArgumentException("Has de tener capacidad de al menos un elemento");
            _maxNumberOfElems = elems;
            _list = new LinkedList<T>();
#if DEBUG            
            // Invariantes
            Invariant();
#endif
        }

// Método de una pila
        public bool Push(T data)
        {
            // Precondiciones
            if (_maxNumberOfElems == _list.NumberOfElements)
                throw new ArgumentOutOfRangeException("La pila está llena");

            int previous = _list.NumberOfElements;
            _list.Add(data);
#if DEBUG
            // PostCondiciones
            Debug.Assert(_list.NumberOfElements > previous); // Asegurarnos de que se incrementó el número de elementos

            // Invariante
            Invariant();
#endif
            return true;
        }

// Invariante
#if DEBUG
        private void Invariant()
        {
            Debug.Assert(_maxNumberOfElems >= 0);
            Debug.Assert(_maxNumberOfElems >= _list.NumberOfElements);
            Debug.Assert(_list != null);
        }
#endif
```

## Genericidad

- Se usa `T`
	- No confundir con tipo polimórfico (donde se usa `object`)
- El tipo por defecto es `default(T)`

- Ejemplo de método genérico

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

- Ejemplo de clase Genérica:

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

## Genericidad acotada

- Se indica con el `where T: IComparable<T>`
	- Útil en métodos de ordenación donde haya una lista con elementos de varios tipos

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

## `IEnumerable<T>`

- Esta interfaz representa una colección de elementos genérica
- Un objeto que implemente `IEnumerable` se puede recorrer con un `foreach`
- La interfaz `IEnumerable` sólo posee un método: `GetEnumerator()`
	- Este método construye un **iterador**

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
```

## Tipos anulables

- Hay que poner `?` al tipo simple: `int?`, `double?` ...
- Sus principales miembros son las propiedades:
	- `HasValue:bool`
	- `Value:T`

## Colecciones

- Existe la librería: `System.Collections.Generics`, que incluye: 
	- `List<T>`: vector cuyo tamaño es variable dinámicamente
	- `Dictionary<Key,Value>`: colección de pares clave/contenido organizados mediante _hashing_ de la clave
	- `HashSet<T>`: colección en la que los elementos no pueden estar repetidos (conjuntos)
	- `LinkedList<T>`: lista doblemente enlazada
	- `Queue<T>`: colección con política FIFO (cola)
	- `Stack<T>`: colección con política LIFO (pila)
	- `SortedDictionary<T>`: colección de pares clave/contenido ordenados por clave