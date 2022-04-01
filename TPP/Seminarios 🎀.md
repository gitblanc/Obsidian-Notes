# 1 Abril 2022
---
![[Clausulas Seminario 5.png]]
![[Ej 1 Seminario 5.png]]
```c#
//Ejercicio 1
var c = Contador();
Enumerable.Repeat(0,100).Map(x => c());
int i = 0;
new int[1000]().Map(x => i++);
```
---
![[Ej 2 Seminario 5.png]]
- Para que sea un bucle infinito -> () => true
- Para que no sea siempre un bucle infinito -> () => x >= 100
```c#
static int Suma(int[] a){
	int i = 0;
	int res = 0;
	BucleWhile(() => i < a.Length, res += a[i++]);
	return res;
}
```
---
![[Ej 3 Seminario 5.png]]
- Elementos de switch:
	- Switch (IEnumerable< (Func< bool>,Func< T>)>)
```c#
T Switch (IEnumerable<(Func<bool>,Func<T>)>){
	foreach(var v in collection){
	if(v.First())
		return v.Second();
	}
}
```
---
![[Ej 4 Seminario 5.png]]

---