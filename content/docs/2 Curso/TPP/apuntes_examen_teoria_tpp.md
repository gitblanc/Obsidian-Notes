---
title: Apuntes Examen Teoría 👅
---
# Tema 1. Lenguajes y Paradigmas de la Programación

## Lenguaje de programación

- Un **lenguaje de programación** es un lenguaje artificial utilizado para escribir instrucciones, algoritmos o funciones que pueden ser ejecutadas por un ordenador.
	- Es un lenguaje que permite **acercar el nivel de abstracción** humano al nivel de abstracción de una máquina

## Traductor, Compilador e Intérprete

- Un **traductor** es un programa que procesa un texto fuente (origen) y genera un texto objeto (destino)
- Un **compilador**  es un traductor que transforma código fuente de un lenguaje de alto nivel al código fuente de otro lenguaje de bajo nivel
	- Es un caso particular de traductor
- Un **intérprete** ejecuta las instrucciones de los programas escritos en un lenguaje de programación

## Clasificaciones de los Lenguajes según sus características

Se suelen clasifican en base a:
- Nivel de abstracción
- En función de su dominio
- Soporte de concurrencia
- En función de su implementación (compilados o interpretados)
- En función de cuándo se realizan las comprobaciones de tipos
- En función de cómo se representa el código fuente

### Nivel de abstracción

- Puede ser **alto** o **bajo**
- Mide en qué medida el nivel de abstracción del lenguaje está más próximo al lenguaje humano (alto nivel) o más próximo al ordenador (bajo nivel)

### En función de su dominio

Existen de propósito general o específicos de un dominio (DSLs):
- **DSL** : son lenguajes específicos de un dominio (SQL, R, CSound...)
- **Propósito general**: pueden ser usados para resolver cualquier problema computacional (Java, Python, C...)

### Soporte de concurrencia

La concurrencia forma parte de aquellos lenguajes que permiten la creación de programas mediante un conjunto de procesos o hilos que interaccionan entre sí y que pueden ser ejecutados de forma paralela.

Los programas concurrentes pueden ser ejecutados:
- **En un único procesador**: intercalando la ejecución de cada uno de los procesos
- **En paralelo**: asignando a cada proceso o hilo a procesadores distintos que pueden estar en una o distintas máquinas

### En función de su implementación

- Pueden ser **compilados** o **interpretados**.
- Java y `C#` son compilados e interpretados

Un **compilador JIT** (*Just In Time*) transforma el código a interpretar en código nativo propio de la plataforma donde se ejecuta el intérprete justo antes de su ejecución

Si esta transformación se realiza previamente a la ejecución se denomina **AoT** (*Ahead of Time*) 


| Naturaleza                                  | Lenguaje                           |
| ------------------------------------------- | ---------------------------------- |
| interpretada                                | Perl, Tcl, JavaScript, Matlab, PHP |
| compilada                                   | C, C++, Go, Pascal, Eiffel, Ada    |
| primero: compilados, después: interpretados | Java, UCSD Pascal                  |
| compilados JIT                              | Self, `C#`                         |
| compilados e interpretados nativamente      | Haskell, Lisp                      |

### Sistema de Tipos

Las comprobaciones de tipo pueden ser **estáticas** (en tiempo de compilación) o **dinámicas** (en tiempo de ejecución)

La **comprobación estática** de tipos suele ofrecer:
- Detección temprana de errores
- Un mayor rendimiento (no hay comprobaciones en tiempo de ejecución)

La comprobación dinámica suele ir ligada a:
- Una mayor adaptabilidad dinámica
- Metaprogramación dinámica

### Representación del código fuente

Puede tratarse de lenguajes visuales o "textuales" (no visuales):
- **Visuales**: representan las entidades de su dominio mediante una notación visual, en lugar de textual
- **Textuales**: usan ficheros de texto para contener su código fuente

## Lenguajes Script y dinámicos

Los lenguajes con comprobación dinámica de tipos son comúnmente denominados:
- Lenguajes de ***Scripting***: lenguajes con comprobación dinámica de tipos comúnmente orientados a la unión de componentes (bash, Perl, JavaScript...)
- **Lenguajes dinámicos**: poseen características que permiten desarrollar aplicaciones finales usando sólo ese lenguaje de programación (SmallTalk, Python, Ruby, Lua, JavaScript...)

