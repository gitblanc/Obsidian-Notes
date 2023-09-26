# Lab 1
## Introducción

- En esta nota se expondrán diversas notas tomadas en los laboratorios de Estructuras de Datos
## Ejemplos de recursividad

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

## Iterativo vs. Recursivo

- Iterativo: `5^4 = 5 * 5 * 5 * 5`
- Recursivo:
	- `5^4 = 5^3 * 5`
	- `5^3 = 5^2 * 5`
	- `5^2 = 5 * 5`
	- ...

# Lab 2
## Introspección

- **Introspección**: La vamos a usar para mediciones de tiempos. Consiste en que un programa es capaz de mirar el código y la clase que tiene que ejecutar sin saberla a priori, pudiendo modificar el comportamiento de una clase en tiempo de ejecución
	- Por *n* algoritmos que tengamos, vamos a realizar *n* tests

## ¿Por qué declaramos un método como *static*?

- Declaramos un método como *static* para no tener que instanciar la clase

## Notas de interés para la entrega

- Hacer gráficos para: linear, quadratic, cubic, logarithmic y las 4 recursivePow
- Los gráficos tienen que tener título, nombres en los ejes y leyenda
- Número para lanzar: carga 1-10 mínimo, 5 veces cada uno de ellos por cada carga de trabajo: 5-1-10

````java
public class TestBench {

	// className: Nombre clase
	// methodName:Nombre mÃ©todo
	// n: parÃ¡metro que pasamos al mÃ©todo (carga de trabajo)
	public static Object testAlgorithm(String className, String methodName, int n) {
		try {
			Object obj = Class.forName(className).getDeclaredConstructor().newInstance();
			Method method = obj.getClass().getMethod(methodName, int.class);
			return method.invoke(obj, n);
		} catch (Exception e) {
			System.out.println(e.getMessage());
			e.printStackTrace();
		}
		return null;
	}

	// CronÃ³metro
	public static void test(String output, int times, int startN, int endN, String className, String methodName)
			throws IOException {
		FileWriter file = null;
		PrintWriter pw;
		try {
			file = new FileWriter(output);
			pw = new PrintWriter(file);
			for (int workLoad = startN; workLoad < endN; workLoad++) {
				long startTime = System.currentTimeMillis();

				for (int time = 0; time < times; time++)
					testAlgorithm(className, methodName, workLoad);

				long finalTime = System.currentTimeMillis();
				long timeResult = ((finalTime - startTime) / times);
				
				pw.println(workLoad + ";" + timeResult);
			}
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			if (file != null)
				file.close();
		}
	}
````