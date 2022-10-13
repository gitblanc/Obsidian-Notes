# 15 Sept 2022 🐁
---
- **JDBC** es una API Java, clases e interfaces, que permite a aplicaciones Java acceder a fuentes de datos mediante la ejecución de sentencias SQL. Es como un **middleware**.
- El fabricante proporciona un controlador o **driver** que hace de intermediario entre el cliente y el SGBD (se encarga de traducir de un lenguaje al otro, como un middleware)
- Permite la independencia de la base de datos
- Si cambiamos la base de datos sólo hay que cambiar el driver
- El cliente sólo crea objetos y hace llamadas (como que el driver)

## Arquitectura JDBC

![[jdbc arch.png|500]]

## Proceso de desarrollo (no en las diapos.)
- **Instalar el driver**
- **Cargar el driver**: el cliente va a necesitar una instancia de la clase driver. Esta clase traduce el execute statement (o lo que necesite) a la base nativa del SGBD. Esta clase se llama DriverManager. Esta clase busca entre todos los .jar, el que sea necesario para el cliente.
- **Crear la conexión con la BBDD**
- **Crear sentencia SQL**
- **Ejecutar la sentencia**
- **Recuperar los resultados**
- **Liberar los recursos**

### ~ Proyecto de ejemplo hecho en clase ~
NOTA: hay que crear una carpeta para los drivers llamada **lib** (en la que irán los .jar) y configurar el build path relativo a estos.
````java
private static Connection c = null;
private static Statement s = null;
private static ResultSet rs = null;
private String url = "jdbc:hsqldb:hsql://localhost"

String plateNum; //num matricula
try{
	c = DriverManager.getConnection(url); //creamos la conexión
	s = c.createStatement(); //creamos un statement
	String query = "select * from tvehicles where model = 'golf'";
	rs = s.executeQuery(query);
	while (rs.next()){
		plateNum = rs.getString("platenumber");
		sysout(plateNum);
	}
} catch (SQLException e){
	e.printStackTrace();
} finally{
	rs.close();
	s.close();
	c.close();
}
````

- El objeto **ResultSet** es un proxy, no contiene realmente la tabla de la base de datos. Se hace una carga perezosa. Cuando se ejecuta la query se crea una tabla con los valores buscados, y la aplicación tiene una forma de aceder a ell (no tiene la tabla como tal)
- Un **cursor** permite la navegación (por defecto secuencial y read only (no modificable))
- Es importante liberar los recursos cerrando las conexiones una a una
- Por defecto no se puede haer un previous(), sólo se puede hacer un next() en un ResultSet
- El valor null significa que no hay valor, no es que no exista

## ~Ejercicio carWorkShop~
````java
private static Connection c = null;
private static Statement s = null;
private static ResultSet rs = null;
private String url = "jdbc:hsqldb:hsql://localhost"

String plateNum, identifier, vehicle, invoice, amount = null;

try{
	c = DriverManager.getConnection(url); //creamos la conexión
	s = c.createStatement(); //creamos un statement
	String query = "select * from tvehicles";
	rs = s.executeQuery(query);
	while (rs.next()){
		plateNum = rs.getString("platenumber");
		identifier = rs.getString("mechanic_id");
		vehicle = rs.getString("vehicle_id");
		invoice = rs.getString("invoice_id");
		amount = rs.getString("amount");
		sysout(plateNum + identifier + vehicle + invoice + amount);
	}
} catch (SQLException e){
	e.printStackTrace();
} finally{
	rs.close();
	s.close();
	c.close();
}
````
- Evitar usar los getXXX() ya que devuelven datos primitivos (y null), en su lugar usar los wasNull() para reasignar los valores no asignados

### Usando String.format
````java
private static Connection c = null;
private static Statement s = null;
private static ResultSet rs = null;
private String url = "jdbc:hsqldb:hsql://localhost"

String plateNum, identifier, vehicle, invoice, amount = null;

try{
	c = DriverManager.getConnection(url); //creamos la conexión
	s = c.createStatement(); //creamos un statement
	String query = String.format("select * from tvehicles where model = '%s'", "POLO");
	rs = s.executeQuery(query);
	while (rs.next()){
		plateNum = rs.getString("platenumber");
		identifier = rs.getString("mechanic_id");
		vehicle = rs.getString("vehicle_id");
		invoice = rs.getString("invoice_id");
		amount = rs.getString("amount");
		sysout(plateNum + identifier + vehicle + invoice + amount);
	}
} catch (SQLException e){
	e.printStackTrace();
} finally{
	rs.close();
	s.close();
	c.close();
}
````

### Usando marcadores -> ? se necesitas PreparedStatements
````java
private static Connection c = null;
private static PreparedStatement s = null;
private static ResultSet rs = null;
private String url = "jdbc:hsqldb:hsql://localhost"

double money;
String query2 = "seLect platenumber from tvehicles where client_id = ?";

try{
	c = DriverManager.getConnection(url); //creamos la conexión
	s = c.createStatement(); //creamos un statement
	String query = "select id from tclients where city = 'llanes'"
	rs = s.executeQuery(query);
	while (rs.next()){
		sysout("CLIENTE: " + r,getString(1));
		r2 = c.prepareStatement(query2);
		r2.setString(1, r.getString(1));
		while (r2.next()){
			sysout("matricula: " + r2.getString(1));
		}
	}
} catch (SQLException e){
	e.printStackTrace();
} finally{
	rs.close();
	s.close();
	c.close();
}
````
- Así evitamos compilar las queries varias veces, sólo se hace 1, y en tiempo de ejecución sólo inyecto el valor que falta
- Previene las  sql injections

## Tipos de ResultSet
- **Sensitivity**: el ResultSet es consciente de los cambios realizados por otros (desde fuera de la transacción que ejecuta). Presupone que la propia transacción tiene ajustado un nivel de aislamiento que permite que los cambios sean visibles.

- **Scrollability and positioning**: el cursor puede moverse en ambas direcciones y posicionarse en una fila cualquiera.

- **Updatability**: el ResultSet puede ser actualizado en cualquier momento.

## Conexiones
- La **conexión tradicional** tiene un mayor acomplamiento, pues el cliente depende de datos de los que no debería depender
- La **conexión avanzada** es totalmente desacoplada, no la maneja el cliente

---
# 22 Sept 2022 ⚽️
## Conexión avanzada
- Para hacer las conexiones de manera desacoplada usamos la interfaz DataSource
- El objeto **DataSource** lo despliega el administrador de la base de datos
````java
OracleDataSource ods = new OracleDataSource();
ods.setDriverType(driverType);
````
- El objeto **DataSource** también nos permite el pool de conexiones (conjunto de conexiones físicas con la base de datos)
- **RowSet**: como un ResultSet (no navegables ni sensibles, sólo permiten rs.next y no permiten borrar, actualizar ni insertar) pero mejorado.
	- **CachedRowSet**: un ResultSet pero en caché. No es ideal para grandes volúmenes de datos

---