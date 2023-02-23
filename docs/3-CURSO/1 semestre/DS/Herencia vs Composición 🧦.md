## Herencia

Empecemos con la definición: **Herencia es cuando un objeto o clase se basa en otro objeto o clase, usando la misma implementación o comportamiento**. Esto es un mecanismo para la reutilización de código para permitirnos extensiones independientes del software original mediante clases públicas e interfaces.

Bien, no te preocupes si te suena un poco a chino, lo entenderás con el desarrollo que vamos a ir haciendo. Pero permíteme pedirte que recuerdes eso de _extensiones independientes_.

Para simplificar esta definición y ajustar al máximo lo que debe ser la herencia vamos a hacer un ejercicio de abstracción y vamos a decir que **la herencia tiene cabida donde existe una relación “es un/una”**. ¡Cuidado!, esta relación es unidireccional hacia la clase padre. Pongamos un ejemplo para verlo mejor:

[![Esquema de herencia](http://devexperto.com/wp-content/uploads/2016/04/concepts-bikeHierarchy.gif)](http://devexperto.com/wp-content/uploads/2016/04/concepts-bikeHierarchy.gif)

La bicicleta simple arriba sería la super clase, y los tipos concretos abajo, diríamos que son las subclases. Es decir el supertipo o abstracción es la superclase de los subtipos o concreciones. Además decimos que una bicicleta de carretera es siempre una bicicleta, pero sin embargo, una bicicleta no tiene por qué ser siempre de carretera, puede ser de cualquier otro tipo concreto. Esto quiere decir que es unidireccional, el hijo es un tipo concreto de lo que es el padre.

### Polimorfismo

Esto nos otorga también una propiedad que se llama **polimorfismo, que quiere decir que cualquiera de las formas hijas pueden adoptar la forma padre**, o lo que es lo mismo, el padre puede estar enmascarando a cualquier hijo mediante su forma.

Una de las principales potencias de la herencia es el polimorfismo que nos permite abstraernos del objeto concreto que usamos y trabajar con los supertipos.

### La relación de «ser» vs «tener»

La connotación de la relación “es un” es más fuerte de lo que creemos, porque ha de ser de por vida, ¿qué quiere decir esto? lo vemos mejor con un ejemplo:

A ti te encanta correr, y podríamos decir que “eres un runner”, pero claro, es posible que cuando tengas 10 nietos y 80 años prefieras dedicar tu tiempo a la fotografía por ejemplo y dejes de ser un runner. Pues ahí tienes una falsa relación “es un”.

**Hubiera sido un error plantear la clase que representa tu persona como herencia de runner porque tú no eres un runner de por vida** (lo siento por mucho que queramos, y eso que a mi también me gusta correr). Simplemente en ese momento de tu vida tenías un Rol. Y te pido que de nuevo recuerdes, esta vez, el verbo “Tener”.

¿Por qué tanto énfasis en el significado de “ser o no ser” en la herencia? porque realmente es necesario tener en cuenta esto y la herencia no hubiera cogido tanta mala fama si antes de usarla todos nos hubiéramos planteado esa pregunta de la forma que arriba os comento.

### Ventajas de la herencia

La mala fama de la herencia no es por que sea mala per se, es porque **en el 95% de los casos que vas a usar herencia, si no te planteas las preguntas correctas la vas a usar mal**. Porque la herencia engatusa. Sí sí, te seduce con sus beneficios, es el lado oscuro, y tiene todas estas ventajas:

-   La herencia es atractiva porque permite reutilizar código de una manera rápida, sencilla y evidente.
-   La herencia es poderosa porque me permite jugar con el polimorfismo con facilidad.
-   La herencia me permite sobrescribir métodos, así que si algo no es exactamente como espero siempre puedo cambiarlo si fuera necesario, por lo que es versátil.
-   La herencia usando algo parecido al patrón de diseño [Template Method](https://es.wikipedia.org/wiki/Template_Method_(patr%C3%B3n_de_dise%C3%B1o)) me permite crear clases abstractas que hacen que al heredar de ellas me quede un desarrollo guiado por la plantilla creada, ahorrando así tiempo y quedando un desarrollo guiado muy sencillo.

Son un montón de ventajas que nos empujan a usar herencia en nuestros primeros razonamientos y además son, en cierto modo, verdad. Pero en algún momento se volverán contra ti, con todas sus fuerzas.

### ¡Alerta! Cuándo la herencia se vuelve en tu contra

La experiencia en muchos proyectos, y de muchos desarrolladores, lo ha demostrado. Hay más razones que te pueden llevar a usar herencia en un primer momento, pero estas son las que primero se nos vienen a la cabeza. Vamos a ver por qué se vuelven contra nosotros estos “caramelitos”.

La principal razón es bastante obvia aunque no lo parezca. En un proyecto que se enmarca en un proceso de desarrollo ágil, donde los requisitos cambian constantemente y no están para nada bajo control, es imposible hacer suposiciones del tipo: “esta pantalla va a tener que realizar siempre esta acción”, “esta respuesta de servidor siempre tiene 4 listados”. **Borra de tu mente la palabra siempre, siempre guía de forma equivocada en nuestra mente a “es un” y eso guía a herencia**.

Por lo tanto en etapas iniciales del proyecto, que es donde precisamente más incertidumbre tenemos, **es prácticamente imposible intentar modelar comportamiento basado en pautas que podamos considerar constantes**, porque nos guste o no, todo está sujeto a cambio.

Por ese motivo, si empezamos a usar comportamientos heredados, aunque podamos a priori obtener resultados rápidos y robustos, en algún momento empezarán a sucederse cosas que yo categorizo con nombres como estos: “la fiesta de los override”, “el aluvión de métodos heredados inservibles”, “la herencia de 7 niveles”, “el quiero heredar y no puedo porque estoy sujeto a otra herencia” y un montón de inconvenientes muy muy divertidos que van a ensuciar nuestro código con el cambio, y el cambio es cuestión de tiempo.

Pues bien, el problema de los problemas, es mal usar la herencia, es decir, utilizar herencia en el lugar y momento inadecuados. De hecho hacer eso es lo más parecido que hay a hipotecar tu software: al principio todo es muy bonito y todo funciona, pero cuando empieces a pagar intereses… ¡Ay! pobre de ti.

## Composición

La definición viene a decir algo así: **Composición quiere decir que tenemos una instancia de una clase que contiene instancias de otras clases que implementan las funciones deseadas**.

Es decir, estamos delegando las tareas que nos mandan a hacer a aquella pieza de código que sabe hacerlas. El código que ejecuta esa tarea concreta está sólo en esa pieza y todos delegan el ella para ejecutar dicha tarea. Por lo tanto estamos reutilizando código de nuevo.

Vamos a ver un esquema como en el caso anterior:

[![Esquema de composión](http://devexperto.com/wp-content/uploads/2016/04/composicion-esquema.png)](http://devexperto.com/wp-content/uploads/2016/04/composicion-esquema.png)

En este caso decimos que el coche esta compuesto por ruedas, volante, cinturones de seguridad, luna… es decir, el coche tiene elementos o usa elementos para hacer todas las funciones que puede realizar. Delega sus responsabilidades en colaboradores designados para cada responsabilidad.

¿Te acuerdas de «tiene» en el contexto del rol del runner? Tenías el rol de runner, es decir, era una cualidad de tu persona en ese momento. Lo que aplica en ese caso por lo tanto es la composición también.

En este caso, el coche como tal no está atado a nada que le diga que tiene que usar unos neumáticos concretos en sus ruedas como podía pasar en la herencia por ejemplo. Las ruedas de hecho son una pieza modular e intercambiable que tiene interacción con el coche por medio de una interfaz. Pero las ruedas saben como ser rueda y qué neumático les viene bien. Es su labor.

Esta forma de diseñar nuestro software **nos permite que el resultado sea un sistema mucho más flexible en tiempo de programación e incluso en tiempo de ejecución**.

## Comparativa

Todo parecen ventajas con la composición, ¿no? Bueno no es tan fácil, algo malo ha de tener… Vamos a ver una tabla que hace una comparativa.

Como podemos ver, **un diseño basado en composición requiere mucho más tiempo**. Es un software más mimado, más pensado, que requiere de un número mayor de clases que hacen cosas más concretas

¿Te acuerdas del [principio de responsabilidad única](http://devexperto.com/principio-responsabilidad-unica/)? Pues eso es, muchas piezas interactuando entre sí, donde cada una tiene una y sólo una tarea que es su razón de existir.

![Comparación Herencia vs Composición](http://devexperto.com/wp-content/uploads/2016/04/Captura-de-pantalla-2016-04-15-a-las-22.01.51.png)

Por seguir marcando diferencias entre la herencia y la composición, cabe destacar que **la herencia se relaciona en una forma 1:1**. Esto evidentemente es provocado por la relación “es un”, donde un subtipo “contiene” un y sólo un subtipo, entre comillas porque no lo contiene realmente, es él mismo “per se” es padre e hijo al mismo tiempo.

Sin embargo, **haciendo uso de composición podemos elegir si vamos a tener 0, 1 o N elementos con los que interactuar del mismo tipo**. Esto es muy versátil en tiempo de ejecución incluso, ya que podemos hacer que un objeto que tenía un rol deje de tenerlo, por ejemplo.

Esto hace que a su vez **en la composición entre en juego la creación/destrucción de elementos dentro del objeto compuesto**. Esto no existe por ejemplo en herencia ya que el objeto ya tiene lo que viene dado y lo que pueda implementar por extensión.

### Usando polimorfismo en la composición

Y aquí viene lo peor de la composición, pero no te asustes, podemos solucionarlo. **La composición por si misma no es polimórfica**. Esto era de esperar, pero hay una solución muy potente a esto: ¿Qué pasa si hacemos que nuestros objetos compuestos implementen las interfaces que nosotros queramos?

¡Efectivamente! **Con el uso de interfaces, podemos hacer que nuestros objetos compuestos se hagan pasar por la forma que nos venga bien**. Y lo que es mejor, puedes implementar varias interfaces en cualquier momento o dejar de implementarlas con muchas más versatilidad que en la herencia, sin estar atado a nada más que los métodos que implemente esa interfaz concreta.

Veamos un ejemplo:

[![Polimorfismo en la composición](http://devexperto.com/wp-content/uploads/2016/04/Captura-de-pantalla-2016-04-15-a-las-22.38.42.png)](http://devexperto.com/wp-content/uploads/2016/04/Captura-de-pantalla-2016-04-15-a-las-22.38.42.png)

Como puedes ver _MainActivity_, que puede ser una pantalla cualquiera en Android, tiene una funcionalidad que le viene dada por medio de un elemento que contiene y no por heredar de nada, y la forma que tiene de decir al resto del mundo que sabe navegar es usando la interfaz _NavigationInterface_.

Si dejara de tener esa cualidad, no tendría más que dejar de implementar la interfaz y no hacer uso del objeto o eliminarlo. **Si esto fuera herencia, y tuviéramos dos niveles de herencia ¿que pasaría si ya no quiero o necesito tener la funcionalidad del primer nivel pero necesito la del segundo? Como puedes ver, el segundo nivel de herencia esta fuertemente acoplado al primero** y no podemos tener el segundo sin el primero.

Además ¿que hubiera pasado su cambiamos primer y segundo nivel para nuestras necesidades y más clases dependen de ellos? Todo eso provocaría fallos, efectos de lado.

Sin embargo, en este caso, al igual que tenemos la funcionalidad de navegación, podríamos asignar y eliminar otras siguiendo la misma estrategia sin que otras clases se puedan ver afectadas por el cambio.

### Cambiando el comportamiento en tiempo de ejecución

Voy más allá: imagina que el _NavigationDelegate_ no es una implementación concreta sino que es una interfaz a su vez. Esto nos permitiría usar un [patrón Strategy](http://devexperto.com/patrones-de-diseno-software/) para que pudriéramos cambiar incluso en tiempo de ejecución la navegación concreta que queremos en cada momento.

Quizás nos interese en un momento bloquear el evento de _back_, y hay una implementación de la interfaz _NavigationDelegate_ que asignamos según nos convenga a nuestro objeto compuesto. Maravilloso ¿no crees?.

Para que no haya pie a la confusión, hemos hablado de dos interfaces:

-   La primera otorga el polimorfismo a nuestro objeto compuesto que se perdía al usar composición, y a su vez sirve como “una declaración de cualidades” que puede tener nuestro objeto compuesto, es decir, define aquello de lo que es capaz de hacer.
-   La segunda otorga a nuestro objeto compuesto la flexibilidad de poder cambiar quién va a implementar la tarea concreta en cualquier momento.

## Cuando la herencia tiene sentido

Bueno, si sigues empeñado en usar herencia en ciertos casos, ¡vamos a ver en qué casos tiene cabida!

-   Si tenemos dos clases directamente relacionadas que están basadas una en la otra y pertenecen al mismo dominio lógico, y **estás seguro de que no van a cruzar fronteras no deseadas** (por ejemplo ni ellas ni ninguna extensión saldrá del paquete), puedes optar por una relación de herencia.
-   Si **la subclase es y será siempre algo basado en la superclase** y además la implementación de la superclase es apropiada e incluso necesaria para la subclase , puedes aplicar herencia sin miedo a equivocarte.
-   Si además de lo que acabas de leer, **la subclase es candidata a sólo añadir nueva funcionalidad y no a sobrescribir nada**, sigues por el buen camino y la herencia es bienvenida.

Todo aquello que vaya en contra de uno de estos consejos debe hacerte dudar de aplicar herencia.

### Modelado de Dominio

Si te das cuenta, todas las premisas se suelen cumplir en un marco bastante común: objetos de negocio, entidades, _value objects_ y otros objetos de este tipo son susceptibles de poder ser modelados con relaciones de herencia.

Aún así te recomiendo que pienses bien tus relaciones de herencia. Por cierto, no viene mal recordar qué es la lógica de dominio de vez en cuando, echa un vistazo a [los artículos sobre Domain Driven Design](http://devexperto.com/domain-driven-design-1/).

### Desarrollo de Frameworks

Otro caso susceptible de modelar mediante el uso de herencia puede ser el desarrollo del frameworks, SDKs, aunque este tiene sus defensores y detractores. **Aún modelando relaciones basadas en herencia, no podemos abusar de ello.**

El framework de Android es un claro ejemplo del abuso de relaciones de herencia. Ahora me estoy dedicando al desarrollo de un SDK y en mi opinión me gusta más dejar la libertad que da la composición a atar al cliente de tu framework a una relación de herencia.

Pero esto como he dicho, aún siendo un campo susceptible de modelarse con herencia en un primer momento, da pie a un largo debate, porque siguen estando presentes muchos de los inconvenientes ya estudiados.

## Casos de mal uso de la herencia

Una vez vistos los casos en los cuales podría tener la herencia cabida, vamos a ver algo que es más interesante si cabe: ejemplos de algunos casos comunes en los cuales nos empeñamos en meter herencia por alguna extraña razón, y ésta no tiene cabida:

### Modelar comportamiento del sistema como si fueran objetos de modelo que representan estado

Por ejemplo: un caso de uso modela comportamiento, y no estado, y **no tenemos por qué heredar de un caso de uso base que tenga métodos que supuestamente vayan a usar todos los casos de uso, porque es muy probable que eso no sea así**.

Esto es un error muy común que se repite con al inicio de muchos diseños de software. Tomamos decisiones demasiado complejas y de muy bajo nivel en etapas tempranas del proyecto.

Ejemplo claro:

No puedo hacer una clase _BaseRequest_ con un método _getJSON()_ que escriba mi objeto con formato JSON. Con eso estoy suponiendo que todos mis _Request_ van a ser JSON, y si en algún momento he de usar un _multipart_ con formato [formulario + imagen], la consistencia de mi sistema estaría comprometida porque no puede heredar de esa request, y me vería obligado a crear otro tipo request.

**Estoy tomando una decisión al principio del proyecto que no está para nada clara** y está atando mi desarrollo a tomar un camino que no se si es el que debo seguir. Por lo tanto estoy saliéndome de la flexibilidad que me otorgara en ese caso un objeto compuesto, el cual me da la oportunidad de retrasar las decisiones de un grano tan fino hasta el último momento.

Imaginemos que forzosamente tenemos que tomar una decisión de ese tipo por algún motivo, **siguiendo el camino de la composición, tendremos la gran ventaja de que los cambios estarán acotados y bajo control**, al menos mucho más que con la herencia, con lo cual cualquier decisión equivocada y su posterior rediseño van a ocasionar unos efectos de lado que implicarán cambios en muchas menos piezas de código.

### Diseños _Template Method_

De igual modo pasa con los diseños en plan _Template Method._ Es muy común crear ciclos de vida totalmente innecesarios mediante una herencia mal aplicada, que en un principio pensamos que nos van a facilitar el desarrollo, pero que acaba convirtiendo cualquier modificación en pesadilla…

¿Es realmente necesario crear un flujo de ejecución o ciclo de vida a los elementos? en la mayor parte de los casos no. Y si lo fuera, ¿es realmente la herencia la solución?

Ten en cuenta lo siguiente: **abstraer comportamiento de piezas del sistema en etapas tempranas del diseño es una de las tareas más complejas de la ingeniería del software**, y crear una relación de herencia no es más que crear una abstracción de algo que siempre va a ser de ese modo. ¿En serio te merece la pena arriesgar tanto?

La respuesta probablemente sea no. Pero si aún así te equivocas, como todos nos equivocamos, y acabas en el “berenjenal”de la herencia, presta atención a los siguientes puntos porque te pueden hacer detectar cuanto antes que la herencia se ha aplicado de mala manera.

## Cómo detectar que estás usando mal la herencia

-   Cuando los **_Overrides_** empiezan a crecer y multiplicarse por tu código de forma exponencial y a veces de forma obligada y sin mucho sentido… ¡Algo huele mal!
-   Si **la relación “Es un” se ha roto** por algún motivo… ¡Mal asunto!
-   Si tu código, cuando crece por extensión, **requiere modificaciones de clases que son supertipos**, y además siempre suelen ser las mismas clases base las que estas tocando… ¡Mal royo!
-   Si **los niveles de herencia empiezan a ser muchos**, te pierdes al tirar del hilo y los efectos de lado empiezan a manifestarse… ¡Se te está pasando el arroz!

Así que si en algún momento sospechas de alguno de estos puntos, echa un ojo de cerca a ese código. Y si se vuelve a manifestar de alguna forma parecida, dale caña al rediseño de esa parte, porque cuanto antes pongas medidas y cortes de raíz, más fácil te resultará. Y recuerda esta vez ir por la vía de la composición.

## Conclusión

Y no me queda mucho más que añadir una conclusión que no deja de ser una opinión personal y que he dicho ya por algún lado. ¡¡La herencia, no es mala!! de hecho puede ser la solución que necesitas en un momento concreto.

El problema es que es muy malo es aplicar mal herencia. Y como en la mayor parte de los sistemas que desarrollamos, por su naturaleza de cambio, es muy fácil caer en aplicarla mal… es muy probable que se vuelva contra ti y los beneficios no sean nada comparados con sus problemas a futuro.

**Por eso acabamos diciendo: ante la duda… ¡no dudes! Favorece composición ante herencia.**