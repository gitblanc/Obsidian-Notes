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
![[tipos simples.png]]

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
![[operadores.png]]

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
![[partial class1.png]]
![[partial class 2.png]]

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
![[constructor alternatives.png]]

---
## Strings
- El operador `+` concatena strings.
- Los objetos de tipo **string** son **inmutables**, no se puede modificar su estado.
- Si queremos modificar su estado, debe usarse la clase **StringBuilder**
- Los strings que comienzan por `@` permiten definir múltiples líneas
![[strings 1.png]]
![[strings 2.png]]

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
![[arrays.png]]
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
![[structs.png]]

---
## Paso de parámetros
Hay tres tipos:
- **Por valor**: el parámetro formal es una copia del parámetro real (argumento). En el paso de objetos lo que se copia es la referencia (el objeto es el original).
- **Por referencia de entrada y salida**: el parámetro formal es un alias del parámetro real (argumento). Se pasa con un valor de entrada y se le puede pasar otro de salida, modificando el original. Se usa la palabra reservada `ref`.
- **Paso por referencia de salida**: el parámetro formal es un alias del parámetro real (argumento). Se pasa sin valor de entrada y sirve para devolver más de un valor. Se usa la palabra reservada `out`.
![[por valor.png]]
![[por referencia.png]]
![[por salida.png]]
![[resultados parametros.png]]