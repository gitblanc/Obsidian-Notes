# TEMA 4 🐯
---
## Arquitecturas multinúcleo
- La tendencia actual es que los ordenadores amplíen el número de núcleos en lugar de la frecuencia de reloj
- Los **microprocesadores multinúcleo** incluyen más de un procesador en una misma CPU
- Ofrecen **computación paralela** (**paralelismo**) no sólo a nivel de proceso, sino también a nivel de hilo (**thread**)
- Las arquitecturas multinúcleo poseen una **memoria compartida**

---
## Memoria distribuida
- En los **sistemas multiprocesador con memoria distribuida**, cada procesador posee una memoria privada
- Si un procesador requiere datos de otro, tiene que comunicarse con éste a través de un **canal**

---
## Programación concurrente
- **Concurrencia**: es la propiedad por la que varias tareas se pueden ejecutar simultáneamente y potencialmente interactuar entre sí
	- Pueden ejecutarse en varios núcleos, varios procesadores o *simulada* en un único procesador
	- Las tareas pueden ser hilos o procesos
	- La programación concurrente **enfatiza la interacción** entre tareas

---
## Programación paralela
- **Paralelismo**: es un caso particular de concurrencia, en el que las tareas se ejecutan de forma paralela (simultáneamente, *no simulada*)
	- Con la **concurrencia**, la simultaneidad **puede ser simulada**
	- Con el **paralelismo**, la simultaneidad **debe ser real**
- El paralelismo **divide el problema** en dos partes más pequeñas

---
## Proceso
- Programa en ejecución que:
	- Consta de instrucciones, estado de ejecución y valores de datos en ejecución
	- En los sistemas de memoria distribuida, las tareas concurrentes en distintos procesadores son procesos
	- Todo proceso cuenta con un identificador (PID)

---
## Hilo
- Un proceso puede constar de varios hilos de ejecución (threads)
- **Hilo**: tarea de un proceso que puede ejecutarse concurrentemente, compartiendo la memoria del proceso con el resto de sus hilos
	- Cada hilo cuenta con un contador de programa, la pila de ejecución y el valor de los registros
	- En los procesadores multinúcleo, los hilos pueden ser tareas paralelas de un mismo proceso

---
## Procesos e hilos en .Net
![[procesos 2.png]]
![[hilos.png]]

---
# Hilos
---
## Paralelización de algoritmos
Existen dos escenarios:
- **Paralelización de tareas**: tareas independientes que pueden ser ejecutadas concurrentemente
- **Paralelización de datos**: ejecutar una misma tarea que computa porciones de los mismos datos
![[paralel algs.png]]

---
## Creación explícita de hilos
- La clase `Thread (System.Threading)` encapsula un hilo de ejecución de forma explícita
![[crea hilo.png]]

---
## Ejemplo de programa concurrente
![[pc1.png]]
![[pc2.png]]
![[pc3.png]]
![[pc4.png]]
![[pc5.png]]

---
## Condición de carrera
- Se dice que múltiple tareas están en condición de carrera cuando su resultado depende del orden en el que éstas se ejecutan
	- Un programa concurrente no debe tener **condiciones de carrera**
- Son un foco de errores en programas y sistemas concurrentes

---
## Parámetros
- Se le pueden pasar parámetros a los hilos
![[parameters.png]]

---
## Variables libres (free)
- Si se usan funciones lambda hay que tener cuidado con sus variables libres
- Cada hilo posee una **copia de la pila** en ejecución **a partir del ámbito en el que se creó** (el resto de la pila se comparte con el thread nuevo)
- Las variables locales ya declaradas serán compartidas por todos los hilos

- Las alternativas son el **paso de parámetros** y la **copia de variables**:
![[vlibres 1.png]]
![[vlibres 2.png]]

---
## Excepciones asíncronas
![[exc asinc.png]]

---
## Context Switch
- El **contexto** de una tarea (hilo o proceso) es la información que tiene que ser guardada cuando éste es interrumpido para que luego pueda reanudarse su ejecución
- El **cambio de contexto** es la acción de almacenar/restaurar el contexto de una tarea para que pueda ser reanudada su ejecución
- Esto permite la ejecución concurrente de varias tareas en un mismo procesador
- El cambio de contexto requiere:
	- **Tiempo de computación** para almacenar y restaurar el contexto de varias tareas
	- **Memoria adicional** para almacenar distintos contextos
- Por tanto, el usar un número elevado de tareas en relación con el número de procesadores puede conllevar una **caída de rencimiento** 