## Sistemas de tipos vs Compilación

- Los lenguajes con sólo comprobación estática son compilados
- No existen lenguajes interpretados puros con sólo comprobación estática
- Existen varios lenguajes compilados con comprobación dinámica
- Los lenguajes que sólo poseen comprobación dinámica tienen una fase de interpretación


|               | Sólo comprobación estática | Comprobación Estática y Dinámica                 | Sólo comprobación Dinámica                |
| ------------- | -------------------------- | ------------------------------------------------ | ----------------------------------------- |
| Compilados    | C, Fortran, Pascal         | C++, Ada, ObjectiveC, Scala                      | Python, Ruby (compilados e interpretados) |
| Interpretados |                            | GHCi Haskell, OCaml (compilados e interpretados) | Smalltalk, Prolog                         |

## Paradigmas de Programación

- Un **paradigma** de programación es una aproximación para construir programas caracterizada por las abstracciones y conceptos utilizados para representar dichos programas
	- El paradigma de programación se usa también para clasificar lenguajes de programación
	- Un lenguaje de programación puede seguir más de un paradigma (**multiparadigma**)
	- Un paradigma de programación no constituye una característica del lenguaje

## Imperativo vs Declarativo

- **Imperativo**: describe los programas en términos de sentencias que cambian el estado del programa
	- El programador especifica al ordenador cómo realizar una tarea
	- Sus abstracciones suelen ser más cercanas al ordenador que los lenguajes declarativos
	- Ejemplos de lenguajes: C, Java, `C#`, Pascal
	- Ejemplos de paradigmas imperativos: Estructurado basado en procedimientos y Orientado a objetos (POO)
- **Declarativo**: estos paradigmas se basan en escribir programas que especifican qué se quiere obtener, intentando no especificar cómo
	- El programador declara lo que quiere obtener
	- Se usan abstracciones del paradigma específico para representar el qué (*Funciones, predicados, consultas, restricciones*)
	- Ejemplos de lenguajes declarativos: Prolog, SQL, Maude, Haskell
	- Ejemplos de paradigmas declarativos: Lógico, Funcional, Basado en restricciones y De reescritura de reglas y árboles

## Principales paradigmas

- **Estructurado basado en procedimientos**: paradigma imperativo en el que se utilizan tres estructuras de control (secuencial, condicional e iterativa), pudiendo agrupar éstas en procedimientos o subrutinas
- **Orientado a objetos**: paradigma comúnmente imperativo que utiliza los objetos, unión de datos y métodos, como principal abstracción, definiendo programas como interacciones entre objetos
- **Funcional**: paradigma declarativo basado en la utilización de funciones que manejan datos inmutables
- **Lógico**: paradigma declarativo basado en la programación de ordenadores mediante lógica matemática

### Estructurado basado en procedimientos

- Comúnmente llamado **imperativo**
- Viene de la unión de paradigma **estructurado** y paradigma **procedural**
- Se evitan las instrucciones de **salto**, tanto condicionales como incondicionales
- Se aumenta la legibilidad y mantenibilidad de los programas
- Las estructuras de control se pueden anidar
- Define el procedimiento o subrutina como el primer mecanismo de descomposición
- Incorporó la programación estructurada
- Incluye el concepto de **ámbito**, previniendo el acceso indebido a variables
- Un procedimiento que devuelve un valor se define como una función
	- Es distinto a la función de la programación funcional
	- Pueden generar efectos colaterales
	- No suelen ofrecer funciones de orden superior
	- No implementan el concepto de cláusulas
- Ejemplos: Algol, Ada, C, Pascal, Fortran, Cobol...

### POO (orientado a objetos)

