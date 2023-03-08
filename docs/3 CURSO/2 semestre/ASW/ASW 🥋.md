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
# 22 Febrero 2023 🍐

## ADD: Attribute-driven design
- No se usa en las empresas porque es difícil de seguir


- Es importante hacer un registro de decisiones arquitectónicas

- **Riesgo**: algo malo que puede o no ocurrir
- Se suelen crear tablas de riesgo (tablas de matriz de riesgo)
![[Pasted image 20230222113230.png]]

- Los problemas que no se arreglan pueden generar una deuda técnica (**technical debt**)

## Técnicas de arquitectura del software

### Herramientas de un arquitecto del software
- **Tácticas**: estrategia a seguir para resolver un atributo de calidad
- **Estilos arquitectónicos**: definen la forma general del sistema
- **Patrón arquitectónico**: solución general y reutilizable a algún problema  recurrente que aparece en un contexto. Hay 3 tipos:
	- Estructurales
	- Runtime (comportamiento)
	- Despliegue
- **Patrón vs Estilo**:
	- Los estilos, en general, son independientes entre sí
	- Un patrón puede relacionarse con otros patrones
- Arquitecturas de referencia
- Componentes desarrollados externamente (**stack tecnológico**): tecnologías que suelen ir muy bien de la mano

## Taxonomía del software, patrones, estilos y tácticas

- Cada vez más el software se está volviendo un servicio en lugar de ser un producto.
- Tenemos que afrontar que el software va a cambiar
- Tenemos que ser capaces de atomatizar la contrucción
- Modelo en V
![[Pasted image 20230222121354.png]]
- **Big Design Up Front**: dedicarse únicamente a diseñar es una mala práctica
- Hay que intentar que las pruebas sean automáticas
- Principios FIRST:
	- Fast
	- Independent
	- RepeatableSelf-checking
	- Timely

---

# 1 Marzo 2023 🗳️

- Módulo: algo que identificamos a la hora de construír
- Componente: algo que se puede identificar en tiempo de ejecución

- Principio de Responsabilidad Única: un módulo debe tener una única responsabilidad
- Un módulo debería ser abierto para extender pero cerrado para modiicar su propio código


---
# 8 Marzo 2023 🌹

## Flujos de datos

|Tipo|Ventajas|Inconvenientes|
|-----|-----|-----|
|Secuencial - Batch|Poco acoplamiento entre componentes, reconfigurabilidad y depuración|Sin interfaz, requiere intervención externa, sin concurrencia y alta latencia|
|Pipes & Filters|Comprensión global, reconfiguración, evolución y extensibilidad, testabilidad y rendimiento|Posibles retardos, difícil pasar estructuras de datos complejas, sin interactividad, backpressure(se reciben más datos de los que se pueden procesar)|
|Pipes & Filters-Interfaz uniforme|Facilita el desarrollo independiente de filtros, más fácil de comprender, fácil reconfiguración|Emperora el rendimiento si los datos deben transformarse|
|Master-slave|Computacuón paralela, tolerancia a fallos|Dificultad de coordinación entre los nodos slaves, dependencia del Master, dependencia de configuración física|
|MVC|Múltiples vistas del mismo modelo, sincronización de vistas, separación de incumbencias, facilidad para crear nuevas vistas y controladores, potencial para creación de marcos genéricos|Mayor complejidad en desarrollos de GUIS, Acoplación entre Modelos y Vistas, Controlador/Vista depende de la nterfaz del modelo, Dificultades con herramientas GUI|
|PAC|Separación de responsabilidades, soporte para cambios y extensiones, multitarea|Complejidad del sistema, del componente de control y rendimiento |
|Datos compartidos|Componentes independientes, facilita comunicación entre componentes, consistencia de datos|Punto de fallo único, posible cuello de botella, Sincronización en acceso a memoria compartida|
|Blackboard|Experimentación, reusabilidad, tolerancia a fallos|Depuración, rendimiento, alto coste de desarrollo|
|Sistemas basados en reglas|Mantenibilidad, separación de responsabilidades, reutilización|Depuración, rendimiento, creación y mantenimiento de las reglas|
|Call-return|Sencillo de implementar|Ejecución concurrente, entornos distribuidos|
|Cliente-Servidor|Servidores pueden estar distribuidos, separación de funcionalidad cliente/sevidor, funcionalidad general disponible para todos los clientes|Cada servidor puede ser un punto de fallo, rendimiento impredecible, seguridad|
|Servidor replicado|Mejora tiempos de respuesta, menor latencia, tolerancia a fallos|mantenimiento de consistencia, sincronización|
|Cliente-Servidor con caché|Menor carga en la red, menor tiempo de respuesta|Complejidad de configuración, no apropiado en ciertos dominios|
|Basado en eventos|desacoplamiento, atemporalidad, asincronicidad|Solución no secuencial, consistencia del sistema, dificultad de depuración|
|Publish-subscribe|calidad de comunicación, bajo acoplamiento, escalabilidad|se añade nivel de indirección, implementación compleja|
|Modelos de actores|paralelismo, transparencia y escalabilidad, modelos de actores no locales|envío de mensajes, coordinación entre actores, sistemas no consistentes por definición|
|CQRS|escalabilidad, facilita descomposición de equipos|operaciones híbridas(consulta/comando), complejidad, sincronización|
|Event-Sourcing|tolerancia a fallos, trazabilidad, reconstrucción, escalabilidad|novedad desarrollo, consistencia de datos, actualización software, gestión de recursos|
|Plugins|extensibilidad, personalización|consistencia, rendimiento, seguridad, gestión de plugins y dependencias|
|Microkernel|portabilidad, flexibilidad y extensibilidad, seguridad y fiabilidad|rendimiento, complejidad del diseño, punto de fallo único|
|Reflection|flexibilidad|implementación, rendimiento, seguridad|
|Intérpretes y DSLs|flexiilidad, usabilidad, adaptabilidad|diseño del lenguaje, complejidad de implementación, rendimiento, seguridad|
|Código móvil|flexibilidad y adaptación a diferentes entornos|complejidad de la implementación, seguridad|
|Código bajo demanda|mejora experiencia de usuario, extensibilidad, adaptación a entorno del cliente|seguridad, coherencia|
|Evaluación remota|Aprovechar capacidades de terceras partes|seguridad, configuración|
|Agentes móviles|reducción del tráfico en la red, paralelismo implícito, tolerancia a fallos de red, conceptualmente sencillos, adaptación a cambios en el entorno|complejidad de la configuración, seguridad|

---