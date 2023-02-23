# 31 Enero 2022 👻
---
- Las bases de datos se hayan el el área de persistencia. Una base de datos es un **mecanismo de persistencia de datos**.
- La memoria **no volátil** es mucho más lenta que la memoria volátil (DRAM, actual usada).
- Disco duro -> memoria secundaria
- Los **ficheros** logran la persistencia de datos.
- **Base de datos:** conjunto de datos relacionados entre sí. Almacena datos y metadatos (datos acerca de los datos). Por ejemplo: se almacena Oviedo (dato) cuya temperatura son 7°C (metadato).
- Para interactuar con una base de datos necesitamos un **Sistema de Gestión de Bases de datos** (SGDB).
---
# 4 Febrero 2022 🩳
---
- **Restricciones de integridad:** limitaciones a los datos de las bases de datos.
- Necesitamos un intermediario para acceder a las bases de datos.
- **Lenguaje de datos:** interfaz de comunicación con las bases de datos (SQL).
- Un Sistema de Bases de datos ha de ser:
	- **Cómodo** (que tarde poco, lenguaje de alto nivel)
	- **Eficiente** (que tarde poco, que sea rápido)
- **Lenguaje de manejo de datos (LMD):** permite recuperar/leer datos/hacer consultas (QUERIES)
- En una base de datos se puede:
	1. Recuperar
		- SELECT -> consultar
	2. Modificar
		- INSERT -> insertar
		- DELETE -> eliminar
		- UPDATE -> actualizar
- **Lenguaje de definición de datos (LDD):** qué esquema conceptual se va a definir en la base de datos.
![[CREATE.png]]
- **Niveles de abstracción:**
	- **Físico:** cómo se guardan los datos
	- **Conceptual:** qué es lo que se guarda
	- **Visión:** muestra al usuario una vista personalizada del nivel conceptual. Se le enseña al usuario un subconjunto de las estructuras conceptuales.
 ![[Niveles de abstraccion.png | 400]]

---
# 7 Febrero 2022 🧞‍♂️
---
- **CLAVE primaria (priomary key):** no se puede repetir el código definido como clave primaria.
- **CLAVE externa (foreign key):** hace referencia a cuando una clave aparece en otra tabla. Tiene una restricción llamada restricción de integridad diferencial. Comprueba que no estés haciendo referencias que no existen. Por ejemplo: un alumno que no exista en la tabla de matriculados no puede ser añadido a la asignatura TPP. Sólo se aceptan valores **existentes**.
![[matriculados.png|400]]
- **Modelo de datos:** herramienta para definir un esquema (conceptual, físico o de visión).
- **Modelo relacional/diseño conceptual:** define el esquema de la base de datos que representa fielmente el universo del discurso.
- **Modelo entidad relación:** no tiene tablas.
![[mentidadrelacion.png|400]]
- **Modelo orientado a objetos:**
![[orientado a objetos.png|400]]

NOTA: esquema != instancia (datos existentes en un determinado momento)

- **Modelo entidad-relacional**
	- **Entidad:** cosa que existe por sí misma, que se pueda diferenciar de otras y que tenga datos descriptivos.
	- **Atributos:** permiten asociar valores a las entidades.
---
# 14 Febrero 2022 💕
---
![[14 feb.png |400]]

### Restricciones
- **Cardinalidad(máxima):** n° de elementos con los que puedes conectar. (Por ejemplo: el número de asignaturas en las que está matriculado un alumno) Se representa con un 1 (->) o n (-).
- **Cardinalidad mínima:** n° mínimo obligatorio de elementos relacionados. Valores genéricos: 0 o 1.
- **Cardinalidad concreta:** se pone un valor concreto.
---
- Como definir el esquema de la base de datos:
	- Lenguaje de modelado
	- Lenguaje externo (notas de texto: reducir su uso a lo mínimo)

