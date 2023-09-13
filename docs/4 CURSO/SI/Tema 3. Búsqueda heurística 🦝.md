- Se refiere a lo contrario de búsqueda a ciegas
- Los algoritmos de búsqueda heurística se fijan en lo que representan los estados y van a definir las funciones f en función del contenido de esos estados.

# Introducción

- **Heurístico**: estrategia de resolución de problemas que usa conocimiento específico sobre esos problemas

![](./img/Pasted%20image%2020230913170317.png)

## Clases de problemas

### P
- Problemas fáciles, que se resuelven con algoritmos de complejidad polinomial
### NP
- Son problemas no deterministas polinomiales, es decir, si nos dan una solución, podemos determinar en tiempo polinomial el coste de dicha solución
### NP-duros y NP-completos
- Nadie encontró un algoritmo polinomial que los resuelva de forma exacta. Son difíciles de resolver

# El algoritmo A*

![](./img/Pasted%20image%2020230913171154.png)

- La función h la tenemos que definir nosotros
- g*(inicial) = 0, por ello: f*(inicial) = h*(inicial)
- g(n) es una función que se define en los nodos que vamos encontrando con valor n.PATH-COST
- h(n) es el heurístico donde dado un nodo nos dé una estimación de lo que va a costar hacer la solución con dicho nodo

## Ejemplos de herurísticos

![](./img/Pasted%20image%2020230913171222.png)

## Propiedades de la función h importantes a recordar

- Una **h bien definida** ha de cumplir: 
	- h(n) >= 0 para todo n
	- h(obj) = 0 (h para cualquier objetivo es 0)
- Un heurístico es **admisible** si:
	- h(n) <= h*(n) para todo n
	- La consecuencia es que A*(h) es admisible (**admisibilidad**)
	- Una h que vale siempre es aquel que h(n) = 0
- Si tenemos dos heurísticos para el mismo problema que cumplen:
	- h1(n) <= h2(n) <= h*(n) para todo n
	- h2 domina o está más informado que h1 porque está más cerca de h* (**dominancia**)
	- Resulta que A*(h2) expande menos nodos que A*(h1)
- **Monotonía o consistencia**:
![](./img/Pasted%20image%2020230913174646.png)


---