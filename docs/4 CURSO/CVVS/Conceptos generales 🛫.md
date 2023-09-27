# Problemática general

![](./img/Pasted%20image%2020230920182345.png)

# Causas de los defectos en el software

- **Múltiples causas**
	- Falta de experiencia (proyecto, tecnologías, herramientas)
	- Falta información (requisitos mal documentados)
	- Falta de comunicación
	- Las presión y prisas durante el desarrollo
	- Recortes en los esfuerzos en testing y calidad
	- Descuidos
- **Múltiples lugares**
	- Especificación, diseño, implementación
- **Deberíamos garantizar**
	- Que hace lo que debe hacer (esperado)
	- Que no hace lo que no debe hacer (no esperado)
	- ¿Para todas las combinaciones de factores? ¡¡¡Infinito!!!

- No vamos a poder probar al 100% nada. No podemos garantizar que un sistema está absolutamente libre del problema
- ==Es mejor hacer pocos pero buenos tests==

# Error, defecto y fallo

- **Error:** Acción humana que produce un resultado incorrecto
- **Defecto:** Manifestación de un error. “Desperfecto” en un componente/sistema que puede causar que el software no realice su función requerida
- **Fallo:** Desviación en un componente o sistema respecto de su comportamiento esperado

- ==Suele caer en el examen==

![](./img/Pasted%20image%2020230920184610.png)

# CV&V Contexto

- **Conseguir calidad implica:**
	- **Hemos hecho las cosas correctamente**: El producto satisface los requisitos: Funcionales y de rendimiento (explícitos), de Calidad (implícitos)  
	- **Hemos hecho el sistema correcto**: Los requisitos corresponden a las necesidades del usuario

![](./img/Pasted%20image%2020230920184722.png)

# Definición de calidad

- Ability of a product, service, system, component, or process to meet customer or user needs, expectations, or requirements (ISO/IEC 24765:2009 Systems and software engineering vocabulary)

- The totality of characteristics of an entity that bear on its ability to satisfy stated and implied needs (ISO/IEC 9126-1:2001 Software engineering -- Product quality -- Part 1: Quality model)

- Definición informal (empresa de automoción): Filosofía, éxito de negocio, satisfacción del cliente (interno y externo), involucrar a todos, mejora continua (procesos, productos y servicios), y por tanto, coste.

- **Calidad del producto**: Grado en el que el producto software cumple los requisitos y necesidades
- **Calidad del proceso**: En qué medida se sigue el proceso y si se cumplen los estándares

# Verificación y Validación

- **Verification**: Confirmation, through the provision of objective evidence, that specified requirements have been fulfilled (ISO/IEC 12207:2008 Systems and software engineering--Software life cycle processes) (ISO/IEC 15288:2008 Systems and software engineering-- System life cycle processes)
- **Validation**: Confirmation, through the provision of objective evidence, that the requirements for a specific intended use or application have been fulfilled (ISO/IEC 15288:2008 Systems and software engineering--System life cycle processes, 4.37). In a life cycle context, the set of activities ensuring and gaining confidence that a system is able to accomplish its intended use, goals and objectives (ISO/IEC 12207:2008 Systems and software engineering--Software life cycle processes, 4.54)

- **Validación**: comprobar si lo que se satisface son los **requisitos** que se han especificado. Permite conocer si el producto se está haciendo correctamente
- **Verificación**: confirmación de si el sistema cumple las **necesidades** del cliente. Debe cumplir lo que el usuario desea hacer con el sistema, esté o no en los requisitos
# Múltiples formas

![](./img/Pasted%20image%2020230920190821.png)

- El **testing estático** no puede detectar fallos, porque no ejecuta la aplicación. Puede encontrar defectos
- En **testing dinámico** encontramos fallos, porque puede ejecutar la aplicación

# Revisiones

