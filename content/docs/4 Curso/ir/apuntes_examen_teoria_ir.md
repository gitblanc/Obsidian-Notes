---
title: Apuntes Examen Teoría 🎷
---
# Tema 1. Fundamentos de la Ingeniería de Requisitos

- Los requisitos son una especificación de lo que se debería implementar
	- Descripciones de cómo debería comportarse el sistema
	- Descripciones de atributos o propiedades del sistema
	- También podrían ser una restricción en el proceso de desarrollo del sistema

- Ingeniería de requisitos
	- Es importante porque los errores no descubiertos en esta fase, implican correcciones en fases posteriores

![](img/Pasted%20image%2020231207142324.png)

![](img/Pasted%20image%2020231207142424.png)

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

![](img/Pasted%20image%2020231207143151.png)

## Otras clasificaciones de requisitos

![](img/Pasted%20image%2020231207143304.png)

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

![](img/Pasted%20image%2020231207144632.png)

![](img/Pasted%20image%2020231207144717.png)

## Otros procesos de IR. Pohl

![](img/Pasted%20image%2020231207144857.png)

## Kotonya y Sommerville

![](img/Pasted%20image%2020231207145010.png)

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

![](img/Pasted%20image%2020231207153304.png)

## Recomendaciones: preguntas

![](img/Pasted%20image%2020231207153358.png)

![](img/Pasted%20image%2020231207153417.png)

## Recomendaciones: uso de modelos

![](img/Pasted%20image%2020231207153452.png)

## Recomendaciones: obtención

![](img/Pasted%20image%2020231207153531.png)

# Tema 4. Análisis de requisitos

## Modelos visuales

### Diagramas de casos de uso

![](img/Pasted%20image%2020231208120245.png)

### Diagramas de actividad

![](img/Pasted%20image%2020231208120317.png)

### Diagramas de flujo de datos

- Adecuados para sistemas de procesamiento de transacciones
- Describen el movimiento de datos de un sistema
- Útiles para extraer requisitos de datos
- A menudo usados en **entrevistas**

![](img/Pasted%20image%2020231208120406.png)

### Diagramas swimlane

- Representan las operaciones a realizar para ejecutar un proceso del sistema

![](img/Pasted%20image%2020231208120629.png)

### Diagramas de estado

- Describen los cambios de estado de un sistema bajo unas condiciones determinadas
- Uso típico en sistemas de tiempo real y en la gestión de pedidos, inventarios y similares

![](img/Pasted%20image%2020231208120806.png)

### Mapas de diálogo

- Describen la interfaz de usuario a un nivel de abstracción alto
- Permite explorar el flujo de interacciones entre usuarios y sistema sin entrar en detalles de los procesos o cuestiones de diseño de IU

![](img/Pasted%20image%2020231208120939.png)

### Árboles de decisión

- Representan una secuencia lógica de acciones a tomar por el sistema bajo unas condiciones determinadas
- Adecuados para documentar restricciones de negocio

![](img/Pasted%20image%2020231208121052.png)

### Diagramas entidad-relación

- Representa entidades y relaciones entre ellas
- Se emplean para definir Bases de datos (BD)

![](img/Pasted%20image%2020231208121227.png)

### Diagramas de clase

- Alternativa a los diagramas Entidad-Relación
- Los atributos que un E-R obviaba, aquí se especifican

![](img/Pasted%20image%2020231208121328.png)

### Matrices CRUD

- Relaciona acciones del sistema y datos para estudiar cuando estos se crean, leen, actualizan o eliminan (CRUD)

![](img/Pasted%20image%2020231208121454.png)

## Atributos de calidad

![](img/Pasted%20image%2020231208121528.png)

## Atributos de calidad internos vs externos

- **Externos**: características observadas durante la ejecución del sistema, que influencian al usuario y su experiencia.
- **Internos**: propiedades percibidas por el equipo técnico durante su interacción con el sistema, que pueden afectar indirectamente a los usuarios

![](img/Pasted%20image%2020231208121735.png)

## Disponibilidad

![](img/Pasted%20image%2020231208121818.png)

Ejemplo: *El sistema estará disponible un 99% del tiempo entre las 6.00 y las 24:00.*

## Fiabilidad

![](img/Pasted%20image%2020231208121904.png)

