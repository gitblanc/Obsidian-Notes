# Clase 1 - Conceptos básicos

## Fases de un traductor
- Si se clasifican por su **función** se dividen en: **Fases de análisis y Síntesis**
- Si se clasifican por su **dependencia de la máquina destino**, se dividen en **Front-end** y **Back-end**
![[slide_12.2133bc32.png]]
## Fases de análisis y Síntesis
- Las **fases de análisis** tienen el objetivo de comprobar la validez de la entrada, y en caso positivo identificar su estructura. Las fases de análisis son:
	- Análisis Léxico
	- Análisis Sintáctico
	- Análisis Semántico
- Las **fases de Síntesis** son las que dada una entrada válida, se encargan de generar el código de salida. Las fases de síntesis son:
	- Generación de código
	- Optimización

- **Léxico**: separa en tokens
	- Comprueba que las palabras sean válidas
	- Se asigna a cada lexema un token único
````java
pri**#**nt ; a
````
- **Sintáctico**: crea el AST
	- Forma estructuras  a partir de tokens
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

## Árbol Abstracto (AST)
- Es el árbol mínimo que preserva la semántica de la entrada.
- Para decidir qué debería haber en el AST de un lenguaje, hay que decidir qué es lo mínimo que necesitarían saber las siguientes fases para generar el código destino. 
Ejemplo:
El de abajo sería el AST y el del medio un árbol concreto.
![[slide_33.01b18c08.png]]

# Léxico
- Comprueba que todo lo que se ha escrito en la entrada sean secuencias de caracteres válidas.
- Va leyendo de la entrada carácter a carácter hasta que detecta una cadena válida (lexema) o una cadena errónea.
- Una vez encontrado un lexema, le asigna un número llamado **Token** (al cual se le puede ver como el tipo o la categoría a la que pertenece el lexema)
- Entran caracteres y salen tuplas
- Las tuplas son una clase de token (conjunto de lexema + token)
- Cuando no hay más tokens, se llama a una convención END (**EOF**) = 0

El léxico facilita las fases posteriores creando tokens que representan dichas palabras reservadas.
![[Pasted image 20230513100644.png]]
Dado que sería engorroso trabajar con números, se definen constantes para simplificar su manejo:
![[Pasted image 20230513100809.png]]

Ejemplo de analizador léxico:
![[slide_23.e6f92c05.png]]

## Qué no hace el léxico
- No se ocupa de que las cadenas aparezcan en el orden adecuado (eso lo hace el sintáctico)
```java
altura = ; 25   // Esto no es problema del léxico!!
```

## Representación de los tokens
- Los tokens se definen como constantes
- Sin embargo, si el token está formado por un sólo lexema y dicho lexema tiene sólo un caracter, se le asocia como número el token de código ASCII
```java
static final int WHILE = 257;
static final int IF = 260;
...
static final int IGUAL = ‘=’;
static final int P_COMA = ‘;’;
```
Esto permite hacer una simplificación de código, ya que es un número conocido y no es necesario definir dichas constantes por ser redundante:
```java
static final int IDENT = 256;
static final int WHILE = 257;
static final int IF = 260;
...

// static final int IGUAL = ‘=’;
// static final int P_COMA = ‘;’;
```

## Implementación de un token
```java
public class Token {

    public Token(String lexeme, int tokenType, int line, int column) {
        this.lexeme = lexeme;
        this.tokenType = tokenType;
        this.line = line;
        this.column = column;
    }

    public String getLexeme() { return lexeme; }
    public int getType() { return tokenType; }
    public int getLine() { return line; }
    public int getColumn() { return column; }

    private String lexeme;
    private int tokenType, line, column;
}
```

## ¿Cómo hacer una especificación? Pasos
Expresiones regulares
1. **Determinar los tokens**: hay que definir de una forma lo más clara posible lo que representa un token
	En definitiva, la solución correcta para los delimitadores es hacer un token por cada uno:
```java
class Lexico {
    static final int IDENT = 256;
    static final int WHILE = 257;
    ...
	//no hacer static final int DELIMITADOR = 261; // Lexemas: '(' ')' '{' '}'
    static final int PARENT_A = ‘(’;
    static final int PARENT_C = ‘)’;
    static final int LLAVE_A = ‘{’;
    static final int LLAVE_C = ‘}’;
}
```
3. **Definir un patrón para cada token**: hay que decidir qué es válido y qué no.
```
_a
hol#a
_32
```
¿Són lexemas válidos? ¿Són _identificadores_ (_IDENT_)? -> depende de las decisiones de diseño tomadas en los **metalenguajes**

