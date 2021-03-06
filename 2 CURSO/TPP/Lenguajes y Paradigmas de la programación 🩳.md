# TEMA 1 馃惈
---
## Lenguaje de programaci贸n, compilador e int茅rprete
- **Traductor**: programa que procesa un texto fuente (origen) y genera un texto objeto (destino)
- **Compilador**: traductor que transforma c贸digo fuente de un lenguaje de alto nivel al c贸digo fuente de otro lenguaje de bajo nivel. Es un caso particular de traductor.
- **Int茅rprete**: ejecuta las instrucciones de los programas escritos en un lenguaje de programaci贸n.

Los lenguajes suelen clasificarse en base a una serie de caracter铆sticas:

#### Nivel de abstracci贸n
Mide cu谩nto se parece el lenguaje al humano (alto nivel) o al m谩quina (bajo nivel)

#### En funci贸n de su dominio
- Los DSL son lenguajes espec铆ficos de un dominio (SQL, R, ...).
- Los lenguajes de **prop贸sito general** pueden ser utilizados para resolver cualquier problema computacional (Java, Python, ...).

#### Concurrencia
- **Lenguajes concurrentes**: Aquellos lenguajes que permiten la creaci贸n de programas mediante un conjunto de procesos o hilos que interasccionan entre s铆 y que pueden ser ejecutados de forma paralela.
- Estos programas pueden ser ejecutados:
	- En **un 煤nico procesador**, intercalando la ejecuci贸n de cada uno de los procesos.
	- **En paralelo**, asignando cada proceso o hilo a procesadores distintos.

#### Implementaci贸n
- Pueden ser compilados o interpretados.
- Con la **compilaci贸n JIT** (Just in Time), esta diferenciaci贸n se ve difuminada. Este compilador transforma el c贸digo nativo propio de la plataforma donde se ejecuta el int茅rprete justo antes de su ejecuci贸n.

#### Sistema de tipos
- En funci贸n de cu谩ndo se realizan las comprobaciones de tipos.
- Estas comprobaciones (aplicables a variables u objetos) pueden ser **est谩ticas** (en tiempo de compilaci贸n) o **din谩micas** (en tiempo de ejecuci贸n).
- La **comprobaci贸n est谩tica** suele ofrecer: comprobaci贸n de errores en tiempo de compilaci贸n y un mayor rendimiento.
- La **comprobaci贸n din谩mica** suele ir ligada a una mayor adaptabilidad din谩mica y a la metaprogramaci贸n.

#### En funci贸n de c贸mo se representa el c贸digo fuente
Hay lenguajes visuales (no hay c贸digo, es todo visual) y textuales (usan ficheros para contener el c贸digo fuente).

---
## Paradigmas de Programaci贸n
Un **paradigma** es una aproximaci贸n para construir programas caracterizada por las abstracciones y conceptos usados para representar dichos programas. Se usa tambi茅n para clasificar lenguajes de programaci贸n.

Hay dos tipos:
- **Imperativo**: describe los programas en t茅rminos de sentencias que cambian el estado del programa (el programador especifica lo que debe hacer el ordenador)
- **Declarativo**: programas que especifican qu茅 se quiere obtener, intentando no especificar c贸mo (el programador declara lo que quiere obtener con funciones, predicados, consultas, ...).

#### Principales paradigmas
- **Estructurado basado en procedimientos**: uso de procedimientos o subrutinas.
- **Orientado a objetos**: usa objetos (uni贸n de datos y m茅todos). Es puro cuando toda abstracci贸n ofrecida es un objeto.
- **Funcional**: uso de funciones que manejan datos inmutables (los datos nunca se modifican, se llama a una funci贸n que devuelve una copia modificada). Usa la recursividad en lugar de la iteraci贸n.
- **L贸gico**: usa la l贸gica matem谩tica.

---

Siguiente lecci贸n -> [[Actividades previas al paradigma orientado a objetos 馃]]