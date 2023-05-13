
*Ejemplo 110:*
La entrada a traducir es la siguiente, implementada en un lenguaje ficticio al estilo _C_.
```c
int x, y;
y = x + (int) 3.14;
```
- **Léxico**: encontrar todos los tokens
![[slide_79.5d489f92.png]]
- **Sintáctico**: una vez tenemos los tokens, mostrar el AST
![[slide_81.36db6838.png]]
- **Semántico**: validar el AST
![[slide_82.e7b1f579.png]]
- **Generación de código**: generar el código resultante
![[slide_84.4acd89fd.png]]
![[slide_85.c066df4e.png]]

# Léxico
1. 
![[Pasted image 20230510111324.png]]
![[Pasted image 20230510111357.png]]

2. Supóngase un programa:
````java
Lexico lex = new Lexico(new FileReader(“prog.txt"));
Token token;
while ((token = lex.nextToken()).getType() != Lexico.END) {
    System.out.println(token.getLexeme());
    System.out.println(token.getType());
    System.out.println(token.getLine());
}
````
Ahora supóngase la siguiente entrada:
```java
altura
+
1.75
```
Y finalmente, supóngase que se han definidos las siguientes constantes asociadas a los tokens del lenguaje:

```java
class Lexico {
    static final int END = 0;
    static final int IDENT = 257;
    static final int IF = 258;
    static final int LITENT = 259;
    static final int LITREAL = 260;
    …
}
```
El resultado es:
| |(getLexema, getTipo, getLinea)|
|---|---|
|1|("altura", 257, 1)|
|2|("+", 261, 2)|
|3|("1,75", 260, 3)|
|4|(?, 0, 2)|

==Nota: el ? indica EOF==

3. Hacer el analizador léxico del siguiente lenguaje usando ANTLR.

```java
edad = 65;	 # Comentario de una línea
print a
read b;
print "fin"
```

```g4
IGUAL: '=';
PCOMA: ';';

PRINT: 'print';
READ: 'read';

LITENT: [0-9]+;
IDENT: [a-zA-Z]*[a-zA-Z0-9]*;

STRING: '"' (~[\r\n])* '"';

COMMENT: '#'.*? '\n' -> Skip; //CON EL OPERADOR NON-GREEDY
COMMENT: '#' ~[\r\n]* -> Skip; //SIN EL OPERADOR NON-GREEDY

WS: [ \t\r\n]+ -> skip;
```

---

# Sintáctico

1. 
![[Pasted image 20230510111456.png]]
![[Pasted image 20230510111521.png]]

2. 
![[Pasted image 20230510114029.png]]
![[Pasted image 20230510114120.png]]

3. 
![[Pasted image 20230510114253.png]]
![[Pasted image 20230510114310.png]]

==NOTA: los ejs 2 y 3 son gramáticas equivalentes==

4. Decir si es una sentencia válida
![[Pasted image 20230510114513.png]] ![[Pasted image 20230510114550.png]]
![[Pasted image 20230510114612.png]]
![[Pasted image 20230510114704.png]]

5. Dada la siguiente gramática G: ==(IGUAL QUE EL 4)==
```g4
programa ⟶ programa def
        | ε

def ⟶ tipo listaId ‘;’

tipo ⟶ INT | DOUBLE

listaId ⟶ IDENT
        | listaId ‘,’ IDENT
```

Determinar si la siguiente entrada es válida. En caso afirmativo, construir su árbol de análisis gramatical (árbol concreto).

```java
int a, b;
double x;
```
Si que es válida, pues se puede llegar a la cadena realizando transformaciones a partir de **programa**
![[Pasted image 20230510121004.png]]

6. Dada la siguiente gramática, implementar un parser de la misma utilizando la técnica _recursiva descendente_.
```g4
prog ⟶ decl decl

decl ⟶ variables | typedef

variables ⟶ VAR IDENT restoIdents

restoIdents ⟶ ‘,’ IDENT restoIdents
	     | ‘:’ tipo

tipo ⟶ INT | FLOAT

typedef ⟶ TYPE IDENT restoIdents
```

Solución:
```java
public class RecursiveParser {
    ...

    public void prog() throws ParseException {
        decl();
        decl();
        match(Lexicon.EOF);
    }

    void decl() throws ParseException {
        if (token.getType() == Lexicon.VAR)
            variables();
        else if (token.getType() == Lexicon.TYPE)
            typedef();
        else
            error();
    }

    void variables() throws ParseException {
        match(Lexicon.VAR);
        match(Lexicon.IDENT);
        restoIdents();
    }

    void restoIdents() throws ParseException {
        if (token.getType() == Lexicon.COMA) {
            match(Lexicon.COMA);
            match(Lexicon.IDENT);
            restoIdents();
        } else if (token.getType() == Lexicon.PUNTOS) {
            match(Lexicon.PUNTOS);
            tipo();
        } else
            error();
    }

    void tipo() throws ParseException {
        if (token.getType() == Lexicon.INT)
            match(Lexicon.INT);
        else if (token.getType() == Lexicon.FLOAT)
            match(Lexicon.FLOAT);
        else
            error();
    }

    void typedef() throws ParseException{
        match(Lexicon.TYPE);
        match(Lexicon.IDENT);
        restoIdents();
    }
}
```

7. Hacer una especificación ANTLR para un lenguaje con las siguientes características:
![[Pasted image 20230510121917.png]]

Solución:
- Primero implementamos el léxico del lenguaje:
```
lexer grammar Lexicon;

NUM : [0-9]+;
IDENT : [a-zA-Z0-9_]+;

WS : [ \t\r\n]+ -> skip;
```
- Ahora la gramática:
```g4
grammar Grammar;

import Lexicon;

start : 'print' expr ';';

expr:
	NUM
	| IDENT
	| '(' expr ')'
	| expr ('*' | '/') expr
	| expr ('+' | '-') expr
	| expr ('==' | '!=') expr
	| expr '&&' expr
	| expr '||' expr
	;
```

8. 
![[Pasted image 20230510123020.png]]
![[Pasted image 20230510123048.png]]

9. Describir los nodos que hay y decir qué hijos tiene cada uno. Crear la gramática abstracta para el lenguaje del ejemplo.
![[Pasted image 20230510123227.png]]
Solución:
```g4
programa ⟶ defVariable* sentencia*
defVariable ⟶ nombre:string tipo

intType:tipo ⟶  ε
realType:tipo ⟶ ε

escritura:sentencia ⟶ expresion
if:sentencia ⟶ condicion:expresión cierto:sentencia* falso:sentencia*

exprBinaria:expresion ⟶ left:expresión operator:string right:expresion
invocacion:expresion ⟶ nombre:string args:expresion*
variable:expresion ⟶ lexema:string
literalInt:expresion ⟶ lexema:string
literalReal:expresion ⟶ lexema:string
```

10. Dada la siguiente especificación sintáctica en ANTLR y la gramática abstracta que define los nodos del AST, añadir la especificación de ANTLR el código que cree el AST de las entradas:
Abstracta:
```
programa ⟶ definicion print;

definicion ⟶ tipo nombre:string;

tipoInt:tipo ⟶  ;
tipoReal:tipo ⟶ ;

print ⟶ expr:expresion;

variable:expresion ⟶ nombre:string;
literalEntero:expresion ⟶ valor:string;
```
Gramática
```g4
start
	: definicion print EOF
	;

definicion
	: tipo IDENT ';'
	;

tipo
	: 'int'
	| 'float'
	;

print
	: 'print' expr ';'
	;

expr
	: IDENT
	| LITENT
	;
```

Solución:
El parser sería:
```g4
@parser::header {
    import ast.*;
}

start returns[Programa ast]
	: definicion print EOF { $ast = new Programa($definicion.ast, $print.ast); }
	;

definicion returns[Definicion ast]
	: tipo IDENT ';' { $ast = new Definicion($tipo.ast, $IDENT.text); }
	;

tipo returns[Tipo ast]
	: 'int'		{ $ast = new TipoInt(); }
	| 'float'	{ $ast = new TipoReal();}
	;

print returns[Print ast]
	: 'print' expr ';' { $ast = new Print($expr.ast); }
	;

expr returns[Expresion ast]
	: IDENT		{ $ast = new Variable($IDENT.text); }
	| LITENT	{ $ast = new LiteralEntero($LITENT.text); }
	;
```

11. Dada la siguiente gramática:
```g4
programa: sent*
sent: PRINT expr ';'
expr: IDENT
	| INT_CONSTANT
	| expr '*' expr
	| expr '+' expr
```
a) Añadir la invocación de funciones y procedimientos en BNF y EBNF.
Ejemplos:
- `print a+f();`
- `print log(n,2);`
- `print doble(doble(a));`
- `print (23)`
b) Añadir el uso de arrays de 1 dimensión y tipos primitivos y registros de tipos primitivos
c) Añadir el uso de arrays de cualquier dimensión y tipo y registros de cualquier tipo
d) Añadir la asignación a=4 (múltiple)

