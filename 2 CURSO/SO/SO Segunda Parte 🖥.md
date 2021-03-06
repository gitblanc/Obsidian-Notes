鈾伙笍 Primera parte -> [[SO Primera Parte 馃捇]]
# 17 Marzo 2022 馃Ж
---
- El mapa del proceso se crea en el disco. Se usa asignaci贸n no contigua.
---
### Principio de localidad de referencias
- **Temporal:** es bastante probable que una referencia se repita. Contribuyen mucho los bucles.
- **Espacial:** si accedo a una posici贸n de memoria, en un futuro es posible que acceda a posiciones cercanas a esta.
---
### Ventajas de la Memoria Virtual
1. El tama帽o del proceso puede ser mayor que el de la propia memoria.
2. Aumenta el grado de multiprogramaci贸n.
3. La gesti贸n corre a cargo del procesador.
---
- **Paginaci贸n:** se siguen criterios f铆sicos (se divide el proceso en trozos de igual tama帽o).
- **Segmentaci贸n:** se siguen criterios l贸gicos (se tiene en cuenta el contenido del proceso).
---
### Memoria virtual, paginaci贸n
![[paginacion.png]]

---
---
# 22 Marzo 2022 馃尳
---

### Memoria virtual, segmentaci贸n
---
2. *Mediante segmentaci贸n:*
	- Se divide el proceso siguiendo procesos l贸gicos, agrupando en cada segmento datos relacionados entre s铆. 
	- Tendremos una tabla de segmentos que tendr谩 informaci贸n sobre cada segmento.
	- La memoria se divide en trozos de distinto tama帽o.
	- Es m谩s compleja.
	- Ahora tenemos la direcci贸n de comienzo del segmento.
	- Ahora se hace una suma, mientras que antes se concatenaba.
	
	**Ventajas**
	- Aumenta la multiprogramaci贸n.
	- Contempla la gesti贸n de regiones, un segmento puede ser compartido por varios procesos.
	
	**Desventajas**
	- Problemas de gesti贸n de almacenamiento real.
	- Es m谩s complejo
3. *Segmentaci贸n+paginaci贸n*
	- Necesitamos una tabla de segmento por proceso.
	- La traducci贸n es m谩s complicada.
	- Requiere dos accesos adicionales, por tanto el tiempo de traducci贸n es mayor que en paginaci贸n, ya que requiere un acceso m谩s.
	
	Ventajas
	- Multiprogramaci贸n, protecci贸n de procesos,...
	Inconvenientes
	- M谩s lento, complicado,...
---
### Decisiones de dise帽o
1. Dependientes del Hardware
	- Paginaci贸n, segmentaci贸n, segmentaci贸n con paginaci贸n.
2. Dependientes del Software
	- Qu茅 hacer cuando se produce un fallo de p谩gina, mediante el **sistema operativo**.
	- Un **fallo de p谩gina** es una excepci贸n que se genera cuando la p谩gina buscada no est谩 en memoria.
---
##  Administraci贸n del almacenamiento virtual 馃オ

### Pol铆tica de lectura
Determina cuando se debe cargar un programa en memoria.
- **Paginaci贸n por demanda:** se traen a memoria cuando se produce el fallo.
- **Prepaginaci贸n:** se traen a memoria varias p谩ginas contiguas. Mayor eficiencia de carga. Es m谩s eficiente leer un bloque grande una vez que 4 veces bloques peque帽os.
Generalmente se suele usar prepaginaci贸n.
---
### Pol铆tica de reemplazo
Determina qu茅 p谩gina se reemplaza eb memoria principal cuando se debe cargar otra y no hay espacio para ella.
- **Alcance global:** se reemplaza una p谩gina de cualquier proceso en memoria.
- **Alcance local:** una p谩gina del proceso que la necesita.
---
### Pol铆tica de asignaci贸n
Determina cu谩ntos marcos se asignan a un proceso.
Busca el n煤mero ideal (Equilibrio):
- Pocas para que quepan m谩s procesos en memoria.
- Suficientes para que no se produzca hiperpaginaci贸n.
```
hiperpaginaci贸n: se generan continuamente fallos de p谩gina.
```
Estrategias de asignaci贸n:

