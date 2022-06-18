# TEMA 1
---
## Lenguaje de programación, compilador e intérprete
- **Traductor**: programa que procesa un texto fuente (origen) y genera un texto objeto (destino)
- **Compilador**: traductor que transforma código fuente de un lenguaje de alto nivel al código fuente de otro lenguaje de bajo nivel. Es un caso particular de traductor.
- **Intérprete**: ejecuta las instrucciones de los programas escritos en un lenguaje de programación.

Los lenguajes suelen clasificarse en base a una serie de características:

#### Nivel de abstracción
Mide cuánto se parece el lenguaje al humano (alto nivel) o al máquina (bajo nivel)

#### En función de su dominio
- Los DSL son lenguajes específicos de un dominio (SQL, R, ...).
- Los lenguajes de **propósito general** pueden ser utilizados para resolver cualquier problema computacional (Java, Python, ...).

#### Concurrencia
- **Lenguajes concurrentes**: Aquellos lenguajes que permiten la creación de programas mediante un conjunto de procesos o hilos que interasccionan entre sí y que pueden ser ejecutados de forma paralela.
- Estos programas pueden ser ejecutados:
	- En **un único procesador**, intercalando la ejecución de cada uno de los procesos.
	- **En paralelo**, asignando cada proceso o hilo a procesadores distintos.

#### Implementación
- Pueden ser compilados o interpretados.
- Con la **compilación JIT** (Just in Time), esta diferenciación se ve difuminada. Este compilador transforma el código nativo propio de la plataforma donde se ejecuta el intérprete justo antes de su ejecución.

#### Sistema de tipos
- En función de cuándo se realizan las comprobaciones de tipos.
- Estas comprobaciones (aplicables a variables u objetos) pueden ser **estáticas** (en tiempo de compilación) o **dinámicas** (en tiempo de ejecución).
- La **comprobación estática** suele ofrecer: comprobación de errores en tiempo de compilación y un mayor rendimiento.
- La **comprobación dinámica** suele ir ligada a una mayor adaptabilidad dinámica y a la metaprogramación.

#### En función de cómo se representa el código fuente
Hay lenguajes visuales (no hay código, es todo visual) y textuales (usan ficheros para contener el código fuente).

---
## Paradigmas de Programación
Un **paradigma** es una aproximación para construir programas caracterizada por las abstracciones y conceptos usados para representar dichos programas. Se usa también para clasificar lenguajes de programación.

Hay dos tipos:
- **Imperativo**: describe los programas en términos de sentencias que cambian el estado del programa (el programador especifica lo que debe hacer el ordenador)
- **Declarativo**: programas que especifican qué se quiere obtener, intentando no especificar cómo (el programador declara lo que quiere obtener con funciones, predicados, consultas, ...).

#### Principales paradigmas
- **Estructurado basado en procedimientos**: uso de procedimientos o subrutinas.
- **Orientado a objetos**: usa objetos (unión de datos y métodos). Es puro cuando toda abstracción ofrecida es un objeto.
- **Funcional**: uso de funciones que manejan datos inmutables (los datos nunca se modifican, se llama a una función que devuelve una copia modificada). Usa la recursividad en lugar de la iteración.
- **Lógico**: usa la lógica matemática.