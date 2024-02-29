## Ejercicio: ¿Cómo calcularías el mínimos de 3 números?

````c
// Es una forma más declarativa que simplemente hacer varios if/else
// También tiene un mayor nivel de abstracción
return Arrays.sort({a, b, c})[0];
````

# Tema 1. Paradigmas de programación

## Declarativo vs Imperativo

- Lo **declarativo** es de más alto nivel (qué quiero obtener pero sin especificar el cómo), mientras que **imperativo** es de más bajo nivel (qué quiero obtener especificando el cómo)

## Paradigmas

- **No estructurado**: hay saltos en cualquier sitio del código. Difícil de entender y mantener
- **Estructurado basado en procedimientos**
- **Orientado a objetos**
- **Funcional**: los datos manejados son inmutables (a diferencia de el POO, ej: un setter que modifica un objeto)
- **Lógico**

## Tecnología de la Programación

- `C#` es un lenguaje multiparadigma

# Tema 2. Paradigma Orientado a Objetos

- **Encapsulamiento**: ocultación de la información

## Propiedades

- Sintaxis para realizar los getters y los setters
- Permiten acceder al estado de los objetos como si de atributos se tratase
- Las propiedades son **azúcar sintáctico**

## Acoplamiento y Cohesión

- **Acoplamiento**: nivel de interdependencia entre módulos
- **Cohesión**: uniformidad entre las responsabilidades de un módulo (fácil entendimiento)

## Herencia vs polimorfismo vs enlace dinámico

- **Herencia**: mecanismo de reutilización de código por el cual una clase hija extiende y comparte el comportamiento de una clase más general. 
- **Polimorfismo**: En la clase hija se puede modificar o ampliar el comportamiento de la clase padre
- **Enlace dinámico**: la redefinición de la implementación de un método en una clase hija que hereda de la clase padre

## Asertos

- Excepciones que se deben cumplir para que la ejecución del programa sea correcta

````cs
# if DEBUG
...
#else
...
#endif
````

## Ejercicio Diseño Reloj

![Créditos a Dani](./img/Pasted%20image%2020240208154910.png)

## Genericidad

- Usar `<T>`, lo que se conoce como **variable de tipo**

### Genericidad acotada

![](./img/Pasted%20image%2020240208160029.png)

La diferencia es que en el primero el T pueden ser de la clase Personas y además esas Personas han de implementar la interfaz IComparable, mientras que en el segundo, el vector está compuesto exclusivamente de IComparable.

En la segunda versión, sólo tenemos los métodos de IComparable, mientras que en la primera podemos invocar cualquier método del tipo:

````cs
// Supón la clase Persona, con Edad, Nombre...
//Caso 1
Puedes llamar a -> v[0].getEdad, v[0].getNombre()...
//Caso 2
Puedes llamar a -> v[0].compareTo(...) exclusivamente
````

# Paradigma funcional

- El tipo de una función es su tipo de retorno + el tipo de sus parámetros

## Expresiones Lambda

- `λx.M` (x son los parámetros y M es el retorno)

## Reducción ß

`(λx.M)N` -> `M[x:=N]`

- Para `(λx.x+x)(3)`
	- M es lo que va dentro de la función (x+x)
	- N es el valor que va a recibir (3)

- Ejemplo de **retorno**:
	- Se devuelve un resultado `(λx.x+x)3` -> `3+3`
	- Se devuelve otra función:`(λx.x)λy.y*2` -> `λy.y*2`

## Conversión α

- Calcular el doble del doble de n: `(λf.(λx.f(fx)) (λx.x+x)n` -> `(λf.(λx.(λy.y+y) ((λy.y+y)x)n` -> `(λx.(λy.y+y) ((λz.z+z)x)n` -> `(λy.y+y) ((λz.z+z)x)n` -> `((λz.z+z)n) ((λz.z+z)x)n` -> `(n+n) + (λx.x+x)n)` -> `(n+n)+(n+n)`


# Tipos delegados predefinidos

- `Func<T>` o `Func<T1,T2>`: siempre devuelve algo (no tiene por qué tener parámetros)
- `Action` o `Action<T>`: método que no devuelve nunca nada (puede tener o no parámetros)
- `Predicate<T>`: método que retorna un `bool` y recibe un `T`

# Expresiones Lambda

![](./img/Pasted%20image%2020240222153315.png)

```cs
IDictionary > calculadoraFuncional = new Dictionary>(); calculadoraFuncional["add"] = (op1, op2) => op1 + op2; calculadoraFuncional["sub"] = (op1, op2) => op1 - op2; calculadoraFuncional["mul"] = (op1, op2) => op1 * op2; calculadoraFuncional["div"] = (op1, op2) => op1 / op2; calculadoraFuncional[“add"](3, 4); // 7 
IList> condiciones = new List>(); 
condiciones.Add(s => s.Length < 5); 
condiciones.Add(s => !s.StartsWith("F")); 
condiciones.Add(s => s.EndsWith(“i")); string str = “Hi"; 
foreach (var cond in condiciones) { if (!cond(str)) {…} }
```

# Bucles y Recursividad

![](./img/Pasted%20image%2020240222155753.png)

![](./img/Pasted%20image%2020240222160334.png)

## Combinador de Punto Fijo

![](./img/Pasted%20image%2020240222160542.png)

![](./img/Pasted%20image%2020240222160601.png)

# Currificación

![](./img/Pasted%20image%2020240222164215.png)

![](./img/Pasted%20image%2020240222164648.png)

# Aplicación parcial

![](./img/Pasted%20image%2020240222164929.png)

# Transparencia referencial

- Si un lenguaje ofrece clausuras, ¿puede ofrecer transparencia referencial?
	- Si

# Memoización

- Si una expresión posee trasparencia referencial, se puede optimizar mediante memoización
	- La primera vez que se invoca, se guarda en una caché

```cs
static class FibonacciMemoizacion {
	private static IDictionary<int, int> valores = new Dictionary<int, int>();
	internal static int Fibonacci(int n) {
		if (valores.Keys.Contains(n))
			return valores[n];
		int valor = n <= 2 ? 1 : Fibonacci(n - 2) + Fibonacci(n - 1);
		valores.Add(n, valor);
		return valor;
	}
}
```

- Tiene como ventaja ahorrar secuencias de fibonacci previamente calculadas

```python
eval("10 + 20")
# returns 30
```

