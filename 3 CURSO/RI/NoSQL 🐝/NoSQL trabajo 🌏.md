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