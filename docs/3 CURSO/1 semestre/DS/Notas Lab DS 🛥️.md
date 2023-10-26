*Nota: las soluciones de una práctica están en la siguiente*
# Lab 1
- Solución: aplicar un **Strategy**
# Lab 2
- Solución: aplicar un **Template Method**
- Contraseña: sol2

- Nota: método execute() y doExecute() que es el que varía 
# Lab 3
- Patrón **State**
	- Sirve si: Quiero cambiar dinámicamente su implementación (su estado)
	- El State es la herramienta (distintas formas de mover, soltar y pinchar)
- El método doCreaFigura(Editor editor) es privado.
	- Le llamamos así porque es el método a redefinir en cada clase que extiende de la abstracta
- No empezar por la clase abstracta, sólo crearla si es necesario y vemos código repetido
- contraseña: 3sol
# Lab 4

- Solución: aplicar patrón **Strategy** (la primera parte hasta ValidadorPredefinido) y el patrón **Composite** para el resto de validaciones
	- Es un poco mejor la solución de Raúl
- Contraseña: solval

# Lab 5

Solución: patrón **Command**. Sabe el cuándo pero no el qué. El qué le pasa un comando al cuándo.

Al Command lo caracteriza el tiempo entre que se crea y se ejecuta.

````java
new CommandX().execute() //<-- suspenso directo xd
````

- contraseña: csol
# Lab 6