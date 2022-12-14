# 1. Modelo de objetos
---
- **Análisis**: pone énfasis en una investigación del problema y los requisitos, en vez de la solución
- **Diseño**: pone énfasis en una solución conceptual que satisface los requisitos
- **Diseño orientado a objetos** (DOO): definición de los objetos software y cómo colaboran para satisfacer los requisitos
- **Programación estructurada**: separa las estructuras de datos de los algoritmos que las manipulan

- Los objetos **colaboran** entre sí
- Cada objeto realiza unas **operaciones** que lo caracterizan
- No importa cómo las realice, sino **cuáles** realiza
- La implementación de esas operaciones son los **métodos**
- Un objeto lleva a cabo una **operación** cuando recibe una petición (o **mensaje**) de un cliente
- Las operaciones son el único modo de cambiar el estado interno del objeto
- Por ese motivo se dice que el estado interno del objeto está encapsulado

- **Interfaz de un objeto**: el conjunto de todas las signaturas públicas definidas por él, es decir, las peticiones que pueden hacérsele
- **Tipo**: nombre usado para denotar una determinada interfaz
- Un objeto puede tener muchos tipos, así como muchos objetos muy diferentes pueden compartir un mismo tipo
- **Enlace dinámico**: asociación en tiempo de ejecución que tiene lugar entre la petición a un objeto y una de sus operaciones, lo que permite el **polimorfismo**
	- **Polimorfismo**: cualquier objeto que implemente una interfaz concreta podrá ser reemplazado por otro que implemente esa misma interfaz
- **Polimorfismo**: capacidad de dos o más tipos de objetos de responder al mismo mensaje, cada uno a su manera. Nos permite tener una lista de figuras y dibujarlas todas sin conocerlas:
![[Pasted image 20221214170838.png]]
![[Pasted image 20221214170906.png]]
- La **clase** es una de las formas de crear tipos en Java
- Se dice que un objeto es una **instancia** de una clase
- El operador "**new**" crea un nuevo objeto y devuelve una referencia a él

- Síntomas de mala programación orientada a objetos:
	- Métodos largos (más de 10 líneas)
	- Abundancia de llamadas a métodos del mismo objeto

- El diseño de una clase **NO** se empieza por sus atributos, sino que se plantean primero las acciones que debe realizar el objeto (usando o bien atributos o bien delegación en otros objetos)

- **Operando**: objeto que el método necesita para operar. Permanecen estables
- **Opción**: forma de operar con los operandos. Pueden variar a medida que la clase evolucione

- Los parámetros de un método deben ser sólo operandos
![[Pasted image 20221214171825.png]]
![[Pasted image 20221214171840.png]]
![[Pasted image 20221214171859.png]]
![[Pasted image 20221214172008.png]]
![[Pasted image 20221214172019.png]]

- **Estado de un objeto**: combinación de los valores de los atributos de un objeto. Guardar el estado de un objeto supone guardar la suficiente información para que al recuperarla se obtengan exacmtamente las mismas respuestas ante la misma secuencia infinita de mensajes tanto del original como del objeto recuperado. Generalmente basta con guardar los atributos
- Normalmente no se debe dar acceso a los datos internos de un objeto (**encapsulación**), sino que se deben de usar **métodos de acceso**, es decir, getters y setters. Permite controlar las modificaciones del atributo.
- Ocultar los atributos permite modificar la implementación sin afectar a los clientes

- **Criterio de independencia**: cuanto menos se sepa de la implementación de un objeto, menos afectarán sus cambios. Por eso una clase no debe saber de otra. Lo único importante de un objeto son los mensajes que puede recibir

- **Estado concreto**: se define en función de los atributos, puede variar
- **Estado abstracto**: se define en función de las respuestas a los mensajes
- Cuando hablamos de estado siempre nos referimos al estado abstracto

### Como ***no*** diseñar clases
- Basarse en objetos reales
- Extraer nombres y verbos del lenguaje natural

## Guía para crear una clase
1. **Elegir una tarea a realizar: el qué**
	a) Decidir qué tipo de objeto lo hará
	b) ¿Puede hacerla alguna de las clases que ya tenemos?
2. **Decidida la clase y la responsabilidad, tocan los mensajes**
	- Dividir la responsabilidad en operaciones (atómicas para que se puedan combinar)
	- Parámetros con información imprescindible
	- Sacar partido de que los objetos recuerdan lo que se les ha mandado
3. **Implementación de las operaciones (métodos)**
	- No preocuparse por la eficiencia hasta el final

# 2 Interfaces y clases abstractas
---
![[Pasted image 20221214173858.png]]
![[Pasted image 20221214173933.png]]

## Interfaces
- Permiten comunicar objetos que ==no se conocen==
- Un objeto que quiera ser contratado debe cumplir con el contrato (es decir implementar la interfaz en cuestión)
![[Pasted image 20221214174122.png]]
- La revisión del contrato se hará de manera estática (se sabe en tiempo de compilación)
![[Pasted image 20221214174230.png]]

