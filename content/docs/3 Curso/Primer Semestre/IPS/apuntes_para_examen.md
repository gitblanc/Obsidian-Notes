---
title: Apuntes para Examen Teoría IPS 🤩
---
- ==**Requisitos**==: necesidades del cliente o del usuario. Describen el qué de un producto software (qué debe hacer, qué debe ser y que limitaciones tiene). Hay varios tipos:
	- **Funcionales**: servicios y funciones que tendrá el producto. Qué hace el sistema, como se debe comportar y qué no debe hacer
	- **No funcionales**: restricciones de cómo se implementará el producto, seguridad, almacenamiento...
	- Integración con otros sistemas
	- Implantación y migración 
	- Normativos

- ==**Pliego de condiciones**==: documento en el cuál se establecen  las condiciones o cláusulas de un contrato

- ==**SCRUM**==:
	- Es un Framework más que una metodología
	- Ciclos cortos (sprints de 1 a 4 semanas)
	- Entregas tras cada ciclo
	- Equipo multifuncional
![](img/Pasted%20image%2020221217121532.png)
![](img/Pasted%20image%2020221217125008.png)

- ==**Roles**==:
	- **SCRUM Team** = Product Owner+ Scrum Master + Development Team
	- **Product Owner**: es el dueño del producto
		- Realiza el papel del cliente
		- Representa al negocio y a los clientes (toma las decisiones)
		- Interactúa activa y frecuentemente con el equipo
	- **SCRUM Master**: gestor de SCRUM
		- Ayuda a aplicar SCRUM (coach)
		- Elimina impedimentos (como bloqueos por recursos)
		- También puede realizar trabajos como el equipo de desarrollo
		- No es el jefe del equipo (no existe jefe)
		- Se adapta a la experiencia del equipo
	- **Development Team**:
		- Autogestionado
		- Decide cómo realizar el trabajo
		- Se encarga de todos los procesos de desarrollo
		- Aunque tenga expertos en temas concretos, no debe ser una limitación (aprendizaje múltiple)
		- Está compuesto de 7+-2 personas

- **Pila de producto** (==**Product Backlog**==):
	- Lista priorizada de funcionalidades (ordenada)
	- Evoluciona a lo largo del proyecto
	- Incluye funcionalidades, objetivos de mejora, correciones, ...
	- Las estimaciones las suministra el equipo de desarrollo
	- Sigue las propiedades ==**DEEP**==:
		- D: detallado apropiadamente
		- E: estimado
		- E: emergente, refinado regularmente
		- P: priorizado, ordenado

- ==**Historias de usuario**==:
	- **Objetivo**: definir los detalles del sistema a implementar y definir las tareas a realizar (backlog)
	- **Historias de usuario**: forma de que el dueño del producto provea al equipo de los requisitos de la aplicación (conversaciones y criterios de aceptación)
	- **Formato**: Como < tipo de usuario > quiero < hacer algo > para < crear algún valor >// Para < conseguir un objetivo/crear algún valor > como < usuario > quiero < hacer algo >
Si las historias de usuario no deben ser demasiado grandes, deben poder realizarse en un sprint. Las demasiado grandes se denominan "Epics". Hay que empezar por la más prioritaria.
Las historias de usuario constituyen el **backlog** del producto.

- ==**Planificación de cada Sprint**==:
	- Dos reuniones (un día en total)
	- **Reunión 1** (medio día):
		- Definir **qué** se va a hacer
		- Product Owner y equipo de desarrollo discuten/revisan el Product backlog
		- Scrum Master presta asistencia a todos
		- Se establece un compromiso de lo que se realizará en el sprint
	- **Reunión 2** (medio día):
		- Definir **cómo** se va a hacer
		- Selección final de los element9os de la pila para el Sprint
		- El Product Owner puede no asistir, pero debe estar disponible por si hay algo que revisar

- ==**Sprint backlog**==: lista de todas las historias acordadas para el sprint

- ==**Burndown Chart**==: representa en forma gráfica lo que queda por hacer (Gráfico de Tiempo Restante)

- ==**Backlog grooming**==: refinamiento del product backlog
	- Participa todo el equipo de SCRUM
	- Facilita la planificación de sprints posteriores, manteniendo características del product backlog (DEEP)
	- Se hace durante un sprint en referencia a los elementos futuros que no están incluídos en él
	- Típicamente ocupa 5-10% del tiempo de un sprint

- **==Story Mapping==**: mapeo de historias
	- El product backlog es unidimensional
	- Con esto le damos estructura bidimensional
		- **Columnas**: agrupa usuarios, procesos y funcionalidades
		- **Filas**: las historias con sus prioridades
	- Permite mejorar la visión del producto
	- Es dinámico pues evoluciona con el proyecto
![](img/Pasted%20image%2020221217131527.png)

