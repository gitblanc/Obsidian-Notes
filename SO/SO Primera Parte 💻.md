# ---TEMA 1, introducción 🐳---
---
# 1 Febrero 2022 🌐
---
![[procesador.png]]

---
# 3 Febrero 2022 ♿️
---
- **ROM:** sólo lectura. Direcciones más bajas. En ella se encuentra la BIOS. Es una memoria **no volátil**, es decir, cuando el ordenador está apagado hay una pequeña zona de la memoria con código.
- Intrucción **TRAP:** intrucción que genera una interrupción que no se corresponde con ningún comportamiento anormal. Permite buscar información en otros sitios, haciendo que se salte a otro programa.
- **Tabla de vectores de interrupción:** estructura de datos que asocia una lista de manejadores de interrupciones con una lista de solicitudes de interrupciones.
- **iRET:** coge lo que hay en la memoria y lo pasa a los registros.

NOTA: siempre que se ejecuta el SO se genera una interrupción.
NOTA: cuando se produce una interrupción no tiene por qué tomar el control el SO

---
# 8 Febrero 2022 🔆
---
- **Llamada al sistema:** nombre alternativo para las funciones incluídas en la API del sistema operativo.
- **API:** primera interfaz que ofrece el SO. A través de esta capa se comunican los programas.
- El usuario interacciona con el SO a través de una interfaz de usuario.
---
## Tipos de sistemas operativos
---
- **Estructurados por capas:**
 ![[so por capas.png]]
- Problemas: de diseño (qué meto en cada módulo y cuantos módulos tengo), imposible de jerarquizar, y de rendimiento.
---
- **Estructurado micronúcleo:** 
![[micronucleo.png]]
- Ventajas: se puede "parar en caliente" (Se ejecuta menos tiempo en modo núcleo que en uno monolítico).
- Problemas: para cualquier operación hay muchos mensajes. Para cada mensaje hay que cambiar entre usuario y núcleo. Pésimo rendimiento, peor que uno monolítico.
---
- **Híbridos:** aprovechan lo mejor de los monolíticos y los estructurados, haciendo una mezcla.
---
- **Distribuídos:**
	1. Puro:  el hardware que controla pertenece a máquinas distintas.
	2. Middleware: capa software por encima del SO que permite compartir recursos entre sí.
---
# 15 Febrero 2022 🍀
---
- Al principio no se trabajaba por lotes, se usaban tarjetas perforadas (procesamiento en serie).
- **Multiprogramación (años 60):** sistema que en el momento en que un programa pasa a E/S, se ejecuta otro programa, es decir, se aprovechan los tiempos muertos de cada programa.
- Surgen los miniordenadores (años 70).
- **Llamada al sistema:** manera de decir que un programa de usuario invoca a una función del SO a partir de la API.
---
# ---TEMA 2, gestión de procesos 🦚---
---
# 17 Febrero 2022 🍄
---
- **Proceso:** programa en ejecución.
- **Recursos necesarios de los procesos:**
	- Tiempo de CPU
	- Memoria
	- Archivos
	- Dispositivos de E/S
- Los recursos se asignan a un proceso cuando se crea o durante la ejecución.
- Los procesos son dinámicos (vivos). Cambian durante su ejecución.
---
- **Funciones del SO como gestor de procesos:**
	- Creación, gestión y eliminación de procesos.
	- Planificación de procesos.
	- Sincronización y comunicación de procesos.
	- Bloqueos mutuos.
- **Sobrecarga:** trabajo adicional que hace la CPU para ejecutar el SO.
---
- _Un proceso es_:
	- Texto
	- Datos, variables globales y memoria dinámica
	- Pila, datos temporales
	- Situación actual del procesador (valor del PC, palabra de estado PSW, registros)
	- Información de otros recursos
	- Información de control
---
- **PCB**
	- Contiene los elementos de un proceso
	- Hace posible interrumpir un proceso y después retormar la ejecución
	- Creado y gestionado por el SO
	- Soporte de múltiples procesos
---
# 22 Febrero 2022 🐚
---
NOTA: la zona de memoria de un proceso es privada, lo que sí comparte es la CPU.

- ¿Qué tipo de interrupciones provocan sí o sí un cambio de proceso en ejecución?
	- Llamada al sistema cuando un proceso termina.
	- Se le acaba el tiempo de ejecución al proceso.
---
# 24 Febrero 2022 🌺
---
- **Planificador:** responsable de decidir los procesos que pasan de estado listo a ejecutándose.
- **Despachador:** pasa el proceso a ejecutando.
- **Proceso swapped:** que no está en memoria.

