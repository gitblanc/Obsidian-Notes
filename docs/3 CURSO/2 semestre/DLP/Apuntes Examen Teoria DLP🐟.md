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

Mirar ejercicios en [[Ejercicios Examen Teoria DLP🐲]]

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

