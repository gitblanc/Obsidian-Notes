# Ejemplo: El TSP

![](img/Pasted%20image%2020230925181246.png)

- Se usa como algoritmo genético porque es fácil generar soluciones

## Método de resolución del TSP

![](img/Pasted%20image%2020230925181426.png)

## Codificación con permutaciones para el TSP

![](img/Pasted%20image%2020230925181640.png)

- ***La idea de los algoritmos genéticos es***: Hay que trabajar sobre esos códigos, generar unos pocos y después de alguna forma combinarlos

## *Ejemplo de combinación no productiva*

![](img/Pasted%20image%2020230925181803.png)

## *Ejemplo de combinación productiva*

![](img/Pasted%20image%2020230925182005.png)

# Propiedades de la codificación y de los operadores

- Propiedades de los métodos de codificación 
	- Deben ser exhaustivos  
	- Deben permitir operadores eficientes
- Propiedades de los operadores
	- Que produzcan soluciones factibles
	- Que no sean muy costosos computacionalmente
	- Que los hijos hereden características relevantes de los padres
	- Y alguna más . . . .

# Otro ejemplo: ¿Se podría pintar una réplica de Mona Lisa usando sólo polígonos semitransparentes?

![](img/Pasted%20image%2020230925182601.png)

## Mona Lisa Evolutiva

![](img/Pasted%20image%2020230925182954.png)

# ¿Qué es un algoritmo genético?

- Los **Algoritmos Genéticos** son algoritmos de optimización y búsqueda que se basan en los mecanismos de la evolución natural, en particular en la selección natural y la herencia genética.
- Fueron introducidos por John Holland y sus colaboradores en la Universidad de Michigan a principios de los años 70 (Holland 1975. Adaptation in Natural and Artificial Systems).
- Se clasifican dentro de las denominadas metaheurísticas.

# La metáfora evolutiva
## El lenguaje que se usa en los algoritmos genéticos

![](img/Pasted%20image%2020230925183334.png)

## Componentes principales de un algoritmo genético

- Un **esquema de codificación**, por ejemplo cadenas de dígitos binarios (0 y 1).
- Una **función de evaluación** o ==fitness== para evaluar la calidad de los cromosomas.
- Algún método para generar la **población inicial**: aleatorio, heurístico, ...
- Un **conjunto de operadores genéticos**: selección, cruce, mutación, reemplazo, ...
- **Varios parámetros**: probabilidad de cruce, probabilidad de mutación, tamaño de la población, número de generaciones, ...

# Un algoritmo genético convencional

