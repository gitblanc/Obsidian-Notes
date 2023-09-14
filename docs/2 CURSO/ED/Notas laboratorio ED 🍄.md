# Ejemplos de reursividad

- **Caso base**: aquel en que para el método recursivo
- **Caso general**: solución a la recursividad

- Potencias con exponentes enteros:
	 >a^0 = 1 -> caso base
	 a^n = a^(n-1) `*` a (n > 0) (Ejemplo 5^4 = 5^3 * 5, que es el caso general)
- Factorial:
	> 0! = 1
	 n! = (n-1)! * n
- Fibonacci:
	> fib(1) = 0
	 fib(2) = 1
	 fib(n) = fib(n-1) + fib(n-2)

- Es muy importante definir bien el caso base

