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