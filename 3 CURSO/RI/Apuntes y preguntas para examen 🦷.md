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


---


# Preguntas 🎅🏻
## Preguntas JDBC

1. ¿Cuáles son los errores que pueden surgir durante la carga del controlador? ==ClassNotFoundException==
2. Errores surgidos durante el acceso a la BBDD: ==SQLException==
3. ¿Cómo evitar NULL? 
	- ==Evitar usar métodos getXXX()==
	- ==Usar clases envoltorio (wrapper) junto con wasNull()==
	- ==Usar tipos de datos primitivos junto con wasNull()==