- Usa los objetos como la principal abstracción, definiendo programas como interacciones entre objetos
- Se basa en la idea de modelar **objetos reales** mediante la codificación de **objetos software**
- Un programa está constituido por un conjunto de objetos pasándose mensajes entre sí
- Típicamente es un paradigma **imperativo**
- Elementos propios de este paradigma: *encapsulamiento, herencia, polimorfismo y enlace dinámico*
- Existen dos modelos computacionales de OO:
	- **Basado en clases**:
		- Todo tiene que ser **instancia** de una clase
		- La clase es del **tipo** del objeto
		- La clase define la **estructura** y **comportamiento** de sus instancias
		- C++, Java, `C#`, Smalltalk, Eiffel
	- **Basado en prototipos** (basado en objetos):
		- No existe el concepto de clase, los objetos son la única entidad
		- Se define un objeto **prototipo** y el resto de objetos con una estructura similar se **clonan** a partir de éste
		- Self, Cecil, JavaScript, Lua
- Un **lenguaje OO** se dice **puro** cuando toda abstracción ofrecida es un objeto: Smalltalk, Eiffel, Ruby

### Paradigma Funcional

- Paradigma declarativo basado en la utilización de funciones que manejan **datos inmutables**
	- Los datos nunca se modifican
	- En lugar de ello, se llama a una función que devuelve el dato modificado sin modificar el original
- Un **programa** se define mediante un **conjunto de funciones invocándose entre sí**
- Las funciones no generan **efectos (co)laterales** (secundarios, *side effects*):
	- El valor de una expresión depende exclusivamente de los valores de los parámetros
	- Devolviendo siempre el mismo valor en función de éstos (paradigma funcional puro)
- Se hace uso exhaustivo de la **recursividad**, en lugar de la iteración
- Los **lenguajes funcionales puros** no utilizan ni la asignación ni la secuenciación de instrucciones
- Sus orígenes se remontan al cálculo lambda de Church Kleene
- Ejemplos de lenguajes funcionales puros: Miranda, Clean y Haskell
- Ejemplos de lenguajes funcionales: Scheme, Lisp...

### Paradigma Lógico

- Paradigma declarativo basado en la programación de ordenadores mediante **lógica matemática**
- El programador describe un conocimiento mediante **reglas lógicas** y axiomas (hechos)
- Un demostrador de teoremas con **razonamiento hacia atrás resuelve problemas a partir de consultas**
- Primer lenguaje lógico: Absys
- El lenguaje de programación lógica por excelencia es **Prolog**

## Otros paradigmas de programación

- Orientación a aspectos
- Basado en restricciones
- Tiempo real
- Guiado por eventos
- Programación basada en autómatas
- Programación reactiva

## Tecnología de la programación

**Tecnología de la programación**: aquellos elementos y técnicas ofrecidos por los distintos paradigmas y lenguajes de programación para diseñar, construir y mantener aplicaciones de forma correcta, robusta, segura y eficiente

## Características de `C#`

- Lenguaje de alto nivel
- De propósito general
- Concurrente y paralelo
- Compilado y ejecutado por una máquina virtual con compilación JIT
- Comprobación estática y dinámica (y sistema de tipos estático y dinámico)
- Textual
- Imperativo (principalmente)
- Base orientada a objetos, pero incluye elementos de programación funcional

# Tema 2. Paradigma Orientado a Objetos

 >[!Tip]
 >Te recomiendo echarle un ojo a [notas_de_c_sharp_🍉](notas_de_c_sharp_🍉.md) para mucho más detalle

- Utiliza los **objetos**, unión de datos y métodos, como principal abstracción, definiendo programas como interacciones entre objetos
- Se basa en la idea de modelar **objetos reales** mediante la codificación de objetos software

## Abstracción

- **Abstracción**: expresa las características esenciales de un objeto, las cuales distinguen al objeto de los demás
	- El principal mecanismo de los lenguajes de programación para representar sus abstracciones son sus **tipos**

## Encapsulamiento

- **Encapsulamiento**: proceso de almacenar en un mismo compartimento los elementos de una abstracción que constituyen su estructura y su comportamiento
	- Los objetos encapsulan en una misma entidad datos y comportamiento
- La **ocultación de la información** permite discernir entre qué partes de la abstracción están disponibles al resto de la aplicación y qué partes son internas de la abstracción
- Para ello, los lenguajes ofrecen diversos niveles de ocultación

### Beneficios del encapsulamiento

