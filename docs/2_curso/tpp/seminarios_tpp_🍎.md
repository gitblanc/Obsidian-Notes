# Seminario 1. Polimorfismo y Enlace Dinámico

## Ejercicio 1

![](Pasted%20image%2020240202191146.png)

![](Pasted%20image%2020240202191207.png)

````cs
public class Person implements Comparable{
	public uint CompareTo(Object obj){
		if(obj as Person){
			if(this.Surname1.CompareTo(obj.Surname1) == 0){
				if(this.Surname2.CompareTo(obj.Surname2) == 0){
					if(this.Name.CompareTo(obj.Name) == 0)
						return 0;
					else if(this.Name.CompareTo(obj.Name) == 1)
						return -1;
					else
						return 1;
				}
			}
		}
		throw IllegalArgumentException();
	}
}

public class Main{

	void Sort(Comparable[] vector) { 
		for (int i=0; i < vector.Length; j-‐-‐) 
			if (vector[i] > vector[j]) { 
			int temp = vector[i]; 
			vector[i] = vector[j]; 
			vector[j] = temp; 
			} 
		}
	}
}
````

## Ejercicio 2

![](Pasted%20image%2020240202193709.png)

````cs
void Sort(Comparable[] vector, Comparador c) { 
		for (int i=0; i < vector.Length; j-‐-‐) 
			if (vector[i] > vector[j]) { 
			int temp = vector[i]; 
			vector[i] = vector[j]; 
			vector[j] = temp; 
			} 
		}
	}

public interface Comparador{
	//No usamos objetos Comparable porque no vamos a usar el CompareTo
	public uint Compara(Object obj1, Object obj2);
}

public class ComparadorNIF implements Comparador{
	public override uint Compara(Object obj1, Object obj2){
		if(obj1 as Person && obj2 as Person){
			return obj1.NIF.CompareTo(obj2.NIF);
		}
		throw IllegalArgumentException();
	}

}
````

# Seminario 2. Genericidad

## Ejercicio 1

````cs
public interface IComparable<T> 
{
	int CompareTo(T obj);
}

//Genericidad acotada (el where)
void Sort<T>(T[] vector) where T : IComparable<T>
{
	...
}
````

## Ejercicio 2

````cs
public interface IIgualado<T>
{
	bool Equals(T o);
}

//Genericidad acotada (el where)
int IndexOf<T>(T[] vector, T obj) where T : IIgualado<T>
{
	foreach...
		elem.Equals(o);
		return i;
}
````

# Seminario 3. Cálculo lambda

- Recordatorio de cálculo Lambda

![](Pasted%20image%2020240301170956.png)

- Lenguaje universal:

![](Pasted%20image%2020240301171026.png)

- Lógica  booleana:

![](Pasted%20image%2020240301171053.png)

- Representan dos funciones que reciben dos parámetros y devuelven una función
	- **true** devuelve el primer parámetro
	- **false** devuelve el segundo parámetro

```cs
true (3) (4) -> 3
false (3) (4) -> 4
```

## Ejercicio 1

![](Pasted%20image%2020240301171613.png)

- El if else es equivalente al *operador ternario*
- Recibirá 3 parámetros: `[  ]?[  ]:[  ]`

```cs
if-else = λcond.λparte_true.λparte_false.M
(if-else)(x > 100)(3)(4)
			|
			v
if-else = (λcond.λparte_true.λparte_false. cond parte_true parte_false)
// Los λ son los parámetros de la función lambda y el resto es el cuerpo de la función
```

- Función **máximo**:

```cs
maximo = λnum1.λnum2. (if-else) (num1 > num2) (num1) (num2)
maximo = λnum1.λnum2. (num1 > num2) (num1) (num2) //la lógica booleana ya implementa la función if-else, por lo que no es necesaria especificarla
```

## Ejercicio 2

![](Pasted%20image%2020240301173855.png)

```cs
operator_and = λcond1.λcond2. (cond1) (cond2) (false)
```

![](Pasted%20image%2020240301174553.png)

```cs
operator_or = λcond1.λcond2. (cond1) (true) (cond2)
```

```cs
operator_not = λcond. (cond) (false) (true)
```

# Seminario 4. Funciones de primera clase

![](Pasted%20image%2020240315194231.png)

- Una estructura que se puede recorrer
- Iterar

## Funciones de orden superior

*Nota: como ya están hechos en los laboratorios, vamos a hacer las llamadas a los métodos*

## Ejercicio 1

![](Pasted%20image%2020240315194303.png)

```cs
a.Filtrar(n => n % 2 == 0);
a.Filtrar(n => esPrimo(n));
```

## Ejercicio 2

![](Pasted%20image%2020240315194313.png)

```cs
a.Map(s => s.Length);
a.Map(f => f.Substract(DateTime.Today));
```

## Ejercicio 3

![](Pasted%20image%2020240315194324.png)

```cs
a.Reduce(1, (acu,x) => acu * x); //el 1 es el opcional
```