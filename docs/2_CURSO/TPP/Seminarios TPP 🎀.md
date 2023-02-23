# 4 Febrero 2022
---
![[seminario 1.1.png]]
![[seminario 1.2.png]]

---
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
# 22 Abril 2022, Seminario 6 🥖
---
### Ej 1
![[ej1 s6.png||500]]
![[ej 1 s6 2.png||500]]
Solución: 
```c#
public void Ejecutar(){
	lock(Rec1){
		Rec1.Procesar();
	}
	lock(Rec2){
		Rec2.Procesar();
	}
}
```

### Ej 2
![[ej 2 s6.png||500]]
```c#
[namespace TPP.Seminarios.Concurrente.Seminario6 {  
/// <summary>  
/// Cada uno de los tenedores disponibles  
/// </summary>  
class Tenedor {  
/// <summary>  
/// Número de tenedor  
/// </summary>  
private int numero;  
public Tenedor(int numero) {  
this.numero = numero;  
}  
}  
}  
using System;  
using System.Threading;  
namespace TPP.Seminarios.Concurrente.Seminario6 {  
class Filosofo {  
/// <summary>  
/// ID del filósofo  
/// </summary>  
private int numeroFilosofo;  
/// <summary>  
/// El tiempo que tarda pensando  
/// </summary>  
private int milisPensar;  
/// <summary>  
/// El tiempo que tarda comiendo  
/// </summary>  
private int milisComer;  
/// <summary>  
/// Los tenedores izquierdos y derechos  
/// </summary>  
private Tenedor tenedorIzquierdo, tenedorDerecho;  
public Filosofo(int numeroFilosofo, int milisPensar, int milisComer,  
Tenedor tenedorIzquierdo, Tenedor tenedorDerecho) {  
this.numeroFilosofo = numeroFilosofo;  
this.milisPensar = milisPensar; this.milisComer = milisComer;  
this.tenedorIzquierdo = tenedorIzquierdo;  
this.tenedorDerecho = tenedorDerecho;  
new Thread(new ThreadStart(ComerYPensar)).Start();  
}

private void ComerYPensar() {  
for (;;) {  
lock (this.tenedorIzquierdo) {  
lock (this.tenedorDerecho) {  
Console.WriteLine("El filósofo " + numeroFilosofo +  
" está comiendo...");  
Thread.Sleep(milisComer);  
}  
}  
Console.WriteLine("El filósofo " + numeroFilosofo +  
" está pensando...");  
Thread.Sleep(milisPensar);  
}  
}  
}  
}  
namespace TPP.Seminarios.Concurrente.Seminario6 {  
class Program {  
static void Main(string[] args) {  
const int milisPensar = 0, milisComer = 0;  
Tenedor[] tenedor = new Tenedor[5];  
for (int i = 0; i < tenedor.Length; i++)  
tenedor[i] = new Tenedor(i);  
new Filosofo(0, milisPensar, milisComer, tenedor[0], tenedor[1]);  
new Filosofo(1, milisPensar, milisComer, tenedor[1], tenedor[2]);  
new Filosofo(2, milisPensar, milisComer, tenedor[2], tenedor[3]);  
new Filosofo(3, milisPensar, milisComer, tenedor[3], tenedor[4]);  
new Filosofo(4, milisPensar, milisComer, tenedor[4], tenedor[0]);  
}  
}  
}]()
```
Solución:
- Poner un timeout al tenedor dereho para que no haya un bloqueo.

- ¿Cómo sé si un tenedor está o no libre?
	Necesito un manejador de tenedores (Manager)
```c#
class ManagerTenedores{
	public CogerTenedor(int t1, int t2){
		lock(instance){
			//Comprueba
		}
	}
}

private void ComerYPensar(){
	while(true){
		if(manejador.CogerTenedor(t1,t2))//siendo t1,t2 los índices de los tenedores
		{
			//Puedo comer
			manejador.LiberarTenedor(t1,t2);
		}else{
			//Me pongo a pensar
		}
	}
}
```
- Nota: el patrón de diseño Singleton es un objeto común al que acceden todos los elementos.