Ejemplo: *El tiempo medio entre fallos del subsistema X será de 42 días.*

## Instalabilidad

![](img/Pasted%20image%2020231208121948.png)

## Integridad

![](img/Pasted%20image%2020231208122016.png)

Ejemplo: *El sistema no redondeará el tiempo transcurrido desde el arranque del sistema al registrar el valor medido.*

## Interoperabilidad

![](img/Pasted%20image%2020231208122243.png)

Ejemplo: *El sistema podrá importar cualquier modelo 3D exportado de la herramienta Autodesk 3ds Max (versión 2021 o anterior).*

## Rendimiento

![](img/Pasted%20image%2020231208122329.png)

Ejemplo: *El sistema situará la placa giratoria en la posición indicada por el usuario en un máximo de TIEMPO_MAXIMO_GIRO segundos.*

## Robustez

![](img/Pasted%20image%2020231208122401.png)

Ejemplo: *Si el editor de imágenes se cierra antes de que el usuario guarde el archivo, la próxima vez que el usuario inicie el editor el sistema recuperará los contenidos del archivo de, como máximo, TIEMPO_MAXIMO_RECUPERACIÓN antes del fallo.*

## Seguridad (safety)

![](img/Pasted%20image%2020231208122435.png)

Ejemplo: *El sistema finalizará inmediatamente el proceso de radiación ionizante si detecta niveles de radiación anómalos.*

## Seguridad (security)

![](img/Pasted%20image%2020231208122525.png)

Ejemplo: *El sistema no permitirá a los usuarios reutilizar contraseñas que haya empleado previamente.*

## Usabilidad

![](img/Pasted%20image%2020231208122608.png)

Ejemplo: *Un usuario con, al menos, tres meses de experiencia será capaz de solicitar una miniatura en un tiempo medio de 5 minutos y un máximo de 10 minutos.*

## Eficiencia

![](img/Pasted%20image%2020231208122644.png)

Ejemplo: *El 33% de la memoria RAM disponible para el sistema se dejará libre durante los períodos de máxima carga previstos.*

## Escalabilidad

![](img/Pasted%20image%2020231208122720.png)

Ejemplo: *La capacidad del sistema debe ser capaz de incrementarse de 420 transacciones al día a 1500 transacciones al día en un máximo de 24 horas.*

## Modificabilidad

![](img/Pasted%20image%2020231208122812.png)

Ejemplo: *Un programador de mantenimiento con al menos un año de experiencia podrá modificar los algoritmos de cálculo de impuestos para adaptarlos a cambios en la normativa tributaria en un máximo de 10 horas de trabajo.*

## Portabilidad

![](img/Pasted%20image%2020231208122855.png)

Ejemplo: *El sistema permitirá importar las características del perfil entre IoS y Android.*

## Reusabilidad

![](img/Pasted%20image%2020231208122930.png)

Ejemplo: *Los algoritmos de cálculo de impuestos serán reusables en futuras aplicaciones de compra-venta.*

## Verificabilidad

![](img/Pasted%20image%2020231208123020.png)

Ejemplo: *La máxima complejidad ciclomáticade un módulo del sistema será de 21.*

# Tema 5. Especificación de Requisitos Software

## Estándar IEEE 830

![](img/Pasted%20image%2020231210172029.png)

## Cualidades deseables de los requisitos

- Según BABOK
	- Atómicos
	- Completos
	- Comprensibles
	- Consistentes
	- Factibles
	- No ambiguos
	- Priorizados
	- Verificables
- Según Hull
	- Abstractos
	- Atómicos
	- Claros
	- Factibles
	- Legales
	- Precisos
	- Únicos
	- Verificables
- Según Weagers y Beatty
	- Completos
	- Correctos
	- Consistentes
	- Factibles
	- Necesarios
	- No ambiguos
	- Priorizados
	- Verificables

# Tema 6. Validación de requisitos

## Validación

- Consiste en comprobar que los requisitos obtenidos son adecuados para construir un producto que satisfaga los requisitos de negocio

## Validación vs Verificación

- **Validación**: determinar si los requisitos satisfacen las necesidades de los stakeholders
- **Verificación**: determinar si los requisitos satisfacen los criterios de calidad

Primero se hace la verificación y después la validación

## Criterios de calidad

