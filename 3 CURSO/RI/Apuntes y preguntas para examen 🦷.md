# Apuntes

## JDBC 🪖

- **JDBC** es una API Java, clases e interfaces, que permite a aplicaciones Java acceder a fuentes de datos mediante la ejecución de sentencias SQL. Incluye métodos para:
	- Establecer una conexión entre cliente y SGBD
	- Ejecutar sentencias SQL
	- Recibir los resultados o errores y procesarlos
 El fabricante debe proporcionar un **driver**

- **Driver**: conjunto de clases que implementan la API JDBC formando adaptadores que:
	- Crea y mantiene las conexiones con la BBDD
	- Traduce las llamadas a métodos JDBC del cliente en llamadas nativas a la API del DBMS
	- Convierte tipos SQL en clases Java y viceversa, los envía al cliente o al SGBD
	- Convierte las condiciones de error en excepciones
 Los drivers se cargan y utilizan en tiempo de ejecución en el lado del cliente

### Características JDBC

- **Independencia de la base de datos**: el cliente es independiente de los detalles de trabajar con una BBDD u otra
- **Mapeo objeto-relacional**: virtualización de una BBDD orientada a objetos sobre la relacional

### Arquitectura JDBC

![[Pasted image 20230103105809.png]]

### Proceso de desarrollo

![[Pasted image 20230103105955.png]]


- Para soliccitar la conexión a la BBDD se usa el Driver Manager:
````java
Connection c = DriverManager.getConnection(url, user, pass);
````
- DriverManager itera a través de los drivers registrados y les pide la conexión. Si el driver no es compatible con el protocolo, devolverá **null**, sino crea la conexión y devuelve un objeto `java.sql.Connection` 

- **ResultSet**: es un **proxy** que virtualmente contiene filas y columnas y ofrece métodos para recuperarlos y procesarlos
````java
ResultSet rs = st.executeQuery(query);
````

### Métodos para leer los datos

````java
getXXX(String field);
getXXX(int columnnField);
previous(); //navega a la fila anterior
first(); //navega hasta la primera fila
last(); //navega hasta la última fila
beforeFirst(); //si después ejecutamos next, devuelve la primera fila
afterLast(); //si después ejecutamos previous devuelve la última fila
relative(int numOfRows); //navega hacia delante o atrás unas filas desde el cursor
absolute(int rowNumber); //navega a la fila indicada
````

- Es importante liberar los recursos en memoria usando el método **close()** (Connection, Statement y ResultSet)
- No hay que dejar que el ususario final vea los errores de la BBDD

### Esquema del proceso de desarrollo

![[Pasted image 20230103112125.png]]

### Interfaz Statement

- **Statement**:
	- Para ejecutar consultas SQL estáticas en tiempo de ejecución
	- Aceptable si la sentencia se ejecuta únicamente una vez
	- Sentencia completamente construida antes de ejecutarla
	- Útil principalmente para sentencias DDL CREATE, ALTER, DROP, ...
	- Rendimiento pobre
- **PreparedStatement**:
	- Para ejecutar repetidamente una consulta
	- Para parametrizarla en tiempo de ejecución
	- Mejor rendimiento
	- Mayor seguridad contra inyecciones SQL
- **CallableStatement**
![[Pasted image 20230103113554.png]]


### Tipos de ResultSet

- **ResultSet Type**: establece la navegabilidad, posicionamiento y sensibilidad del ResultSet
- **ResultSet concurrency**: determina si el objeto ResultSet es read-only o puede ser modificado

### Type

- **Type-forward-only**: sin scroll, sin posicionamiento, insensible a cambios en la BBDD
- **Type-scroll-insensitive**: scroll, posicionamiento, insensible a cambios en la BBDD (a menos que se ejecute nuevamente la consulta)
- **Type-scroll-sensitive**: scroll, posicionamiento, sensible a cambios en la BBDD

### Concurrency

- **Concur_read_only**: el ResultSet no puede ser actualizado
- **Concur_updatable**: el ResultSet puede ser actualizado

### ¿Puede un objeto ResultSet ver los cambios realizados al propio ResultSet?

![[Pasted image 20230103114830.png]]

### Pool de conexiones

- Es una caché de objetos *Connection* cuyo objetivo es reducir la sobrecarga derivada de conectarse a la base de datos. Son reutilizables.
![[Pasted image 20230103115058.png]]

### Transacciones

- Una **transacción** es una secuencia de una o más operaciones (lectura/escritura) que refleja una única operación en el mundo real
![[Pasted image 20230103115821.png]]

- Por defecto cada sentencia SQL individual se ejecuta de forma transaccional (*AutoCommit = true*)
- Una transacción finaliza cuando:
	- termina la conexión actual
	- **Commit** implícito o explícito
	- **Rollback** que hace que se cancele