NOTA: cuantos más hilos usemos a partir de cierto punto, peor será el rendimiento ante un algoritmo secuencial

---
## Thread Pooling
- La **creación y destrucción de hilos** es un proceso que también implica un coste computacional y de memoria. Por ello se debe:
	- **Limitar** el número máximo de hilos creados por un proceso
	- Minimizar el número de hilos creados (**reutilizarlos**)

![[thread pooling 1.png]]
![[thread pooling 2.png]]

---
## Foreground y Background Threads
- Hilos **foreground**: la aplicación no finalizará hasta que acabe la ejecución de todos los hilos creados
- Hilo **background** (daemon): aquel que será terminado cuando no queden hilos foreground en ejecución. Normalmente son proveedores de servicios
	- No confundir con hilos secundarios o workers

![[daemon.png]]

---
## Inconvenientes del uso de hilos
- **Condiciones de carrera**: debemos esperar explícitamente (`Join`) hasta que todos los hilos han terminado de realizar sus cálculos
- **Parámetros**: sin parámetros o sólo un objeto, variables libres compartidas
- **Excepciones asíncronas**: las excepciones generadas en un hilo no son capturadas por bloques `try-cath` pertenecientes a un hilo diferente
- **Rendimiento de los cambios de contexto**: no hay optimización automática del número de hilos creados. Si el número es demasiado alto no se consigue mejorar el rendimiento e incluso se empeora

---
# Tasks
---
## Tareas
- Tiene un nivel de abstracción mayor que los hilos y proporcionan más funcionalidades, facilitando la programación paralela
- Una **Task** representa una operación asíncrona y su uso tiene dos beneficios principales:
	- **Uso más eficiente y escalable de recursos** (el número óptimo de hilos que esté ejecutando el proceso se determina automáticamente)
	- **Mayor control de ejecución** (comparado con Thread)

---
## Creación y ejecución explícita de tareas
- Una tarea que no devuelve valores está representada por la clase `System.Threading.Tasks.Task`
- Una tarea que devuelve valores está representada por la clase `System.Threading.Tasks.Task<TResult>`
- Para crear una task es necesario suministrar un delegado que encapsule el código a ejecutar
- La propiedad `Status` permite consultar si una tarea ha empezado a ejecutarse, se ha terminado, cancelado, ...
- La propiedad `Wait` espera hasta que la tarea termine

![[crearcion.png]]
- Método `Run`

![[metodo run.png]]

- Método `WaitAll`
![[waitall.png]]

- Propiedad Result: se bloquea si la tarea no ha terminado
![[result.png]]

- Cuando se usa una expresión lambda como código de una tarea, las variables libres que ya han sido creadas son compartidas por todas las tareas que la usen
![[expr lambda.png]]

- state object
![[state object.png]]

- async state
![[async state.png]]

---
## Composición de tareas
- `Task` y `Task<TResult>` tienen varios métodos para componer tareas:
	- `Task.WhenAll`: espera de forma asíncrona a que terminen **varios** objetos `Task` o `Task<TResult>`
	- `Task.WhenAny`: espera de forma asíncrona a que terminen **uno o varios** objetos `Task` o `Task<TResult>`
	- `Task.Delay`: crea un objeto `Task` que acaba tras un tiempo determinado

![[composicion 1.png]]
![[composicion 2.png]]

---
## Manejo de excepciones con tareas
- Cuando una tarea lanza una o varias excepciones, todas ellas se encapsulan en una excepción de tipo `AggregateException`
- Esta excepción se propaga al hilo vinculado a la tarea
- Se podrán tratar con un `try/catch` en los siguientes métodos:
	- Wait
	- WaitAll
	- WaitAny
	- Result

![[exceptions.png]]

---
## Paso asíncrono de mensajes
- Un método para crear hilos es el paso de mensajes asíncrono, cada mensaje crea un nuevo hilo
- En C# esto se obtiene mediante delegados
- **Síncrono** -> secuencial

![[sinc asinc.png]]

- Paso síncrono de mensajes:
![[sin 1.png]]
![[sin 2.png]]

- Paso asíncrono de mensajes:
	- Existen las palabras reservadas `async` y `await`
	- Forma antigua:
	![[asinc 1.png]]
	
- Un método async normalmente devuelve una `Task` o `Task<Result>` que representa el trabajo que se está realizando en el método
- Esta tarea tiene información que puede usar quien ha invocado el método asíncrono
- El operador `await` se aplica sobre la Task devuelta por un método `async`
	- `await` no se puede usar sobre métodos que no sean asíncronos
- `await` nos asegura que la Task finaliza antes de continuar con la ejecución

