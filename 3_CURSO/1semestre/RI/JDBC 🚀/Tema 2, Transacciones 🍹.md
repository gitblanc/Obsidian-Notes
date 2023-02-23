# 22 Sept 2022 🧃
---
- Usaremos **concurrencia** para usar a la vez la **memoria** y el **disco** (saldrán **bloqueos**)

## Organización de memoria asociada a un SGBD
1. Local
2. Global o compartida
3. Disco
4. Log

- **Transacción**: conjunto de operaciones que se reflejan como una única operación (ej: sacar dinero, incluyendo varias lecturas y escritura)
- Cada ejecución SQL se ejecuta de forma **transaccional** (valor de la propiedad AutoCommit = true). Si lo ponemos a false, las operaciones se ejecutarán cuando nosotros queramos
	- Se puede hacer:
		- Commit (implícito o explícito)
		- Rollback
- Propiedades **ACID** (atomicidad, consistencia, asilamiento, durabilidad)
	- **Atomicidad**: o todas o ninguna (ocurre completamente o no ocurre)
	- **Consistencia**: asegurarse de que los datos sean consistentes (años > 0)
	- **Aislamiento**: el efecto de las transacciones concurrentes ha de ser el mismo que si se ejecutasen una detrás de otra
	- **Durabilidad**: los efectos de las operaciones han de ser permanentes (persistentes)
- Una transacción es una lista de operaciones:
	- Las operaciones son:
		- lecturas -> R(O)
		- escrituras -> W(O)
	- Las transacciones terminan con **Commit** o **Abort**
- **Planificación**: intercalado de operaciones de un conjunto de transacciones
- El planificador decide el plan de ejecución (planificación)
- Comprobar si una planificación es serializable -> se crea un **grafo de precedencia**
- Una planificación es **serializable** si no hay ciclos en el grafo de precedencia
![[ej 1 teoria.png|500]]
## Conflictos
- **Lecturas sucias**: conflicto de lectura escritura
- **Lecturas no repetibles**: conflicto de dos lecturas y los resultados son distintos cuando deberían ser el mismo
- **Lecturas fantasmas**
- **Lecturas inconsistentes**
- **Pérdida parcial de la actualización**
![[ej 2 teoria.png|500]]

## ¿Cómo gestionar los conflictos?
### Enfoque pesimiesta
- Evitar conflictos empleando un mecanismo de bloqueos (Lock-Based Concurrency Control)
- Dos tipos de locks:
	- Compartidos: para leer
	- Exclusivos: para escribir, y prohibe lecturas y escrituras de los demás. Para acabar, hago un unlock
- PROBLEMAS: interbloqueos debido a la competencia

### Enfoque optimista
- Control de versiones para detectar si han ocurrido conflictos
- Tres fases de transacciones:
	- Fase de simulación
	- Fase de validación
	- Fase de escritura

---