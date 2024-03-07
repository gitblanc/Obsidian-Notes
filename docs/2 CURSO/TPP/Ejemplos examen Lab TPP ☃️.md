# Ejercicio métodos coincidentes

````cs
/*
         * Crear un método que reciba dos colecciones que implementen IEnumerable<T>
         * Y devuelva como resultado un IEnumerable<T> con los valores que coincidan en la misma posición.
         * Resolver el ejercicio utilizando ITERADORES (IEnumerator).
         * Probar enviando:
         * Un array de caracteres y un string.
         * Una lista de caracteres y un string.
         * Vuestra lista con caracteres y otra lista vuestra con caracteres.
         * El resultado se recorre en un foreach y se imprime elemento a elemento.
        */

        //EJEMPLO EXAMEN
        public static IEnumerable<T> Coincidentes<T>(IEnumerable<T> vector1, IEnumerable<T> vector2)
        {
            IEnumerator<T> iterador1 = vector1.GetEnumerator();
            IEnumerator<T> iterador2 = vector2.GetEnumerator();
            IEnumerable<T> result = new List<T>();

            while (iterador1.MoveNext() && iterador2.MoveNext())
            {
                if (iterador1.Current.Equals(iterador2.Current))
                    result = result.Append(iterador1.Current);
            }

            return result;
        }
````

# Ejercicios currificación (y aplicación parcial)

## Find con currificación

```cs
//Ejercicio 1.. (No de examen, para ver el de examen justo el siguiente :D)

//Implementar de forma currificada el método Buscar entregado en la sesión anterior.
//Demostrar el uso de su invocación y de la aplicación parcial.
public static T Find<T>(IEnumerable<T> collection, Predicate<T> predicate)
{
    foreach (var item in collection)
    {
        if (predicate(item))
            return item;
    }
    return default;
}

public static Func<Predicate<T>, T> FindCurrificado<T>(IEnumerable<T> collection)//, Predicate<T> predicate)
{
    return predicate =>
    {
        foreach (var item in collection)
        {
            if (predicate(item))
                return item;
        }
        return default;
    };
}
```

## División

```cs
//Ejercicio 2. EXAMEN

// Si - > 5 / 3 = 1 ; Resto = 2

// Entonces -> 3 * 1 + 2 = 5;

//Currifíquese la función y compruébese mediante el uso de la aplicación parcial el siguiente ejemplo:

// Se sabe que la división:  20 / 6 = 3. Se desconoce el valor del resto.
// Partiendo del valor 0, e incrementalmente, obténgase el resto.

public static bool ComprobarDivision(int divisor, int dividendo, int cociente, int resto)
{
    return dividendo == cociente * divisor + resto;
}

public static Predicate<int> ComprobarDivisionCurrificada1(int divisor, int dividendo, int cociente)//, int resto)
{
    return resto => dividendo == cociente * divisor + resto;//return dividendo == cociente * divisor + resto;
}

public static Func<int, Predicate<int>> ComprobarDivisionCurrificada2(int divisor, int dividendo)//, int cociente)//, int resto)
{
    return cociente =>
    {
        return resto => dividendo == cociente * divisor + resto;
    };
}

public static Func<int, Func<int, Predicate<int>>> ComprobarDivisionCurrificada3(int divisor)//, int dividendo)//, int cociente)//, int resto)
{
    return dividendo =>
    {
        return cociente =>
        {
            return resto => dividendo == cociente * divisor + resto;
        };
    };
}

///-----------------------------------///
// Probar en un Main con lo siguiente:
///----------------------------------///

// EJERCICIOS EXAMEN
// Nota: en la versión currificada, el primer parámetro es lo que devuelve la división, el segundo es el dividendo, el tercero es el divisor y el cuarto es el resto
Console.WriteLine($"División sin currificar: {Ejercicio.ComprobarDivision(5, 3, 1, 2)}");
Console.WriteLine($"División aplicación parcial 1: {Ejercicio.ComprobarDivisionCurrificada1(5, 3, 1)(2)}");
Console.WriteLine($"División aplicación parcial 2: {Ejercicio.ComprobarDivisionCurrificada2(5, 3)(2)(1)}");
Console.WriteLine($"División currificada: {Ejercicio.ComprobarDivisionCurrificada3(5)(2)(1)(3)}");
//Ejemplo al reves
Console.WriteLine($"División currificada modificada: {Ejercicio.ComprobarDivisionCurrificada3(1)(5)(3)(2)}");
// Se sabe que la división:  20 / 6 = 3. Se desconoce el valor del resto.
// Partiendo del valor 0, e incrementalmente, obténgase el resto.
int resto = 0;
while (!Ejercicio.ComprobarDivisionCurrificada3(3)(20)(6)(resto))
{
    resto += 1;
}
Console.WriteLine($"resto de hacer 20/6: {resto}");
```

