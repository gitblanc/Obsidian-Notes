# Seminario 1. Stakeholders

## ¿Qué es un stakeholder?

- Son las personas interesadas o implicadas en el proyecto y en la especificación de requisitos

## Tipos de stakeholders

- Internos
	- Empresas cliente, equipo de desarrollo...
- Externos
	- Clientes finales, inversores, competidores...

## Importancia de identificación de los stakeholders

- Distintos stakeholders proporcionan puntos de vista diferentes
- No identificarlos correctamente podría provocar insatisfacción
- Errores al identificar requisitos resultarán errores en las fases posteriores del proyecto

## Ejercicio 1. Identificar stakeholders

![](./img/Pasted%20image%2020231204142225.png)

- S1: personal médico
- S2: usuarios registrados (pacientes)
- S3: personal de administración
- S4: personal de la centralita
- S5: usuario administrador del sistema IRMed
- S6: todos los centros de salud de Asturias
- S7: usuarios no registrados
- S8: cliente (Conserjería de Salud)
- S9: equipo de traducción
- S10: equipo de marketing
- S11: equipo de desarrollo
- S12: proveedor de certificados
- S13: proveedor de nombre de dominio

## Ejercicio 2. identificar funcionalidades relacionadas con stakeholders previos

|Funcionalidad|S1|S2|S3|S4|S5...|
|---|---|---|---|---|---|
|Traducción a español e inglés|||||X|
|Todo usuario con tarjeta sanitaria puede registrarse en la aplicación|||||||
|Todo usuario registrado podrá realizar reservas que se verán en el calendario de reservas|||||||
|Los usuarios no registrados no podrán realizar reservas|||||||
|Todo usuario (registrado y no registrado) podrá ver el calendario de reservas|||||||
|El personal médico del centro podrá ver el calendario de reservas, pero no podrá hacer modificaciones|||||||
|La aplicación tendrá un único usuario administrador|||||||
|El administrador puede añadir roles a los administrativos del centro de salud|||||||
|El administrador puede dar permisos a los administrativos del centro de salud en caso de nuevas incorporaciones|||||||
|Gestión de cuentas de usuario|||||||

# Seminario 2. Requisitos no funcionales

## ¿Qué son los requisitos no funcionales?

- Son restricciones a las funcionalidades que ofrece el sistema
- Detallan cómo debe funcionar el sistema en vez de sus funcionalidades (requisitos funcionales)

## ¿Por qué son importantes?

- Ignorarlo ahora supone tener que arreglarlo en la fase de implementación

## Clasificación según Someville

![](./img/Pasted%20image%2020231204143019.png)

## Requisitos de producto

- Especifican cómo debe comportarse el software
	- De usabilidad
	- De eficiencia
	- De dependencia (disponibilidad, mantenibilidad, fiabilidad, integridad)
	- De seguridad

## Ejercicio. Clasificar requisitos de producto

![](./img/Pasted%20image%2020231204143319.png)

![](./img/Pasted%20image%2020231204143422.png)

## Requisitos organizacionales

- Estos requisitos derivan de políticas de la empresa cliente y de la empresa desarrolladora
	- De entorno
	- Operacionales
	- De desarrollo

## Requisitos externos

- Requisitos derivados de factores externos al sistema, por ejemplo, requisitos necesarios para que el sistema sea aprobado por un organismo regulador
	- Regulatorios
	- Éticos
	- Legislativos

## Ejercicio. Organizacionales vs Externos

![](./img/Pasted%20image%2020231204143715.png)

## Atributos de calidad

- Disponibilidad
- Fiabilidad
- Extensibilidad
- Escalabilidad
- Mantenibilidad
- Seguridad
- Usabilidad

## Ejercicio 1. Identificar requisitos no funcionales

![](./img/Pasted%20image%2020231204143847.png)

- RNF1: Un mensaje entre un usuario emisor y otro receptor ha de llegar del usuario emisor al receptor en menos de 2 segundos
- RNF2: Un usuario ha de poder autenticarse mediante contraseña
- RNF3: El sistema debe permitir autenticación de tipo MFA
- RNF4: El sistema debe almacenar los datos encriptados en una mongodb
- RNF5: El sistema debe permitir al usuario recuperar sus datos mediante un código previamente otorgado en la creación de su cuenta
- RNF6: El sistema debe cumplir los estándares de usabilidad para personas con discapacidad visual del W3C

# Seminario 3. Casos de uso

## ¿Qué es un caso de uso?

- Un caso de uso es la descripción de una funcionalidad del sistema y cómo interactúa dicho sistema con actores externos o actores

## ¿Qué es un escenario?

- Cada secuencia de interacciones posible de un caso de uso es un escenario
- Por tanto, un caso de uso contiene todos los escenarios posibles para que el actor primario consiga su objetivo

## ¿Qué es un actor?

- Es una persona, grupo de personas o incluso otro sistema
- Cada caso de uso está asociado con el objetivo de un actor, que es el actor primario

## Stakeholders vs actores

- Todos los actores son stakeholders, pero no todos los stakeholders son actores (no todos interactúan con el sistema) 

## ¿Cómo escribir un diagrama de caso de uso?

![](./img/Pasted%20image%2020231204144838.png)

## Elementos de un diagrama de caso de uso

![](./img/Pasted%20image%2020231204144821.png)

## Relación entre actor y caso de uso

![](./img/Pasted%20image%2020231204144906.png)

## Relaciones entre actores

![](./img/Pasted%20image%2020231204144937.png)

## ¿Cuál es la diferencia entre estos diagramas?

![](./img/Pasted%20image%2020231204145046.png)

- En el primero, los dos actores participan en el caso de uso a la vez
- En el segundo, lo hacen de forma individual

## Relaciones entre casos de uso

![](./img/Pasted%20image%2020231204145153.png)

## Includes

![](./img/Pasted%20image%2020231204145220.png)

## Extends

![](./img/Pasted%20image%2020231204145325.png)

## Generalización

![](./img/Pasted%20image%2020231204145345.png)

## Ejercicio 1. Escribir un caso de uso

![](./img/Pasted%20image%2020231204145502.png)

![](./img/Pasted%20image%2020231204145517.png)

![](./img/Pasted%20image%2020231204145559.png)

## Ejercicio 2. Diagrama de casos de uso

![](./img/Pasted%20image%2020231204145654.png)

![](./img/Pasted%20image%2020231204145723.png)

![](./img/Pasted%20image%2020231204145831.png)