- **Fija:** con reemplazo local. No se adapta a las necesidades de memoria del proceso.
- **Din谩mica:** con reemplazo global o local.
---
## Algoritmos de reemplazo b谩sicos 馃, asignaci贸n est谩tica
- 脫ptimo
- LRU
- FIFO
- Reloj
---
### 脫ptimo 鉂?
- Genera el m铆nimo n煤mero de fallos de p谩gina.
- Reemplaza la p谩gina que tardar谩 m谩s tiempo en volver a usarse.
- Es imposible de implementar.
---
### FIFO (first in first out)
- Reemplaza la p谩gina que m谩s tiempo lleva en memoria.
- Sencillo de implementar.
- P茅simo rendimiento.
- Sufre la anomal铆a de Belady, si un proceso tiene m谩s marcos de p谩gina asignados, m谩s fallos se generan.
---
### LRU 鉁?
- Reemplaza la p谩gina que m谩s tiempo hace que no se utiliza.
- Se aproxima bastante bien al algoritmo 贸ptimo.
- Es dif铆cil de implementar.
---
### Reloj o FIFO segunda oportunidad
- Se implementa como una cola circular.
- Cada p谩gina tiene un bit de uso, cuando se accede a la p谩gina se pone a 1. Cuano hay que reemplazar una p谩gina miramos si el bit est谩 a 1, si lo est谩 se pone a 0 y se avanza.
- Comportamiento similar al FIFO.
---
# 29 Marzo 2022 馃殠
---
- **Pol铆ticas de lectura:** cuando leer las p谩ginas
- **Pol铆tica de asignaci贸n:** es la m谩s importante. Interesa asignar el n煤mero justo de marcos a un proceso, porque si asignamos demasiado ese proceso ocupa mucha memoria que no est谩 siendo usada, y si est谩 ocupando demasiado poco puede generar muchos fallos de p谩gina dando lugar a la hiperpaginaci贸n.
---
### Estrategia del conjunto de trabajo
---
- **Conjunto residente:** conjunto de p谩ginas que tiene el proceso cargado en memoria en cada momento. Su tama帽o es el n煤mero de marcos que tiene asignado ese proceso.
- **Conjunto de trabajo:** se calcula en un instante T y para un tama帽o de ventana lambda(鈲?). Es el conjunto de p谩ginas a las que el proceso ha hecho referencia 煤ltimamente. Representa las p谩ginas que hac铆an falta para ejecutar el proceso en ese intervalo de tiempo. Aproxima el comportamiento futuro a trav茅s del comportamiento pasado.

NOTAS:
- Si el proceso tiene en memoria el conjunto de trabajo se produce una baja tasa de fallos de p谩gina.
1. Una p谩gina deber铆a ejeutarse s贸lo si su conjunto de trabajo se encuentra en memoria.
2. Una p谩gina no deber铆a ser retirada de memoria si es miembro del conjunto de trabajo de un proceso.

- Si el proceso falla a menudo, no tiene su conjunto de trabajo cargado. 
- Si hay muchos fallos de p谩gina el proceso tiene pocos marcos.
---
### Buffering de p谩ginas
---
- T茅cnica que almacena cosas que nos vayan a hacer falta (que sean referenciadas) en un futuro (Ej, la cach茅 del procesador).
- En todo momento se mantiene una lista de marcos de p谩gina libres en el sistema.
---
# TEMA 5, Gesti贸n de entrada salida 馃毃
---
- Es importante que el sistema operativo generalice la aceptaci贸n de dispositivos (diversidad).
- Partes de los dispositivos:
![[partes dispositivos.png | 500]]

- Un controlador tiene las siguientes partes:
	- Registro de control
	- Registro de estado
	- Registro de direcci贸n
	- Registro de datos
- Cada registro tiene asignado un puerto
---
# 31 Marzo 2022 馃洨
---
- C贸mo podr铆a planificarse un sistema de entrada salida:
![[funcionamiento Entrada salida.png]]
- **IORB**-> Input Output Request Block, forma de funcionar el manejador independiente de dispositivo.
- **Manejador independiente:**: verifica los par谩metros, crea el IORB y avisa al manejador dependiente del dispositivo (hay uno en el sistema).
- **Manejador dependiente del dispositivo (driver):** Hay uno por cada dispositivo o tipo de dispositivo. Es el driver del dispositivo. Da las 贸rdenes para cumplir la petici贸n (hay uno por cada dispositivo).
---
- **Buffering:** mecanismo acelerador que aparece por ejemplo en la cach茅, que almacena los 煤ltimos bloques de discos accedidos.
- **Spooling:** mecanismo por el cual no hay interbloqueo en los sistemas operativos.
---
# 5 Abril 2022 馃Ы
---
- **El reloj:** se encarga  de la verificaci贸n de que el cuanto del proceso ha terminado.

### Elementos de un disco duro
- Partes f铆sicas
	- Platos
	- Ejes
	- Cabezas de L/e
