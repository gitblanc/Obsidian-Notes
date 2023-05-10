# Clase 1 - Conceptos básicos

## Fases de análisis
![[Pasted image 20230510110706.png]]
- **Léxico**: separa en tokens
	- Comprueba que las palabras sean válidas
	- Se asigna a cada lexema un token único
````java
pri**#**nt ; a
````
- **Sintáctico**: crea el AST
	- Comprueba que las palabras estén en el orden adecuado
	- Encuentra estructuras mayores (árbol AST)
````java
print **; a**
````
- **Semántico:** comprueba que la sentencia se pueda realizar. Tiene dos fases:
	- **Identificación**: busca las definiciones
	- **Comprobación de tipos**: valida el AST con predicados, atributos y funciones semánticas
- **Generación de código**: dos fases:
	- **Gestión de memoria**: asigna direcciones
	- **Selección de instrucciones**: genera código usando plantillas

## Léxico
- Entran caracteres y salen tuplas
- Las tuplas son una clase de token (conjunto de lexema + token)
- Cuando no hay más tokens, se llama a una convención END (**EOF**) = 0

## ¿Cómo hacer una especificación? Pasos
Expresiones regulares
1. Determinar los tokens
2. Definir un patrón para cada token

### Implementación (que puede ser manual o con herramienta)
1. Ignorar comentarios y token comentario
2. Comprobar patrones
3. Notificar error (no hay token error)