- Cada requisito individual debería ser:
	- Completo
	- Conciso
	- Correcto
	- No ambiguo
	- Factible
	- Necesario
	- Priorizado
	- Verificable
- El SRS en su conjunto debería de ser:
	- Completo
	- Consistente
	- Conforme a los estándares
	- No redundante
	- Organizado
	- Trazable

![](img/Pasted%20image%2020231216153543.png)

## Técnicas de validación y verificación

- Revisiones (importantes para la verificación)
- Generación de casos de prueba
- Prototipado
- Criterios de aceptación

## Revisiones 

![](img/Pasted%20image%2020231216153732.png)

## Revisiones formales

![](img/Pasted%20image%2020231216153810.png)

![](img/Pasted%20image%2020231216153825.png)

## Revisiones técnicas

![](img/Pasted%20image%2020231216153958.png)

## Revisiones: checklists

![](img/Pasted%20image%2020231216154059.png)

## Generación de casos de prueba

![](img/Pasted%20image%2020231216154304.png)

## Prototipado

![](img/Pasted%20image%2020231216154409.png)

![](img/Pasted%20image%2020231216154426.png)

![](img/Pasted%20image%2020231216154446.png)

![](img/Pasted%20image%2020231216154505.png)

## Criterios de aceptación

![](img/Pasted%20image%2020231216154556.png)

![](img/Pasted%20image%2020231216154624.png)

# Tema 7. Gestión de Requisitos

## Desarrollo y gestión de requisitos

![](img/Pasted%20image%2020231216154848.png)

## Gestión

![](img/Pasted%20image%2020231216155129.png)

## Línea base de requisitos

![](img/Pasted%20image%2020231216155334.png)

![](img/Pasted%20image%2020231216155401.png)

## Categorías del proceso de gestión

- Control de versiones
- Control de cambios
- Seguimiento del estado de los requisitos
- Trazado de los requisitos

## Control de versiones

![](img/Pasted%20image%2020231216155548.png)

## Seguimiento del estado de los requisitos

![](img/Pasted%20image%2020231216155633.png)

![](img/Pasted%20image%2020231216155719.png)

![](img/Pasted%20image%2020231216155736.png)

![](img/Pasted%20image%2020231216155803.png)

## Gestión de problemas

![](img/Pasted%20image%2020231216155843.png)

## Control de cambios

![](img/Pasted%20image%2020231216155919.png)

## Corrupción del alcance

![](img/Pasted%20image%2020231216160006.png)

![](img/Pasted%20image%2020231216160030.png)

![](img/Pasted%20image%2020231216160104.png)

## Política de control de cambios

![](img/Pasted%20image%2020231216160132.png)

## Proceso de control de cambios

![](img/Pasted%20image%2020231216160246.png)

## Comité de control de cambios

![](img/Pasted%20image%2020231216160322.png)

## Métrica de cambios

![](img/Pasted%20image%2020231216160423.png)

## Estabilidad de cambios

![](img/Pasted%20image%2020231216160511.png)

## Impacto de cambios

![](img/Pasted%20image%2020231216160758.png)

## Trazado de requisitos

![](img/Pasted%20image%2020231216160842.png)

![](img/Pasted%20image%2020231216160930.png)

![](img/Pasted%20image%2020231216161002.png)

# Tema 8. Ingeniería de requisitos en los Métodos Ágiles

## Métodos Ágiles

![](img/Pasted%20image%2020231216161724.png)

![](img/Pasted%20image%2020231216161745.png)

## Proceso de IR en metodologías ágiles

![](img/Pasted%20image%2020231216161830.png)

## Historias de Usuario

![](img/Pasted%20image%2020231216162406.png)

![](img/Pasted%20image%2020231216162432.png)

![](img/Pasted%20image%2020231216162524.png)

## Obtención 

![](img/Pasted%20image%2020231216162607.png)

## Análisis

![](img/Pasted%20image%2020231216162628.png)

![](img/Pasted%20image%2020231216162727.png)

## Especificación

![](img/Pasted%20image%2020231216162754.png)

![](img/Pasted%20image%2020231216162836.png)

![](img/Pasted%20image%2020231216163058.png)

## Validación

![](img/Pasted%20image%2020231216163146.png)

## Línea base

![](img/Pasted%20image%2020231216163219.png)

## Gestión

![](img/Pasted%20image%2020231216163251.png)