Solución:
```
programa: sent*
sent: PRINT expr ';'
	| expr ';' //asignación múltiple
expr: IDENT
	| INT_CONSTANT
	| expr '*' expr
	| expr '+' expr
	| IDENT '(' expr ')' //invocación a funciones
	| IDENT '[' expr ']' //arrays de cualquier dimensión
	| expr '=' expr //asignación simple
	
```
![[Pasted image 20230511163635.png]]


---

# Semántico

1. 
![[Pasted image 20230510111647.png]]

2. 
![[Pasted image 20230510151010.png]]
![[Pasted image 20230510151037.png]]
![[Pasted image 20230510151109.png]]

Solución:
**(G):**![[Pasted image 20230510151037.png]]
**(A):**
`{expression.lvalue} dominio=booleano`

**(R):**
```java
(4) expression.lvalue = true
(5) expression.lvalue = false
(1) expression1.lvalue = false //no se permite en el enunciado
(2) expression1.lvalue = expression2.lvalue
(3) expression1.lvalue = true //lo pone en el enunciado
```

3. 
![[Pasted image 20230510153801.png]]
Solución:
![[Pasted image 20230510153921.png]]

4. ¿Cuál es el tipo Java de esta tabla de símbolos?
![[Pasted image 20230510154648.png]]
![[Pasted image 20230510154903.png]]