---
## Uso de async y await
- El operador `await` dice al compilador que el método `async` no puede continuar la ejecución hasta que el método asíncrono esperado no haya completado su ejecución
- Si un método `async` no usa operadores `await`, se ejecuta como un método síncrono

![[async await.png]]

- De forma concurrente:
![[concurrent async.png]]

---
## Características de los métodos Async
- No puede usar parámetros **ref** o **out**, pero puede llamar a métodos que los tenga
- Devuelven una `Task` o una `Task<TResult>`
	- Esta Task encapsula información sobre el estado del método asíncrono (el resultado o la excepción que se pudo producir)
	- Si se especifica `Task<TResult>` el método ha de tener una sentencia **return**
	- Se puede usar Task si el método no tiene **return**
- Se puede devolver **void**, pero no se puede hacer un `await` a esos métodos
	- En ese caso se le puede pasar una función como parámetro para que se invoque cuando el método `async` finalice (**función de Callback**)
-  En un método `async`, un operador await se aplica a una Task que es devuelta de invocar a otro método `async`

---
## Sincronización de Hilos
- Un mecanismo básico es el `Thread.Join`, que permite que un hilo espere a la finalización de otro
- La necesidad más típica de sincronización de hilos es por acceso concurrente a recursos compartidos
- Evitar el uso simultáneo de un recurso común se denomina **exclusión mutua**
- Una **sección crítica** es un fragmento de código que accede a un recurso compartido que no debe ser accedido concurrentemente por más de un hilo de ejecución
- La sincronización de hilos debe usarse para conseguir la **exclusión mutua**

![[exclusion mutua.png]]

---
## Lock
- Es la principal técnica para sincronizar hilos en C#
- Consigue que únicamente un hilo pueda ejecutar una **sección crítica** simultáneamente -> **exclusión mútua**
- Requiere especificar un objeto (referencia) como parámetro
````c#
lock(referencia){
	seccion critica
}
````
- Si otro hilo ejecuta el lock sobre un objeto que ya está bloqueado, entonces se podrá en modo de espera y se bloqueará hasta que el objeto sea liberado

![[lock 1.png]]
![[lock 2.png]]
![[lock 3.png]]

---
## Asignaciones
- No todas las asignaciones son atómicas: 
![[asignaciones 1.png]]
![[asignaciones 2.png]]

- Por tanto, las asignaciones multihilo de una misma variable deben sincronizarse
- Una alternativa es usar **lock**
- Otra alternativa es usar métodos de la clase `Interlocked (System.Threading)`
	- Es mucho más eficiente que usar **lock**
	- Los métodos más usados son:
		- Increment
		- Decrement
		- Exchange

![[ejecucion 1.png]]
- Mostrará un valor Random, ya que se está accediendo al recurso compartido valor

![[ejecucion 2.png]]
- Mostrará 0

---
## Mutex y Semaphore
- La sincronización entre procesos se puede conseguir con **mutex** y **semáforos**
- Un **Mutex** es un mecanismo de sincronización entre procesos (también válido entre hilos)
	- Su funcionamiento es similar al **lock**
	- Su coste de rendimiento es mucho mayor al de **lock**
	- Sólo puede haber un mutex con el mismo nombre
- Los **semáforos** permiten el acceso a n procesos (o hilos) concurrentes
	- Se suelen usar para limitar la concurrencia (acotar un número máximo de hilos/procesos)

![[mutex 1.png]]

---
## Interbloqueo (deadlock)
- Se produce un **interbloqueo** entre un conjunto de tareas si todas y cada una de ellas están esperando por un evento que sólo otra puede causar
- Todas las tareas se bloquean permanentemente
- El caso más común es el acceso a recursos compartidos

Interbloqueo:
![[deadlock 1.png]]

Sin interbloqueo:
![[deadlock 2.png]]

---
## Condición de espera circular
![[cecirc.png]]

---
## Evitando el interbloqueo
- El **interbloqueo** se evita impidiendo que se dé la condición de espera circular
- Para ello, hay que saber los recursos que necesita cada proceso
	- La **obtención de recursos** debe ser llevada a cabo de forma que el sistema no entre en un **estado inseguro** (no pueden darse interbloqueos)
	- No siempre es posible conocer los recursos de un proceso en tiempo de compilación, pues dependen de su ejecución (**valores dinámicos**)

- Podemos evitar la espera circular:
	- De forma directa:
	![[forma directa.png]]
	
---
## Thread Safety
- Se dice que un programa, método o función es **thread-safe** si funciona correctamente cuando es usada por varios hilos simultáneamente
- **El hecho de programar usando elementos thread-safe, no implica que el código sea thread-safe**

