# Tema 1. Fundamentos de la Ingeniería de Requisitos

- Los requisitos son una especificación de lo que se debería implementar
	- Descripciones de cómo debería comportarse el sistema
	- Descripciones de atributos o propiedades del sistema
	- También podrían ser una restricción en el proceso de desarrollo del sistema

- Ingeniería de requisitos
	- Es importante porque los errores no descubiertos en esta fase, implican correcciones en fases posteriores

![](./img/Pasted%20image%2020231207142324.png)

![](./img/Pasted%20image%2020231207142424.png)

## Problemas típicos

- Los requisitos no reflejan las necesidades de los usuarios
- Requisitos excesivamente cambiantes
- Requisitos ambiguos
- El cliente pide características de escaso valor
- El desarrollador añade funcionalidades no solicitadas
- Stakeholders no tenidos en cuenta
- Solucionar estos problemas afecta a la planificación

## Niveles y tipos de requisitos

- Requisitos de negocio
- Requisitos de usuario
- Requisitos funcionales
	- Se documentan en una Especificación de Requisitos Software (**SRS**)
- Requisitos del sistema
- Reglas de negocio: legislación, políticas y estándares
- Atributos de calidad: seguridad, accesibilidad...
- Interfaces externas
- Restricciones

## Requisitos funcionales vs No funcionales

- **Requisitos funcionales**: describen el comportamiento del sistema bajo unas condiciones determinadas
- **Requisitos no funcionales**: suelen asociarse con los atributos de calidad, restricciones, interfaces externas, reglas de negocio...

## Requisitos no funcionales (RNF) según Kotonya y Somerville

![](./img/Pasted%20image%2020231207143151.png)

## Otras clasificaciones de requisitos

![](./img/Pasted%20image%2020231207143304.png)

## Requisitos de producto y de proyecto

- **Requisitos de producto**: describen propiedades del sistema a desarrollar
- **Requisitos de proyecto**: no forman parte del sistema a desarrollar, pero son necesarios para completar el proyecto (documentación, certificación del producto, adquisición de licencias...)

# Tema 2. Proceso de la Ingeniería de Requisitos

- **Proceso de la Ingeniería de Requisitos**: conjunto estructurado de actividades que se siguen para obtener, validar y mantener un documento de requisitos del sistema

## Obtención de requisitos

1. Identificar tipos de usuarios y otros stakeholders
2. Entender tareas y objetivos de los usuarios y los objetivos de negocio relacionados
3. Comunicación con los usuarios para obtener sus necesidades y expectativas
4. Comprender el contexto del producto

## Análisis de requisitos

1. Analizar la información obtenida de los usuarios
2. Detallar adecuadamente requisitos de alto nivel
3. Estudio de los atributos de calidad
4. Derivar requisitos funcionales a partir de otros requisitos
5. Definir prioridades
6. Identificar requisitos necesarios o incompletos

## Especificación de requisitos

- Consiste en representar y almacenar el conocimiento de requisitos de forma clara y organizada

1. Producir requisitos escritos
2. Generar diagramas adecuados para el uso y comprensión

## Validación

1. Revisar la documentación en busca de errores

## Gestión

1. Definir la línea base de requisitos
2. Evaluar cambios propuestos
3. Incorporar cambios aprobados de forma controlada
4. Trazar requisitos individuales con diseños, código y pruebas derivados
5. Realizar un seguimiento del estado de los requisitos y del historial de cambios

## Flujo del proceso

- No es lineal, sino iterativo

![](./img/Pasted%20image%2020231207144632.png)

![](./img/Pasted%20image%2020231207144717.png)

## Otros procesos de IR. Pohl

![](./img/Pasted%20image%2020231207144857.png)

## Kotonya y Sommerville

![](./img/Pasted%20image%2020231207145010.png)

## Tema 3. Técnicas de obtención de requisitos

## Tipos de stakeholders

- Externos a la organización desarrolladora
- Organización desarrolladora
- Equipo del proyecto