### Propiedades de las transacciones (ACID)
- **Atomicity**: las instrucciones agrupadas en una transacción son atómicas (o todas o ninguna)
- **Consistency**: cualquier transacción debe conducir la BBDD de un estado consistente a otro estado consistente. **Durante** se adminten temporalmente datos inconsistentes, pero **al finalizar** sólo datos consistentes que cumplan las restricciones (clasves primarias, valores negativos...)
- **Isolation**: aunque varias transacciones se ejecuten concurrentemente, el efecto final debe ser el mismo que si cada transacción se ejecutase una tras otra. Las transacciones han de ser **ejecutadas completamente** o que el SGBD maneje los detalles de intercalar varias transacciones
- **Durability**: una vez que la transacción ha sido confirmada (**commited**), sus efectos deben ser permanentes, incluso si después falla el sistema

### Concurrencia, Planificación y Serialización

![[Pasted image 20230103120921.png]]

- **Planificación**: intercalado de operaciones de un conjunto de transacciones. El planificador decide el plan de ejecución (planificación). Hay dos tipos:  
- ![[Pasted image 20230103121303.png]]
	- **Serie**: las operaciones no se intercalan, se ejecutan una tras otra ![[Pasted image 20230103121409.png]]
	- **Serializable**: su efecto en la BBDD es el mismo que alguna planificación serie

### Comprobar si una planificación es serializable

![[Pasted image 20230103121811.png]]

![[Pasted image 20230103122013.png]]

### Dirty read / Lectura sucia

![[Pasted image 20230103122513.png]]

### Unrepeatable read / Lectura no repetible

![[Pasted image 20230103122624.png]]

### Phantom read / Lectura fantasma

![[Pasted image 20230103122838.png]]

### Inconsistent read / Lectura inconsistente

![[Pasted image 20230103122929.png]]

### ¿Cómo gestionar los conflictos?

- Han de evitarse empleando un mecanismo de bloqueo, pesimista o Lock-based Concurrency Control
- Cada lectura requiere un bloqueo compartido (**shared lock**) 
- Cada escritura requiere un bloqueo exclusivo (**exclusive lock**)
- El bloqueo genera competencia por los recursos

### Control de concurrencia basado en versiones

![[Pasted image 20230103123445.png]]

### Niveles de aislamiento

1. Lectura no confirmada (Read Uncommited)
2. Read committed
3. Repeatable read
4. Serializable

### Anomalías vs Niveles de aislamiento
![[Pasted image 20230103161028.png]]

### Atributos de calidad para el software
- **Escalabilidad**: a medida que el sistema crece, qué alternativas razonables existen de lidiar con ese crecimiento
- **Mantenibilidad**: costes relativos a la reparación o actualización a lo largo de su vida útil
- **Reusabilidad**: capacidad del softwar de ser reusado en otras aplicaciones
- **Extensibilidad**: facilidad de adaptar el software a los cambios sin modificar lo que ya existe

### Patrones

#### 1. Separación en capas

- Secuencia ordenada de capas donde cada capa ofrece servicios que pueden ser usados por componentes que residen en la capa superior
- Cada capa expone a la capa superior una **interfaz** simple para usar un sistema potencialmente complejo
- Cada capa llama a métodos de la API de la capa inferior
	- La capa de **presentación** se ocupa del cliente
	- La capa de **negocio** implementa las reglas del problema
	- La capa de **acceso a datos** interactúa con los datos persistentes ![[Pasted image 20230103124528.png]]

#### 2. Fachada / Façade

- Proporciona una interfaz sencilla (pero limitada) a un conjunto de objetos existentes (sistema complejo)
- Los clientes interactúan con el subsistema a través de la fachada pero ésto no impide el acceso a las clases del subsistema
- Podría haber más de una interfaz para el mismo subsistema
- Oculta los detalles detrás de la interfaz 
![[Pasted image 20230103125048.png]]

#### 3. Factoría simple / Class Factory

- Una clase Simple Factory es una clase que crea objetos sin mostrar al cliente la lógica de creación de instancias
![[Pasted image 20230103130322.png]]

#### 4. Patrón DAO (Data Access Object)

- Permite aislar la lógica de negocio de la persistencia interponiendo un interfaz abstracta. Esto permite que ambas capas evolucionen por separado sin saber nada una de la otra
- Proporciona métodos CRUD: inserción, actualización, borrado y consulta de información
![[Pasted image 20230103130636.png]]

#### 5. Row Data Gateway

- Actúa como un gateway de un único registro en una fuente de datos
- Representa exactamente una única fila devuelta por una consulta
- Cada columna de la tabla es un campo del objeto
- No tiene lógica de dominio

#### 6. Table Data Gateway (TDG)