5. Dada la siguiente CFG, definir una gramática atribuida para realizar la fase de Identificación. Nota, se puede usar el objeto **st** del ejercicio anterior.
	Una vez que se ha definido la AG, impleméntelo en Java utilizando el patrón de diseño Visitor.
**(G):**
![[Pasted image 20230510155120.png]]
Solución:
**(A):**
|Atributo|Afecta a|Dominio|
|--|--|--|
|definition|variable|VarDefinition|

**(R):**
```java
Nota: las que no se incluyen es porque no requieren nada
(2) IF (!st.put(ID, definition)) print("Variable duplicada")
(7) IF (!st.get(ID)) ERROR("Variable no definida");
	expression.definicion = st.get(ID) //else
```

6. 
![[Pasted image 20230510162041.png]]
**(G):**
![[Pasted image 20230510162117.png]]
**(A):**
|Atributo|Afecta a|Dominio|
|--|--|--|
|type|expression|{int, double, char, error, array}|
**(R):**
```java
//Buena solución: NO USAR INSTANCEOF PARA CADA TIPO
//Usamos el patrón Composite para el tratamiento uniforme de objetos simples y compuestos
(1) expression.type -> expression2.type.arithmetic(expression3.type)
```

7. 
![[Pasted image 20230510163214.png]]
![[Pasted image 20230510163326.png]]
![[Pasted image 20230510163348.png]]
![[Pasted image 20230510163514.png]]
8. 
![[Pasted image 20230510163627.png]]
**(G):**
![[Pasted image 20230510163744.png]]
**(A):**
|Atributo|Afecta a|Dominio|
|--|--|--|
|returnType|statement|type|
**(R):**
```java
(1) statement* -> foreach(statement -> statement.returnType = definition.type.returnType)
(2) expression.mustPromoteTo(statement.returnType)//comprueba si un entero se puede convertir a un double (si promociona)
```

---
# Generación de código

1. Nota: un entero ocupa 2 bytes
![[Pasted image 20230510111746.png]]

2. Dado el siguiente programa de alto nivel:
```java
a = 3;
b = a;
```
Escribir el código destino MAPL.
Suponer que:
- Las direcciones de memoria de a y b son 0 y 2
- Ambas son variables enteras

