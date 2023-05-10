
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

COMMENT: '#'.*? '\n' -> Skip;

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


---

# Semántico

1. 
![[Pasted image 20230510111647.png]]

# Generación de código

1. Nota: un entero ocupa 2 bytes
![[Pasted image 20230510111746.png]]