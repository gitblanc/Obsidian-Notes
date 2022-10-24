# 23 Sept 2022 🍮
---
## Seminario 1
## Herencia

### Ejercicio 1
**¿Una pila es un vector (ArrayList)?**
- No porque si heredamos, en este caso se hereda todo, y puede no servirnos la implementación. Se podrían insertar elementos en cualquier lugar de la pila, cosa que no se puede hacer.

- Hay que evitar que al modificar código afecte al cliente. Nuestro código ha de ser transparente para él.

- No sirve el criterio **Es-un**. No sirve que nos suene bien. No es un criterio válido para aplicar la herencia: ¿un dibujo **es una** figura? -> NO tiene por que

**Criterio para decidir si algo es subtipo de otro** -> ***criterio de pertenecia***: un objeto pertenecerá a una jerarquía si se quiere poder conectar a un cliente para que éste lo use como a uno más de la misma

¡Nunca debe surgir una jerarquía como una manera de clasificación!


### Ejercicio 3
No es correcto porque si existiese un método double getValor(), ¿qué devolvería?. Que compile es una cosa, y que tenga sentido es otra muy distinta.

- **Las interfaces surgen por la necesidad de declarar unas responsabilidades que un objeto ha delegado**
- **La jerarquía surge con alternativas de implementación de dichas responsabilidades**

### Ejercicio 4
**¿Un cuadrado es un rectángulo?**
- No es lo mismo redimensionar un rectángulo que un cuadrado
- Hay que razonarlo todo siempre en función de los clientes
- Para el cliente, un cuadrado no es un rectángulo

---
# 7 Octubre 2022 🍬
## Seminario 2
### Principios SOLID
- **SRP** (principio de responsabilidad única)
	- Una clase debería tener un único motivo para cambiar
- **OCP** (principio abierto cerrado)
	- Las clases deberían estar abiertas para la extensión pero cerradas a la modificación
- **LSP** (principio de sustitución de Liskov)
	- Si metemos una nueva necesidad, podemos declararla o tratar la excepción
- DIP (principio de inversión de dependencias)

==SOLUCION TAREA 4 lab: Crear dos interfaces y que luego el objeto implemente las dos==

---
# 21 Octubre 2022 🧸
## Seminario 3

Ej: Crear una clase Logger que permita mostrar mensajes de traza en una aplicación
`logger.log("¡Hola mundo!")`

¿Cómo podríamos garantizar que de dicha clase sólo exista un único objeto?

==Es un patrón singleton==: cuidado con ellos. Al fin y al cabo un singleton es una variable global.
PROBLEMAS de Singleton:
	- Casa mal con temas de concurrencia
VENTAJAS de Singleton:
	- Sigue siendo un objeto normal. Podríamos aplicarle herencia o composición por encima
````java
public class Logger{
	//la única instancia se crea desde dentro de Logger
	//inicialización perezosa
	private static final Logger instance = new Logger();

	//hacemos el constructor privado para que nadie pueda crear instancias
	private Logger(){}
		
	public void log(String cad){
		System.out.println(cad);
	}

	//método que devuelve la instancia
	public static Logger getInstance(){
		return instance;
	}
}
````