# Ejercicios Clausuras

## Número aleatorio inferior

```cs
/* Examen 21/22 EXAMEN

Ejercicio 1 (A – 1,50 puntos).

    Dado un valor inicial, impleméntese una clausura que, en cada invocación,
    devuelva un número aleatorio inferior al anterior devuelto.Una vez llegue al valor
    cero y lo devuelva, el generador se reiniciará al valor inicial de forma automática.

    (B – 1,00 punto).

    Cree una versión del anterior que permita tanto reiniciar el generador de forma manual
    como modificar el valor inicial.


    Añádase código en el método Main para probar ambas versiones.

 */


public static Func<int> MetodoAleatorioInferiorv1()
{
    Random random = new Random();
    int _valor = 50;

    return () =>
    {
        _valor = random.Next(0, _valor);
        return _valor;
    };
}

// Permite reiniciar
public static void MetodoAleatorioInferiorv2(int inicial, out Action reset, out Func<int> get, out Action<int> modify)
{
    Random random = new Random();
    int _valor = inicial;


    reset = () => _valor = inicial;
    get = () => _valor = random.Next(0, _valor);
    modify = newValue => _valor = newValue;
}

///-----------------------------------///
// Probar en un Main con lo siguiente:
///----------------------------------///

// EJERCICIOS EXAMEN
// Ejercicio 1
// Versión 1
Func<int> aleatorio = Ejercicio.MetodoAleatorioInferiorv1();
int val = aleatorio();
while (val != 0)
{
    Console.WriteLine(val);
    val = aleatorio();
}
Console.WriteLine(val);
Console.WriteLine("Versión 2");
// Versión 2
Action<int> Modify;
Action Reset;
//get no recibe nada y devuelve un valor
Func<int> GetValorGenerador;
Ejercicio.MetodoAleatorioInferiorv2(50, out Reset, out GetValorGenerador, out Modify);
val = GetValorGenerador();
while (val != 0)
{
    Console.WriteLine(val);
    val = GetValorGenerador();
}
Console.WriteLine(val);
Console.WriteLine("RESET");
Reset();
val = GetValorGenerador();
while (val != 0)
{
    Console.WriteLine(val);
    val = GetValorGenerador();
}
Console.WriteLine(val);
Console.WriteLine("MODIFY 450");
Modify(450);
val = GetValorGenerador();
while (val != 0)
{
    Console.WriteLine(val);
    val = GetValorGenerador();
}
Console.WriteLine(val);
```

## Fibonacci con clausuras

```cs
public static Func<int> GetFibonacciGenerator()
{
	int prev = 0, next = 1; // Inicializar los dos primeros números de la secuencia.

	// La clausura captura y recuerda 'prev' y 'next' entre llamadas.
	return () =>
	{
		int current = prev;
		int newNext = prev + next;

		// Preparar para la siguiente llamada.
		prev = next;
		next = newNext;

		return current;
	};
}

///-----------------------------------///
// Probar en un Main con lo siguiente:
///----------------------------------///

// Obtener un generador de Fibonacci.
var fiboGenerator = GetFibonacciGenerator();

// Generar y mostrar los primeros 10 números de Fibonacci.
for (int i = 0; i < 10; i++)
{
	Console.WriteLine(fiboGenerator());
}
```

# Bucle While con enfoque funcional

```cs
 public static void BucleWhileFuncional(Func<bool> condicion, Action cuerpo) { 
	if (condicion()) 
	{ 
		cuerpo(); 
		BucleWhileFuncional(condicion, cuerpo); 
	} 
}

///-----------------------------------///
// Probar en un Main con lo siguiente:
///----------------------------------///

int i = 0; BucleWhile( () => i < 10, () => { Console.Write(i); i++; } );
```