Solución:
```assembly
PUSHA 0 //meto una direccion
PUSHI 3 //meto un 3 ocupando 2 bytes
STOREI //escribo un 3 ocupando 2 porciones de memoria
PUSHA 2
PUSHA 0
LOADI //va a la dirección 0 y lo deja en el tope de la pila
STOREI
```
3. 
![[Pasted image 20230510171309.png]]
```assembly
//read myInteger;
pusha 0
ini
storei

//real = myInteger * 3.4 -7;
pusha 2
pusha 0
loadi
i2f
mulf
pushi 7
i2f
subf
storef

//write real;
pusha 2
loadf
outf
```

4. (CREO QUE NO ESTÁ BIEN)
![[Pasted image 20230510174139.png]]
![[Pasted image 20230510174326.png]]

5. ==EJ TIPICO EXAMEN==
![[Pasted image 20230510202713.png]]
![[Pasted image 20230510202733.png]]
Solución:
1. Añadir un nuevo método **getNumberOfBytes():int** a todos los tipos
2. Hay dos estrategias para calcular los desplazamientos de los campos de registro:
	1. Iterando el nodo principal a través de los nodos secundarios de RecordField
	2. En los nodos secundarios RecordField, modificando una variable global declarada como un campo en el Visitor
1 para campos y 2 para variables globales
**(R):**
```java
(8) int byteFilesSum = 0;
	for(RecordField field ; fieldSum){
		field.offset = bytes.byteFilesSum += field.type.getNumberOfBytes();
	}
```
3. Desplazamiento de las variables globales:
**(R):**
```java
vardefinition.offset = bytesGlobalSum;
bytesGlobalSum += type.numberOfBytes;
```
4. Implementación es trivial
`---FIN EJERCICIO---`

6. 
![[Pasted image 20230510203936.png]]

7. 
![[Pasted image 20230510204201.png]]
**(R):**
```java
(1) int LocalBytesSum = 0;
	for(VarDefinition vardef : vardefinition*){
		localBytesSum += varedf.type.getNumberOfBytes();
		vardef.offset = -localBytesSum
	}
(3) int paramBytesSum = 0;
	for(int i = vardefinition*.length() - 1; i--){
		vardf.offset = 4 + paramBytesSum;
		paramBytesSym += vardef.type.number();
	}
```

8. AGs para Generación de Código
![[Pasted image 20230510204717.png]]
**(G):**
![[Pasted image 20230510204848.png]]
**(A):**
code
**(R):**
```java
(1) expression.code = "PUSHB" + (int)CHAR_CONSTANT + "\n" 
(2) expression.code = "PUSHI" + INT_CONSTANT + "\n"
(3) expression.code = "PUSHF" + REAL_CONSTANT + "\n"
(4) if (expression.definition.scope == 0)
		expression.code = "PUSHA" + expression.definition.offset + "\n"
	else
		expression.code = "PUSHBP \n" + "PUSHI" + expression.definition.offset + "\n" + "ADDI \n";
	expression.code += "LOAD" + expression.type.getSuffix() + "\n";
(5) expression1.code = expression2.code + expression2.type.convertTo(expression1.type) + expression3.code + expression3.type.convertTo(expression1.type);
	expression1.code += getOperator(expression1.operator);
	expression1.code += expression1.type.suffix() + "\n"
```

9. Ejercicio de contexto:
![[Pasted image 20230510205821.png]]
**(G):**
![[Pasted image 20230510205907.png]]
**(A):**
code y pushValue
**(R):**
```java
(1) expression1.pushValue = false;
	expression2.pushValue = true;
	statement.code = expression1.code + expression2.code + "STOREI \n"
(2) expression.code = "PUSHA" + expression.definition.offset + "\n"
	if(expression.pushValue)
		expression.code += "LOADI \n"
```

10. 
![[Pasted image 20230510212323.png]]
Solución:
![[Pasted image 20230510212525.png]]

11. 
![[Pasted image 20230510213031.png]]
Solucion:
![[Pasted image 20230510213105.png]]
![[Pasted image 20230510213157.png]]
![[Pasted image 20230510213227.png]]
![[Pasted image 20230510213237.png]]

12. 
![[Pasted image 20230510213806.png]]
![[Pasted image 20230510213829.png]]
