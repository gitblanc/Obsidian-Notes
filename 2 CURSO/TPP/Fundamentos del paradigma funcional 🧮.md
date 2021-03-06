# TEMA 3 馃獮
---
## Paradigma funcional
- Paradigma **declarativo** basado en la utilizaci贸n de funciones que manejan datos inmutables.
	- Los datos nunca se modifican
	- En lugar de cambiar un dato, se llama a una funci贸n que devuelve una copia modificada del dato original
- Un programa ser谩 un conjunto de funciones invoc谩ndose entre s铆
- Las funciones no generan efectos colaterales secundarios

---
## Expresiones Lambda
- En el c谩lculo lambda, una **expresi贸n lambda** es:
	- Una **abstracci贸n** lambda  **位x.M** (M , N , M1 , M2)
	- Una **aplicaci贸n** **M N** donde M y N son expresiones lambda
- Ejemplos (**funci贸n identidad** y **funci贸n doble**):
![[lamda.png]]

---
## Aplicaci贸n (reducci贸n 尾)
- La aplicaci贸n de una funci贸n representa su invocaci贸n
- **reducci贸n-尾** o **sustituci贸n** ejemplos:
![[reduccion beta.png]]

---
## Teorema de Church-Rosser
- Establece que el orden en el que se hagan las reducciones no afecta al resultado final
- Los **par茅ntesis** se usan normalmente para **delimitar t茅rminos lambda**, no indican precedencias

![[church rosser.png]]

---
## Variables libres y ligadas, conversi贸n-伪
- En una abstracci贸n **位x.xy**:
	- La variable x est谩 **ligada** (bound)
	- La variable y es **libre** (free)
- En la sustituci贸n s贸lo se sustituyen las variables libres
- En la conversi贸n-伪 todas las apariciones de una variable **ligada** en una misma abstracci贸n se pueden renombrar a una **nueva** variable
![[variables libres.png]]

---
## Conversi贸n-伪
- Gracias a ella, podemos aplicar funciones a s铆 mismas
- Ejemplos:
![[ejemplos conversion.png]]

---
## L贸gica booleana
- El literal **true** puede representarse como:
	true = 位t.位f.t
- Y **false** como:
	fasle = 位t.位f.f
Representan una funci贸n que devuelve dos par谩metros
![[ej 1 sem 3.png]]
![[ej 1 sem 3 res.png]]

---
## Problema de la parada
- Dada la especificaci贸n de un programa, demostrar si 茅ste finalizar谩 o no
- Programa que no termina:
	(位x.xx) (位x.xx) -> (位x.xx) (位x.xx)
	
---
## Isomorfismo (Curry-Howard)
- Establece una relaci贸n directa entre programas software y demostraciones matem谩ticas
- Correspondencia entre tipos y proposiciones:
![[curry howard.png]]

---
## Funciones, Entidades Primer Orden
- El paradigma funcional identifica las funciones como **entidades de primer orden** (funciones de primer orden)
- Esto significa que las funciones son un tipo m谩s, pudi茅ndose instanciar variables del tipo funci贸n:
	- Se pueden asignar, pasar como par谩metros y retornarlas como valores
- Se dice que una funci贸n es de orden superior si:
	- Recibe alguna funci贸n como par谩metro
	- Retorna una funci贸n como resultado

---
## Delegados
- Es un tipo que representa un m茅todo de instancia o de clase (static)
- Las variables de tipo delegado representan un modo de referenciar un m茅todo
- Por tanto:
	- El paso de estas variables implican el paso de funciones a otras funciones
- `public delegate int Comparacion(Persona p1, Persona p2)`
- Es posible declarar el siguiente m茅todo independiente del cirterio de ordenaci贸n:
````c#
static public void OrdenarPersonas(Persona[] vector, Comparacion comparacion)
````
Y hacer uso del delegado del siguiente modo:
````c#
if(comparacion(vector[i], vector[j]) > 0)
	...
````
![[sortpeople.png]]
- Funci贸n doble aplicaci贸n:
![[funcion doble.png]]

---
## Patr贸n Observer
- Es un patr贸n de dise帽o para el uso de delegados
![[observer.png]]
- Una instancia de un delegado puede coleccionar un conjunto de m茅todos
- Cuando se invoca a un delegado se producir谩 una invocaci贸n a todos los suscriptores registrados en ese delegado
![[observer 2.png]]
![[observer 3.png]]