- Aumento de la eficiencia
- Mejora de la mantenibilidad del código
- Mayor reutilización de código
- Se aumenta la robustez, evitando así errores de inconsistencia

## Propiedades

`C#` ofrece el concepto de **propiedad** para acceder al estado de los objetos como si de atributos se tratase, obteniendo los beneficios del encapsulamiento:
- Se oculta el estado interno del objeto, ofreciendo un acceso indirecto mediante las propiedades
- Se puede cambiar la implementación de la propiedad sin modificar el acceso por parte del cliente
Las propiedades pueden ser de lectura o escritura.

## Modularidad

- Propiedad que permite subdividir una aplicación en partes más pequeñas (módulos), siendo cada una de ellas tan independiente como sea posible
- Cada módulo ha de poder ser compilado por separado para ser utilizados en diversos programas (reutilización)

## Acoplamiento y cohesión

- **Acoplamiento**: nivel de interdependencia entre módulos
- **Cohesión**: nivel de uniformidad y relación que existe entre las responsabilidades de un módulo

- Un bajo acoplamiento y una alta cohesión favorecen la reutilización y mantenibilidad del software

## Sobrecarga de métodos

- La **sobrecarga de métodos** permite dar distintas implementaciones a un mismo identificador de método

## Herencia

- La **herencia** es un mecanismo de **reutilización de código**
- El **estado** de una instancia derivada está definido por la unión (herencia) de las estructuras de las clases base y derivada
- El conjunto de mensajes (**interfaz**) que puede aceptar un objeto derivado es la unión (herencia) de los mensajes de su clase base y derivada

## Polimorfismo

- Es un **mecanismo de generalización** que hace que la abstracción más general pueda representar abstracciones más específicas
	- El tipo general representa, por tanto, varias formas (*poli morfismo*)
- Por ello las referencias derivadas promocionan a referencias base (subtipado)

![](img/Pasted%20image%2020240518125127.png)

- La conversión descendente ha de forzarse con un **cast**
- Operadores is, as

## Enlace Dinámico

- Los métodos heredados se pueden **especializar** en las clases derivadas
	- Mecanismo por el cual, en tiempo de ejecución, se invoca al método del tipado dinámico implementado por el objeto (no al estático declarado en su clase)

![](img/Pasted%20image%2020240518125356.png)

- `C#` no tiene enlace dinámico por defecto
	- Para que exista tenemos que:
		- Poner la palabra reservada `virtual` al método que reciba el mensaje
		- Redefinir su funcionalidad utilizando la palabra reservada `override` en los métodos derivados

![](img/Pasted%20image%2020240518125723.png)

## Clases y métodos abstractos

- Cuando en una abstracción necesitamos que un mensaje forme parte de su interfaz, pero no podemos implementarlo, este mensaje se declara como método abstracto
- Todo método abstracto ofrece enlace dinámico
- En su redefinición hay que usar la palabra `override`
- Toda clase que posea, al menos, un método abstracto, será una **clase abstracta**

## Herencia múltiple

- Se produce cuando una clase hereda, directamente, de más de una clase
- La herencia múltiple produce dos conflictos:
	- **Coincidencia de nombres**: se produce cuando se hereda de dos o más clases un miembro con igual identificador. Se produce una ambigüedad en su acceso
	- **Herencia repetida**: se produce cuando se hereda más de una vez de una clase por distintos caminos.

## Interfaces

- Conjunto de métodos públicos que ofrecen un conjunto de clases
	- Tiene los beneficios del polimorfismo (mantenibilidad) sin establecer relaciones de herencia entre abstracciones

### Interfaces vs Composición

- Se usa **composición** si se busca reutilizar implementaciones, pero sin buscar el polimorfismo
- Se usan **interfaces** si se busca el polimorfismo, es decir, que una clase promocione a múltiples tipos

## Excepciones

- Una **excepción** es un evento que se produce en un momento de ejecución y que impide que la ejecución prosiga por su flujo normal
- En `c#` todas las excepciones son ***unchecked***

## Asertos

