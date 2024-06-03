# Generalidades de los algoritmos de búsqueda

![](img/Pasted%20image%2020230911192448.png)

- El árbol de búsqueda crece mucho, siendo uno de los principales problemas
- Con los nodos se va construyendo el árbol de búsqueda
- En cada paso, el algoritmo escoge uno de los nodos hoja, y lo va desarrollando
- Los algoritmos se diferencian en la forma de elegir los nodos hoja que se desarrollarán

![](img/Pasted%20image%2020230911192915.png)

![](img/Pasted%20image%2020230911193211.png)

# Algoritmos de Búsqueda en Árboles

## Best First Search (BFS) para búsqueda a ciegas en árboles

![](img/Pasted%20image%2020230911193317.png)

- Dado un problema y la función heurística de evaluación (da un valor para cada nodo, es decir, lo bueno o malo que es) parte de un único nodo inicial
- **Frontera**: nodos del árbol de búsqueda que se van desarrollando. En cada paso se va extrayendo un nodo de la frontera
- Si no es solución se expande el nodo: a partir de ese nodo se generan tantos hijos como procedan
- Se le conoce como búsqueda en árboles
- **Problema**: En frontier pueden haber nodos diferentes que tengan el mismo estado al ir insertando nodos

### Expansión de nodos

![](img/Pasted%20image%2020230911193452.png)

- Es importante que el número de estados sucesores sea finito

### Ejemplo BFS

![](img/Pasted%20image%2020230911193750.png)

- Es un espacio de búsqueda abstracto
- El grafo presenta 3 soluciones distintas al problema

![](img/Pasted%20image%2020230911193826.png)

(Ver diapositivas para comprender la resolución)
- Está usando recorrido en profundidad

## Casos particulares del Algoritmo General BFS

![](img/Pasted%20image%2020230911194126.png)

- **PATH-COST**: el coste desde un nodo al inicial

# Propiedades de un algoritmo de búsqueda

- Siempre encuentra solución -> búsqueda en anchura
- Siempre encuentra la solución óptima -> coste uniforme
- Coste computacional alto -> búsqueda en profundidad

# Si aplicamos las 3 estrategias

![](img/Pasted%20image%2020230913161747.png)

# Algoritmos de búsqueda no informada

- La diferencia entre búsqueda en grafos y búsqueda en árboles es la gestión de nodos con estados repetidos
    - En búsqueda en grafos, no hay dos nodos con el mismo estado en el árbol de búsqueda. 
    - En búsqueda en árboles, puede haber varios nodos, incluso infinitos, con el mismo estado.
- En búsqueda en grafos, cuando aparece un nodo con un estado repetido debemos quedarnos con el que represente el mejor camino desde el inicial al estado.
- Cuando el espacio de búsqueda es un grafo, se pueden utilizar algoritmos de búsqueda en grafos o en árboles.
- Si el espacio de búsqueda es un árbol, los algoritmos de búsqueda en árboles y en grafos son equivalentes.

# El algoritmo Best First Search

![](img/Pasted%20image%2020230913162226.png)

![](img/Pasted%20image%2020230913162247.png)

- La N mayuscula se refiere al nodo. El nodo N contiene al estado n

![](img/Pasted%20image%2020230913163330.png)

- El N5' es mejor que el N5 porque representa un camino mejor
- Lo mejor sería eliminar la rama N2 - N5, pero eso es muy costoso

# Problema del viajante de comercio (TSP)

![](img/Pasted%20image%2020230913164340.png)

- **Camino Hamiltoniano**: una vez pase por una ciudad, no vuelva a pasar por ella

## Paso 1: Definir Espacio de búsqueda

![](img/Pasted%20image%2020230913164413.png)

![](img/Pasted%20image%2020230913164435.png)

# Otros algoritmos de Búsqueda Heurística

![](img/Pasted%20image%2020231002181105.png)

## Algoritmos e-admisibles

![](img/Pasted%20image%2020231002181239.png)

## Algoritmos no admisibles

![](img/Pasted%20image%2020231002181432.png)

## Algoritmos de búsqueda heurística en árboles

![](img/Pasted%20image%2020231002182803.png)

---