---
## Tipos delegados predefinidos
- Los m谩s usados son:
	- `Func<T>`: m茅todo sin par谩metros que retorna un T
	- `Func<T1, T2>`: m茅todo con un par谩metro T1 que retorna un T2
	- `Action`: m茅todo sin par谩metros ni retorno
	- `Action<T>`: m茅todo con un par谩metro T sin retorno
	- `Predicate<T>`: m茅todo que retorna un bool y recibe un T

Operaciones suma y resta con delegados:
![[del 1.png]]
![[del 2.png]]

Operaciones suma y resta con funci贸n que recibe 2 par谩metros y devuelve un entero:
![[del 4.png]]

Operaci贸n doble aplicaci贸n, es par, imprimir en rojo y devolver personas mayores de edad:
![[del 3 1.png]]
![[double.png]]
![[red.png]]
![[personas.png]]

---
## Delegados an贸nimos
- En funcional, es com煤n escribir la funci贸n 煤nicamente en el momento de pasarla
- La primera aproximaci贸n fueron los delegados an贸nimos
- Mala sintaxis
![[del anonim.png]]
![[del anonim 2.png]]
![[del anonim 3.png]]

---
## Expresiones lambda
- Permiten escribir el cuerpo de funciones completas como expresiones
- Son una mejora de los delegados an贸nimos
- Sintaxis:
	- Se especifican los par谩metros separados por comas
	- Se pueden anteponer los tipos
	- Si hay m谩s de un par谩metro se deben usar par茅ntesis
	- Si no hay par谩metros se indica con `()`
	- El s铆mbolo `=>` indica la separaci贸n de los par谩metros y el cuerpo de la funci贸n
	- Si el cuerpo tiene varias sentencias se separan por `;`
	- En el cuerpo se usa `return` para devolver valores
	- Si el cuerpo es una 煤nica sentencia no es necesario escribir `return` ni llaves
![[expresiones lambda.png]]

- Los tipos de las expresiones lambda promocionan a los tipos de delegados predefinidos (Func, Predicate y Action)
![[lamda 2.png]]
![[lamda 3.png]]

![[funcional 4.png]]

---
## Bucles y recursividad
- La programaci贸n funcional pura no posee el concepto de **iteraci贸n**, sino que hace uso de la **recursividad**
- Las funciones recursivas se han de expresar como funciones de orden superior que se reciben a s铆 mismas

---
## Combinador de punto fijo
- Es una funci贸n de orden superior que cumple lo siguiente (**funci贸n fix**)
![[combinador.png]]
Factorial:
![[factorial.png]]

## Cl谩usulas
- Una **cl谩usula** (closure) es una funci贸n de primer orden junto con su 谩mbito: una tabla que guarda las referencias a sus variables libres
![[clausula.png]]
- Pueden representar objetos
- Pueden representar estructuras de control
![[closure 1.png]]
![[closure 2.png]]
![[closure 3.png]]
![[closure 4.png]]
![[closure 5.png]]
![[closure 6.png]]
![[closures 7.png]]

---
## Currificaci贸n
- Es la t茅cnica para transformar una funci贸n de varios par谩metros en una funci贸n que recibe un 煤nico par谩metro
	- La funci贸n recibe un par谩metro y retorna otra funci贸n que se puede llamar con el segundo par谩metro
- Su principal beneficio es la **aplicaci贸n parcial**
![[currification.png]]
![[currification 2.png]]
![[currification 3.png]]

## Aplicaci贸n parcial
- Cuando las funciones est谩n currificadas es posible realizar su aplicaci贸n (invocaci贸n) parcial
- La aplicaci贸n parcial consiste en pasar un n煤mero menor de par谩metros en la invocaci贸n de una funci贸n
![[2 CURSO/TPP/img/app parcial.png]]
![[app parcial 2.png]]
![[app parcial 3.png]]

- La aplicaci贸n parcial nos permite ahorrar mucho c贸digo y reutilizarlo
![[currificada version.png]]

---
## Continuaciones
- Una continuaci贸n representa el **estado de computaci贸n** en un momento de ejecuci贸n
- El estado de computaci贸n est谩 compuesto por:
	- El estado de la pila de ejecuci贸n
	- La siguiente instrucci贸n a ejecutar

---
## Generadores
- Un **generador** es una funci贸n que simula la devoluci贸n de una colecci贸n de elementos sin constru铆r toda la colecci贸n devolviendo un elemento cada vez que la funci贸n es invocada
- Es m谩s eficiente
- Un generador es una funci贸n que se comporta como un iterador
- C# implementa los generadores mediante `yield`
![[generadores.png]]
![[generadores 2.png]]
![[fibonaccis.png]]
![[fibonaccis 2.png]]