- **Aserto**: son condiciones que se han de cumplir en la correcta ejecución de un programa
	- Si se producen, se detiene la ejecución del programa
	- Están orientadas al proceso de desarrollo
	- Se pueden desactivar para la release
- La técnica más utilizada para implementar asertos está basada en **compilación condicional**

![](img/Pasted%20image%2020240518130550.png)

## Genericidad

- La **genericidad** es la propiedad que permite construir abstracciones modelo para otras abstracciones
- Ofrece **dos beneficios** principales:
	- Una mayor robustez (detección de errores en tiempo de compilación)
	- Un mayor rendimiento
- Se hace uso de `default(T)` para el tipo por defecto

## Genericidad Acotada

- La **genericidad acotada** (*bounded*) permite hacer más específicos los tipos genéricos
	- Limitan (acotan) su genericidad
	- El beneficio es que se permite un mayor paso de mensajes

![](img/Pasted%20image%2020240518130902.png)

## Inferencia de tipos

- La **inferencia de tipos** es la capacidad para deducir automáticamente el tipo de una expresión
	- Cuanta menos información de tipos provea el programador, más avanzada será la inferencia de tipos
- `var` en `C#`

# Tema 3. Fundamentos del paradigma funcional

- Paradigma declarativo basado en la utilización de funciones que manejan datos inmutables
	- Los datos nunca se modifican
	- En lugar de cambiar un dato, se llama a una función que devuelve el dato modificado sin modificar el original
- Un programa se define mediante un conjunto de funciones invocándose entre sí
- Las funciones no generan efectos (co)laterales:
	- el valor de una expresión depende exclusivamente de los valores de los parámetros
	- devolviendo siempre el mismo valor en función de éstos (paradigma funcional puro)

## Cálculo lambda

- El **cálculo lambda**  es un sistema formal basado en la definición de funciones (abstracción) y su aplicación (invocación)
	- Hace uso exhaustivo de la recursión

## Expresiones Lambda

- En el cálculo lambda, una expresión lambda se define como:
	- Una **abstracción** lambda `λx.M` (M. N. M1, M2...) donde x es una variable (x, y, z, x1, x2...) -parámetro- y M es una expresión lambda -cuerpo de la función
	- Una aplicación M N donde M y N son expresiones lambda

- Ejemplos:
	- Función identidad: `f(x)=x` -> `λx.x`
	- Función doble: `g(x)=x+x` -> `λx.x + x`

>[!Tip]
>A partir de aquí echarle un ojo a [seminarios_tpp_🍎](seminarios_tpp_🍎.md)

## Variables Libres y Ligadas

- En una abstracción `λx.y` se dice que:
	- La variable `x` está **ligada**
	- La variable `y` es **libre**

## El problema de la parada

Es imposible describir un algoritmo que demuestre si éste finalizará su ejecución o tendrá una ejecución finita

## Funciones, Entidades de primer nivel

- Las funciones, al igual que el resto de valores (como los objetos), son entidades de primer nivel
- Una función se dice que es de **orden superior** si:
	- O bien recibe alguna función como parámetro
	- O bien retorna una función como resultado

## Delegados

- **Delegado**: constituye un tipo que representa un método de instancia o de clase (`static`)
	- Las variables de tipo delegado representan un modo de referenciar un método

- Los delegados predefinidos son:
	- `Func<T>`: método sin parámetros que retorna un `T`
	- `Func<T1,T2>`: método con un parámetro `T1` que retorna un `T2`
	- ...
	- `Action`: método sin parámetros ni retorno
	- `Action<T>`: método con un parámetro `T` sin retorno
	- ...
	- `Predicate<T>`: método que retorna un `bool` y recibe un `T`

## Delegados Anónimos

- En la programación funcional es común escribir la función en el momento de pasarla
- **Delegado anónimo**: sintaxis para definir una variable delegado indicando sus parámetros y su cuerpo (código)

![](img/Pasted%20image%2020240518160447.png)

## Expresiones Lambda

- Permiten escribir el cuerpo de funciones completas como expresiones

![](img/Pasted%20image%2020240518160531.png)

## Clausura

- Una **clausura** (*closure*) es una función de primer nivel junto con su ámbito: una tabla que guarda las referencias a sus variables libres
- Las variables libres de una clausura representan **estado**
	- Este estado puede además estar oculto cuando el ámbito de la variable finaliza
