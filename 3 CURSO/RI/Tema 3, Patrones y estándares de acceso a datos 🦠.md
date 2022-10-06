# 29 Sept 2022 🔫
---
- Si tengo código **enmarañado** (tangled, todo en un método) tengo una baja cohesión
- Si tengo código **disperso** (scattered, todo en demasiados métodos de demasiadas clases) tengo un alto acoplamiento

## Atributos de calidad para el software
- **Escalabilidad**: a medida que crece, qué alternativas existen para lidiar con el crecimiento
- **Mantenibilidad**: los costes relativos de reparación o actualización
- **Reusabilidad**: capacidad del código para ser usado en otras aplicaciones
- **Extensibilidad**: la facilidad de adaptar el software sin modificar el ya existente

La clave para crear código de calidad es bajo acoplamiento y alta cohesión.
- **Acoplamiento**: las dependencias existentes entre módulos
- **Cohesión**: responsabilidad única

## Patrón arquitectónico: Separación en capas
![[separacion en capas.png|600]]
Ventajas:
- **Reutilización**: una vez hecha una capa, se puede usar por muchos clientes distintos
- **Cohesión**: cada capa se ocupa de una responsabilidad
- **Mantenibilidad**: mientras se mantenga la interfaz, las capas ignoras los cambios de implementación de otras capas

Desventajas:
- No siempre es posible una división estricta -> Las transacciones hay que manejarlas desde la capa superior, porque sino habra comunicación entre la misma capa
- Las capas adicionales pueden degradar el rendimiento
- La arquitectura en capas exige dependencias hacia abajo

## Patrón DTO (Data Transfer Objects, información que fluye entre capas)
- Colocar en la capa business y en la de persistencia para que la capa correspondiente sólo tenga dependencias de la capa de debajo.

## Patrón Fachada
![[patron fachada.png|500]]
- Además oculta los detalles detrás de la interfaz.

## Factoría
- Clase que crea instancias de interfaces ocultándole al cliente cómo las crea
![[factoria.png|500]]

---
#  6 Octubre 2022 🫐

## Patrón DAO
- Define que nuevos objetos tienen que aparecer, dónde tienen que aparecer y es un intermediario entre la capa de negocio y el acceso a los datas
- Los DAO proporcionan métodos CRUD: inserción, actualización, borrado y consulta de información

## Row Data Gateway
- Patrón que solicita implementar un objeto por cada fila de una tabla que tu recuperes

## Table Data Gateway
- Es un DAO implementado uno para cada tabla

![[gateway.png]]
![[organizacion base de datos.png|700]] 
![[organizacion base de datos png.png]]

## Patrones para la capa de negocio

- Transaction scripts

---