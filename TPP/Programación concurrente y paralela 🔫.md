# Tema 4🥭
---
```
Ejemplos de código en generics/inference
````

## Ley de Moore
- El número de transistores se duplica cada 24 meses sin encarecer el precio.
- Este crecimiento dejará de cumplirse entre 2017 y 2022, porque el tamaño de los transistores se está acercando cada vez más al átomo.

- https://github.com/karlrupp/microprocessor-trend-data	gráfica
---
## Arquitectura Multinúcleo
- Se usa en pc de escritorio.
- Nuestra CPU tiene varios núcleos y una memoria compartida. Cada uno de esos cores puede ejecutar programas distintos (hilos).
---
## Memoria distribuida
- Se usa en servidores.
- Cada procesador tiene una zona de memoria privada. Para que un procesador acceda a otra memoria ha de usar ciertos mecanismos más lentos (canal).
---
## Programación concurrente y Paralela
- *Diferencia entre programación concurrente y paralela:* **concurrencia** es la propiedad por la que varias tareas se pueden ejecutar simultáneamente (puede ser simulada en un único procesador). **Paralelismo** es siempre real, al menos dos tareas se ejecutan de forma paralela.
---
## Proceso
- Es un programa en ejecución. Consta de instrucciones, estado y valores de datos. Un proceso no puede acceder a la memoria de otro proceso.
- Un proceso puede constar de varios hilos de ejecución (threads).
---
## Hilo
- Un hilo es una tarea de un proceso que puede ejecutarse concurrentemente, compartiendo la memoria del proceso, con el resto de sus hilos.
- En los procesadores multinúcleo, los hilos pueden ser tareas paralelas de un mismo proceso.
- Si dos hilos modifican los mismo a la vez es un problema. Hay que implementar un mecanismo de sincronización.

````C#
 var procesos = Process.GetProcesses();
 foreach (Process proceso in procesos) { 

Console.WriteLine("PID: {0}\tNombre: {1}\tMemoria

virtual: {2:N} MB“, proceso.Id, proceso.ProcessName, proceso.VirtualMemorySize64/1024.0/1024);
````
---
## Paralelización de algoritmos
- **Paralelización de tareas:** cada tarea se ejecuta en un hilo.
- **Paralelización de datos:**  divide los datos para procesarlos de forma dividida.
---
## Pipeline
- Son varias tareas interconectadas y sincronizadas para llegar a un resultado.
---
# Hilos (Threads)🫐
---
## Creación Explícita de hilos
````C#
// Lo creamos

Thread hilo = new Thread(delegado);  //le pasas una función al hilo
// Lo nombramos (opcional)  
hilo.Name = "Hilo secundario"; Thread.CurrentThread.Name = "Hilo principal"; // Le asignamos una prioridad (opcional) 
hilo.Priority = ThreadPriority.BelowNormal; 
// Lo lanzamos
hilo.Start(); //ejecuta una tarea en segundo plano, la función delegado
...
````
- **Principal diferencia con Java:** la clase ha de implementar Runnable y ejecutar el método run(). Enfoque orientado al paradigma orientado a objetos. En C# está orientado al paradigma funcional.
````
Ejemplos en: threads/vector.modulus
````
- **Master thread:** hilo principal.
---
## Ejemplo
````C#
internal class Worker {  
	private short[] vector;  
	private int índiceDesde, índiceHasta;  
	private long resultado;  
	internal long Resultado { get { return this.resultado; } } 
	internal Worker(short[] vector, int índiceDesde,int índiceHasta) {
	 this.vector = vector; 

	 this.índiceDesde = índiceDesde; 

	 this.índiceHasta = índiceHasta; }

	internal void Calcular() {  
	this.resultado = 0;  
	for(int i= this.índiceDesde; i<=this.índiceHasta; i++)
		this.resultado += this.vector[i] * this.vector[i]; 
	}}}

 

public class Master {  
	private short[] vector;  
	private int numeroHilos;  
	public Master(short[] vector, int numeroHilos) {

	 if (numeroHilos < 1 || numeroHilos > vector.Length)
	 throw new ArgumentException("El número de hilos ha 
		de ser menor o igual que los elementos del 
		vector."); this.vector = vector;

	 this.numeroHilos = numeroHilos;
	   }
								 
	 

	public double CalcularModulo() {  
		Worker[] workers = new Worker[this.numeroHilos];  
		int elementosPorHilo = this.vector.Length/numeroHilos; 
		for(int i=0; i < this.numeroHilos; i++)
			workers[i] = new Worker(this.vector, i*elementosPorHilo, 			  			   	  		(i<this.numeroHilos-1) ? // ¿último?
		    (i+1)*elementosPorHilo-1: this.vector.Length-1 ); 
		Thread[] hilos = new Thread[workers.Length];

		for(int i=0;i<workers.Length;i++) {  
			hilos[i] = new Thread(workers[i].Calcular); hilos[i].Start();

		}  
		foreach (Thread hilo in hilos)
			hilo.Join(); 
			long resultado = 0;  
		foreach (Worker worker in workers)
			resultado += worker.Resultado; 
		return Math.Sqrt(resultado); } }
````
- El **Join()** sirve para sincronizar los hilos.
---
## Condición de Carrera
- Multiples tareas están en condición de carrera cuando su resultado depende del orden en el que éstas se ejecutan. Son algo malo. Tenemos que escribir programas que independientemente del número de hilos, siempre de el mismo resultado.
- Un programa concurrente no debe tener condiciones de carrera.
---
## Parámetros
```c#
static void Mostar10Numero(object desde) { 
	if (!(desde is int))

		throw new ArgumentException("...");  
		int desdeInt = (int)desde;  
		for (int i = desdeInt; i < 10 + desdeInt; i++) {
			Console.WriteLine(i); 
			Thread.Sleep(1000); 
		}
	}

