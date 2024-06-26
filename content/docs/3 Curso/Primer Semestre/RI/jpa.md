---
title: JPA 🚥
---
# 13 Octubre 2022 🏖
---
- Ahora vamos a utilizar el modelo de dominio, que hace que el esfuerzo de implementación sea mucho más estable
- **Mapeadores Objeto-Relacional**
	- Permite la persistencia y es transparente a objetos en BBDD relacionales
	- Mínima intrusividad en el código
	- Soporta concurrencia
	- Se programa pensando en objetos
	- No es necesario escribir JDBC

Diferencias estructurales y dinámicas entre modelo relacional y modelo OO:
- **Estructurales**
	- **Granularidad**: hay varios tipos de clases (entidades y value types)
	- **Identidad**: en java el == o el equals o el hashCode, en BDD relacional la clave primaria define la identidad
	- **Subtipado**
	- **Asociaciones**: *navegabilidad* (unidireccional o bidireccional) y *cardinalidad* (uno a uno, uno a muchos, muchos a muchos)
- **Dinámicas**: generan pérdidas de eficiencia en tiempo de ejecución
	- **Navegación**: *eager loading* (se carga un objeto y sus asociados, puede sobrecargar la memoria con objetos no necesarios) y *lazy loading* (se carga sólo lo necesario, pero genera el problema de las n+1 consultas)
	- **Cacheado**: optimiza el rendimiento al reducir el trasiedo de la BBDD y permite hacer optimizaciones (write-behind delayed o batch load/update)
	- **Concurrencia**: si hay varios hilos de ejecución se crea una caché por hilo y la BDD gestiona las transacciones

---
# 20 Octubre 2022 💡
## Gestión de objetos persistentes en JPA

Ciclo de vida de un objeto:
- new
- en memoria
- a la basura

- Con un **mapeador** entrando en juego, el estado de memoria se divide en tres estados diferentes:
	- **transient**: cuando no tengo el mapeador y hago un new(), el objeto está únicamente en memoria (no existe en la bbdd)
	- **persistent**: existe en la base de datos, y está vigilado por el mapeador (si se hacen modificaciones de escritura, se sobreescriben en la base de datos). Vamos de transient a persistent a través del método *persist()*. Es un estado gestionado
	- **detached**: un objeto que sigue en memoria despueés de la sesión. Existe en Java y en la BBDD
- El merge crea un nuevo objeto  y lo devuelve

## Mapeo de clases
- La información necesaria para persistir objetos se añade en forma de metadatos (anotaciones en el código)


---

# 27 Octubre 2022 🦩

## Multiplicidad en JPA
- One to many 
- Many to one

## Estrategias para mapear herencia
- Tabla única para toda la jerarquía
- Tabla po cada clase no abstracta
- Tabla por cada clase

## JPQL
==SIEMPRE ENTRA EN EL EXAMEN==
- En lugar de tablas, se usan entidades.
- Ojo con getSingleResult(), porque casca si devuelve un null con una PersistenceException

````java
select v from Vehicle v

select v from Vehicle v where lower (v.make) like '%nissan%'

select c from Client c where lower (c.address.city) = 'oviedo'

select w from WorkOrder w where w.status = uo.ri.cws.domain.WorkOrder.WorkOrderStatus.FINISHED

//Con un join 
select w from WorkOrder w 
	join w.vehicle v 
	where v.platenumber= ?!
//CONSULTAS EQUIVALENTES
select i from Invoice i 
	join i.workOrder w 
	join w.vehicke v
	where v.platenumber=?1

select i from Vehicle v
	join v.workOrders w
	join w.invoice i
	where v.platenumber=?1

select w.invoice from WorkOrder w where w.vehicle.platenumber = ?1

//----
select i.workorder.vehicle Intervention i where i.mechanic.dni=?1

select i from CreditCard cc
	join cc.charge c
	join c.invoice i
	where cc.number = ?1

select s.intervention.workorder.vehicle.client from Substitution s where s.sparePart.code = ?1
````

---