- Organizaci贸n
	- Caras
	- Pistas
	- Sectores
	- Cilindros
   ![[disco.png|400]]
   驴C贸mo funciona un disco? -> https://www.youtube.com/watch?v=kdmLvl1n82U
   - El disco sabe leer y escribir un sector.
   
### Acciones del disco
- **B煤squeda:** desplazamiento de la cabeza hasta el cilindro correspondiente.
- **Latencia:** espera a que el sector solicitado se alinee con la cabeza de lectura escritura.
- **Lectura/Escritura y transmisi贸n(Transferencia)**

*F脫RMULAS*
- **T acceso** =  T. Bu虂squeda + T. Latencia + T. Lectura/escritura . Es directamente proporcional al n煤mero de pistas.
- **T.Bu虂squeda** = T.Arranque + T.entre pistas * nu虂mero de pistas
- **T. Latencia** : Depende de la velocidad de rotacio虂n

	---
## Planificaci贸n del disco
Pretende:
- Aumentar la productividad del disco
- Disminuir tiempos de respuesta
- Disminuir varianza de tiempos de respuesta (que los tiempos sean semejantes)
- Evitar inanici贸n de peticiones
---
- **FCFS(First Come First Served)**, igual que la FIFO
![[fcfs.png|400]]
 - **SSTF (Shortest Seek Time First)**, 贸ptimo en rendimiento, pero discrimina peticiones
 ![[sstf.png|400]]
 - **Scan y Look**, tambi茅n conocida como pol铆tica del ascensor. 
 Diferencia entre scan y look: El scan siempre hace barridos completos, llega hasta el final, mientras que el loop se ahorra el tramo en el que no quedan peticiones.
 ![[scan look.png|400]]
 - **Scan Circular (C-Scan) y C-look**, en lugar de dar la vuelta mirando las peticiones, al llegar al final se vuelve al principio.
 ![[scan circular.png|400]]
 - NO EST脕 EN DIAPOS-> **Scan o loop N-Pasos**, empieza el recorrido partiendo la cola en dos. Se trata la primera mitad de peticiones en primer lugar. Cuando se termina esa partici贸n, se comienza un nuevo recorrido con otra partici贸n. No hay posibilidad de inanicion.
 ---
# Tema 6, Gesti贸n de ficheros 鉀碉笍
---
- **Sistema de gestor de ficheros:** parte del SO encargada de gestionar los ficheros, crearlos, gestionar la memoria para los accesos, ...
 Funciones:
 - Interfaz de llamadas al sistema
 - Gestionar ficheros
 - Gestionar directorios
 - Gestionar espacio libre
 - Gestionar la cach茅
 - Proporcionar protecci贸n
 - Comunicarse con el Sistema de Gesti贸n de E/S
---
- **Fichero:** abstracci贸n del sistema operativo para almacenar datos de manera persistente. Agrupaci贸n de datos con un nombre.

### M茅todos de acceso
- Secuencial
- Directo por direcci贸n
- Directo por clave
---
- El SO guarda la informaci贸n de los ficheros en un **Descriptor del Fichero**.
---
# 7 Abril 2022 鈾匡笍
---
- El disco se organiza en bloques.
- Los ficheros se dividen en bloques.
- Dos posibilidades de asignaci贸n:
	- **Contigua:** bloques consecutivos
	- **No contigua:** bloques no consecutivos
---
### Asignaci贸n contigua
- Alta fragmentaci贸n externa.
- No es adecuado para ficheros con alta volatibilidad. Se usa en ficheros que se usen muy poco.
---
### Asignaci贸n no contigua
- Rendimiento pobre.
	#### Asignaci贸n enlazada
	![[enlazada.png|500]]
	#### Asignaci贸n con FAT
	- Usado en dispositivos externos (SD, usb).
	- Cada entrada es de 32 bits.
  ![[fat.png|500]]
	#### Asignaci贸n indexada con tabla de 铆ndices
  ![[indexada.png|500]]
	#### Asignaci贸n indexada con 谩rboles equilibrados
	![[arboles.png|500]]
---
## Directorios
- Asocia los nombres que el usuario le da al fichero con el descriptor interno usado por el sistema operativo.
Estructura y almacenamiento de los directorios:
-En los **FAT**, Los directorios son ficheros que contienen un descriptor para cada fichero o directorio (un directorio dentro de otro) que almacenan y su nombre.
- En los **ficheros indexados**, son ficheros que contienen un descriptor para cada fichero o directorio (un directorio dentro de otro) que almacenan y el n煤mero del descriptor de ficheros.
---
## El sistema de ficheros
- Los discos se dividen en una o varias particiones.
-  **Sistema de ficheros:** modo de organizacio虂n de la informacio虂n en el disco, en un formato inteligible para el sistema operativo
---