- Por tanto, pueden representar objetos
- Además, también pueden representar estructuras de control:

![](img/Pasted%20image%2020240518160812.png)

## Currificación

- La **currificación** (*currying*) es la técnica para transformar una función de varios parámetros en una función que recibe un único parámetro
- Su principal beneficio es la **aplicación parcial**

## Aplicación parcial

- Cuando las funciones están currificadas es posible realizar su aplicación (invocación) parcial
- La **aplicación parcial** consiste en pasar un número menor de parámetros en la invocación de una función
	- El resultado es otra función con un número menor en su aridad (número de parámetros)

## Generadores

- Un **generador** es una función que simula la devolución de una colección de elementos sin construir toda la colección devolviendo un elemento cada vez que la función es invocada
- El hecho de no construir toda la colección hace que sea más eficiente:
	- Requiere menos memoria
	- El invocador obtiene el primer elemento de forma inmediata
	- Sólo se generan los elementos que se usan
- `C#` usa `yield`

## Evaluación perezosa

- La **evaluación perezosa** (lazy) es la técnica por la que se demora la evaluación de una expresión hasta que ésta es utilizada
	- Lo contrario es la evaluación eager (ansiosa)
- Los beneficios de la evaluación perezosa son:
	- Un menor consumo de memoria
	- Un mayor rendimiento
	- La posibilidad de crear estructuras de datos potencialmente infinitas

## Transparencia referencial

- Una expresión es **referencialmente transparente** si ésta se puede sustituir por su valor sin que cambie la semántica (significado) del programa
- Tiene los siguientes beneficios:
	- Se puede aplicar el razonamiento matemático a los programas
	- Se pueden realizar transformaciones en los programas (simplificación, paralelización, optimización...)

## Memoización

- Técnica de optimización que puede ser aplicada sobre expresiones con transparencia referencial

## Pattern Matching

- **Pattern Matching**: es el acto de comprobar si un conjunto de elementos siguen algún patrón determinado

## Funciones de Orden superior típicas

- **Filter** (Where): aplica un predicado a todos los elementos de la colección, devolviendo otra colección con aquellos elementos que satisfagan el predicado
- **Map** (Select): aplica una función a todos los elementos de una colección, devolviendo otra nueva colección con los resultados obtenidos
- **Reduce** (Aggregate): se aplica una función a todos los elementos de una lista, dado un orden, devolviendo un valor

# Tema 4. Fundamentos de la programación concurrente y paralela

## Ley de Moore

*El número de transistores por unidad de superficie en circuitos integrados se duplica cada 24 meses, sin encarecer su precio*

En dos años, tendremos un procesador el doble de potente al mismo precio

## Programación Concurrente

- **Concurrencia**: es la propiedad por la que varias tareas se pueden ejecutar simultáneamente y potencialmente interactuar entre sí
	- Las tareas pueden ser hilos o procesos

## Programación paralela

- **Paralelismo**: es un caso particular de la concurrencia, en el que las tareas se ejecutan de forma paralela (simultáneamente, no simulada)
	- Con la concurrencia, la simultaneidad *puede ser simulada*
	- Con el paralelismo, la simultaneidad debe ser real
- El paralelismo comúnmente enfatiza la división de un problema en partes más pequeñas
- La programación concurrente enfatiza la interacción entre tareas

## Proceso

- Un **proceso** es un programa en ejecución
	- Consta de instrucciones, estado de ejecución y valores de los datos en ejecución
	- En los sistemas de memoria distribuida, las tareas concurrentes en distintos procesadores son procesos

## Hilo

- Un proceso puede constar de varios hilos de ejecución
- Un hilo de ejecución es una tarea de un proceso que puede ejecutarse concurrentemente, compartiendo la memoria del proceso, con el resto de sus hilos

## Condición de carrera

- Se dice que múltiples tareas están en **condición de carrera** cuando su resultado depende del orden en el que éstas se ejecutan
	- Un programa concurrente no debe tener condiciones de carrera

## Context Switch