## Tipos de usuarios

- Usuarios **deseados**
- Usuarios **no deseados** (los que no deberían usarlo por cuestiones legales o de seguridad)
- Usuarios **ignorados** (pueden usar el producto, pero no son el objetivo)
- Usuarios **indirectos** (no usan el producto, pero acceden a sus datos a través de otros medios)

## Técnicas de obtención de requisitos

### Entrevistas
- Individuales o en grupos pequeños
- Pueden ser:
	- **Estructuradas**: preparadas de antemano para conocer una información concreta
	- **Semi-estructuradas**: se sigue una estructura, pero con libertad para que el entrevistador se desvíe si es necesario
	- **No estructuradas**: conversación improvisada con el objetivo de reunir información
- Tipos de preguntas:
	- **Abiertas**: el entrevistado tiene infinitas respuestas posibles
		- ¿Qué opina de la empresa?
	- **Cerradas**: el entrevistado tiene un número de respuestas finito
		- ¿Nº medio de transacciones diarias en la empresa?
- Consejos:
	- Construir una relación con el entrevistado
	- Mantenerse fieles al tema
	- Tener algunas preguntas preparadas de antemano
	- Sugerir ideas a los interlocutores
	- Escuchar activamente
### Talleres

- Reunión estructurada en la que un grupo selecto de stakeholders y expertos definen, crean, refinan y cierran entregables que representan requisitos
- Permiten obtener requisitos de múltiples stakeholders a la vez
- Consejos:
	- Definir reglas básicas
	- Definir roles
	- Elaborar planificación
	- Ceñirse al alcance del proyecto
	- Capturar cuestiones de relevancia
	- Asignar un tiempo a cada tema
	- Grupos pequeños son preferibles (+6 participantes es inmanejable)
	- Procurar la participación de todos los integrantes

### Grupos focales

- Grupo de usuarios representativos que aporta información e ideas sobre los requisitos de un producto
- Permiten conocer las necesidades, preferencias y expectativas de los usuarios
- Variantes:
	- Múltiples grupos focales de usuarios del mismo tipo
	- Grupo focal de usuarios de todos los tipos relevantes
- Requieren facilitación

### Observaciones

- En ocasiones, las descripciones de los usuarios no son suficientes para comprender las tareas que realizan 
- La observación de los usuarios en su entorno de trabajo puede aportar información útil
- Consumen mucho tiempo
	- por lo que deberían hacerse en tareas importantes o de alto riesgo
- Permiten identificar problemas a resolver, temas a profundizar y corroborar la información obtenida previamente
- Pueden incluir interacción con el usuario

### Cuestionarios

- Permiten encuestar a grandes cantidades de usuarios sin interacción directa
- Equivalentes a una entrevista estructurada escrita
- Consejos:
	- Usar preguntas abiertas o cerradas según los objetivos
	- Las opciones de respuesta han de ser exclusivas y exhaustivas
	- Escalas consistentes
	- Probar el cuestionario antes de su uso
	- Nº limitado de preguntas

### Análisis de interfaces de sistema

- Estudio de los sistemas externos a los que deba conectarse nuestro producto
- El objetivo es identificar funcionalidades en otros sistemas que impliquen requisitos en el sistema a construir
- Los diagramas de contexto son un buen punto de partida

### Análisis de interfaces de usuario

- Estudio de sistemas preexistentes con el objetivo de descubrir requisitos
- Permite conocer las tareas habituales de los usuarios

### Análisis de documentación

- Estudio de la documentación de sistemas preexistentes o similares

## ¿Cuándo emplear las técnicas?

![](./img/Pasted%20image%2020231207153304.png)

## Recomendaciones: preguntas

![](./img/Pasted%20image%2020231207153358.png)

![](./img/Pasted%20image%2020231207153417.png)

## Recomendaciones: uso de modelos

![](./img/Pasted%20image%2020231207153452.png)

## Recomendaciones: obtención

![](./img/Pasted%20image%2020231207153531.png)



