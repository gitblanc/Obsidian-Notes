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

![](./img/Pasted%20image%2020240129124408.png)

![](./img/Pasted%20image%2020240129124438.png)

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

![](./img/Pasted%20image%2020240129124736.png)

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

![](./img/Pasted%20image%2020240129130257.png)

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

![](./img/Pasted%20image%2020240129132037.png)

# For

![](./img/Pasted%20image%2020240129132101.png)

# Switch

![](./img/Pasted%20image%2020240129132132.png)

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