- Encapsula los datos de una tabla o vista de una base de datos
- Un gateway para cada tabla
- Con una única instancia se gestiona el acceso a todas las filas de una tabla
- Getters retornan colecciones de DTO
![[Pasted image 20230103131055.png]]

#### 7. Service Layer

- Define los límites de una aplicación con una capa de servicios que establece el conjunto de operaciones disponibles y coordina la respuesta de la aplicación en cada operación
- Controla las transacciones
![[Pasted image 20230103131356.png]]

#### 8. Transaction script

- Organiza la lógica de negocio por procedimientos donde cada procedimiento implementa una sóla solicitud de la capa de presentación
- Usa TDGs
- Usa DTOs

#### 9. Command

- Convierte una solicitud en un objeto independiente que contiene toda la información sobre la solicitud

---
## JPA 🦜

### Entidades y Value Types

- **Entidades**: tienen identidad propia, evolucionan a lo largo del tiempo y participan en asociaciones
- **Value Types**: no se necesita conocer su identidad, sólo su valor (String, Date, Time, Integer...). Son atributos de entidades y su ciclo de vida está ligado al de la clase

### Identidad

- En Java:
	- **Identidad** (a == b), *dos referencias apuntan al mismo objeto*
	- **Equivalencia** (a.equals(b)), *dos objetos representan la misma cosa*
- En BDD relacional:
	- La **clave primaria** define la identidad (no hay dos filas con la misma clave)

Hay 3 identidades:
![[Pasted image 20230103155735.png]]

### ¿Cómo vincular la identidad de la entidad con la identidad Java y la clave primaria?
A través de *equals()* y *hashCode()*

### Encapsulación
![[Pasted image 20230103160552.png]]

### Asociaciones
![[Pasted image 20230103155947.png]]

### Concurrencia

Para controlar las transacciones ACID se usa una única caché por hilo y la BDD gestiona las transacciones

### Implementación de asociaciones
![[Pasted image 20230103161518.png]]

- Las cardinalidades UNO o sin especificar se interpretan como un único elemento:
````java
private Factura factura;
````
- Las cardinalidades MUCHO se representan con un 0..* o 1..*
````java
private Set<Averia> averias = new HashSet<Averia>();
````

- Es fundamental mantener las referencias cruzadas (*link* y *unlink*)
![[Pasted image 20230103161959.png]]
![[Pasted image 20230103162022.png]]

- Dos getters para el mismo atributo (el público y el de paquete)
![[Pasted image 20230103162117.png]]
- Setter restringido
![[Pasted image 20230103162218.png]]


### Entidades

- Representa la existencia de algo en el dominio que es de interés y que tiene identidad propia
	- Sus propiedades pueden cambiar a lo largo del tiempo, pero sigue siendo "ella"
	- Puede estar asociada con otras entidades
	- Su ciclo de vida es independiente de otras entidades
	- Representamos su **identidad** basándonos en algún rasgo o característica (*atributo(s)*). Los atributos que forman identidad son **inmutables**. Existen dos tipos de identidad:
		- **Identidad natural**:
			- Basada en atributos naturales del dominio
			- Siempre debe existir atributo o combinación que formen identidad natural
		- **Identidad artificial**:
			- Basada en atributo extra (artificial) con valor generado sin repetición posible
````java
private String id = UUID.randomUUID().toString(); //identidad artificial
private String dni; //identidad natural
````

### Value Type

- Son conceptos del dominio (nombre, email, apellidos...)
- Representan un valor, no tienen identidad (su **valor es inalterable**)
- Son atributos de una entidad (dependen de la entidad de la que forman parte)
- Son **inmutables** (no tienen setters), como los tipos básicos de Java: *Integer, Double, String...*

![[Pasted image 20230103163112.png]]
![[Pasted image 20230103163126.png]]

### Clases asociativas

- Representan a la vez clase y asociación
- Permiten añadir atributos y funcionalidad a una asociación
- Cada instancia representa un enlace
- Identidad compuesta por los dos extremos -> dos objetos sólo pueden estar enlazados una vez
![[Pasted image 20230103163433.png]]

![[Pasted image 20230103163514.png]]

### equals() y hashCode()

- **Entidades**:
	- Sólo son redefinidos sobre los atributos que determinan la identidad (*Si se opta por identidad artificial va sobre ese atributo*)
	![[Pasted image 20230103163803.png]]
- **Value Types**:
	- Son redefinidos sobre TODOS los atributos
	![[Pasted image 20230103163740.png]]

### toString()

- Es útil para la depuración
- No incluir referencias a otras entidades
![[Pasted image 20230103164120.png]]

### Ciclo de vida de un objeto persistente
![[Pasted image 20230103164347.png]]

### Estados de persistencia

- **Transient**: objeto recién creado que no ha sido enlazado con el gestor de persistencia (sólo existe en la memoria)
- **Persistent**: un objeto enlazado con la sesión en el que todos los cambios que se le hagan serán persistentes
- **Detached**: un objeto persistente que sigue en memoria después de que termina la sesión (existe en java y en la BDD)