---
## Estructuras de datos Thread-Safe
![[estructs thread safe.png]]

---
## Implementación EEDD Thread-Safe
![[eedd safe.png]]
![[eedd safe 2.png]]
![[eedd safe 3.png]]
- En este caso, se trata de una composición
- La clase de la izquierda usa a la clase de la derecha.

- Para realizar un **lock** es mejor usar el *this* porque la referencia es pública, en lugar de ser privada (this.lista).
- Esto puede afectar al rendimiento del programa o incluso generar interbloqueos.
- Es una implementación sencilla pero ineficiente.
- El **lock** no permite diferenciar entre lectura y escritura. No se deben de bloquear dos operaciones de lectura, pero sí dos de escritura de forma simultánea.
- Las escrituras deben bloquear a otras lecturas y escrituras
- Para ello se añadió la clase `ReaderWriterLockSlim`

---
## ReaderWriterLockSlim
- Permite proteger un recurso compartido por varios hilos de ejecución de forma más eficiente que **lock**
- Permite a los hilos bloquear el acceso a un recurso de tres modos:
	- **Modo de lectura**: puede haber cualquier número de hilos sobre una misma instancia ReaderWriterLockSlim sin ser bloqueados
	- **Modo de escritura**: si un hilo en ejecución ha entrado en un bloqueo en este modo sobre una instancia ReaderWriterLockSlim, ningún otro puede entrar en el bloqueo sobre ella en cualquiera de los tres modos.
		- Tiene **acceso exclusivo** al recurso
		- Todos los demás hilos esperarán a que se libere	
	- **Modo de lectura actualizable**: bloqueo de lectura especial que puede actualizarse a modo de escritura sin tener que abandonar el acceso de lectura al recurso
		- Solo puede haber un hilo en ejecución en este modo
		- El hilo que ha bloqueado puede acceder a la sección crítica al mismo tiempo que otros hilos que han bloqueado a la instancia en modo lectura
	
	- El código protegido por ReaderWriterLockSlim no puede tener llamadas recursivas
	- Esto disminuye la posibilidad de interbloqueos y mejora el rendimiento

---
# TPL y PLINQ
---
## Task Parallel Library (TPL)
- Ofrece las siguientes ventajas:
	- Simplifica la paralelización de aplicaciones
	- Escala dinámicamente el número de hilos creados en función del número de cores
	- Escala y gestiona dinámicamente el número de hilos creados en función del Thread Pool
	- Ofrece paralelización mediante la división de datos procesados
	- Ofrece paralelización mediante tareas independientes

- Ofrece un modelo mucho más declarativo de implementar aplicaciones paralelas

---
## Data Parallelism con TPL
- Los dos métodos más usados son **ForEach** y **For** de la clase `System.Threading.Tasks. Parallel`
	- Ambos reciben la tarea a ejecutar como un delegado (Action)
	- **ForEach** crea potencialmente un hilo por cada elemento de un **IEnumerable**
	- **For** crea potencialmente un hilo a partir de un **índice** de comienzo y final, no incluyendo el final
	- Añade una sincronización para que en la siguiente instrucción todos los hilos hayan finalizado

![[data parallelism tpl.png]]

---
## Task parallelism con TPL
- Para obtener la paralelización mediante división de tareas independientes, TPL ofrece el método `Invoke` de la clase `Parallel`
	- Recibe una lista variable de delegados de tipo Action
	- Crea un hilo por cada Action pasado
	- Añade una sincronización para que en la siguiente instrucción todos los hilos hayan finalizado

![[task parallelism.png]]

---
## Parallel LINQ
- Es una implementación paralela de LINQ
- Comparación PLINQ - LINQ
![[comp linq.png]]
![[linq plinq.png]]

---
## Ley de Amdahl
- La mejora de rendimiento de un programa completo está limitada por el tiempo de ejecución de la parte secuencial de dicho programa
- Cuanto más tiempo de eejecución tenga la parte secuencial, menor mejora de rendimiento tendrá la aplicación completa paralela

---
## MapReduce
- Modelo de programación de aplicaciones paralelas (distribuidas) mediante división de datos
- Hace uso de dos funciones de orden superior:
	- **Map**: procesa los elementos de una lista y genera otra
	- **Reduce (fold)**: procesa los elementos de una lista generando un valor
- MapReduce trabaja con diccionarios (clave, valor) en lugar de con listas

---
Siguiente lección -> [[Tipado dinámico y Metaprogramación 👽]]