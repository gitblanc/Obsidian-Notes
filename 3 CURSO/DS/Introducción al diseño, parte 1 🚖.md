# 20 Sept 2022 🚆
---
- El problema del software es que los requisitos van a **cambiar**. Por tanto, un código mal diseñado, en el momento funcionará, pero en un futuro es probable que deje de hacerlo, y si se diseña bien desde el principio será mucho más fácil mantenerlo.
- El DOO (diseño orientado a objetos) construye las aplicaciones mediante una estructura de objetos que colaboran entre sí.
- Cada objeto realiza unas operaciones que lo caracterizan (no importa cómo las realiza, sino cuáles realiza)
- La implementación de esas operaciones son los **métodos**

- **Signatura de la operación**: cada operación declarada por un objeto específica (su nombre, los objetos que recibe como parámetros y el tipo de valor devuelto por la operación).
- **Tipo**: nombre usado para denotar una determinada interfaz. Un objeto puede tener muchos tipos, así como objetos muy diferentes pueden compartir un mismo tipo (**polimorfismo**)
- La operación que se ejecuta cuando se envía una petición a un objeto depende de la **petición** (el método) y del **objeto receptor** (figura.dibujar)
- El **enlace dinámico** permite:
	- Escribir programas que esperen un objeto con una interfaz determinada, sabiendo que cualquier objeto que tenga esa interfaz aceptará esa petición.
- **Polimorfismo**: capacidad de dos o más tipos de objetos de responder al mismo mensaje, cada uno a su manera. Nos permite tener una lista de figuras y poder dibujarlas todas sin conocerlas.

-  A - - - > B: A crea objetos de B, A implementa objetos de B
- A ------> B: 
- `<<create>>`: para definir tipos

## Creación de objetos
- Ya no sólo hay que decidir qué hacer, sino también quién debe hacerlo (sis e aprende a hacer las cosas sin un quién luego no se ve la necesidad de introducirlo)
- **Síntomas de programación estructurada encubierta**: **IMPORTANTE**
	- *Métodos largos* (más de 10 líneas). Si sucede mirar:
		- No está delegando funcionalidad (un método que haga dos o más cosas, sólo debería hacer 1 cosa)
	- *Abundancia de llamadas a métodos del mismo objeto*
	- *Preguntarse cómo se calcula un factorial en un lenguaje OO* (lo importante es quién lo va a hacer, no cómo)
	- *Típica clase utilidades* (Utils, Manager, ...). No se encuentra el quién, por lo que se agrupan funcionalidades.

- **Atributos**: guardan el estado entre la invocación de un método a otro.
- **Regla para saber si es atributo o no**: ¿Ese dato afecta al comportamiento de otra operación como para que deba recordarlo?

## Criterios
- Un objeto no puede presuponer una secuencia de mensajes determinada
- Cada mensaje debe ser tratado de acuerdo al estado actual del objeto
- No debe haber ninguna secuencia de mensajes que corrompa al objeto

## Parámetros
- Son la forma de enviar información junto al mensaje
- **Los operandos** permanecen estables mientras que las opciones pueden variar a medida que la clase evolucione
- Un parámetro es una opción si se puede encontrar un valor predeterminado adecuado

## Encapsulación
- Normalmente no se debe dar acceso a los datos internos de un objeto (métodos get). Permite controlar las modificaciones del atributo.
- Hay que diferenciar entre **estado concreto** y **estado abstracto**.

## Lo que no funciona
- Basarse en objetos reales
- No sirve extraer nombres y verbos del lenguaje natural
- Además puede expresarse de varias maneras

## Guía práctica
1. Elegir una tarea a realizar: el qué
	- Decidir qué tipo de objeto lo hará
	- ¿Puede hacerla alguna de las clases que ya tenemos?
2. Decidida la clase y la responsabilidad, tocan los mensajes (métodos), para dividir la responsabilidad en operaciones
3. Implementación de las operaciones
	- No preocuparse por la eficiencia hasta el final
