---
title: Notas de Lab de DS 🛥️
---
*Nota: las soluciones de una práctica están en la siguiente o en la misma* 

Si se quiere mirar ejemplos de cualquier lenguaje de un patrón de diseño, consultar la página [Refactoring Guru](https://refactoring.guru/es)
# Lab 1
- Solución: aplicar un **Strategy**
# Lab 2

- Es importante sacar un loader para que la Máquina Virtual no tenga 2 responsabilidades (cargar el programa y ejecutarlo)
- Solución: aplicar un **State** y un **Template Method**
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

- Solución: patrón **Command**. Sabe el cuándo pero no el qué. El qué le pasa un comando al cuándo.

- Al Command lo caracteriza el tiempo entre que se crea y se ejecuta.

````java
new CommandX().execute() //<-- suspenso directo xd
````

- contraseña: csol
# Lab 6

- Solución: patrón **Adapter**.
- Contraseña: solc
- Para la extensión del miniformulario, crear una interfaz Editable con los métodos correspondientes (getters y setters de la interfaz *Editable*: primer valor, segundo valor, primer nombre, segundo nombre). El main quedará tal que:
````java
for (Foto foto : db.selectFotos()) {
	map.add(new FotoAdapterEditable(foto));
}
````

- No hay que crear un adaptador para todo
	- Crear un adaptador para cada cosa específica

# Lab 7

- Para la solución inicial (clase 7 mejorada) -> patrón Strategy
- Solución: **patrón Decorator**
- Contraseña: decorator

# Lab 8

- La clase UserInterface no se toca
- Solución: patrón **Observer** y **Decorator** para la encapsulación
- Contraseña: FALTA -> pedir a raúl

### Comparativa Observer vs Command

- **Command**: Tengo un objeto que cuando ocurre un evento ejecuta uno (o varios) comando(s). Su misión no es almacenar datos, sino saber cuando se lanza un evento y ejecutar dichos comandos. ==*Si no tiene comandos registrados, no tiene sentido que exista, pues no hay ningún dato que consultar*==
- **Observer**: es útil aunque no haya eventos porque guarda datos (por ejemplo un contador de votos a favor y en contra en una encuesta). ==*Tiene sentido que exista aunque no contenga eventos, pues aún así contiene datos que pueden ser utilizados por otras partes de la aplicación*==

# Lab 9

- Solución: patrón **Visitor**

### Lab 9 2024

- Solución 1: **Strategy**
- Solución 2: **Template Method**

**Explicación**:

- Utilizar un **Strategy** sería adecuado en caso de que el cliente desee cambiar en tiempo de ejecución la plataforma en la que ejecutar el juego (por ejemplo un debugger o un desarrollador).

- Utilizar el **Template Method** sería adecuado para un cliente que ejecute el juego directamente en la consola, es decir, no quiera cambiar en tiempo de ejcución la plataforma de juego

**Relación**: Template Method trabaja al nivel de la clase, por lo que es estático. Strategy trabaja al nivel del objeto, permitiéndote cambiar los comportamientos durante el tiempo de ejecución.


