# 24 Nov 2022 🦂

## Modelo y SGBD Relacional
- Peristencia
- Control de concurrencia
- Control de integridad y seguridad
- Productividad 
- Integración de aplicaciones
- **Agnosticismo en consultas**: no darle vueltas a consultas enormemente parecidas, tendrán un rendimiento muy disperso
- Es un modelo conocido y estandarizado

## Desventajas del modelo relacional
- No siempre es la mejor solución
	- Adaptación a necesidades de aplicaciones
		- Esquema flexible (personas de distinto tipo)
		- Muchos tipos de objeto
		- Objetos complejos
	- Desadaptación de impedancias
- Evaluar alternativas
	- Sistemas con compromisos de diseño diferentes
- **Persistencia políglota** (tener distintas bases de datos dependiendo de cada necesidad de conjunto)

## Hacia otros modelos de datos

- Bases de datos de aplicación no compartidas (microservicios)
- Big Data
- Rendimiento para sitios web masivos
- Escalabilidad horizontal (clusters (añadir servidores))
- Distribución

## NoSql

- NoSql es un término "paraguas" (no tiene una definición exacta), Not only SQL
- Características:
	- Modelo de datos no relacional, basado en agregados
	- Esquema flexible (*schemaless*)
	- Orientación a clusters
	- Open Source
	- Orientación a los problemas de los grandes servicios web
- No es una solución mágica
	- Están menos desarrolladas
	- Atomicidad elemental sin transacciones o transacciones de bajo nivel
	- Funcionalidad típica de bases de datos limitada
		- Sin control de seguridad
		- Sin control de integridad
		- Consultas elementales
		- Sin lenguaje especializado
	- Orientado a procesos -> no agnóstico en consultas (hay consultas que en función de cómo se hagan pueden cambiar)
- Implementación del resto de funcionalidad típica en la aplicación

## Principales modelos de datos NoSQL

- Clave-valor
- Documental
- Almacenamiento en columnas
- Grafo

## Modelos de datos orientados a agregados

- **Agregado**: conjunto de objetos relacionados tratado como unidad
- Unidad típica para:
	- Persistencia (almacenamiento)
	- Consistencia/atomicidad (transacciones)
	- Distribución (los datos han de estar en un único nodo, no pueden estar particionados)
- Denormalización habitual

## Almacenes Clave-Valor

- Asociación clave-valor
- Recuperación de valor buscando por clave
- Valor es un agregado opaco a la base de datos
	- Sin semántica, tipo void
	- La aplicación da semántica
- Unidad de consistencia/atomiciddad

## Bases de datos documentales

- Sistema clave-valor
- Valor no opaco, documento agregado con estructura (un json, un gif, un .txt ...)
- Consulta por clave
- Consulta por contenido del documento

## Bases de datos de grafo

- Estructura de datos de grafo
	- Nodos con propiedades
	- Relaciones entre nodos (arcos)
		- También tienen propiedades
		- Unidireccionales/bidireccionales
- Diferente al resto de NoSQL
	- Poco orientadas a distribución
	- Transacciones ACID
	- Énfasis en relaciones
	- Consultas complejas

---
# 1 Dic 2022 🪺
## Bases de datos en grafo

- Escalabilidad de datos:
	- **Vertical**: para pequeñas empresas
	- **Horizontal**: para empresas grandes (añades más clústers)
- Distribución de datos:
	- Los datos se reparten entre distintos servidores
	- Mayor rendimiento, disponibilidad
	- Mayor complejidad
- Alternativas distribución
	- Servidor único (con o sin fragmentación y replicación)

- **Fragmentación** (sharding): fragmentar los datos y repartirlos entre servidores. Cada servidor es responsable de un fragmento (adecuado para datos necesarios en el mismo servidor (agregados)).
- **Replicación Maestro-Esclavo**: replicar los datos entre los nodos. Estro proporciona escalabilidad en lecturas
	- **Maestro**: gestiona actualizaciones, retransmite actualizaciones a esclavos, defimnidos manualmente o automáticamente
	- **Esclavos**: repiten los datos
- **Replicación entre iguales**: todas son réplicas equivalentes (todas pueden hacer actualizaciones y escrituras). Mayor robustez, pues no hay un maestro único.
- **Fragmentación + replicación**: almacenamiento en columnas

==TEOREMA CAP==

libro -> https://www.amazon.es/NoSQL-Distilled-Emerging-Polyglot-Persistence/dp/0321826620

---