## Metalenguajes
- Un **metalenguaje** es un lenguaje que se caracteriza porque aquello que describe es otro lenguaje. Necesitan dos propiedades:
	- **Precisión**: ante cualquier entrada no haya duda de si es válida o no para ese token
	- **Concisión**: que la regla sea lo más compacta posible para facilitar su entendimiento e implementación
 Sin embargo, no hay un metalenguaje que sirva para todo. Hay que usar distintos metalenguajes para definir mejor cada aspecto por separado. Los dos metalenguajes más usados son **Autómatas finitos** y **expresiones regulares**

## Expresiones regulares. Operadores
![[Pasted image 20230513111300.png]]
Ejemplo:
```java
pa+ // pa paa paaa paaaa paaaaa...
(pa)+ // pa papa papapa papapapa...
```

## Tareas de un léxico
En cada llamada al método `nextToken()`
- Ignorar los comentarios
- Ignorar los espacios en blanco y los saltos de línea
- Comprobar los patrones de la especificación
- Notificar errores

## Implementación (que puede ser manual o con herramienta)
1. Ignorar comentarios y token comentario
2. Comprobar patrones
3. Notificar error (no hay token error)

## Notación de ANTLR. Aspectos generales
### Operadores
![[Pasted image 20230513112059.png]]
La versión normal (_greedy_) y la versión _non-greedy_ se diferencian en el momento en el que paran de reconocer una cadena. La versión _non-greedy_ dejar de reconocer en cuanto ha encontrado un lexema válido. La versión normal (o _greedy_) sigue reconociendo por si puede formar un lexema más largo que también cumpla el patrón (si no lo consigue, devolvería lo mismo que la versión _non-greedy_). Es decir, la versión normal intenta formar el lexema más largo que cumpla el patrón.

Por ejemplo, supóngase el siguiente patrón con la versión normal del '*':
```java
T: '@' .* '@';
```

Ante una entrada como la siguiente:
```
@hola@@adios@
```

Sin embargo, usando la versión _non-greedy_ del operador:
```java
T: '@' .*? '@';
```
En la primera llamada a _nextToken_ se formaría sólo el lexema "@hola@" (deja de leer más caracteres en cuanto la entrada cumple el patrón) y en una segunda llamada a _nextToken_ ya se devolvería "@adios@".

## Prioridades de las reglas
¿Qué pasa si una misma entrada casa con más de un patrón? Hay que conocer las reglas de prioridad de ANTLR.

Supóngase la situación con el fichero de ANTLR de la izquierda y la entrada "32954".
![[slide_43.a3d56383.png]]
Cumpliendo esas reglas, se podría reconocer esa entrada de las tres formas que se muestra en la imagen: la primera devolvería dos lexemas, la segunda tres y la última sólo uno. ¿Cuál de ellas produce el método _nextToken_ generado por ANTLR?
- ==NORMA1: Cuando una entrada puede ser reconocida por más de una regla, se elige aquella que forme el lexema más largo==
- ANTLR elegiría la regla _T2_ ya que forma el lexema "32954" que es más largo que el lexema "32" que formaría _T1_.
![[slide_44.fe240e55.png]]

Supóngase ahora la siguiente situación en la que se cambia la cadena de entrada y pasa a ser "32ALJ".
![[slide_45.bf90962d.png]]
En este caso ambas reglas forman un lexema del mismo tamaño, por lo que la norma 1 no es de ayuda.
- ==NORMA2: Cuando varias reglas forman un lexema del mismo tamaño, se elige la regla que se haya definido primero==
- Siguiendo la norma 2, _nextToken_ devolvería ahora el token _T1_ con el lexema "32".