- **Diseño conceptual:** modelo entidad relación (más potente)
- **Diseño lógico:** modelo relacional
---
### Normas del paso a tablas
- Cada conjunto genera una tabla
- La clave es la unión de las entidades que asocia
- Si hay una flecha 1, se genera una clave
- Si hay una flecha 1, la tabla intermedia es opcional
- Por omisión no se pone la tabla intermedia (mayor rendimiento)
---
# 21 Febrero 2022 🛸
---
- **Superclave:** conjunto de elementos que no se pueden repetir. La unión de todos los atributos siempre es una superclave.
![[superclave.png |400]]
- **Clave candidato:** superclave mínima, no se puede quitar ningún atributo, todos son esenciales.
- **Clave primaria:** una de las claves candidato. La principal para identificar el conjunto. Escogida por el diseñador. Se suelen preferir números a cadenas, ya que los números son más rápidos de comparar. Mantiene la integridad de entidad (no puede haber elementos repetidos).
- **Atributo natural:** algo que ya tienes implícito.
- **Clave externa:** clave primaria de una tabla que aparece en otra tabla. Mantiene la integridad referencial.
- **Dependencia por existencia:** la existencia de una entidad depende de la de otra con la que está relacionada.
![[dependencia.png|400]]
- **Conjunto de entidades fuerte:** aquel que tiene suficientes atributos propios para hacer de clave primaria.
- **Discriminador:** miniclave para el conjunto de entidades que dependen de otro conjunto. Lo tienen los conjuntos de entidades débil.
- **Conjunto de entidades débil (CED):** conjunto que no se puede repetir dentro del mismo conjunto. En el ejemplo de arriba un paso a nivel existe en una vía. 
- **Clave CE débil:** clave de la entidad de la que dependen más el discriminador.
- **Relación bitácora:** apuntan todo lo relacionado.
![[claves.png|500]]
- **Clave subrogado:** creadas aleatoriamente, que no tienen significado.
- **Generalización:** partir de algo concreto que ya existe y generalizarlo.
![[generalizacion.png|400]]
![[generalizacionespecializacion.png|400]]
- **Solapamiento:** una cuenta de ahorro es a su vez una cuenta corriente.
---
# 28 Febrero 2022 🗿
---
- **Agregación:** la relación ternaria son siempre 3 patas. Si existe algún caso en el que son menos, es una agregación.
![[agregacion.png|400]]
- **Relaciones reflexivas:** las dos entidades que asocian son del mismo tipo.
![[reflexivas.png|400]]
- **Relaciones ternarias:** tres partes.
![[ternarias.png|400]]
- **Atributo derivado:** aquel cuyo valor se calcula a través de una fórmula.
---
# 7 Marzo 2022 🏙
---
- **Relación de exclusión:** la existencia de elementos en un conjunto excluye la existencia en el otro.
- **Restricción de subconjunto:** un grupo ha de ser el subconjunto de otro.
![[exclusion.png|400]]

### Desventajas del sistema de procesamiento de ficheros (COBOL)
- **Redundancia:** repetición innecesaria de datos.
- **Integridad:** si hay un agujero de integridad se pueden colar datos incorrectos (Por ejemplo no hacer comprobaciones).
- **Seguridad:** controlar que no todos los usuarios tengan todos los permisos (GRANT REVOKE).
- **Concurrencia:** en qué orden se han de ejecutar los procesos. Los procesos se han de sincronizar entre sí para no perder datos.
---
# 14 Marzo 2022 💸
---
- **Atomicidad:** recuperación de fallos.
- Los ficheros no implementan la atomicidad.
- El archivo .log permite guardar información en memoria de forma persistente.
- Rollback -> deshacer los cambios.
- **Front-end** -> gestor de consultas.
- **Back-end** -> procesador de almacenamiento.
![[estructura sql.png|400]]
- **Índices:** estructuras que permiten acelerar las búsquedas sobre los datos (es un optimizador).
- **Diccionario de datos:** donde se guardan los metadatos.
- **Propiedades ACID:**
	- **Atomicity:** o se hace todo o no se hace nada, nada a medias.
	- **Consistence:** cuando termina, se cumplen todas las reglas de integridad.
	- **Isolation:** aislamiento.
	- **Durability:** los cambios perduran en el sistema.

- Restricciones de integridad:
	- **Diferidas:** la verificación se hace al terminar.
	- **Inmediatas:** siempre tienen que ser verdad (al final y en todo momento).
---
# 21 Marzo 2022 🍓 
---
 ![[database system internals.png |300]]
- Para poder usar una biblioteca necesitamos una API.

#### _Técnicas de despliegue de servidores_:
---
1. **Biblioteca nativa:** las instruciones que usa por defecto están impuestas por el fabricante.
2. **Biblioteca genérica (JDBC):** la biblioteca no conecta directamente con el producto. Tiene dos partes, el equivalente a la API fija, el frontal(habla con el cliente), y tiene la posibilidad de plugins. Es la más habitual.
3. **SQL inmerso (embedded):** consiste en programar sin usar bibliotecas. En lugar de hacer los accesos a una base de datos de forma indirecta, se escriben directamente en el código. El código en sql lo pasas por un preprocesador que lo convierte al código utilizado.
    ````c
	Tu ves y haces -> 2+3
	La librería hace -> add(2,3)
	````
4. **Lenguajes 4G (de cuarta generación):** lenguaje de programación cuyas sentencias del manejo de datos son parte del lenguaje. Un ejemplo sería PLSQL. Están pensados para realizar aplicaciones de gestión de los 1990-2000. De fábrica manejan menús. El lenguaje maneja formularios de fábrica.
- Todos estos mecanismos se basan en cursores.
- Ejemplo de código:
http://di002.edv.uniovi.es/~darioa/bdatos/mysql/Ejemplo_programa_MySQL_C_API.htm

---
*¿En qué se diferencia un create table frente a una búsqueda?*
El create sólo se hace una vez, la búsqueda la puedes realizar de forma ilimitada.

---
### **ENTRA:**
- *MODELO RELACIONAL:* relacion -> tabla, 
											   atributos -> columna, 
											   valores de atribs. en: dominio -> tipo de datos, 
											   dominios son: atómicos
											   tuplas -> fila
1. Una base de datos relacional tiene **integridad de entidad**, es decir, tiene clave primaria. Impide que haya datos repetidos.
2. Una base de datos mantiene la **integridad referencial**, es decir, tiene claves externas. Los valores de la clave externa tienen que existir donde son clave primaria.
---
♻️ Segunda parte -> [[BD Segunda parte 📀]]