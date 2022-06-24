♻️ 	Parte anterior -> [[Invariants, preconditions, postconditions 🦠]]
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
- Son de muy bajo nivel
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
# 24 Marzo 2022 🏀
---
## Tasks
- Es un mecanismo de **más alto nivel** que los hilos.
- En las transparencias es casi equivalente a los hilos.
- Tienen un nivel de abstracción mayor y proporcionan más funcionalidades que los hilos.
- TPL, PLINQ
-   https://docs.microsoft.com/en-us/dotnet/standard/parallel-programming/task-based-asynchronous-programming

	---
- Una task representa una operación síncrona. Presenta dos beneficios:
	- Uso más eficiente y escalable de los recursos: las Tasks se encolan automáticamente en el ThreadPool.
	- Mayor control de ejecución
- En .NET -> Task y TPL

	---
- Una tarea que no devuelve valores está representada por System.Threading.Tasks.Task
- Una tarea que devuelve valores está representada por la clase System.Threading.Tasks.Task "Tresult"
	
````c#
// Crea una tarea y proporciona una expresión lambda con el código a ejecutar  
Task firstTask = new Task(() => Console.WriteLine(“Ejecutando primera tarea (Thread {0})", Thread.CurrentThread.ManagedThreadId));

// Arranca la tarea 

firstTask.Start();

// Imprime un mensaje desde el hilo que la llama 

Console.WriteLine(“Ejecutando thread principal (Thread {0})",
 Thread.CurrentThread.ManagedThreadId); 

// Espera a que la tarea termine 

firstTask.Wait();
````

````
Consultar código en tasks/explicit.task.creation
````
---
### Creación y ejecución explícita de tareas
 
```c#
Task[] taskArray = new Task[10];  
for (int i = 0; i < taskArray.Length; i++) {

//Pasa un objeto TaskData como segundo parámetro para contener el estado

taskArray[i] = Task.Factory.StartNew((Object obj) => { TaskData data = obj as TaskData;  
if (data == null) return;  
data.ThreadNum = Thread.CurrentThread.ManagedThreadId;

}, new TaskData() { Name = i, CreationTime = DateTime.Now.Ticks }); }

Task.WaitAll(taskArray);  
foreach (var task in taskArray) {

 var data = task.AsyncState as TaskData;
 if (data != null) 

}
```
---
- También existe un Task genérico. 
- Los task genéricos evitan las condiciones de carrera.
````
Código en tasks/task.result
````
NOTA: las task son como los hilos pero éstas evitan las condiciones carrera, los cambios de contexto y las excepciones.
````
Código en tasks/task.free.variables
````
````
Código en tasks/task.state.object
````
---
# Composición de tareas
- WhenAll
- WhenAny
- Delay
````
Código en tasks/task.composition
````
---
# Manejo de excepciones con tareas
- Cuando una tarea lanza una excepción o más, todas ellas se encapsulan en una excepción de tipo AggregateException.
- Esta excepción se propaga al hilo vinculado a la tarea.

````c#
 static void CaptureException(){ 
	 try {

var task = Task.Run(() => { throw new ArgumentNullException(); });

 task.Wait();
       } 

catch (AggregateException e) {  
Console.WriteLine("Task lanza la siguiente excepcion: " + e);

}

return; }

static void ReThrowException (){ try {

var task = Task.Run(() => { throw new ArgumentNullException(); });

 task.Wait();
    } 

catch (AggregateException e) {  
Exception[] list = new Exception[] { e };  
throw new AggregateException(“Excepcion relanzada como una

AggregateException", list); }

return; }
````
````
Código en tasks/task.exception
````

---
# Paso asíncrono de mensajes
- Cada mensaje crea un nuevo hilo
- En C# esta funcionalidad se obtiene mediante delegados
![[paso asincrono.png]]
````
Código en delegates/sequential
````


### Esquema
1. Pasar el primer mensaje de forma asíncrona.
2. Pasar el segundo se forma síncrona.
3. Obtener el número de imágenes del segundo mensaje.
4. Tomar el número de imágenes del primer mensaje.
5. Mostrar los resultados
---
## Uso de async y await
- Actualmente se usa async y awat.
- Un método **async** devuelve una Task o una Task-Result-
- El operador **await**se usa sobre la Task devuelta
- Para conocer su uso ver el enlace ->https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/async/task-asynchronous-programming-model
![[await async.png]]
- Como es una ejecución asíncrona, el hilo pricipal puede continuar(método GetUrlContentLengthAsync())

**Ejemplos de uso**
```c#
public async Task<int> GetNumberOfImagesAsyncTask()
    { 

 var client = new WebClient();
 Console.WriteLine("Getting the web page in the asynchronous 

method.");

//Call and API asynchronous method. Wait for this asynchronous //task to finish. Yields control to the caller.  
var html = "";  
await Task.Run(() => html = client.DownloadString(url));

 var html = await client.GetStringAsync(url); 

 Console.WriteLine("Obtained the web page in the asynchronous
    method."); 

}

return Ocurrences(html.ToLower(), "<img");
```
```c#
private static async void GetImagesAsync() {  
var school = new WebPage("http://www.ingenieriainformatica.uniovi.es"); var uniovi = new WebPage("http://www.uniovi.es");  
...  
//Begin task. Yields the control to the caller  
//when its await line is reached.  
Task<int> taskGetImagesUniovi = uniovi.GetNumberOfImagesAsyncTask(); Console.WriteLine("Returned from the asynchronous method"); Console.WriteLine("Performing synchronous work");

//Synchronous call: Performing tasks while we wait for the //async task to finish  
int numberOfImgsInSchool = school.GetNumberOfImages(); Console.WriteLine("Synchronous work finished");

 //Wait for the asynchronous task to finish 

var numberOfImgsInUniovi = await taskGetImagesUniovi;
```

### Particularidades
- No pueden llamar a ref o out, pero pueden llamar a métodos que los tengan.
- Se puede devolver void, pero no se puede hacer un await.

---
# Sincronización de hilos
- Los hilos pelean por la CPU.
- El mayor problema es el uso de recursos compartidos. Con operaciones de lectura no hay problema, pero no es posible que varios hilos escriban a la vez.
- Hay que evitar el uso de un recurso (exclusión mutua)
- Esto se aplica a hilos y a Tasks.

- Una sección crítica es un fragmento de código que accede a un recurso compartido que no debe ser accedido concurrentemente por más de un hilo de ejecución
---
# Lock
- Consigue que únicamente un hilo pueda ejecutar una sección crítica simultáneamente (exclusión mutua).
- Requiere especificar un objeto (referencia) como parámetro
![[lock.png]]
- No se puede acceder a la seccion crítica 1 y a la 2 por separado, ya que hacen referencia al mismo objeto.
---
# Asignaciones
- No todas las asignaciones son atómicas.
- Las de 32 bits sí lo son.
- Las de 64 no en sistemas de 32 bits.
- **ALTERNATIVA AL LOCK** -> usar la clase InterLocked(System.Threading) (mucho más eficiente que usar un lock).
````
Código en synchronization/interlocked
````
---
# Mutex y semáforos
- Mecanismos de sincronización entre procesos.
- **Mutex:** funcionamiento similar al lock pero mucho más lento.
- **Semáforo:** permiten el acceso a n procesos concurrentes. Se suele usar para limitar la concurrencia.
````
Código en synchronization/mutex
````
````
Código en synchronization/semaphores
````
---
# Interbloqueo
- Se produceentre un conjunto de tareas si todas y cada una de ellas están esperando por un evento que sólo otra puede causar. Todas se bloquean de forma permanente.
- El caso más común es el acceso a recursos compartidos.
![[interbloqueo.png]]
````
Código en deadlock/
````

---
# 31 Marzo 2022 ☕️
---
### Estructuras de datos Thread-Safe
- El lock no impide que otro proceso actúe sobre la sección concreta.
- El lock se hace sobre un recurso compartido, e indica si ese recurso está libre o no. Si está libre, lo ejecuta, y sino se duerme hasta que esté libre.
```c#
static void AñadirYMostrarThreadSafe(List lista) {

lock (lista) lista.Add("Item " + lista.Count); string[] items;  
lock (lista) items = lista.ToArray();  
lock (Console.Out)

foreach (string s in items) {
	Console.WriteLine(s); }
```
---
## Implementación EEDD Thread-Safe
- **Composición:** Si tenemos A composición B. A no puede vivir sin B. Es una relación más fuerte.
- **Agregación:** Si tenemos A agrega B, A tiene un objeto de tipo B. A y B son objetos independientes. Es una relación más débil.
![[thread safe.png]]
- En este caso, se trata de una composición
- La clase de la izquierda usa a la clase de la derecha.

- Para realizar un **lock** es mejor usar el *this* porque la referencia es pública, en lugar de ser privada (this.lista).
- Esto puede afectar al rendimiento del programa o incluso generar interbloqueos.
- Es una implementación sencilla pero ineficiente.
- El **lock** no permite diferenciar entre lectura y escritura. No se deben de bloquear dos operaciones de lectura, pero sí dos de escritura de forma simultánea.
---
## ReaderWriterLockSlim
- Tiene modo lectura, modo escritura y modo lectura actualizable.
- Esta política disminuye la posibilidad de interbloqueos y mejora el rendimiento.
````
Código en ReaderWiterLockSlim
````
![[readerwriterlock.png]]

---
## TPL y PLINQ 🍉
---
### Task Parallel Library
Ventajas:
- Simplifica la paralelización.
- Escala dinámicamente
- División de datos procesados.
- Tareas independientes.
https://docs.microsoft.com/es-es/dotnet/standard/parallel-programming/task-parallel-library-tpl
---
![[pregunta paralelo.png]]
```c#
vector.Select(x => x^2).Sum().Math.sqrt()
```
---
♻️ Parte siguiente -> [[Tipado dinámico y Metaprogramación (clase)🍒]]