Mirar ejercicios en [[Ejercicios Examen Teoria DLP🐲#Léxico]]

---
# Sintáctico

- Se encarga de que los tokens estén en el orden adecuado.

Ejemplo:
Supóngase este programa:
```java
if a > b then
    print a;
```
Lo que haría el analizador sintáctico, una vez recibidos los tokens, sería encontrar las estructuras resaltadas en negrita encima de los tokens:
![[slide_26.6e1c24b8.png]]
Ahora, el analizador sintáctico forma un árbol que muestra la composición del programa analizado. A este árbol se le denomina árbol de análisis gramatical. En estetexto se le llamará **árbol concreto**:
![[slide_30.82dae4fa.png]]

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

Supóngase la siguiente entrada:
```java
print v[i] + 2;
```
¿Qué cosas podrían estar mal en cuanto a las sentencias anteriores?
- Que v no esté definida
- Que i no esté definida
- Que i esté definida pero no sea de tipo entero
- Que v esté definida pero no sea un array
- Que `v[i]` fuera de tipo no numérico, y no se pudiese sumar con el 2

Se subdivide en dos fases:
- **Identificación**
- **Comprobación de tipos**

- **Sintaxis**: conjunto de reglas formales (gramática) que definen la estructura correcta de los programas de un lenguaje.
- **Semántica**: conjunto de reglas formales que definen el significado de los programas sintácticamente correctos.

- Los **intérpretes** tienen que conocer toda la semántica que hay.

- El **análisis semántico** de un procesador de lenguaje es la fase que hace cumplir las reglas semánticas del lenguaje. Es la última oportunidad para detectar errores en el programa. Después de esta fase comienzan las fases de síntesis.

## Fase de Identificación
- Comprueba que todo símbolo que se use en el programa (variables, funciones, estructuras, clases...) haya sido definido en algún lugar del programa. Si no es así no tiene sentido seguir compilando
- Si volvemos al ejemplo `print v[i] + 2;` esta etapa detectaría que las variables v e i estén definidas en el programa:

Ejemplo de realización de la etapa:
![[slide_37.f7034af6.png]]
Lo que hace esta etapa es recorrer el AST, y cada vez que encuentre una referencia a una variable (un nodo var), se busca si existe una definición con el mismo nombre de la variable (un nodo defVar)
![[slide_38.b52611eb.png]]
![[slide_40.8d4b4121.png]]
Una vez que se ha comprobado que todo símbolo ha sido definido, el programa quedaría validado por esta etapa.

### Enlace de definiciones
- En esta etapa, además de comprobar que todo nodo var(n) tiene su defVar(n) hace algo más. Las fases posteriores necesitarán saber cómo se ha definido cada símbolo (tipo, ámbito...). Para que no tengan que repetir la búsqueda la definición del símbolo que ya se ha hecho aquí, esta etapa deja un enlace desde el símbolo a su definición

En el ejemplo anterior añadimos el enlace:
![[slide_41.0cc28050.png]]

## Etapa de Comprobación de Tipos
- Esta etapa se encarga de comprobar toda aquella situación relativa a los tipos. Algunos ejemplos de situaciones son:
	- Operar tipos incompatibles
	- Llamadas a funciones con un número o tipo erróneo en los argumentos
	- Asignaciones a variables de valores incorrectos

Volviendo al ejemplo inicial:
```
print v[i] + 2;
```
De los cinco errores inicialmente indicados, esta etapa sería la que detectaría los tres últimos:
-   Que _i_ no fuera de tipo entero.
-   Que _v_ no fuera un array.
-   Que `v[i]` no fuera un tipo no numérico.

### Predicados, atributos y funciones semánticas
Supóngase la siguiente programa entrada y su AST correspondiente:
![[slide_44a.eb45116d.png]]
Para comprobar que las operaciones se están realizando con operandos del tipo adecuado, se asocian al AST **predicados** que detectan aquellas situaciones que no sean válidas. Son las condiciones que deben cumplir los nodos del árbol para que sean considerados válidos.

Supongamos que en este lenguaje hay dos normas:
- No se puede asignar un valor real a un entero
- Los operandos de una suma deben ser numéricos

Estas normas se reflejan mediante predicados que se asocian a ciertos nodos del árbol:
![[slide_44b.dec4d4ed.png]]
Pero esta etapa necesita algo más de información del AST, por lo que hay que añadirla. Esta información se la llama **atributos**. En este caso los atributos serían los 4 valores tipo añadidos a los nodos var, aritmetica y litReal:
![[slide_44c.bd7a54b8.png]]
Para saber el valor de ese atributo están las **funciones semánticas**, que indican qué valor tiene que tomar cada atributo en cada nodo:
![[slide_44d.4210003f.png]]

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
Los principales subproblemas de la generación de código son:
1. Asignación del almacenamiento
2. Selección de instrucciones
3. Asignación de registros

## Entornos de ejecución
- Un compilador debe:
	- **Asignar estáticamente la dirección de memoria** que tendrá cualquier variable en tiempo de ejecución (ha de hacerlo en tiempo de compilación)
	- **Generar código** que gestione la organización de la memoria en tiempo de ejecución y mantenga la información para guiar el proceso de ejecución

## Símbolos y tipos
- Los **símbolos** (Variable) en el análisis semántico se enlazan a sus definiciones para inferir sus tipos (fase de identificación). En la generación de código se utilizan para conocer las direcciones de memoria de las variables
- Los **tipos** en el análisis semántico se utilizan para verificar la validez de algunas construcciones sintácticas. En la generación de código incorporan el tamaño y la representación de cada variable

## Tipos
![[Pasted image 20230510172952.png]]
![[Pasted image 20230510173058.png]]
![[Pasted image 20230510173112.png]]

El **número de bytes** para almacenar un **array** es la multiplicación de su tamaño y el número de bytes del tipo de sus elementos.
![[Pasted image 20230510173242.png]]
```java
public int numberOfBytes(){
	return size*elementType.numberOfBytes();
}
```

## Tipos Compuestos: Structs
- Un registro (struct) es una colección de campos de diferentes tipos donde cada campo se identifica por su nombre
	- El **tamaño** de un registro es la suma de los tamaños de los tipos de los campos
	- El **desplazamiento** (offset) de memoria relativo de cada campo es la suma de los tipos de los campos anteriores
![[Pasted image 20230510174109.png]]

## Memoria estática
- El tamaño de la memoria estática permanece fijo durante la ejecución del programa
- La memoria estática se divide en áreas de código y datos
- El tamaño del área de datos en la memoria estática permanece fijo durante todo el proceso de ejecución
- Normalmente se accede a los datos estáticos por sus direcciones de memoria absolutas
- Los datos comunres incluídos en la memoria estática son:
![[Pasted image 20230510202416.png]]
- En MAPL los datos estáticos tienen direcciones de memoria crecientes, comenzando en cero
![[Pasted image 20230510202630.png]]

## Plantillas de código
- Se basan en **semántica denotacional** (formalizar el significado de una construcción sintáctica describiendo el efecto de ejecutarla)
![[Pasted image 20230510210631.png]]

## Elementos de una plantilla de código
![[Pasted image 20230510210743.png]]

## Generación de código Inductiva
![[Pasted image 20230510210830.png]]

## Escribiendo el código generado
![[Pasted image 20230510211008.png]]

## Contexto
![[Pasted image 20230510211104.png]]

## Parametrización de plantillas. Alternativa 1
![[Pasted image 20230510211136.png]]
![[Pasted image 20230510211326.png]]

## Parametrización de plantillas. Alternativa 2
![[Pasted image 20230510211353.png]]
- Las funciones de código que se usan son **address, value y execute**:
![[Pasted image 20230510211416.png]]
![[Pasted image 20230510211532.png]]

## Funciones de código
![[Pasted image 20230510211622.png]]

## Definiciones de funciones de código
![[Pasted image 20230510211709.png]]
![[Pasted image 20230510211845.png]]
Implementación típica: usar 3 visitors -> ExecuteCGVisitor, ValueCGVisitor, AddressVisitor
![[Pasted image 20230510212125.png]]
![[Pasted image 20230510212245.png]]

## Generación de código de estructuras de datos: Definición de variable
![[Pasted image 20230510212918.png]]

## Generación de código de estructuras de datos: Definición de variable Local
![[Pasted image 20230510212946.png]]

## Generación de código de estructuras de datos: Expresiones
![[Pasted image 20230510213405.png]]
![[Pasted image 20230510213417.png]]
![[Pasted image 20230510213442.png]]

## Generación de código de estructuras de datos: Arrays
![[Pasted image 20230510213635.png]]
![[Pasted image 20230510213700.png]]
![[Pasted image 20230510213725.png]]
## Generación de código de estructuras de datos: Registros
![[Pasted image 20230510214332.png]]
![[Pasted image 20230510214359.png]]

## Sentencias de control de flujo. Etiquetas y saltos
![[Pasted image 20230510214548.png]]

## While
![[Pasted image 20230510214626.png]]
![[Pasted image 20230510214643.png]]

## Do while
![[Pasted image 20230510214707.png]]
![[Pasted image 20230510214720.png]]

## For
![[Pasted image 20230510214750.png]]
![[Pasted image 20230510214831.png]]
![[Pasted image 20230510214846.png]]

## If/else
![[Pasted image 20230510214911.png]]
![[Pasted image 20230510214925.png]]

## Funciones/Procedimientos
![[Pasted image 20230510215000.png]]
![[Pasted image 20230510215030.png]]
![[Pasted image 20230510215041.png]]

---





