鈾伙笍 Parte anterior -> [[Programaci贸n concurrente y paralela (clase)馃敨]]
# 31 Marzo 2022 馃
---
## Tipado Din谩mico 
- Es el proceso de posoponer la comprobaci贸n de inferencia de tipos en tiempo de ejecuci贸n
Inconvenientes
- No se detectan errores en tiempo de compilaci贸n.
- Peor rendimiento.
Ventajas
- Adaptabilidad y flexibilidad del c贸digo.
- Mayor nivel de abstracci贸n.

- En c# se usa dynamic.
- Cualquier tipo se puede convertir en dynamic y viceversa.
````
C贸digo en dynamic.typing/dynamic
````
- Se pospone la comprobaci贸n e inferencia de tipos en tiempo de ejecuci贸n.
---
## Duck Typing
- El estado din谩mico de un objeto determina qu茅 operaciones pueden realizarse con 茅l.
---
# 7 Abril 2022 馃寢
---
## Reflexi贸n
- Capacidad de un sistema de razonar por s铆 mismo.
- Tipos de reflexi贸n:
	- **Introspecci贸n:** se puede consultar pero no modificar.
	- **Intercesi贸n:** se permite modificar.
	- **Estructural:** la informaci贸n es la estructura de un programa
	- **De comportamiento:** si un lenguaje tiene reflexi贸n de comportamiento se puede cambiar la sem谩ntica de dicho lenguaje. Para entender mejor ver -> https://www.hedonisticlearning.com/posts/behavioral-reflection.html .
	
---
	
![[atributos.png]]

---
## Generaci贸n din谩mica de c贸digo
- Capacidad de generar programas en tiempo de ejecuci贸n.
- Se hace en .NET a trav茅s de Roslyn.
```
C贸digo en reflection/generative.programming
```
---
## Metaprogramaci贸n
- Capacidad de escribir programas que escriban o manipulen otros programas.