static void Main() {  
	Thread hilo = new Thread(Mostar10Numero); 
	hilo.Start(7); 
	hilo.Join();  
}
```
---
## Variables Libres
- Las variables locales serán compartidas por todos los hilos.
- CUIDADO CON ELLAS.
```c#
 int local = 1;  
Thread hilo1 = new Thread( () => {

 Console.WriteLine("Hilo 1. Local {0}.", local); 

 });
local = 2; 
Thread hilo2 = new Thread( () => { 

 Console.WriteLine("Hilo 2. Local {0}.", local); 

 });
    hilo1.Start();
	hilo2.Start();
```
````
Ejemplo en threads/bound.variables
````
##### Alternativas
- Paso de parámetros
````c#
 int local = 1;

 Thread hilo1 = new Thread( (parametro) => {
 Console.WriteLine("Parámetro {0}.", parametro);
      }); 

 local = 2;
    hilo1.Start(local-1);
````
- Copia de variables
````c#
 int local = 1;

 int copia = local;
 Thread hilo1 = new Thread( () => { 

 Console.WriteLine("Copia {0}.", copia); 

 });
    local = 2;
    hilo1.Start();
````
---
## Excepciones Asíncronas
````c#
static void Main() { 
	try {

		new Thread(() => {  
			Thread.Sleep(500);  
			throw new ApplicationException("Excepción Asíncrona.");
		}).Start();

	//¡La excepción no es capturada y el programa finaliza bruscamente!

	 
	} 

	//El try/catch se debería haber puesto en el código asíncrono, dentro de el propio hilo que lanza la excepción

	catch (Exception) {  
		Console.WriteLine("Se captura la excepción.");

	//Este catch es inútil

	}  
	Thread.Sleep(1000); 
	Console.WriteLine("Fin del programa.");
````
- Ha de ser el propio hilo que lanza la excepción el que la maneje.
```
Ejemplo en threads/asynchronous.exceptions
```
---
## Mejora de rendimiento
- Hay un margen que no se puede sobrepasar al usar hilos.
---
## Context Switch (cambio de contexto)
- **Contexto:** informacion que tiene que ser guardada cuando éste es interrumpido para que luego pueda reanudarse su ejecución.
-  Permite la ejecución concurrente de varias tareas en un mismo procesador.
-  El cambio de contexto perjudica el rendimiento final del algoritmo.
-  Requiere tiempo de computación y memoria adicional.
-  Un número elevado de tareas conlleva a una caída global del rendimiento.
-  A mayor número de hilos, peor rendimiento.
---
## Thread pooling
- En vez de crear muchísimos hilos, crea un número limitado, es decir, un número máximo de hilos creados por cada proceso.
- Se debe reutilizar los hilos.
- Si el proceso lleva un tiempo sin crear nuevos hilos se eliminan los hilos ya existentes.
---
## Foreground & Background Threads
- **Foreground:** Si el hilo principal termina, la aplicación no se muere.
- **BackGround(daemons):** Si acaba el hilo principal, la aplicación termina.
````c#
 static void Main() {
 Thread background = new Thread(() => { 

 int segundos = 0;
 while (true) { 

	 Thread.Sleep(1000);
	 Console.WriteLine("\t\t\t\t\t\t\t\t{0} segundos.", 
	 ++segundos); 

} });  
background.IsBackground = true; // es un daemon background.Start();  
Thread foreground = new Thread(() => {

 for (int i = 0; i < 100; i++) {
	 Console.WriteLine("Iteración {0}.", i + 1);
	 Thread.Sleep(100); 

 }  });
   foreground.Start();
````
---
## Inconvenientes del uso de Hilos
*(Mirar transparencia 38)*
- Condiciones de carrera (este no se puede mitigar)
- Parámetros
- Excepciones asíncronas
- Rendimiento de los cambios de contextos
---

