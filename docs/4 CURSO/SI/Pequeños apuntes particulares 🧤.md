# Búsqueda heurística
## Instrucciones para definir un espacio de búsqueda

1. Definir los estados
2. Definir las reglas para, a partir de un estado, generar más
3. Definir los costes de pasar de uno a otro
4. Definir cómo vamos a reconocer el estado inicial
5. Definir cómo vamos a reconocer el estado final

## Definición de heurístico

- ***Heurístico***: función que aproxima siempre por debajo, el coste desde el estado en el que estamos hasta el estado final. Si el heurístico se pasa, no sería admisible.

![](./img/Pasted%20image%2020231013110450.png)

## Propiedades de un heurístico

- Debe estar bien **construido**/**definido**
	- h(n) >= 0 para cualquier nodo
	- h(n) = 0 en los nodos objetivo
- Ha de ser **admisible**
	- h(n) <= h* para todo n
	- *Pequeño truco: sabemos el coste óptimo desde un principio, porque es un problema pequeño*
	- *Si el heurístico no fuese admisible, no se puede garantizar que siempre nos lleve a la solución óptima*
- Ha de ser **monótono**/**consistente**(si hay varios costes diferentes entre caminos)
	- h(n1) <= h(n2) + C(n1, n2) para todo n1,n2
	- *C(n1, n2) es el coste de ir del nodo 1 al nodo 2*

## Heurístico más informado

- El heurístico más informado es quel que:
	- h(n) <= h* (lo más cerca posible)

## ¿Cómo construir un heurístico?

- Aplicando el **método de la relajación del problema**
	- Consiste en hacerse un listado de las condiciones que me indican en el problema y quitar una o varias de ellas

## Condición de expansión

- `h(n) + g*(n) <= C*`, cumple la condición **necesaria pero no suficiente** para que se pueda expandir
- `h(n) + g*(n) < C*`, cumple la condición **suficiente** de expansión

- La función que decide si un nodo se expande: `f(n) = g*(n) + h(n)`

## Resumen Condición de expansión

- Si `h(n) + g*(n) > C*` *NO SE EXPANDE*
- Si `h(n) + g*(n) <= C*` *IGUAL SE EXPANDE*
- Si `h(n) + g*(n) < C*` *SE EXPANDE SEGURO*

# Algoritmos Genéticos

## Conceptos

- Los algoritmos genéticos se basan en permutaciones

> (1 2 3 4 5)

- **Variaciones**: Influye el orden (1 2 3) (2 3 4)
- **Combinaciones**: No influye el orden (2 5 3) (5 1 3)
- **Permutaciones**: todas las posibles combinaciones

## Fases de un algoritmo genético

1. Encontrar una codificación
2. Generar una población inicial
3. Encontrar un mecanismo para obtener nuevas soluciones
4. Necesitamos una función de evaluación
5. Hay que tener un criterio de selección

## Ejemplos de cruce

![](./img/Pasted%20image%2020231013113215.png)

- Genero un nuevo cromosoma cogiendo parte del primero y el resto **en orden** del otro

![](./img/Pasted%20image%2020231013113230.png)

- Este coge aleatoriamente elementos de uno y de otro y los va mezclando

- *Nota: es mejor el 0x1 porque si ya tenemos una solución no la perdemos en el cromosoma hijo*

## Ejemplos de mutación

![](./img/Pasted%20image%2020231013113608.png)

## Teoría de los Esquemas

- **Longitud:** distancia desde el primer símbolo fijo hasta el último

![](./img/Pasted%20image%2020231013114233.png)

- Para contar el número de asteriscos, hay que contar el número por la izquierda y por la derecha hasta encontrar un número

## Convergencia, exploración y explotación

- **Convergencia**: velocidad en la que el algoritmo genético se acerca a la solución óptima. Se espera que un algoritmo converja lo antes posible
- **Exploración**: mete mucha búsqueda de azar
- **Explotación**: se trabaja sobre un grupo con una buena tendencia a ser solución.
	- Problema: estancamiento de soluciones (*problema de los máximos*)

![](./img/Pasted%20image%2020231013114640.png)


# Posibles preguntas de teoría extra

1. **¿Cuáles son las dos principales consecuencias que tienen los heurísticos consistentes en el comportamiento del algoritmo A*?**

	- Si un heurístico h es consistente o monótono, entonces h es admisible, lo que se traduce en que el algoritmo A* es admisible y en consecuencia siempre encuentra la solución óptima
	- Si un heurístico h es consistente o monótono, entonces cuando el algoritmo A* que lo usa elige un nodo n para ser expandido, ocurre que g(n) = g*(n). Esto se traduce en que no hay que rectificar el camino desde el inicial hasta n o bien reexpandir n, y de esa forma la búsqueda será más eficiente

2. **Explica el cometido del operador de selección en un algoritmo genético y explica qué influencia podría tener en el fenómeno de convergencia prematura. Pon algún ejemplo de operador de selección que conozcas.**

El operador de selección es el encargado de elegir los cromosomas de la población actual que van a ser cruzados para dar lugar a nuevos cromosomas hijos. Un ejemplo es el operador de torneo, que elige a un determinado número de cromosomas aleatorio y de entre ellos selecciona al mejor de todos.
El operador de selección tiene un gran influencia en en el fenómeno de convergencia prematura, ya que si siempre elige a los mejores cromosomas de la población, la diversidad genética caería rápidamente y la evolución de la población se estancaría muy pronto, dando lugar a dicho fenómeno.

3. **En un paso intermedio de la ejecución de un algoritmo A* que emplea un heurístico admisible h, ABIERTA contiene un nodo n tal que, en ese momento, f(n) > C*. ¿Podemos asegurar que el nodo n no se va a expandir?**

No podemos asegurar que el nodo n no se va a expandir. El motivo es que n se podría rectificar en etapas posteriores de la búsqueda, haciendo que g(n) se reduzca y que f(n) = g(n) + h(n) <= C* por lo que el nodo n se podría expandir, al ser h un heurístico admisible.
