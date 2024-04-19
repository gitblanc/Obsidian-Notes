# Seminario 1. Polimorfismo y Enlace Dinámico

## Ejercicio 1

![](img/Pasted%20image%2020240202191146.png)

![](img/Pasted%20image%2020240202191207.png)

````cs
public class Person implements Comparable{
	public uint CompareTo(Object obj){
		if(obj as Person){
			if(this.Surname1.CompareTo(obj.Surname1) == 0){
				if(this.Surname2.CompareTo(obj.Surname2) == 0){
					if(this.Name.CompareTo(obj.Name) == 0)
						return 0;
					else if(this.Name.CompareTo(obj.Name) == 1)
						return -1;
					else
						return 1;
				}
			}
		}
		throw IllegalArgumentException();
	}
}

public class Main{

	void Sort(Comparable[] vector) { 
		for (int i=0; i < vector.Length; j-‐-‐) 
			if (vector[i] > vector[j]) { 
			int temp = vector[i]; 
			vector[i] = vector[j]; 
			vector[j] = temp; 
			} 
		}
	}
}
````

## Ejercicio 2

![](img/Pasted%20image%2020240202193709.png)

````cs
void Sort(Comparable[] vector, Comparador c) { 
		for (int i=0; i < vector.Length; j-‐-‐) 
			if (vector[i] > vector[j]) { 
			int temp = vector[i]; 
			vector[i] = vector[j]; 
			vector[j] = temp; 
			} 
		}
	}

public interface Comparador{
	//No usamos objetos Comparable porque no vamos a usar el CompareTo
	public uint Compara(Object obj1, Object obj2);
}

public class ComparadorNIF implements Comparador{
	public override uint Compara(Object obj1, Object obj2){
		if(obj1 as Person && obj2 as Person){
			return obj1.NIF.CompareTo(obj2.NIF);
		}
		throw IllegalArgumentException();
	}

}
````

# Seminario 2. Genericidad

## Ejercicio 1

````cs
public interface IComparable<T> 
{
	int CompareTo(T obj);
}

//Genericidad acotada (el where)
void Sort<T>(T[] vector) where T : IComparable<T>
{
	...
}
````

## Ejercicio 2

````cs
public interface IIgualado<T>
{
	bool Equals(T o);
}

//Genericidad acotada (el where)
int IndexOf<T>(T[] vector, T obj) where T : IIgualado<T>
{
	foreach...
		elem.Equals(o);
		return i;
}
````

# Seminario 3. Cálculo lambda

- Recordatorio de cálculo Lambda

![](img/Pasted%20image%2020240301170956.png)

- Lenguaje universal:

![](img/Pasted%20image%2020240301171026.png)

- Lógica  booleana:

![](img/Pasted%20image%2020240301171053.png)

- Representan dos funciones que reciben dos parámetros y devuelven una función
	- **true** devuelve el primer parámetro
	- **false** devuelve el segundo parámetro

```cs
true (3) (4) -> 3
false (3) (4) -> 4
```

## Ejercicio 1

![](img/Pasted%20image%2020240301171613.png)

- El if else es equivalente al *operador ternario*
- Recibirá 3 parámetros: `[  ]?[  ]:[  ]`

```cs
if-else = λcond.λparte_true.λparte_false.M
(if-else)(x > 100)(3)(4)
			|
			v
if-else = (λcond.λparte_true.λparte_false. cond parte_true parte_false)
// Los λ son los parámetros de la función lambda y el resto es el cuerpo de la función
```

- Función **máximo**:

```cs
maximo = λnum1.λnum2. (if-else) (num1 > num2) (num1) (num2)
maximo = λnum1.λnum2. (num1 > num2) (num1) (num2) //la lógica booleana ya implementa la función if-else, por lo que no es necesaria especificarla
```

## Ejercicio 2

![](img/Pasted%20image%2020240301173855.png)

```cs
operator_and = λcond1.λcond2. (cond1) (cond2) (false)
```

![](img/Pasted%20image%2020240301174553.png)

```cs
operator_or = λcond1.λcond2. (cond1) (true) (cond2)
```

```cs
operator_not = λcond. (cond) (false) (true)
```

# Seminario 4. Funciones de primera clase

![](img/Pasted%20image%2020240315194231.png)

- Una estructura que se puede recorrer
- Iterar

## Funciones de orden superior

*Nota: como ya están hechos en los laboratorios, vamos a hacer las llamadas a los métodos*

## Ejercicio 1

![](img/Pasted%20image%2020240315194303.png)