---
## Evaluaci贸n perezosa
- La **evaluaci贸n perezosa** (lazy) es la t茅cnica por la que se demora la evaluaci贸n de una expresi贸n hasta que 茅sta es utilizada
	- Es lo contrario a la **evaluaci贸n ansiosa** (eager)
![[eager lazy.png]]
- Ofrecen menor consumo de memoria, mayor rendimiento, posibilidad de crear estructuras de datos infinitas
- Podemos generar colecciones infinitas con `yield` y hacer uso de los m茅todos extensores:
	- `Skip`: para saltarse un conjunto de elementos, devolviendo los restantes
	- `Take` : para devolver un n煤mero concreto de elementos contiguos desde el inicio de una secuencia
![[lazy prime number+.png]]

---
## Transparencia referencial
- Se dice que una expresi贸n es referencialmente transparente si 茅sta se puede sustituir por su valor sin que cambie la sem谩ntica (significado) del programa
	- Lo contrario es la opacidad referencial
- Cuando un lenguaje la ofrece, se dice que es funcional puro
- Elementos que hacen que un lenguaje no ofrezca transparencia referencial son:
	- Variables globales mutables
	- Asignaciones destructivas (=, +=, -=, ...) 
	- Funciones impuras (E/S, random, datetime, ...)
- Las cl谩usulas no ofrecen transparencia referencial pues **guardan las referencias** de los objetos, **no una copia**
- Las **variables mutables** fuera del 谩mbito de una funci贸n hacen que no se obtenga transparencia referencial
- Con las **asignaciones** sucede lo mismo, puesto que la evaluaci贸n de una variable depende de sus asignaciones previas
- La utilizaci贸n de **funciones que no son puras** tambi茅n implican opacidad referencial

- Una funci贸n es pura cuando:
	- Siempre devuelve el mismo valor ante los mismos valores de los argumentos
	- La evaluaci贸n de una funci贸n no genera efectos secundarios (co-laterales)

---
## Memorizaci贸n (memoization)
- T茅cnica de optimizaci贸n aplicada sobre expresiones con transparencia referencial que dice:
	- Si una expresi贸n posee transparencia referencial, 茅sta puede sustituirse por su valor
	- Si la expresi贸n es una funci贸n pura, 茅sta puede sustituirse por el valor de retorno
	- La primera vez que se invoca se retorna el valor guard谩ndolo en una cach茅
	- En sucesivas invocaciones se retornar谩 el valor de la cach茅, sin ejecutar la funci贸n
![[fibo mem.png]]
![[fibo mem 2.png]]
![[fibo mem 3.png]]

---
## Pattern matching
- Es el acto de comprobar si la secuencia de un conjunto de elementos siguen alg煤n patr贸n determinado
![[p match 1.png]]
![[p match 2.png]]

---
## Funciones de orden superior t铆picas
- Una **funci贸n de orden superior** es:
	- Aquella que recibe alguna funci贸n como par谩metro
	- O bien retorna una funci贸n como resultado
- Las m谩s t铆picas son:
	- `Filter`: aplica un predicado a todos los elementos de una colecci贸n, devolviendo una nueva colecci贸n con los resultados obtenidos
	- `Map`: aplica una funci贸n a todos los elementos de una colecci贸n, devolviendo otra nueva colecci贸n con los resultados obtenidos
	- `Reduce (Fold, Accumulate, Compress o Inject)`: se aplica una funci贸n a todos los elementos de una lista, dado un orden, devolviendo un valor

---
## Funciones de Orden Superior en C# (Linq)
- `Filter` -> Where
- `Map` -> Select
- `Reduce` -> Aggregate

![[funciones linq.png]]

- Ejemplos de `Select`-> Map
![[select map.png]]

- Ejemplos de `Where` -> Filter
![[where filter.png]]

- Ejemplos de 	`Aggregate` -> Reduce
![[agregate reduce.png]]

---
## Otras funciones
![[otras funciones.png]]

---
## Listas por comprensi贸n y LINQ
- Las listas por comprensi贸n son una caracter铆stica de un lenguaje que permite crear listas bas谩ndose en listas existentes. Esto se puede realizar usando LINQ:
![[listas comprension.png]]
![[listas comprension 2.png]]

---
## Comparaci贸n Paradigma Orientado a Objetos vs Funcional
![[poof1.png]]
![[poof2.png]]
![[poof3.png]]
![[poof4.png]]
![[poof5.png]]
![[poof6.png]]
![[poof7.png]]
![[poof8.png]]
![[poof9.png]]
![[poof10.png]]

---
Siguiente lecci贸n -> [[Fundamentos de la Programaci贸n Concurrente y Paralela 馃]]