### Control del ciclo de vida

- Se gestiona desde un EntityManager (sesión)
- Un objeto "está en sesión" cuando está en Persistent
- La sesión es una caché de primer nivel que:
	- Garantiza la identidad java y la identidad en BDD
	- Se optimiza el SQL para minimizar tráfico a la BDD
![[Pasted image 20230103164855.png]]
![[Pasted image 20230103164917.png]]

- La identidad sólo está garantizada dentro del contexto:
![[Pasted image 20230103165331.png]]

### Escenarios de mapeo

- **Green Field**:
	- El proyecto empieza de nuevo
	- El diseño no está condicionado por nada anterior
	- El mapeador genera la base de datos a su medida
- **Legacy**:
	- Actualizamos o expandimos un sistema ya existente
	- La base de datos ya existe de antes
	- El mapeador se debe adaptar al diseño de una BDD ya existente y seguramente retorcido

### Condiciones de una clase para ser mapeada

- Clases Java planas (POJO)
- Constructor sin parámetros
- La información necesaria para persistencia se añade en forma de metadatos (@Anotations, xml)
![[Pasted image 20230103170246.png]]
![[Pasted image 20230103170358.png]]

### Posición de @Id
![[Pasted image 20230103170632.png]]

### Metadatos en anotaciones y XML
![[Pasted image 20230103170740.png]]

### Categorías de anotaciones
![[Pasted image 20230103170835.png]]
![[Pasted image 20230103170905.png]]

### Entidades
- Una entidad se mapea siempre a una tabla
![[Pasted image 20230103171014.png]]

### Value Types
- Representan conceptos adicionales del dominio
- Su ciclo de vida depende de la entidad que los posee
- Semántica de composición
![[Pasted image 20230103171316.png]]

@Embeddable marca una clase como ValueType

### Identity vs Equality

- Java identity        a == b
- Object Equality       a.equals(b)
- Database identity        a.getId().equals(b.getId())
	- Sobre la clave primaria de la tabla
	- Se mapean con la etiqueta @Id
	- Todas las clases Entidad deben tener @Id (identificador)

No siempre serán iguales las tres identidades. El período de tiempo que sí lo son se le denomina =="Ámbito de identidad garantizada" o "Ámbito de persistencia"==

### Tipos de claves

- **Candidata**: campo(s) que permiten determinar de forma única una fila
- **Natural**: candidatas con significado para el usuario. Las entiende y las maneja día a día
- **Artificial (subrogada)**: sin significado en el dominio, pero sí en el sistema. Son siempre generadas por el sistema

#### Problema con las claves naturales...
¿Siempre son NOT-NULL?
¿Nunca van a cambiar?
¿Nunca se van a repetir?

#### Estrategia recomendable
- Usar siempre claves artificiales como claves primarias (un Long o un String eficiente)

### Asociaciones en el mapeador

````java
@OnetoOne (mappedBy = "name")
@OnetoMany (mappedBy = "name")
@ManytoOne (mappedBy = "name")
@ManyToMany (mappedBy = "name")
````

### Estrategias para mapear la herencia

- **Tabla única para toda la jerarquía**: `InheritanceType.SINGLE_TABLE`
	- Todas las tablas persisten en una única tabla con la unión de todas las columnas de todas las clases
	- Usa un discriminador en cada fila para distinguir el tipo
	- Todas las columnas no comunes deben ser nulables
	- Van a quedar columnas vacías
	- Puede generar tablas que ocupan mucho con pocos datos
- **Tabla por cada clase no abstracta**: `InheritanceType.TABLE_PER_CLASS`
	- Una tabla por cada clase no abstracta
	- Las propiedades heredadas se repiten en cada tabla
	- Evita los nulos
	- Consultas menos eficientes
	- Cambios en la superclase se propagan a todas las tablas
- **Tabla por cada clase**: `InheritanceType.JOINED`
	- Cada clase de la jerarquía tiene su propia tabla
	- Las relaciones de herencia se resuelven con FK
	- Cada tabla sólo tiene columnas para las propiedades no heredadas
	- Las consultas son más complicadas
	- Para jerarquías complejas el rendimiento puede ser peor



---


# Preguntas 🎅🏻
## Preguntas JDBC

1. ¿Cuáles son los errores que pueden surgir durante la carga del controlador? ==ClassNotFoundException==
2. Errores surgidos durante el acceso a la BBDD: ==SQLException==
3. ¿Cómo evitar NULL? 
	- ==Evitar usar métodos getXXX()==
	- ==Usar clases envoltorio (wrapper) junto con wasNull()==
	- ==Usar tipos de datos primitivos junto con wasNull()==

## Preguntas JPA