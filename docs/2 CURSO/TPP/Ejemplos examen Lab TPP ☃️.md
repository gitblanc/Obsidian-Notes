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

![](img/Pasted%20image%2020240227180210.png)