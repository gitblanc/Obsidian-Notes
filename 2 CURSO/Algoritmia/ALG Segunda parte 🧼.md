# 22 Marzo 2022 馃拡
---
## Programaci贸n din谩mica
- Tenemos un array donde guardamos resultados intermedios para calcular el resultado final.
- Es un m茅todo iterativo, cuyo origen es una funci贸n recursiva. Sustituimos las llamadas recursiva por accesos a las posiciones del array.
![[funcion recursiva.png|300]]
- Se repiten operaciones, por tanto se guardan las calculadas en un array para no recalcularlas varias veces.
---
## Problema del cambio
![[problema cambio.jpeg]]
Lo que no se ve son 10 c茅ntimos :-)
- Buscar el m铆nimo para no pasarse, usando la moneda de la iteraci贸n o de iteraciones anteriores.
---
## Backtracking
- **Problema de las 8 reinas:** colocar 8 reinas en un tablero sin que se coman.
- **Backtracking** explora el grafo, va desarrollando estados hasta que encuentra una soluci贸n. Es un *algoritmo de fuerza bruta*, puesto que lo que hace es desarrollar estados de forma r谩pida hasta encontrar una soluci贸n.
- T茅cnica ineficiente, con complejidades exponenciales.
![[recorrido en profundidad.png]]
- **Grafo impl铆cito:** grafo que se desarrolla a medida que se va recorriendo. Ahorra tiempo de ejecuci贸n y espacio en memoria.
![[grafo implicito.png]]

#### Esquema Backtracking
```java
 

public static void backtracking(Estado e) {

	if (e.esSolucion()) { System.out.println(e); haySolucion= true;

	}  
	else {

		Estado estadoHijo= null; 
		while(e.hasNextHijos() && !haySolucion) {
		// siguiente estado hijo va虂lido 
			estadoHijo= e.nextHijo(); 
			
			if (estadoHijo!=null) // puede que no queden hijos va虂lidos backtracking(estadoHijo);
		}


} }
```
---
# 29 Marzo 2022 馃椏
---
- Backtracking busca todas las soluciones posibles.
- Tambi茅n se puede buscar la soluci贸n 贸ptima.
---
## Poda de nodos
- Consiste en establecer una condici贸n que impida seguir desarrollando nodos aunque sean v谩lidos.
- Se aplica cuando tenemos que buscar una soluci贸n 贸ptima.
- Backtracking tiene complejidad explonencial.
---
### Ejercicio formar palabras a partir de un conjunto de letras
![[formar palabras planteo.png]]
![[formar palabras.png]]
```java
 public static void backtracking (int nivel) {

	if (nivel==m) //hay ya una palabra completa {

		mostrarSolucion();

		cont++; 
	}

	else  {
		for (int i=0;i<n;i++){

			if (!marca[i]) {

				sol[nivel] =vLetras[i]; 
				marca[i]=true; 
				backtracking(nivel+1); 
				marca[i]=false;
			}
		}
	}

}
```
---
### Problema de la asignaci贸n de tareas a agentes
![[tareas agentes.png]]
![[tareas agente res.png]]
```java
 static void backtracking (int nivel) {  
	if (nivel==n) { //hay ya una asignacio虂n completa

		if (coste<costeMejor) { 
			for (int k=0;k<n;k++){
				 asigMejor[k]=asig[k];
			costeMejor=coste; 
			}
		} }

	else {  
		for (int i=0;i<n;i++){

			if (!marca[i] && coste<costeMejor ) //ostemMejor->poda
				asig[nivel]=i;
				coste=coste+w[nivel][i]; 
			    marca[i]=true; 
			    backtracking(nivel+1); 
			    coste=coste-w[nivel][i]; 
				marca[i]=false;
		}

	} 
}
```
- Se podr铆a hacer una poda (costemejor).
---
# 5 Abril 2022 馃數
---
- Aplicamos la poda en los problemas de optimizaci贸n.
### Problema del salto del caballo
```java
 static void backtracking (int salto,int x,int y) {  
	if (salto==n*n+1) { // ya acabo虂 de recorrer tablero

	seEncontro=true;

	mostrarSolucion(); }

	else  
		for (int k=0;k<=7;k++) {

			int u=x+h[k]; // nueva posicio虂n 
			int v=y+v[k];

		if (!seEncontro &&  
			u>=0 && u<=n-1 && v>=0 && v<=n-1 && // dentro tablero       
			tab[u][v]==0) { // casilla no utilizada
			tab[u][v]=salto; 
			backtracking (salto+1,u,v); 
			tab[u][v]=0;

}

} }

```
---
# Tema 7, Ramificaci贸n y poda 馃攰
---
- No hace falta tener una asignaci贸n secuencial.
- Backtracking es recursivo, mientras que poda es iterativo.
```java
 public void realizarAnchura(Estado e) {

	Cola cola= new Cola(); // Cola FIFO (1o en entrar --> 1o en salir) 
	boolean haySolucion= false; // Para buscar la primera solucio虂n Estado actual; 
	Estado actual;

	cola.insertar(e); // mete estado e en la cola 
	while (!cola.esVacia() && !haySolucion)  {

		actual= cola.extraer();  
		// Examinar todos los hijos del estado actual 
		for (Estado estadoHijo : actual.expandir())  {

			if (estadoHijo.esSolucion()) 
				haySolucion= true;

			else
				 cola.insertar(estadoHijo);
		}

} }
```
Diferencias de poda con backtracking:
- Desarrollo de los nodos en anchura.
- Aplicamos heuristico para seleccionar cu谩l de ellos vamos a desarrollar.

![[ramificacion.png|500]]

![[ramifica asignacion.png|500]]
MALA FORMA, sirve para hallar una soluci贸n. Para hallar la soluci贸n 贸ptima es malo.

![[ramifica asignacion good.png|500]]

---
# 19 Abril 2022 鈴?
---
- El heur铆stico de ramificaci贸n permite saber los nodos que llevan a la soluci贸n final
- El heur铆stico de poda permite ir eliminando aquellos nodos que superen la cota.
![[nreinas.png||500]]