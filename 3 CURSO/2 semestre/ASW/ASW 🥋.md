# 1 Febrero 2023 🎱

- **Registro de decisiones arquitectónicas**: anotación de las ventajas e inconvenientes de una arquitectura de software
- Todas las arquitecturas son diseños, pero no todas las decisiones de diseño son arquitecturas
- Cualquier solucion en AS es un *trade-off* (compromiso)

## Leyes de la arquitectura del software
- Todas las soluciones tienen desventajas
- El porqué codificar algo es más importante que el cómo codificarlo

- Las restricciones te evitan tomar decisiones de diseño, pues te vienen impuestas

## Tipos de sistemas
- **greenfield en dominios nuevos**: algo nuevo
- **greenfield en dominios maduros**: algo nuevo en una empresa ya existente
- **brownfield**: software ya existente que se ha de modificar

- **Objetivo de la arquitectura del software**: comentar la solución de diseño al equipo
- El código no explica el software
- La **documentación** ha de:
	- reflejar la realidad
	- ser comprensible por las distintas personas interesadas (stakeholders)
	- adaptarse a cambios
- **Stakeholder**: personas interesadas en el software

---
# 8 Febrero 2023 🛣️
- Arquitecto de software es un rol, no un rango
- Expectativas de un arquitecto:
	- Tomar decisiones arquitectónicas  
	- Analizar continuamente la arquitectura  
	- Estar al día de las tendencias actuales 
	- Asegurar cumplimiento decisiones existentes 
	- Experiencia diversa
	- Conocimiento del dominio de negocio  
	- Poseer habilidades interpersonales 
	- Comprender y navegar en política empresarial
![[Pasted image 20230208115042.png]]

## Maniobra inversa de Conway
![[Pasted image 20230208115727.png]]

## Ley de Brook
- Añadir más personas a un equipo que va retrasado hace que se retrase más todavía

## Identificando stakeholders
![[Pasted image 20230208121025.png]]

## Atributos de calidad
- Son las características de la arquitectura junto con los requisitos no-funcionales

- Tipos de requisitos:
![[Pasted image 20230208121342.png]]
- Los funcionales se suelen cumplir.
- Los no funcionales (velocidad, accesibilidad, disponibilidad) es lo difícil.

- Los atributos de calidad han de comprobarse en los **escenarios** de calidad.
![[Pasted image 20230208122206.png]]
- Árbol de atributos de calidad: usar mindmap
![[Pasted image 20230208122354.png]]

## 4 métricas clave (métricas DORA)
Origen: Informe State of DevOps de DORA (equipo DevOps Research and Assessment
Miden rendimiento de la entrega de software
1. Lead time to change (tiempo de espera para cambios)
Tiempo desde que se hace commit hasta que código va a producción
2. Frecuencia de despliegue
Frecuencia con la que se despliega código en producción
3. Tiempo medio de restauración (MTTR)
Cuánto tiempo se tarda en restaurar un servicio tras un incidente
4. Tasa de fallos tras cambios
Porcentaje de cambios en producción que resultan en fallos
https://www.devops-research.com/quickcheck.html

---