- **==Pruebas==**: hay dos tipos:
	- **TDD** (Test-Driven Development)
		- Definir primero las pruebas
		- Implementar y ejecutar las pruebas
		- Refactorizar
	- BDD (Behaviour-Driven Development)
		- Usar historias de usuario con estructura, que se convierten en pruebas

- ==**Criterios de aceptación**==: condiciones a satisfacer
	- Suministrados por el product owner
	- Obtenidos/refinados mediante conversación
	- No son pruebas de aceptación

- ==**Características INVEST**==:
	- **Independiente**: la historia es independiente de las demás
	- **Negociable**: se puede negociar la historia con el cliente antes de comenzar un sprint
	- **Valioso**: tiene que aportar valor al negocio, al usuario, al cliente... Ha de formar parte del objetivo del Product Owner
	- **Estimable**: se puede determinar el tiempo que se va a tardar en desarrollarla y nos comprometemos a realizarla en ese tiempo
	- **Small**: tiene que ser pequeña en su descripción, en su duración
	- **Testing**: se tiene que poder probar

- El ==**Manifiesto ágil**== valora:
	- **Individuos e interacciones**  más que procesos y herramientas
	- **Software que funciona** más que documentación exhaustiva
	- **Colaboración con el cliente** más que navegación de contratos
	- **Responder ante el cambio** más que el seguimiento de un plan

- ==**Principios del Manifiesto ágil**==:
	- La prioridad es **satisfacer al cliente** con entregas tempranas y que aporten valor
	- **Aceptación de cambios en los requisitos**, incluso si llegan tarde al desarrollo
	- Entrega de **software que funcione**
	- Gente de negocio y desarrolladores deben **trabajar juntos**
	- **Individuos motivados**
	- **Comunicación** en el equipo
	- Medida de progreso: **software que funciona**
	- Desarrollo con **ritmo constante**
	- **Simplicidad**
	- **Equipos autoorganizados**
	- El equipo reflexiona regularmente **cómo ser más efectivo**, se **afina y ajusta su comportamiento** con esto

### Enfoque orientado al proceso

- **==EVS==**: Estudio de Viabilidad del Sistema
	- **Objetivo**: analizar las necesidades del cliente/usuario (requisitos de usuario), para proponer una solución a largo plazo
	- **Resultado**: definición de uno o varios proyectos
	- Analizar/discutir lo que sea necesario
	- El resultado de este estudio irá al **Pliego de Condiciones**

- **==ASI==**: Análisis del Sistema de Información
	- **Objetivo**: obtención de una especificación detallada del sistema de información que satisfaga las necesidades de información de los usuarios y sirva de base para el posterior diseño del sistema
	- Transforma los requisitos de usuario en requisitos del sistema
	- En lugar dfe historias de usuario, tiene casos de uso

- **==DSI==**: Diseño de Sistemas de Información
	- **Objetivo** (partiendo de la especificación ASI):
		- Definir la arquitectura del sistema
		- Definir el entorno tecnológico de soporte
		- Describir los componentes del sistema
		- Modelo físico de datos
		- Especificaciones de construcción, migración, entorno de pruebas ...

### RUP y MEDEP

- **==Proceso unificado==**: proceso iterativo e incremental (RUP, Rational Unified Process)
	- **Estructura**: fases y workflows o disciplinas
	- **Organización**: cada fase se organiza en iteraciones, cada iteración incluye diferentes disciplinas

- **==Fases en RUP==**:
	- **Incepción**:
		- Obtener acuerdo entre las partes interesadas sobre los objetivos
		- Casos de uso
		- Arquitectura candidata
		- Evaluación inicial de riesgos
		- Plan de proyecto inicial
	- **Elaboración**:
		- Implementación inicial de la arquitectura
		- Identificación de todos los casos de uso
		- Elaboración del Plan de Proyecto
	- **Construcción**:
		- Refinar requisitos y diseño
		- Programación
		- Integraciones y pruebas en cada iteración
	- **Transición**:
		- Pruebas (aceptación)
		- Formación 
		- Migraciones

- **==Iteraciones e incrementos==**:
	- **Desarrollo incremental**
		- Mejorar el proceso dividiéndolo en partes
		- En cada iteración se aumentan las funciones del sistema
		- Típicamente entre 2-6 semanas
	- **Desarrollo iterativo**
		- Mejorar el producto reescribiendo parte del producto cuando es preciso

- **==MEDEPA==**: Metodología de Desarrollo de Proyectos del Principado de Asturias

- **==MSI==**: Mantenimiento de Sistemas de Información. Tipos:
	- **Correctivo**: corrige problemas
	- **Evolutivo**: expansión/cambio necesidades de usuario
	- **Adaptativo**: se adapta a diversos entornos
	- **Perfectivo**: mejora la calidad interna

---