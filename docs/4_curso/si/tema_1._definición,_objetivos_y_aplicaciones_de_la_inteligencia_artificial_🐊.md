# Introducción

- [Enlace de interés sobre inteligencia artificial](https://planderecuperacion.gob.es/noticias/que-es-inteligencia-artificial-ia-prtr)

- La **inteligencia artificial** (IA) es un campo de la informática que se enfoca en crear sistemas que puedan realizar **tareas que normalmente requieren inteligencia humana**, como el aprendizaje, el razonamiento y la percepción.
- Lectura recomendable: [Artificial Intelligence: A Modern Approach, 4th US ed.](https://aima.cs.berkeley.edu/)

# Bloques

- Búsqueda de conocimiento
- Representación de dicho conocimiento
- Aprendizaje automático

# Parte 1: Búsqueda

## Objetivos

1. Conocer los fundamentos de los algoritmos de búsqueda y el papel que juegan en la Inteligencia Artificial
2. Conocer el paradigma de Búsqueda en Espacios de Estados y los algoritmos básicos de búsqueda a ciegas y sobre todo de búsqueda inteligente o heurística
3. Conocer otros paradigmas de búsqueda como los Algoritmos Genéticos y otras Metaheurísticas
4. Saber cómo modelar problemas para resolverlos con Algoritmos de Búsqueda, en particular cómo introducir conocimiento específico del dominio del problema

## Introducción y Modelado de Espacios de Búsqueda

- Un espacio de búsqueda hace referencia o es lo mismo que un grafo
- El núcleo de un sistema inteligente es un algoritmo de búsqueda
- Un ***espacio de búsqueda*** representa las distintas formas de resolver el problema
- Un ***algoritmo de búsqueda*** trata de encontrar la mejor solución del espacio de búsqueda

## Ejemplo: Robot en un Mundo de Bloques

### Definición del problema

![](Pasted%20image%2020230911185326.png)

El objetivo es encontrar una secuencia mínima de acciones del robot que partiendo de la situación inicial nos permitan llegar a la situación objetivo, para ello es necesario
- Conocer lo que el agente (el robot) es capaz de entender, es decir el nivel de detalle de las acciones  
- Y definir un modelo de representación de las situaciones (estados) coherente con este nivel de detalle

## Modelado de Estados

![](Pasted%20image%2020230911185620.png)

• En este caso, la descripción de los estados se puede hacer instanciando adecuadamente los siguientes predicados

SobreLaMesa(X) ;; El bloque X está sobre la mesa  
Sobre(X,Y) ;; El bloque X está sobre el bloque Y 
Libre(X) ;; El bloque X no tiene otro bloque encima
Cogido(X)  ;; El robot tiene cogido el bloque X
ManoLibre ;; La mano del robot está libre

## Modelado de acciones

- Lo negro, rojo y verde son reglas de producción:
	- **P**: condiciones a cumplir (si se cumplen, se puede llevar a cabo la regla)
	- **E**: consecuente - resultado

![](Pasted%20image%2020230911185907.png)

## Espacio de búsqueda para la instancia definida por la situación inicial anterior

![](Pasted%20image%2020230911190204.png)

- Se entiende que todos los predicados que no están instanciados están puestos a FALSE
- Con esto tenemos definido el espacio de búsqueda
- Ahora toca buscar una solución (camino más corto del nodo actual a un nodo objetivo)

## Algoritmos de búsqueda adecuados al espacio anterior

- El espacio anterior tiene forma de grafo dirigido simple con costes positivos. En consecuencia, cualquier algoritmo de búsqueda en grafos que permita encontrar un camino entre el estado inicial y uno de los objetivos puede ser de utilidad
- Ejemplos:
    -  Búsqueda primero en anchura 
    -  Búsqueda primero en profundidad
    - Algoritmo de Dijsktra - Backtracking
- Estos son “algoritmos de búsqueda a ciegas” ya que no utilizan información sobre el dominio del problema
- Existen otras opciones, los “algoritmos de búsqueda heurística o búsqueda inteligente” que sí pueden utilizar información específica del problema para mejorar el proceso de búsqueda de soluciones

## Definiciones asociadas a Espacio de búsqueda

- El ***espacio de búsqueda*** es un grafo simple dirigido con arcos etiquetados con costes positivos
- **Nodos**: estados que representan subproblemas
    - 1 estado inicial
    - 1 ó más estados objetivo
- **Arcos**: representan acciones elementales, operadores o reglas
    - Permiten pasar de un estado n1 a un estado sucesor n2
    - Tienen asociado un coste no negativo c(n1, accion, n2) ó c(n1, n2)
- **Solución del problema**
    - Es cualquier camino desde el estado inicial a uno de los estados objetivo
    - El coste de la solución es la suma de los costes de los arcos del camino

## Características de un Espacio de Búsqueda

- Es un modelo simplificado del problema  
	- El nivel de detalle depende de las capacidades del agente que tiene que ejecutar las acciones
- No tiene que estar almacenado en una estructura, se genera a partir de las operaciones
	- EstadoInicial() ;; Genera un nodo con el estado inicial  
	- Sucesores(n) ;; Calcula la lista de sucesores de un estado n, con los costes correspondientes
	- EsObjetivo(n)  ;; Comprueba si un estado es o no objetivo
- En general es finito, pero puede no serlo
- **Los estados son distintos, no hay estados repetidos**
- Suponemos entornos simples
    - Estados totalmente observables y discretos (no continuos)
    - Acciones deterministas
- **El Espacio de Búsqueda es independiente del Algoritmo de Búsqueda**


# Problema: Cálculo de rutas óptimas

## Espacio de búsqueda

![](Pasted%20image%2020230911191637.png)

# Problema: El problema del 8-puzzle

## Espacio de búsqueda

![](Pasted%20image%2020230911192003.png)
  
- Hay un total de !9 combinaciones