## Herencia
### Tipos
- **De interfaz**: declaramos el compromiso de implementar unos métodos (subtipos)
- **De implementación**: creación de una clase a partir de la implementación de otra (reutilización del código)

## ==Criterio de diseño==
- Cuando un objeto deba delegar ciertas operaciones en tro deberá exigírselas mediante una interfaz
	- Importan los mensajes que acepta el objeto
	- No de quién ha obtenido su implementación

## Clases abstractas
- Evitan la duplicación de código en clases que hacen prácticamente lo mismo
![[Pasted image 20221214174842.png]]
![[Pasted image 20221214174855.png]]
![[Pasted image 20221214174911.png]]

- Uno de sus usos es factorizar código propio
- AbstractAdepto se denomina clase base abstracta
	- Quedan mensajes sin implementar, luego no se puede instanciar
	- Se usa como implementación base para otras clases
- Una clase base puede dar implementación a todos los métodos de la interfaz
	- Entonces se denomina **clase base concreta**
	- Pueden instanciarse directamente
- Otro de sus usos es facilitar la extensión
![[Pasted image 20221214175323.png]]

### Uso práctico de las clases abstractas
- A la hora de implementar una interfaz, miraremos primero qué implementaciones nos vienen ya preparadas (escoger la más cercana)
![[Pasted image 20221214175540.png]]![[Pasted image 20221214175554.png]]

Una clase abstracta puede:
- Dejar un método sin implementación para que lo implementen las clases derivadas
- Dar la implementación completa del mensaje

¿Cómo conseguimos que cambie solo parte de la implementación?
![[Pasted image 20221214175815.png]]
- Aquí es donde aparecen los métodos abstractos
- Se separa la parte común y la parte específica de la implementación
	- La clase base contendrá la parte obligatoria
	- Las clases derivadas aportarán la parte específica en nuevos mensajes
	- ¡Para esto sirve el **protected**!
	- Indica que hay que completar una implementación parcial
![[Pasted image 20221214180040.png]]

## Resumen

- La herencia de implementación (clases abstractas) se utiliza como soporte de las interfaces
	- Permiten colocar implementaciones comunes en clases base
- Una clase base puede ser:
	- **Abstracta** si sólo implementa parte de los mensajes (sólo puede ser usada para heredar de ella)
	- **Concreta** si implementa todos los mensajes (puede ser instanciada y usada directamente)
- Para cada operación, una clase abstracta puede:
	- Dar una implementación completa
	- Dar una implementación parcial delegando el resto en otros métodos
- Las clases que deriven de la clase base
	- Tendrán que implementar los mensajes que queden sin implementar completamente o parcialmente (**protected**)
	- Y podrán redefinir los ya implementados aprovechando o no dicha implementación (**super**)

## Extensión
- Las clases en una jerarquía lo normal es que sean implementaciones de una determinada interfaz
- Normalmente los clientes interactuarán con los objetos a través de dicha interfaz

## Jerarquías de interfaces
![[Pasted image 20221214180824.png]]
![[Pasted image 20221214180930.png]]

- ¡No hace falta tener jerarquías para que un diseño sea orientado a objetos!
- Las interfaces surgen por la necesidad de declarar unas responsabilidades
- Por tanto, ==nunca debe surgir una jerarquía como mera clasificación==
	- No hay que buscar un árbol equilibrado, tan sólo hay que comprobar que todas las interfaces tengan al menos un cliente que la use
![[Pasted image 20221214181225.png]]

## Jerarquías de clases abstractas
![[Pasted image 20221214181319.png]]

- ¿De dónde salen las clases abstractas?
	- Del implementador de la interfaz
	- Del implementador de las clases concretas mediante **refactoring**
![[Pasted image 20221214181445.png]]
![[Pasted image 20221214181508.png]]

- Una jerarquía de implementación de clases abstractas no es esencial que sea estable:
	- El cliente sólo conoce la interfaz
	- No le afectan las reorganizaciones que haya en sus implementaciones
- Las jerarquías de implementación son para compartir código común y puede reestructurarse cuantas veces se necesite
	- Si desaparece rombo fusionar FiguraPoligonal y Rectángulo
	- No hace falta pensar en el futuro lejano: reorganizar el árbol en función de las necesidades actuales

- En el análisis no importa el código ni tampoco el diseño, sino los métodos (pero no su implementación interna)

## Resumen Interfaces vs Clases abstractas

Repasemos sus diferencias atendiendo a:
- En qué momento se crea cada una
- Quién es su creador en el proceso de desarrollo (analista, diseñador,
programador)
- ¿Pueden ser raíz de una jerarquía?
- Importancia dentro del paradigma
	- ¿Qué consecuencias tendría para el lenguaje de programación quitar cada una de ellas?
- Qué hacen con respecto a las operaciones de sus ancestros
	- Añadir, redefinir, eliminar
- Impacto en el resto del diseño si cambiamos unas u otras
![[Pasted image 20221214182147.png]]
![[Pasted image 20221214182358.png]]
