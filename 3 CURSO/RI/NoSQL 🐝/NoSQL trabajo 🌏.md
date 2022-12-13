# 7 dic 2022 🎄

## Pasos
- Decargar https://neo4j.com/download-center/#community
- Instalar Java JDK 17 o mayor
- AuraDB servidor en la nube (sólo 1), hay que crear una cuenta
- localhost:7474 <- environment
- Neo4j Sandbox (gratis 3 días) -> https://neo4j.com/sandbox/ (registrarse con email alternativo para evitar correo basura)
- Nuevo proyecto >>> Movies databse (coger esta base de datos)
- MATCH (n) DETACH DELETE n , (elimina todo)
- Intentar no usar nombres para las relaciones (sólo usar verbos). Ej: Ann es dueña de un coche (no usarlo) -> usar Ann posee un coche
- Todo lo que va entre paréntesis es un nodo en las queries

Ejemplo de gql:
```sql

CREATE (TheMatrix:Movie {title:'The Matrix',
released:1999, tagline:'Welcome to the Real World'}) --creacion de un nodo

CREATE (Keanu:Person {name:'Keanu Reeves', born:1974}) --creacion de un nodo

CREATE (Keanu)-[:ACTED_IN {roles:['Neo']}]->(TheMatrix) --relacion
```

---
# 13 Dic 2022 🌯

- El lenguaje consiste en especificar la estructura que quieres encontrar, y el lenguaje te devuelve todas las combinaciones que encajan con esa estructura
- El resultado es una **tabla** con los datos del return
- Sale 1 fila por cada MATCH
- El **WITH** nos permite partir una consulta en trozos

Ejemplos de consultas:
````sql
MATCH (n) DETACH DELETE n --borra todo

--Los actores ordenados por edad
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) WHERE m.released > 1990 RETURN DISTINCT p, p.name ORDER BY p.born DESC
--Los actores ordenados por edad sin fecha de nacimiento nula
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) WHERE m.released > 1990 AND p.born IS NOT NULL RETURN DISTINCT p, p.name ORDER BY p.born DESC
--El actor más joven
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) WHERE m.released > 1990 AND p.born IS NOT NULL RETURN DISTINCT p, p.name ORDER BY p.born DESC LIMIT 1
--Los actores con sus películas(con actores repetidos)
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) WHERE m.released > 1990 AND p.born IS NOT NULL RETURN p.name, m.title ORDER BY p.name
--Los actores con sus películas(sin actores repetidos)
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) WHERE m.released > 1990 AND p.born IS NOT NULL RETURN p.name, COLLECT(m.title) AS peliculas
--Los actores con su número total de películas
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) WHERE m.released > 1990 AND p.born IS NOT NULL RETURN p.name, COUNT(m.title) AS total
--Los actores con su número total de películas ordenados por el total
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) WHERE m.released > 1990 AND p.born IS NOT NULL RETURN p.name, COUNT(m.title) AS total ORDER BY total DESC
--Consulta múltiple usando WITH
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) WHERE m.released > 1990 AND p.born IS NOT NULL WITH p.name AS nombre, COUNT(m.title) AS total WHERE total >= 4 RETURN nombre, total

(a)-[:A|D|W*]-(KB) -- como llegar a un nodo en concreto sin saber los intermedios pero que sean de tipos determinados
````
- ==CHEAT SHEET== -> https://neo4j.com/docs/cypher-cheat-sheet/current/
- Las relaciones sólo pueden tener un tipo, no se pueden realizar operaciones AND

---