```cs
a.Filtrar(n => n % 2 == 0);
a.Filtrar(n => esPrimo(n));
```

## Ejercicio 2

![](img/Pasted%20image%2020240315194313.png)

```cs
a.Map(s => s.Length);
a.Map(f => f.Substract(DateTime.Today));
```

## Ejercicio 3

![](img/Pasted%20image%2020240315194324.png)

```cs
a.Reduce(1, (acu,x) => acu * x); //el 1 es el opcional
```

# Seminario 5. Clausuras

## Ejercicio 1

![](img/Pasted%20image%2020240405190931.png)

```cs
int c = 0;
Func<int> f = () => c ++;

new int[1000].Select(x => f());

//Se podría hacer con IEnumerable.Range(0, 1000);
```

![](img/Pasted%20image%2020240405192315.png)

```cs
static int Suma(IEnumerable<int> collection)
{
	int cont = 0;
	int res = 0;
	Action action = () =>
		{
			res += collection[cont];
			cont+=1;
		}
	BucleWhile(cont < collection.Length, action);
	return res;
}
```

![](img/Pasted%20image%2020240405193028.png)

```cs
static void Switch<T>(T valor, IEnumerable<(Predicate<T>,Action cuerpo)> lista, Action defaultA)
{
	foreach(var item in lista)
		if(item.First(valor))
		{	
			item.Second();
			return;
		}
	defaultA();
}

(v) => v==1, () => {a = 0;}
() => valor==2, () => {b = 0;} //usando Func<bool> en lugar de Predicate<T>
(v) => v%2==0, () => {c = 0;}
```

# Seminario 6. Programación Concurrente

## Ejercicio 1

![](img/Pasted%20image%2020240419190741.png)

![](img/Pasted%20image%2020240419190802.png)

![](img/Pasted%20image%2020240419190834.png)

```cs
using System.Threading;
namespace TPP.Seminarios.Concurrente.Seminario6 {
 /// <summary>
 /// Representa un recurso a adquirir por un hilo
 /// </summary>
 public class Recurso {
	 public string Nombre { get; private set; }
	 public Recurso(string nombre) {
		 this.Nombre = nombre;
	 }
	 public void Procesar() {
		 Thread.Sleep(100); // simula procesamiento...
	 }
 }
}

namespace TPP.Seminarios.Concurrente.Seminario6 {
 /// <summary>
 /// Encapsula un hilo
 /// </summary>
 public class Hilo {
	 public Recurso Recurso1 { get; private set; }
	 public Recurso Recurso2 { get; private set; }
	 public Hilo(Recurso recurso1, Recurso recurso2) {
		 this.Recurso1 = recurso1;
		 this.Recurso2 = recurso2;
	 }
	 /// <summary>
	 /// Este método será llamado concurrentemente en la ejecución del hilo
	 /// </summary>
	 public void Ejecutar() {
		 lock (this.Recurso1) {
		 Recurso1.Procesar();
		 lock (this.Recurso2) {
		 Recurso2.Procesar();
		 }
		 }
	 }
 }
}

using System.Threading;
namespace TPP.Seminarios.Concurrente.Seminario6 {
	 class Program {
		 public static void Main() {
			 Recurso recurso1 = new Recurso("Recurso 1"),
			 recurso2 = new Recurso("Recurso 2");
			 Hilo hilo1 = new Hilo(recurso1, recurso2),
			 hilo2 = new Hilo(recurso2, recurso1);
			 new Thread(hilo1.Ejecutar).Start();
			 new Thread(hilo2.Ejecutar).Start();
		 }
	 }
}
```

- Solución:

```cs
using System.Threading;
namespace TPP.Seminarios.Concurrente.Seminario6 {
 /// <summary>
 /// Representa un recurso a adquirir por un hilo
 /// </summary>
 public class Recurso {
	 public string Nombre { get; private set; }
	 public Recurso(string nombre) {
		 this.Nombre = nombre;
	 }
	 public void Procesar() {
		 lock(this){//Esto permite que sea Thread-safe
			 Thread.Sleep(100); // simula procesamiento...
		 }
	 }
 }
}

namespace TPP.Seminarios.Concurrente.Seminario6 {
 /// <summary>
 /// Encapsula un hilo
 /// </summary>
 public class Hilo {
	 public Recurso Recurso1 { get; private set; }
	 public Recurso Recurso2 { get; private set; }
	 public Hilo(Recurso recurso1, Recurso recurso2) {
		 this.Recurso1 = recurso1;
		 this.Recurso2 = recurso2;
	 }
	 /// <summary>
	 /// Este método será llamado concurrentemente en la ejecución del hilo
	 /// </summary>
	 public void Ejecutar() {
		 //lock (this.Recurso1) {
			Recurso1.Procesar();
				 //lock (this.Recurso2) {
					 Recurso2.Procesar();
				 //}
		 //}
	 }
 }
}

using System.Threading;
namespace TPP.Seminarios.Concurrente.Seminario6 {
	 class Program {
		 public static void Main() {
			 Recurso recurso1 = new Recurso("Recurso 1"),
					 recurso2 = new Recurso("Recurso 2");
			 Hilo hilo1 = new Hilo(recurso1, recurso2),
				  hilo2 = new Hilo(recurso2, recurso1);
			 new Thread(hilo1.Ejecutar).Start();
			 new Thread(hilo2.Ejecutar).Start();
		 }
	 }
}
```

