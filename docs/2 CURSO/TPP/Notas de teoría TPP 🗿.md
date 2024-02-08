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