- El **contexto** de una tarea es la información que tiene que ser guardada cuando éste es interrumpido para que luego pueda reanudarse su ejecución
- El **cambio de contexto** es la acción de almacenar/restaurar el contexto de una tarea para que pueda ser reanudada su ejecución
- Esto permite la ejecución concurrente de varias tareas en un mismo procesador
- El cambio de contexto requiere:
	- Tiempo de computación para almacenar y restaurar el contexto de varias tareas
	- Memoria adicional para almacenar los distintos contextos
- Por lo tanto, la utilización de un número elevado de tareas, en relación con el número de procesadores, puede conllevar una caída global del rendimiento

![](img/Pasted%20image%2020240518165433.png)

## Inconvenientes del uso de hilos

- **Condiciones de carrera**: debemos esperar explícitamente hasta que todos los hilos hayan terminado de realizar sus cálculos
- **Parámetros**: sin parámetros o solo un objeto, variables libres compartidas
- **Excepciones asíncronas**: las excepciones originadas en un hilo no son capturadas por bloques `try-catch` pertenecientes a un hilo diferente
- **Rendimiento de los cambios de contexto**: no hay optimización automática del número de hilos creados

## Tareas (Task)

- Una **Task** representa una operación asíncrona y su uso tiene dos beneficios principales:
	- Uso más eficiente y escalable de recursos
	- Mayor control de ejecución (comparado con Thread)

## Sección crítica

- Una **sección crítica** es un fragmento de código que accede a un **recurso compartido** que no debe ser accedido concurrentemente por más de un hilo de ejecución


## Lock

- Consigue que únicamente un hilo pueda ejecutar una sección crítica simultáneamente (exclusión mutua)

## Interbloqueo

- Se produce **interbloqueo** (*deadlock*) entre un conjunto de tareas si todas y cada una de ellas están esperando por un evento que sólo otra puede causar
	- Todas las tareas se bloquean de forma permanente

# Tema 5. Tipado Dinámico y Metaprogramación

## Tipado Dinámico

- El **tipado dinámico** es el proceso de posponer la comprobación e inferencia de tipos en tiempo de ejecución
	- Ventajas
		- Mayor adaptabilidad y flexibilidad del código
		- En general, mayor nivel de abstracción
	- Inconvenientes
		- Detección de errores de tipo en tiempo de compilación
		- Optimización de código (rendimiento)
- En `C#` se ha de poner `dynamic` a un método
- Tiene como limitación la obligación de usar **single dispatch**
	- Sólo permite resolver un método dependiendo del tipo de un único objeto (**this**)

## Duck Typing

- Significa que el estado dinámico de un objeto determina qué operaciones pueden realizarse con él

## Multiple Dispatch

- Si queremos que la resolución del método dependa de varios tipos, necesitamos multiple dispatch
- Un mecanismo para obtenerlo son los multimétodos

![](img/Pasted%20image%2020240518171336.png)

## Reflexión

- La **reflexión** es la capacidad de un Sistema computacional de **razonar** y **actuar** sobre sí mismo, adaptándose a sí mismo a condiciones cambiantes
- **Introspección**: cuando se puede consultar la representación de un programa pero no modificarla
- **Intercesión**: cuando se permite además modificar dicha representación desencadenando un cambio en lo que éstos representan o significan

## Generación dinámica de código

- **Generación dinámica de código**: es la capacidad de generar programas (parte de los mismos) en tiempo de ejecución:
	- Es decir, programas que generan programas
	- El código generado de esta forma puede ser parte de la aplicación que lo generó
- Se puede utilizar para generar dinámicamente el código de nuevos métodos o clases (**intercesión estructural**)
- El nuevo código se puede crear a partir de:
	- El propio programa: ***Adaptativeness***
	- El usuario (directa o indirectamente): ***Adaptability***
- También se conoce como **programación generativa**

## Metaprogramación

- **Metaprogramación**: es la capacidad de poder escribir programas que escriban o manipulen otros programas
- Están relacionados con la metaprogramación los siguientes elementos de lenguajes:
	- Reflexión
	- Generación dinámica de código
	- Anotaciones o Atributos
	- Tipado dinámico

