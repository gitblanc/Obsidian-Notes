# Seminario 1

## Ejercicio

Especificación:
- Un programa lee tres números cuyos valores son interpretados de forma que representan las longitudes de los lados de un triángulo  
- En la salida muestra un mensaje para cada triángulo: "escaleno", "isosceles" o "equilatero" (en minúsuculas y sin acentos ni comillas) o "error" en cualquier otro caso.  

Tarea a realizar en la clase de seminario:
- Escribir el conjunto de casos de prueba que se consideren adecuados para probar este programa
### Mi solución
Pruebas a realizar:

|Entrada|Salida|
|--|--|
|Cadena vacía -> ""|"error"|
|null|"error"|
|Cadena -> "hola"|"error"|
|Un número negativo y dos bien -> -1,2,2|"error"|
|Dos números negativos y uno bien -> -1,-1,2|"error"|
|Tres números negativos -> -1,-1,-1|"error"|
|Un cero y dos números bien -> 0,2,2|"error"|
|Dos ceros y un número bien -> 0,0,2|"error"|
|Tres ceros -> 0,0,0|"error"|
|Ningún lado igual -> 1,3,2|"escaleno"|
|Dos lados iguales -> 1,2,2|"isosceles"|
|Tres lados iguales -> 2,2,2|"equilatero"|

# Seminario 2

## Condiciones de entrada o prueba del ejercicio del triángulo

- Número de entradas
	- 1 entrada
	- 2 entradas
	- 3 entradas
	- más entradas
- Tipo del lado
	- número
	- entero
	- real
	- no número
- tipo del lado 2
- tipo del lado 3
- longitud del lado 1
	- <0
	- >0
	- =0
- longitud del lado 2
- longitud del lado 3
- tipo de lado del triángulo
	- isósceles
	- escaleno
	- equilátero
	- error
- número de lados iguales
	- 3
	- 2
	- ninguno
- relación entre los lados
	- todos son iguales
	- 2 son iguales
	- ninguno es igual
	- no forman un triángulo
		- línea
		- figura abierta