- **Review**: A process or meeting during which a work product, or set of work products, is presented to project personnel, managers, users, customers, or other interested parties for comment or approval (ISO/IEC 24765:2009 Systems and software engineering vocabulary)
- **Peer Review**: Review of work products performed by others qualified to do the same work (ISO/IEC 24765:2009 Systems and software engineering vocabulary) Note: often performed during development of the work products to identify defects for removal.

# Pruebas. Definición

- Set of activities conducted to facilitate discovery and/or evaluation of properties of one or more test items. Note: Testing activities could include planning, preparation, execution, reporting, and management activities, insofar as they are directed towards testing. (ISO/IEC/IEEE 29119-1:2013 Systems and software engineering – Software Testing - Part 1: Concepts and definitions)
	- Dynamic testing: testing that requires the execution of the test item
	- Static testing: testing in which a test item is examined against a set of quality or other criteria without code being executed
- The process consisting of all lifecycle activities, both static and dynamic, concerned with planning, preparation and evaluation of software products and related work products to determine that they satisfy specified requirements, to demonstrate that they are fit for purpose and to detect defects (ISTQB Standard glossary of terms used in Software Testing, Version 2.1)

- En la realización de pruebas hay que comprobar si se satisfacen los requisitos que nos han especificado
- Un buen caso de prueba es aquel que tiene una alta probabilidad de detectar un nuevo fallo

# Pruebas. Discusión

- ¿Las pruebas son verificación o validación?
	- Ambas
- ¿El objetivo es detectar errores? 
	- No, es detectar fallos y defectos
- ¿Es el único objetivo?
	- No, también lo es acotar un nivel de confiabilidad y acotar la calidad
- ¿Si a corto plazo voy a ser desarrollador, me interesa esto?
	- Si porque es el primero que está interesado en la calidad de lo que desarrolla

# Pruebas. Clasificación

- Ejecución  
	- **Dinámicas**: se ejecuta 
	- **Estáticas**: no se ejecuta
- Visibilidad de la estructura interna 
	- **Caja negra**: no es visible  
	- **Caja blanca**: es visible

- Caja negra es cuando no vemos el código

# Proceso de pruebas dinámicas

![](./img/Pasted%20image%2020230920194523.png)

# Pruebas Continuas

- Evolución hacia Agile y DevOps: 
	- Desarrollo Continuo
	- Pruebas Continuas
- Pero
	-  No basta con que las pruebas se ejecuten de forma automática
	- Deben ser BUENAS pruebas (Importancia del uso de técnicas)

- **Condición de entrada**: se obtienen examinando entradas o salidas de la aplicación

# Partición en Clases de Equivalencia

![](./img/Pasted%20image%2020230927183119.png)

## Problema 1

![](./img/Pasted%20image%2020230927184900.png)

- Condición de prueba y de entrada: importe
- Las clases de equivalencia serían 
	- < 10.000
	- entre 10.000 y 50.000
	- > 50.000
	- < 0 (Clase de equivalencia inválida)
	- = 0 (Clase de equivalencia inválida)

## Problema 2

![](./img/Pasted%20image%2020230927184919.png)

- Condición de prueba y de entrada: saldo
- Las clases de equivalencia serían:
	- < 10.000
	- entre 10.000 y 50.000
	- > 50.000

## Problema 1b

![](./img/Pasted%20image%2020230927185949.png)

- Casos de prueba:

![](./img/Pasted%20image%2020230927190022.png)

- Los **casos de prueba lógicos** describen como son las entradas y las salidas, pero no nos dan valores concretos (Salidas)

- La diferencia entre los casos de prueba físicos y lógicos es que los físicos dan valores concretos y los lógicos no

# Clases de equivalencias de las salidas

![](./img/Pasted%20image%2020230927190708.png)

# Las condiciones de entrada no son necesariamente los parámetros de un programa

![](./img/Pasted%20image%2020230927192148.png)

![](./img/Pasted%20image%2020230927192520.png)

# Análisis de valores límite

![](./img/Pasted%20image%2020230927193937.png)

![](./img/Pasted%20image%2020230927194004.png)


