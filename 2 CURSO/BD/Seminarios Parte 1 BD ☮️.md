
# 18 Febrero 2022, Seminario 2 鉀猴笍
---
![[seminario 2.png |400]]
- **Dominio at贸mico:** s贸lo se puede tomar un valor indivisible
- **Entidad:** es algo principal del universo del discurso, tenemos atributos descriptivos para ella.
![[jugadorentrenador.png|500]]
![[jugadorentrenadortabla.png|400]]

---
# 4 Marzo 2022 , Seminario 3馃彽
---
EJERCICIO A)  
  
Crear un diagrama Entidad-Relaci贸n (que modele capturando la mayor sem谩ntica posible), usando caracter铆sticas extendidas si es necesario y convertirlo posteriormente a una serie de tablas del modelo de datos relacional, para el mantenimiento de aviones en un aeropuerto.  
  
-Cada avi贸n tiene una matr铆cula y pertenece a un 煤nico propietario. Debe conocerse el modelo concreto de avi贸n (ej: Boeing 737).  
  
-Todos los empleados del aeropuerto tienen asignado un n煤mero de empleado, y se registra su nombre y direcci贸n y salario anual. Los controladores tienen que pasar un examen m茅dico anual, cuya fecha debe ser conocida.  
  
-Dentro de la plantilla de empleados del aeropuerto, los t茅cnicos se encargan del mantenimiento de los aviones (por lo que reciben un complemento mensual). Cada t茅cnico tiene un conjunto de modelos de avi贸n en los que est谩 especializado (no pueden ser m谩s de 7). Es posible que varios t茅cnicos est茅n especializados en el mismo modelo de avi贸n. Debe conocerse la fecha en la que cada t茅cnico aprob贸 el examen de especializaci贸n en un modelo determinado.  
  
-El aeropuerto (seg煤n normas internacionales) tiene estandarizadas un conjunto de pruebas de mantenimiento para que sean pasadas por los aviones. Cada prueba tiene un c贸digo internacional, una duraci贸n media aproximada y una puntuaci贸n m谩xima. Algunas pruebas se componen a su vez de otras sub-pruebas (hay que saber adem谩s el orden en que se deben pasar en este caso).  
  
-Debe conocerse las pruebas que ha pasado cada avi贸n y la fecha en la que se pas贸 y la puntuaci贸n concreta que el avi贸n alcanz贸 en cada prueba. Estas pruebas son realizadas por los t茅cnicos (nunca m谩s de 3), y debe registrarse el n煤mero de horas que dedic贸 cada t茅cnico a la prueba. Un t茅cnico no puede realizar una prueba sobre un avi贸n en el que no est茅 especializado.  
  
Indicar en un listado las RESTRICCIONES QUE NO QUEDAN RECOGIDAS EN EL DIAGRAMA.  
Nota: S贸lo es necesario representar aquellos atributos de las entidades que sean fundamentales para comprender el esquema. Representar de manera m谩s amplia (de la manera que parezca m谩s razonable) aquellos aspectos que no queden completamente definidos en el enunciado anterior. Razonar en cada caso la representaci贸n que se elige.
![[seminario 3.png]]

EJERCICIO B)  
  
Crear un diagrama Entidad-Relaci贸n (que modele capturando la mayor sem谩ntica posible), usando caracter铆sticas extendidas si es necesario y convertirlo posteriormente a una serie de tablas del modelo de datos relacional, para una empresa que vende seguros de vida y de hogar:  
  
- La empresa se dedica a vender seguros de vida y/o de hogar a los clientes. Para hacer el contrato de seguro se necesita el DNI, nombre, apellidos y direcci贸n del cliente al que se le hace el contrato (el tomador).  
  
- Todos los seguros que vende la empresa se identifican mediante un c贸digo 煤nico. En cada contrato de un seguro de vida, adem谩s del cliente, se registra la fecha de vencimiento y la cantidad anual del seguro (la prima), as铆 como la indemnizaci贸n por fallecimiento. Tambi茅n debe indicarse quienes son los beneficiarios del seguro (la persona o personas a las que se pagar谩 la indemnizaci贸n) mediante el DNI, nombre, apellidos y direcci贸n del mismo.  
  
- Puede darse el caso de que un seguro de vida tenga, m谩s de un tomador (pero nunca m谩s de 5). Adem谩s, en este caso, cada tomador puede indicar qui茅nes son sus beneficiarios (por ejemplo, un seguro puede ser tomado por Pepe y Lola, y Pepe nombrar como beneficiarios a Pepito y Pedrito, y Lola a Lolita y Luisita). El n煤mero de beneficiarios total (entre todos los tomadores) no puede ser mayor de 10.  
  
- En el caso de los seguros de hogar no es aplicable el concepto de indemnizaci贸n por fallecimiento ni de beneficiario, pero s铆 deben conocerse la cantidad asegurada por continente de la vivienda (鈥渃onstrucci贸n鈥?) y por contenido (鈥渕obiliario鈥?).  
  
- Cada contrato de seguro es gestionado por uno o varios agentes de seguros de la empresa, que recibir谩n cada uno una gratificaci贸n por conseguir el contrato (puede ser diferente para cada uno dependiendo del trabajo que hayan realizado para conseguir el contrato).  
  
- Los agentes de la empresa tienen asignado un c贸digo de empleado que se usa para la gesti贸n de n贸minas, seguros gestionados, etc. Se necesita conocer tambi茅n su nombre, apellidos, direcci贸n y nivel de ventas (alto, medio, bajo) y salario base mensual. Tambi茅n tienen un porcentaje de incremento del salario por productividad. Este porcentaje depende del nivel de ventas, de los contratos gestionados y de la cuant铆a de los mismos (seg煤n unos criterios especificados por la direcci贸n que no vienen al caso de este problema).  
  
- Algunos agentes tienen a su cargo la supervisi贸n del trabajo de otros agentes menos expertos, a los que deben calificar en su trabajo supervisado (mal, regular, bien, muy bien), indic谩ndose la fecha en la que se hizo esa calificaci贸n.  
  
Indicar en un listado las RESTRICCIONES QUE NO QUEDAN RECOGIDAS EN EL DIAGRAMA.  
  
Nota: S贸lo es necesario representar aquellos atributos de las entidades que sean fundamentales para comprender el esquema. Representar de manera m谩s amplia (de la manera que parezca m谩s razonable) aquellos aspectos que no queden completamente definidos en el enunciado anterior. Razonar en cada caso la representaci贸n que se elige.
![[Ej b seminario 2.png]]

---


鈾伙笍 Segunda parte -> [[Seminarios Parte 2 BD 馃巵]]