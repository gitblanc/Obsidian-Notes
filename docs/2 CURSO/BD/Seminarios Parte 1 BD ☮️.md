
# 18 Febrero 2022, Seminario 2 ⛺️
---
![[seminario 2.png |400]]
- **Dominio atómico:** sólo se puede tomar un valor indivisible
- **Entidad:** es algo principal del universo del discurso, tenemos atributos descriptivos para ella.
![[jugadorentrenador.png|500]]
![[jugadorentrenadortabla.png|400]]

---
# 4 Marzo 2022 , Seminario 3🏵
---
EJERCICIO A)  
  
Crear un diagrama Entidad-Relación (que modele capturando la mayor semántica posible), usando características extendidas si es necesario y convertirlo posteriormente a una serie de tablas del modelo de datos relacional, para el mantenimiento de aviones en un aeropuerto.  
  
-Cada avión tiene una matrícula y pertenece a un único propietario. Debe conocerse el modelo concreto de avión (ej: Boeing 737).  
  
-Todos los empleados del aeropuerto tienen asignado un número de empleado, y se registra su nombre y dirección y salario anual. Los controladores tienen que pasar un examen médico anual, cuya fecha debe ser conocida.  
  
-Dentro de la plantilla de empleados del aeropuerto, los técnicos se encargan del mantenimiento de los aviones (por lo que reciben un complemento mensual). Cada técnico tiene un conjunto de modelos de avión en los que está especializado (no pueden ser más de 7). Es posible que varios técnicos estén especializados en el mismo modelo de avión. Debe conocerse la fecha en la que cada técnico aprobó el examen de especialización en un modelo determinado.  
  
-El aeropuerto (según normas internacionales) tiene estandarizadas un conjunto de pruebas de mantenimiento para que sean pasadas por los aviones. Cada prueba tiene un código internacional, una duración media aproximada y una puntuación máxima. Algunas pruebas se componen a su vez de otras sub-pruebas (hay que saber además el orden en que se deben pasar en este caso).  
  
-Debe conocerse las pruebas que ha pasado cada avión y la fecha en la que se pasó y la puntuación concreta que el avión alcanzó en cada prueba. Estas pruebas son realizadas por los técnicos (nunca más de 3), y debe registrarse el número de horas que dedicó cada técnico a la prueba. Un técnico no puede realizar una prueba sobre un avión en el que no esté especializado.  
  
Indicar en un listado las RESTRICCIONES QUE NO QUEDAN RECOGIDAS EN EL DIAGRAMA.  
Nota: Sólo es necesario representar aquellos atributos de las entidades que sean fundamentales para comprender el esquema. Representar de manera más amplia (de la manera que parezca más razonable) aquellos aspectos que no queden completamente definidos en el enunciado anterior. Razonar en cada caso la representación que se elige.
![[seminario 3.png]]

EJERCICIO B)  
  
Crear un diagrama Entidad-Relación (que modele capturando la mayor semántica posible), usando características extendidas si es necesario y convertirlo posteriormente a una serie de tablas del modelo de datos relacional, para una empresa que vende seguros de vida y de hogar:  
  
- La empresa se dedica a vender seguros de vida y/o de hogar a los clientes. Para hacer el contrato de seguro se necesita el DNI, nombre, apellidos y dirección del cliente al que se le hace el contrato (el tomador).  
  
- Todos los seguros que vende la empresa se identifican mediante un código único. En cada contrato de un seguro de vida, además del cliente, se registra la fecha de vencimiento y la cantidad anual del seguro (la prima), así como la indemnización por fallecimiento. También debe indicarse quienes son los beneficiarios del seguro (la persona o personas a las que se pagará la indemnización) mediante el DNI, nombre, apellidos y dirección del mismo.  
  
- Puede darse el caso de que un seguro de vida tenga, más de un tomador (pero nunca más de 5). Además, en este caso, cada tomador puede indicar quiénes son sus beneficiarios (por ejemplo, un seguro puede ser tomado por Pepe y Lola, y Pepe nombrar como beneficiarios a Pepito y Pedrito, y Lola a Lolita y Luisita). El número de beneficiarios total (entre todos los tomadores) no puede ser mayor de 10.  
  
- En el caso de los seguros de hogar no es aplicable el concepto de indemnización por fallecimiento ni de beneficiario, pero sí deben conocerse la cantidad asegurada por continente de la vivienda (“construcción”) y por contenido (“mobiliario”).  
  
- Cada contrato de seguro es gestionado por uno o varios agentes de seguros de la empresa, que recibirán cada uno una gratificación por conseguir el contrato (puede ser diferente para cada uno dependiendo del trabajo que hayan realizado para conseguir el contrato).  
  
- Los agentes de la empresa tienen asignado un código de empleado que se usa para la gestión de nóminas, seguros gestionados, etc. Se necesita conocer también su nombre, apellidos, dirección y nivel de ventas (alto, medio, bajo) y salario base mensual. También tienen un porcentaje de incremento del salario por productividad. Este porcentaje depende del nivel de ventas, de los contratos gestionados y de la cuantía de los mismos (según unos criterios especificados por la dirección que no vienen al caso de este problema).  
  
- Algunos agentes tienen a su cargo la supervisión del trabajo de otros agentes menos expertos, a los que deben calificar en su trabajo supervisado (mal, regular, bien, muy bien), indicándose la fecha en la que se hizo esa calificación.  
  
Indicar en un listado las RESTRICCIONES QUE NO QUEDAN RECOGIDAS EN EL DIAGRAMA.  
  
Nota: Sólo es necesario representar aquellos atributos de las entidades que sean fundamentales para comprender el esquema. Representar de manera más amplia (de la manera que parezca más razonable) aquellos aspectos que no queden completamente definidos en el enunciado anterior. Razonar en cada caso la representación que se elige.
![[Ej b seminario 2.png]]

---


♻️ Segunda parte -> [[Seminarios Parte 2 BD 🎁]]