
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

---
♻️ Segunda parte -> [[Seminarios Parte 2🎁]]