Mirar ejercicios en [[Ejercicios Examen Teoria DLP🐲#Léxico]]

---
# Sintáctico

- Se encarga de que los tokens estén en el orden adecuado.

## Reglas
- Las expresiones usan notación infija
- El número de paréntesis abiertos es siempre igual al de paréntesis cerrados

==Mayúscula --> TOKEN --> Z
minúscula --> no terminal --> a==

## Lenguaje
- Es el conjunto de todas las sentencias de una gramática, es decir, el conjunto de todos los posibles programas

## Tipos de algoritmos
![[Pasted image 20230510114850.png]]
**Dirección**
- **Descendentes**: son aquellos que realizan el proceso a partir del símbolo inicial e intentan llegar a la cadena de entrada (lo que se ha visto en clase)
- **Ascendente**s: realizan el proceso a la inversa. Parten de la cadena de entrada y haciendo transformaciones a la inversa (sustituyendo la parte derecha de una regla por la parte izquierda), intentan llegar al símbolo inicial. Estas transformaciones a la inversa se llaman **reducciones**.

Selección
- **Backtracking** (No determinista): se elige una regla, y si no se llega a la cadena final, se retrocede a un punto en el que se hubiera podido seguir otra regla.
- **Predictivo** (determinista): cuando se presenta la situación de tener que elegirr entre varias reglas candidatas, se asegura de coger la adecuada. Nunca retrocede.
	- **Clasificación de parsers predictivos**
		- **LL(1)**: aquellos que miran como máximo un token de entrada
		- **LL(2)**: aquellos que miran como máximo dos token de entrada

## Tipos de gramáticas
- Las gramáticas reciben el nombre directamente del parser con el que pueden ser tratadas, es decir, el nombre de la gramática indica con qué parser se puede o no implementar.
![[Pasted image 20230510114912.png]]
- **LL(k):** reconocida con un parser LL(k) de manera predictiva sin backtracking y en dirección descendente
- **LR(k)**: reconocida con un parser LR(k) de manera predictiva y en dirección ascendente
![[Pasted image 20230510120757.png]]

![[Pasted image 20230510121625.png]]

### ==Preguntas de examen==

- ANTLR es una herramienta ascendente o descendente? ==descendente==
- Una gramática L(1) puede usar recursividad iszuierda? ==no==
- Si una gramática no pasa únicamente el algoritmo L(1), ¿es ambigua? ==no==

## Tipos de listas
|Tipo de Lista|Cadenas que genera|
|--|--|
|1+ss|_e ee eee eeee ..._|
|0+ss|_ε e ee eee eeee ..._|
|1+cs|_e ese esese ..._|
|0+cs|_ε e ese esese ..._|

## Patrones
Tabla original de Holub con una columna EBNF:
![[Pasted image 20230510122811.png]]
![[Pasted image 20230510122833.png]]

![[Pasted image 20230510122909.png]]

Mirar ejercicios en [[Ejercicios Examen Teoria DLP🐲#Sintáctico]]

---
# Análisis semántico
- **Sintaxis**: conjunto de reglas formales (gramática) que definen la estructura correcta de los programas de un lenguaje.
- **Semántica**: conjunto de reglas formales que definen el significado de los programas sintácticamente correctos.

- Los **intérpretes** tienen que conocer toda la semántica que hay.

- El **análisis semántico** de un procesador de lenguaje es la fase que hace cumplir las reglas semánticas del lenguaje. Es la última oportunidad para detectar errores en el programa. Después de esta fase comienzan las fases de síntesis.

## Interfaz del Analizador Semántico
![[Pasted image 20230510143426.png]]

## Comprobaciones semánticas
- Definición de variables y reglas de ámbito
![[Pasted image 20230510143700.png]]
- **Unicidad**: entidades que deberían ser únicas (enum, cases y switch)
- **Enlaces**: cuando el uso de una entidad debe vincularse a otra construcción (invocación de funciones)
- **Comprobaciones pospuestas por el analizador sintáctico**: l-value obligatorio en asignaciones, al menos una sentencia return en una función...
- **Comprobaciones dinámicas**: realizadas en tiempo de ejecución (accesos a arrays fuera de límites, comprobación de null)
- **Comprobación de tipos**: es la tarea más importante. Un analizador semántico debería:
	- Inferir el tipo de las expresiones sintácticamente válidas
	- Comprobar que las operaciones que se van a aplicar a una expresión son válidas respecto a su tipo

## Anotación del AST
- Un analizador semántico verifica las reglas semánticas recorriendo un AST al que añade información adicional, recibiendo el nombre de **AST decorado**.
- Para decorar los AST vamos a usar **gramáticas atribuidas** (AG)

## Gramáticas Libres de Contexto (CFG)
- Se usan para especificar la sintaxis de los lenguajes de programación. Sin embargo, no pueden representar la información adicional necesaria en las siguientes fases.
![[Pasted image 20230510144730.png]]
![[Pasted image 20230510144750.png]]
![[Pasted image 20230510144927.png]]
![[Pasted image 20230510145226.png]]
![[Pasted image 20230510145243.png]]
![[Pasted image 20230510145302.png]]
![[Pasted image 20230510145421.png]]
![[Pasted image 20230510145452.png]]
### ==Ejemplo de AG==
Dada la siguiente gramática abstracta:
**(G):**
![[Pasted image 20230510145614.png]]
- Añadimosun atributo booleano hasReturn a los símbolos de la gramática funcdefinition y statement
- Calculamos sus valores mediante reglas semánticas

Definir una AG:
**(A):**
`{funcdefinition.hasReturn, statement.hasReturn}`

**(R):**
```java
(1) funcdefinition.hasReturn = statement.stream().anyMatch(stmt -> stmt.hasReturn)
(2) statement.hasReturn = false
(3) statement.hasReturn = true
(4) statement.hasReturn = statement.stream().anyMatch(stmt -> stmt.hasReturn)
```

## Gramáticas atribuidas
- Las **gramáticas atribuidas** añaden atributos a las construcciones sintácticas de un lenguaje
- Las AG especifican, de forma declarativa, **cómo se calculan los valores de los atributos**

## Atributos
- Un **atributo** es una propiedad de una construcción sintáctica. 
	- Para cada atributo, su **dominio** debe ser especificado (ej: type debe ser int, char o double)
	- Cuando un símbolo aparece más de una vez en una producción, se usan sufijos para referirse sin ambigüedades a sus atributos
- **Atributos MÁS comunes**:
![[Pasted image 20230510150549.png]]

## Reglas semánticas
- Especifican cómo se calcula un atributo de un símbolo a partir de los atributos de otros símbolos en la misma producción

## Evaluación de las gramáticas atribuidas
- Cálculo de todos los atributos de un programa dado. 
- Precisa calcular el orden de ejecución de las reglas semánticas

## Algoritmo general para la evaluación de las AGs:
1. Contruir el árbol de sintaxis para un programa específico
2. Crear el grafo de dependencias de atributos
3. Calcular un ordenamiento topológico del grafo dirigido
4. Ejecutar las reglas semánticas, siguiendo dicho ordenamiento topológico

## Gramáticas bien definidas
- Una AG está bien definida (no circular) si, para cada árbol sintáctico, pueden ser evaluados todos los atributos
![[Pasted image 20230510152646.png]]

## Atributos sintetizados
- Para evaluar las AGs usaremos AGs donde los atributos de los nodos padres dependen de los atributos de los nodos hijos (conocidos como atributos sintetizados)
![[Pasted image 20230510152901.png]]

## Atributos heredados
- Se asigna un valor a los atributos de los nodos hijos

![[Pasted image 20230510153240.png]]
![[Pasted image 20230510153350.png]]
![[Pasted image 20230510153405.png]]

## Patrón Visitor
- Para recorrer el ast con un **visitor**, llamaremos al método **accept** (y dentro de este sí podemos llamar a un visit)
![[Pasted image 20230510153653.png]]

## Tipo de las variables
- Debe ser indicado en su definición en los lenguajes con declaración explícita de tipos
![[Pasted image 20230510154142.png]]
- Por lo tanto, tenemos que almacenar el tipo de una variable en su **definición** (**varDefinition**)
- Su tipo de puede consultar posteriormente cuando se utiliza la Variable (nodo Variable)
- Por lo tanto, el nodo **Variable** estará **enlazado a** (decorado con) su correspondiente nodo varDefinition
- Este trabajo lo realiza la fase de **Identificación**
![[Pasted image 20230510154412.png]]

## Tabla de Símbolos
- Estructura de datos temporal donde se almacenan los nodos VarDefinition para permitir su posterior recuperación
- Una vez que los nodos Variable están vinculados a las VarDefinitions correspondientes, la tabla de símbolos **se puede eliminar**

## Ámbito de las variables
- El ámbito es la parte de un programa donde el nombre de una variable está vinculado a una entidad
- global o local

## Comprobación de tipo
- Las reglas semánticas relacionadas con la comprobación de tipos son de las más importantes (ej: `[]` sólo se puede usar en arrays)
- Si la regla no se cumple se produce un error de tipo
- La comprobación de tipo consta de las siguientes dos tareas:
	1. Debe inferirse el tipo de cada subexpresión
	2. Debe verificarse que sean válidas las operaciones acplicadas a cada subexpresión respectivamente

## Fase de compilación
- Aunque la comprobación de tipos y la identificación se pueden realizar en la misma pasada, separarlos en diferentes recorridos normalmente produce un código más fácil de mantener
- La fase de **identificación** se realiza antes de la de **comprobación de tipos**
- Por lo tanto, el recorrido de comprobación de tipos puede confiar en el enlace existente entre cada nodo Variable y su correspondiente Definition (a través del atributo definition)

## Definición de tipo
- Los tipos suelen ser definidos desde 3 puntos de vista diferentes:
	- **Denotacional**: conjunto de valores
	- **Basado en abstracción**: es una interfaz con operaciones
	- **Constructivo**:
		- **built-in**: tipos primitivos
		- **compuesto** aplicando un constructor de tipos (astruct, array, puntero...)

## Expresión de tipo
- Es la representación de un tipo
- Se basan en la definición constructiva de tipo
- Una expresión de tipo es:
	- Un **tipo básico** (built-in) (int, char, double...)
	- O un **tipo compuesto** creado aplicando un constructor de tipo (array...) a otras expresiones de tipo (array(int)...)

## Sistema de Tipos
- Colección de reglas para asignar expresiones de tipo a las diferentes construcciones sintácticas del lenguaje
- Un comprobador de tipos implementa un sistema de tipos y es parte del analizador semántico
- Las gramáticas atribuidas proporcionan un mecanismo para especificar sistemas de tipos

## Patrón Composite
Anotación para resolver el ejercicio 6 de Semántico -> [[Ejercicios Examen Teoria DLP🐲#Semántico]]
![[Pasted image 20230510162824.png]]
![[Pasted image 20230510162842.png]]
![[Pasted image 20230510162856.png]]
![[Pasted image 20230510163105.png]]
![[Pasted image 20230510163139.png]]

Mirar ejercicios en [[Ejercicios Examen Teoria DLP🐲#Semántico]]

---
# Lenguajes y representaciones intermedias
Hay:
- De alto nivel
- De medio nivel
- De bajo nivel

## MAPL: Arquitectura
MAPL es una **representación intermedia de Medio nivel**.

- **IP**, Instruction Pointer: dirección de la instrucción en ejecución
- **SP**, Stack Pointer: dirección del tope de la pila
- **BP**, Base Pointer: dirección del marco de pila activo
![[Pasted image 20230510170136.png]]

## MAPL: Instrucciones push y pop
![[Pasted image 20230510170225.png]]

## MAPL: Instrucciones load
![[Pasted image 20230510170327.png]]

## MAPL: Instrucciones store
![[Pasted image 20230510170413.png]]

## MAPL: Operaciones
![[Pasted image 20230510171142.png]]

## MAPL: I/0 y Conversiones
![[Pasted image 20230510171215.png]]
Ver ejercicios en [[Ejercicios Examen Teoria DLP🐲#Generación de código]]

---
# Generación de código