# Seminario 1. Polimorfismo y Enlace Dinámico

## Ejercicio 1

![](./img/Pasted%20image%2020240202191146.png)

![](./img/Pasted%20image%2020240202191207.png)

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

![](./img/Pasted%20image%2020240202193709.png)

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

