- Si el código es difícil de cambiar, es de **mala calidad**
- La **facilidad del cambio** es más importante que la **solidez** de un problema
- ¿Cómo construír un buen sistema?Aspectos a tener en cuenta:
	- La arquitectura de un sistema depende mucho de las estructuras de los equipos
	- Las estructuras dependen de la forma de trabajar en los equipos
	- Las colaboraciones humanas dependen de sus experiencias de vida
- Objetivos de una arquitetura. El código ha de ser:
	- Fácil de **cambiar**
	- Fácil de **probar**
	- Fácil de **desplegar**
- Principios de una arquitectura:
	- Conoce bien el problema
	- El código ha de ser legible (ahora y siempre)
	- Intenta desacoplar los dominios del sistema (que las partes puedan resolver partes del problema)
	- Aplicar el Single Responsability Principle 
	- **TDD** (Test Driven Development), muy buena herramienta para autodocumentar el código, pues cada test es un contrato implícito de cada parte del código
- Hoy en día no hay prácticamente sistemas con microservicios, sino que hay sistemas **monolitos distribuidos** (varios servicios que usan una misma BBDD por ejemplo).
Monolito vs microservicios:
![[Pasted image 20230215122942.png]]
Monolito distribuido vs microservicios:
![[Pasted image 20230215123004.png|400]]

---