- El **lock** bloquea un trozo de código en base a un objeto
- Hay que hacer las operaciones de forma atómica
	- Separar los locks para que no dependan entre sí y posteriormente implementarlos en el método concreto

## Ejercicio 2

### El problema de los cinco filósofos

![](img/Pasted%20image%2020240419192154.png)

![](img/Pasted%20image%2020240419192230.png)

![](img/Pasted%20image%2020240419192245.png)

![](img/Pasted%20image%2020240419192258.png)

```cs
namespace TPP.Seminarios.Concurrente.Seminario6 {
 /// <summary>
 /// Cada uno de los tenedores disponibles
 /// </summary>
 class Tenedor {
	 /// <summary>
	 /// Número de tenedor
	 /// </summary>
	 private int numero;
	 public Tenedor(int numero) {
		 this.numero = numero;
	 }
 }
}

using System;
using System.Threading;
namespace TPP.Seminarios.Concurrente.Seminario6 {
 class Filosofo {
 /// <summary>
 /// ID del filósofo
 /// </summary>
 private int numeroFilosofo;
 /// <summary>
 /// El tiempo que tarda pensando
 /// </summary>
 private int milisPensar;
 /// <summary>
 /// El tiempo que tarda comiendo
 /// </summary>
 private int milisComer;
 /// <summary>
 /// Los tenedores izquierdos y derechos
 /// </summary>
 private Tenedor tenedorIzquierdo, tenedorDerecho;
 public Filosofo(int numeroFilosofo, int milisPensar, int milisComer, Tenedor tenedorIzquierdo, Tenedor tenedorDerecho) {
	 this.numeroFilosofo = numeroFilosofo;
	 this.milisPensar = milisPensar; this.milisComer = milisComer;
	 this.tenedorIzquierdo = tenedorIzquierdo;
	 this.tenedorDerecho = tenedorDerecho;
	 new Thread(new ThreadStart(ComerYPensar)).Start();
 }
 private void ComerYPensar() {
	 for (;;) {
		 lock (this.tenedorIzquierdo) {
			 lock (this.tenedorDerecho) {
				 Console.WriteLine("El filósofo " + numeroFilosofo +
				 " está comiendo...");
				 Thread.Sleep(milisComer);
				 }
				 }
				 Console.WriteLine("El filósofo " + numeroFilosofo +
				 " está pensando...");
				 Thread.Sleep(milisPensar);
		 }
	 }
 }
}
namespace TPP.Seminarios.Concurrente.Seminario6 {
 class Program {
	 static void Main(string[] args) {
	 const int milisPensar = 0, milisComer = 0;
	 Tenedor[] tenedor = new Tenedor[5];
	 for (int i = 0; i < tenedor.Length; i++)
		 tenedor[i] = new Tenedor(i);
	 new Filosofo(0, milisPensar, milisComer, tenedor[0], tenedor[1]);
	 new Filosofo(1, milisPensar, milisComer, tenedor[1], tenedor[2]);
	 new Filosofo(2, milisPensar, milisComer, tenedor[2], tenedor[3]);
	 new Filosofo(3, milisPensar, milisComer, tenedor[3], tenedor[4]);
	 new Filosofo(4, milisPensar, milisComer, tenedor[4], tenedor[0]);
	 }
 }
}
```

Ideas:
- Hacer lock a un objeto que encapsule 2 tenedores: `lock(new Par(this.tenedorIzq, this.tenedorDer))`
- Hacer un lock global: `lock(objetoGlobal)`
	- Sólo puede comer un filósofo a la vez, no 2
	- Nunca va a caer en un deadlock
- ***Solución***: Hacer un **manejador de tenedores**
	- La solución está en el campus
