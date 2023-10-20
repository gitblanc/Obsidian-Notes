# Seminario 1

## Ejemplo 1. Factorial

|n|Condición `n==0?`|n * factorial (n-1)|
|---|---|---|
|5|NO|5 * fact(4)|
|4|NO|4 * fact(3)|
|3|NO|3 * fact(2)|
|2|NO|2 * fact(1)|
|1|NO|1 * fact(0)|
|0|SI|Devuelve 1|

````java
if(n==0) return 1
else{
	f = n*factorial(n-1);
	return f;
}

//Este devuelve siempre el último (1)
`````

## Ejemplo 2. Suma de dos enteros

````java
public int suma(int a, int b){
	if(b == 0) return a;
	if(b>0) return 1 + suma(a, b-1);
}
````

|a,b|Condición `b==0?`|1 + suma(1,b-1)|
|---|---|---|
|2,5|NO|1 + suma(2, 4)|
|2,4|NO|1 + suma(2, 3)|
|2,3|NO|1 + suma(2, 2)|
|2,2|NO|1 + suma(2, 1)|
|2,1|NO|1 + suma(2, 0)|
|2,0|SI|Devuelve 2|

## Ejemplo 3. Resto de una división

````java
public int resto(int a, int b){
	if(a-b < 0) return a;
	if(a-b >= 0) return resto(a-b, b);
}
````

## Ejemplo 4. Sumatorio de un vector

````java
public int sumaVector(int[] vector, int n){
	if(n==0) return vector[0];
	else return vector[n] + sumaVector(vector, n-1)
}
````

# Seminario 2

## Ejercicio grafos

![](./img/Pasted%20image%2020231006194328.png)

## Ejercicio Dijkstra

![](./img/Pasted%20image%2020231006194404.png)

![](./img/Pasted%20image%2020231006195200.png)

# Seminario 3

## Ejercicio Prim

![](./img/Pasted%20image%2020231020193415.png)

## Ejercicios Recorrido Profundidad

![](./img/Pasted%20image%2020231020194437.png)

![](./img/Pasted%20image%2020231020195200.png)

![](./img/Pasted%20image%2020231020200103.png)