# TEMA 5 馃憖
---
## Tipado din谩mico
- Es el proceso de posponer la comprobaci贸n e inferencia de tipos en tiempo de ejecuci贸n
- Hay lenguajes:
	- Con tipado **est谩tico** (C, Fortran, Pascal)
	- Con tipado **din谩mico** (Python, Ruby, Smalltalk)
	- **H铆bridos** (C#, VB, Boo, Objective-C)

- Ventajas:
	- Mayor adaptabilidad y flexibilidad del c贸digo
	- Mayor nivel de abstracci贸n
- Inconvenientes:
	- Sin detecci贸n de errores de tipo en tiempo de compilaci贸n
	- Peor optimizaci贸n de c贸digo

- En C# se usa el tipo `dynamic` que pospone la comprobaci贸n e inferencia de tipos al tiempo de ejecuci贸n
- Cualquier tipo se puede convertir a `dynamic`
- `dynamic` se puede convertir a cualquier tipo

![[dinamic.png]]

---
## Duck Typing
- Propiedad de la mayor铆a de lenguajes con tipado din谩mico
- Significa que el estado din谩mico de un objeto determina qu茅 operaciones pueden realizarse con 茅l

![[duckyduck.png]]

--
## Multiple Dispatch
- Una de las limitaciones del enlace din谩mico es que supone usar **single dispatch**:
	- s贸lo permite resolver un m茅todo dependiendo del tipo de un 煤nico objeto (this)
- Cuando queremos que la resoluci贸n del m茅todo dependa de varios tipos, necesitamos **multiple dispatch**

---
Para m谩s info. ver -> [[Tipado din谩mico y Metaprogramaci贸n (clase)馃崚]]