- **PLP (planificador a largo plazo) ->** admite y activa procesos. Aumenta la multiprogramación.
- **PMP (planificador a medio plazo)->** suspende procesos. Los lleva a memoria secundaria y decrementa la multiprogramación.
- **PCP (planificador a corto plazo) ->** despacha procesos.
---
#### Planificaciones
- **Sin requisamiento/no expulsivas:** sólo hay un cambio de proceso cuando este termina.
- **Con requisamiento/expulsivas:** hay otros motivos para cambiar de proceso.
- **FIFO:** first in first out.
	- Cuando un proceso está listo para ejecución se coloca al final de la cola.
	- Los procesos abandonan voluntariamente la CPU.
	- Cuando la CPU queda libre el planificador elige al proceso en la cabeza de la cola de listos.
- **SJF:** primero el más corto
	- Se elige el proceso con menor duración total.
	- Exige conocer el tiempo de ejecución antes de ejecutar el trabajo.
	- Política no expulsiva.
	- Puede provocar inanición de procesos largos (el sistema nunca otorga recursos al proceso largo).
- **Planificación cíclica o turno rotatorio:**
	- Consigue un reparto equitativo del procesador.
- **Planificación basada en prioridades:**
	- La cola de listos está ordenada por prioridad.
		- Tipos de prioridad:
			- **Estática:** fija durante toda la vida del proceso
			- **Dinámica:** varía durante la vida del proceso
		- Esta política se combina con otras.

NOTA:  
Políticas actuales: combinación de políticas expulsivas  
Colas multinivel con Prioridades dinámicas + Turno rotatorio

---
# 1 Marzo 2022 🪐
---
- **Hilo:** flujo de ejecución dentro de un proceso. 
- Puede haber varios hilos dentro del mismo programa. 
- Todos los hilos forman parte del mismo proceso.
- Todos los recursos son compratidos, salvo lo que ejecutan en cada momento (no comparten PC, registros, Pila).
- **ULT:** Todas las operaciones con hilos se realizan a nivel de usuario (operaciones mucho más rápidas, pero sin paralelismo).
- **KLT:** las operaciones con hilos se realizan a nivel de kernel (más lentas pero con paralelismo).
---
# ---TEMA 3, concurrencia 🐿---
---
- La concurrencia aparece con la multiprogramación.
- El primer programa concurrente que aparece es el SO.
- **Condicion de carrera:** el resultado del programa no siempre es el mismo con los mismos datos.
---
### Mecanismos de sincronización
- Semáforos
- Mutex
- Variables condicionales
- Señales
---
### Mecanismos de comunicación
- Archivos o ficheros
- Pipes
- Memoria compartida
- Mensajes
---
- **Pipes:** ficheros donde un proceso escribe por un lado mientras que otro lee. Puede haber varios procesos escribiendo/leyendo a la vez. La sincronización está garantizada.
---
### Tipos de comunicación
- **Síncrona total:** emisor dormido hasta que el receptor recibe el mensaje.
- **Síncrona intermedia:** emisor no se duerme pero el receptor se bloquea hasta que recibe el mensaje.
- **Asíncrona:** nadie espera.
---
NOTA: los procesos envían mensajes a los buzones y los reciben de buzones.
![[buzones.png]]

- **Interbloqueo:** se produce cuando un proceso se encuentra esperando a un proceso que no puede ocurrir.
- Estrategias para evitar el interbloqueo:
	- Ignorar (actualmente usada)
	- Detectar y recuperar
	- Evitar
	- Prevención
---
# ---TEMA 4, gestión de memoria 🦖---
---
# 10 Marzo 2022 🌊
---
- Un proceso no puede acceder a la dirección de memoria de otro proceso.
- Actualmente la gestión de memoria resuelve aspectos como:
	- Carga y ubicación de programas
	- Traducción de direcciones lógicas a físicas
	- Presencia simultánea de más de un programa
	- Posibilidad de cargar rutinas en tiempo de ejecución (dll)
	- Compartición de memoria por varios programas
	- Ejecución de programas que no caben completos
	- Gestión eficiente del espacio libre
	![[jerarquia de memoria.png|500]]
	---
	- En ejecución el programa debe acceder a direcciones físicas de memoria principal.
	- En sistemas monoprogramación dir. física = dir. lógica
	- En multiprogramación hay más de un proceso a la vez, cada uno cargado a partir de su dirección base. La dir. física != dir. lógica
---
# 15 Marzo 2022 🍩
---
### Particiones físicas o estáticas
- La memoria real no genera fragmentación externa, porque son particiones estáticas.
- Genera fragmentación interna, ya que el espacio desaprovechado en una partición no puede ser utilizado por otro proceso.
NOTA: fragmentación -> % de memoria desaprovechado
---
### Particiones variables o dinámicas (más complicadas)
- **Condensación de huecos:**  si hay dos particiones libres adyacentes se juntan en una sola.
- **Compactación:** mover todos los procesos y los huecos a otra parte de la memoria.
---

♻️ Segunda parte -> [[SO Segunda Parte 🖥]]