````python
Algoritmo Genético

	Parámetros de entrada (ProbCruce, ProbMutacion, maxGen, PobSize, ... ); 
	numGen <- 0;  
	Inicializar(Pob(0)); // Población inicial  
	Evaluar(Pob(0)); // Función de fitness
	
	while ( numGen < maxGen ) { 
	// Condición de parada numGen <- numGen+1;
	
		Pob’(numGen) = Selección(Pob(numGen-1)); 
		Pob’’(numGen) = Cruce(Pob’(numGen)); 
		Pob’’’(numGen) = Mutación(Pob’’(numGen)); 
		Evaluar(Pob’’’(numGen));
		
		// Selección  
		// Cruce  
		// Mutación  
		// Función de fitness
		
		Pob(numGen) = Reemplazo(Pob’(numGen), Pob’’’(numGen)); // Reemplazo }
	
	return el mejor individuo en Pob(maxGen); 
end
````

- La selección de un cromosoma implica que si hay un cromosoma que tiene 1000 fitness más que otro, va a tener 1000 posibilidades más de ser seleccionado
- La Pob' son los posibles cromosomas a ser seleccionados
- Cruzarlos es recombinarlos (los hijos conforman la Pob'')
- Ahí empiezan a aparecer cromosomas nuevos
- La mutación hace algunos cambios aleatorios (Pob''' es muy parecida a Pob'' pero a algunos cromosomas se les cambió algo)
- Luego se hace un reemplazo 
- Quedarnos con la Pob''' se llama reemplazo incondicional (no hay presión selectiva)
- Se ejerce **presión selectiva** (cuanto más fitness, más fuerte será la presión)
- Un exceso de presión selectiva es malo

![](img/Pasted%20image%2020230925184218.png)

# El esquema de codificación

- Codifica una solución potencial, y el algoritmo de evaluación la debe construir de forma eficiente (en tiempo polinomial)
- Debe tener buena capacidad de representación
    - Al menos de un subconjunto de soluciones buenas
    - A ser posible con una correspondencia de uno a uno
- Debe ser fácil diseñar operadores genéticos que
    - Generen cromosomas factibles
    - Trasladen características relevantes de padres a hijos
    - No sean demasiado costosos computacionalmente
    - Los hijos tengan una “alta” probabilidad de mejorar
- La codificación más habitual es una cadena de símbolos: binaria, permutaciones, vectores de números, ...

# Algunas codificaciones típicas

- Cadenas de dígitos binarios
- Vectores de números reales (Optimización numérica)
	- Optimización de funciones (f:Rn→R)
	- Optimización de parámetros de sistemas físicos
- Permutaciones de símbolos (Optimización combinatoria)
	- Problema del viajante de comercio
		- Una permutación de las ciudades: (5 3 4 1 2)
	- Job Shop Scheduling  
		- Una permutación de las tareas: (1 3 2 4 5)
- Otras estructuras más complejas 
	- Matrices
	- Árboles  
	- Programación Genética
	- . ..

# Algoritmo de decodificación

![](img/Pasted%20image%2020230925185631.png)

- Nos dice cómo el fenotipo se desarrolla en el problema
- Es útil un algoritmo voraz

## Algoritmo de decodificación. Ejemplo con permutaciones

![](img/Pasted%20image%2020230925185744.png)

# El algoritmo Genético Simple (SGA)

- Vamos a detallar el Algoritmo Genético más simple que se puede diseñar: el SGA
	- Codificación binaria (cadenas de bits)
	- Población inicial aleatoria
	- Cruce en un punto
	- Mutación simple
	- Selección proporcional al Fitness (ruleta)
	- Reemplazo generacional con aceptación incondicional (los hijos reemplazan a sus padres)

*El SGA tiene interés especial porque está estudiado formalmente y tiene propiedades que ayudan a entender y a diseñar otras versiones más sofisticadas*

## Codificación binaria

![](img/Pasted%20image%2020230925185954.png)

- Cualquier valor de la variable x es una **solución candidata**
- La propia función de x es el fitness

## Cruce en un punto

![](img/Pasted%20image%2020230925190158.png)

## Mutación simple

![](img/Pasted%20image%2020230925190223.png)

## Selección proporcional al fitness (regla de la ruleta)

![](img/Pasted%20image%2020230925191217.png)

- Lo malo es que hay individuos con fitness mucho mayor al resto y siempre se escogen eso. Por ello, las siguientes generaciones son muy parecidas
- Por ello es necesario que haya variedad de fitness

## Un ejemplo de selección, cruce y mutación

![](img/Pasted%20image%2020230925191245.png)

# Ejemplo de aplicación. Optimización numérica

![](img/Pasted%20image%2020230925192524.png)

# Visualizando el funcionamiento de una AG

![](img/Pasted%20image%2020230925192609.png)

# ¿Por qué un algoritmo como SGA que maneja símbolos de manera ciega puede hacer algo útil?

![](img/Pasted%20image%2020230925192919.png)

- Un esquema es bueno si la media de los cromosomas que pertenecen a ese esquema es alta

# Teorema fundamental de los AGs

- **Teorema de los Esquemas**. Los esquemas de orden bajo, distancia corta y calidad alta aumentan exponencialmente su representación en la población a medida que avanzan las generaciones.

 - **Hipótesis de los Building Blocks**. Un AG obtiene una alta eficiencia gracias a la yuxtaposición de esquemas de orden bajo, distancia baja y calidad alta, denominados “building blocks”.

# Diseño de algoritmos genéticos

- Algunas consideraciones importantes
	- Población inicial
	- Condición de parada 
	- Ajuste de parámetros
	- Convergencia
	- Diversidad del material genético
	- Presión selectiva
	- Disrupción
	- Elitismo
	- . ...

# Convergencia de un AG

![](img/Pasted%20image%2020230925194214.png)

# Una de las claves: Equilibrio entre explotación y exploración

![](img/Pasted%20image%2020230925194326.png)

# AG para el TSP
## Esquema de codificación

![](img/Pasted%20image%2020230925194639.png)

## Operador de cruce

![](img/Pasted%20image%2020230925194713.png)

## Un ejemplo

![](img/Pasted%20image%2020230925194739.png)

- OX: operador basado en el orden

## Mutación, Inicialización y Evaluación

![](img/Pasted%20image%2020230925194825.png)

