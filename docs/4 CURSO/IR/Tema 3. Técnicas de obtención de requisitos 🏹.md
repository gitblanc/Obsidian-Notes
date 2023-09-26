# Introducción

La obtención abarca las actividades relativas al descubrimiento de requisitos:

- Identificar los tipos de usuarios y otros stakeholders.  
- Entender las tareas y objetivos de los usuarios y los objetivos de negocio relacionados.  
- Comunicación con los usuarios tipo para obtener sus necesidades y expectativas. 
- Comprender el contexto del producto.

# Tipos de stakeholders

Podemos clasificar los **stakeholders** en 3 niveles:
- **Externos** a la organización desarrolladora.
	- Usuarios, cliente, contratista, equipo legal, agencias gub., consultores, proveedores...
- **Organización** desarrolladora.
	- Director de desarrollo, márketing; equipos de ventas, producción, soporte, infraestructuras...
- **Equipo** del proyecto.
	- Jefe de proyecto, analistas, director de producto, arquitectos, QA, diseñadores, desarrolladores, administradores de BD, dueño del producto(PO).

- Es importante realizar una más clasificación detallada de los posibles usuarios del sistema

# Tipos de usuarios

Podemos clasificar de forma general a los usuarios en:
- Usuarios **deseados**. Aquellos mejor alineados con los objetivos de negocio.
- Usuarios **no deseados**. Aquellos que no deberían usar el producto por cuestiones legales o de seguridad.
	- Medidas a tomar: seguridad de accesos, roles de usuario, logs, antimalware.
- Usuarios **ignorados**. Pueden usar el producto, pero no son el objetivo.
- Usuarios **indirectos**. No usan el producto, pero acceden a sus datos o servicios a través de informes u otros medios.

## Subtipos de usuario

Debemos realizar una identificación más precisa de los tipos de usuarios. 
- ¿Quién espera el cliente que use el sistema?
- Identificar todos los tipos de usuario posibles. 
	- Acorde a las tareas que realizan.
	- A partir de casos de uso e historias de usuario. 
	- A partir de diagramas organizativos.
	- A partir de los ya identificados.
	- Not a: los usuarios pueden ser no humanos.
- Condensar grupos de usuarios con necesidades similares.

# Técnicas de obtención de requisitos

Las técnicas que estudiaremos son las siguientes:

- Entrevistas.  
- Talleres.  
- Grupos focales.  
- Observaciones.  
- Cuestionarios.  
- Análisis de interfaces.  
- Análisis de documentación.

# Entrevistas

- Técnica más habitual.  
- Individuales o en pequeños grupos.  
- Particularmente útiles en dominios desconocidos. 
- Suele haber mayor confianza entre interlocutores.
-  Puede ser:
	- Estructurada. Contenidos preparados con antelación; tratan temas concretos.
	- No estructurada. Interacción improv isada, al principio del proceso de obtención. Sin profundizar.

# Entrevistas (consejos)

- Establecer una relación.  
- Mantenerse fieles al tema.  
- Tener preguntas preparadas de antemano. 
- Sugerir ideas a los interlocutores.  
- Escuchar activamente.

# Entrevistas estructuradas
- Siguen preguntas preparadas de antemano para obtener una información concreta.
- Ventajas:  
	- Se obtiene información precisa y organizada acorde a unos temas. 
	- Fáciles de realizar y repetir.  
	- Fiables: suelen aportar resultados de interés.
- Inconvenientes:  
	- Evaluación limitada de los resultados obtenidos.  
	- Información precisa pero no particularmente detallada. 
	- Escasa flexibilidad.  
	- Requieren un tiempo significativo.

# Entrevistas semi-estruturadas
- Se sigue una estructura, pero con libertad para que el entrevistador se desvíe si es necesario.
- Ventajas:  
	- El entrevistador puede expandir una pregunta o explorar nuevas ideas. 
	- Flexibles pero guiadas.  
	- El formato de la pregunta depende del entrevistador.  
	- Se consigue información cualitativa.
- Inconvenientes:
	- Comparar respuestas a una misma pregunta puede ser complejo si se desarrollan distintamente.

# Entrevistas no estructuradas
- Conversación improvisada con el objeto de reunir información.
- Ventajas:  
	- Permite construir una relación amistosa con el entrevistado. 
	- Permite aclarar dudas y reformular preguntas.  
	- Extremadamente flexible.
- Inconvenientes:
	- Fiabilidad cuestionable: irregulares.
	- Ceñirse al objetivo puede ser difícil.
		- El entrevistador debe tener en mente en todo momento el propósito de la entrevista, así como las habilidades e intereses del entrevistado.

## Entrevistas. Tipos de preguntas

- **Abiertas**. El entrevistado tiene infinitas respuestas posibles. 
	- Proporcionan muchos detalles (relevantes... o no).  
	- Mayor espontaneidad y comodidad del entrevistado.  
	- Pueden arrojar luz sobre cuestiones inéditas.
	- Su abuso puede percibirse como ignorancia y/o inseguridad por parte del entrevistador.
	- ¿Qué opina acerca del sistema actual de la empresa?  
- **Cerradas**. El entrevistado tiene un no de respuestas finito.
	- Rápidas y directas.  
	- Facilitan la comparación entre entrevistados.  
	- Resultados precisos, pero de escaso detalle.  
	- No involucran al entrevistado.  
	- ¿Cuál es el no medio de transacciones que tienen lugar al día?

# Talleres

- Reunión estructurada en la que un grupo selecto de stakeholders y expertos definen, crean, refinan y cierran entregables que representan requisitos. (Gottesdiener 2002)
- Permiten obtener requisitos de múltiples stakeholders a la vez. 
	- Útiles para resolver desacuerdos entre stakeholders.
- También llamados Joint Application Design (JAD).

- Poseen un rol especial denominado facilitador.  
- Planifica el taller, escogiendo a sus integrantes y guiando el proceso.
- Esta labor suele recaer en el analista de negocio.  
- Es complicado facilitar, anotar los resultados y participar en la discusión para una sola persona.
	- Se suele emplear un escriba que se encargue de recoger los resultados.
	- Si el analista es inexperto, es recomendable que sólo participe como stakeholder y se emplee un facilitador externo.

## Talleres. Consejos

- Definir reglas básicas.
- Definir roles. Escritura, gestión del tiempo y del alcance, moderadores...
- Elaborar planificación.
- Ceñirse al alcance del proyecto. Cuidar el nivel de abstracción correspondiente a la fase.
- Capturar cuestiones de relevancia. Atributos de calidad, restricciones u otros RNF.
- Asignar un tiempo a cada tema.
- Grupos pequeños son preferibles. 
	- 6+ participantes puede resultar inmanejable.
	- Ceñirse a figuras clave: representante del producto, analista, desarrollador, usuarios clave, expertos en la materia... 
 - Procurar la participación de todos los integrantes.

# Grupos focales

- Grupo de usuarios representativos que aporta información e *ideas* sobre los requisitos de un producto.
- Permiten conocer las necesidades, preferencias y expectativas de los usuarios.
- Variantes:  
	- Múltiples grupos focales de usuarios del mismo tipo.  
	- Grupo focal con usuarios de todos los tipos relevantes.
- Requieren facilitación.  
	- La mayoría de los consejos aplicables a los talleres lo son también aquí.

# Observaciones

- En ocasiones, las descripciones de los usuarios no son suficientes para comprender las tareas que realizan.
- La observación de los usuarios en su entorno de trabajo puede aportar información útil.
- Consumen mucho tiempo...  
    - ... por lo que deberían emplearse en tareas importantes o de alto riesgo.
- Permiten identificar problemas a resolver, temas a profundizar y corroborar la información obtenida previamente.
- Pueden incluir interacción con el usuario.
- A tener en cuenta: **efecto Hawthorne** (la gente cuando está siendo estudiada suele actuar de forma distinta).

# Cuestionarios

- Permiten encuestar a grandes cantidades de usuarios sin interacción directa.
- Equivalentes a una entrevista estructurada escrita.  
- Pueden ser usados como entradas para técnicas más detalladas.
# Cuestionarios: consejos

- Usar preguntas abiertas o cerradas según los objetivos.  
- Las opciones de respuesta han de ser exclusivas y exhaustivas. 
- Escalas consistentes.  
- Probar el cuestionario antes de su uso.  
- No limitado de preguntas.

# Análisis de interfaces de sistema

- Estudio de los sistemas externos a los que deba conectarse nuestro producto.
- El objetivo es identificar funcionalidades en otros sistemas que impliquen requisitos en el sistema a construir.
	- Datos que se envían/reciben desde el sistema, formato y validación de aquellos...
- Los diagramas de contexto son un buen punto de partida.

# Análisis de interfaces de usuario

- Estudio de sistemas preexistentes (similares en su defecto) con el objeto de descubrir requisitos.
- Permite conocer las tareas habituales de los usuarios.
- *Cuidado: el sistema a construir no necesariamente ha de incluir toda la funcionalidad presente en otros sistemas relevantes.*

# Análisis de documentación

- Estudio de la documentación de sistemas preexistentes o similares. 
	- Especificaciones de requisitos.  
	- Procesos de negocio.  
	- Manuales de usuario.
	- Reseñas comparativas.
	- Incidencias y retroalimentación de los usuarios.
-  Pueden contener funcionalidad relevante (u obsoleta), restricciones de negocio, problemas frecuentes de los usuarios...

# ¿Cuándo es mejor emplear las técnicas?

![](./img/Pasted%20image%2020230926184106.png)

# Recomendaciones: preguntas

![](./img/Pasted%20image%2020230926184834.png)

![](./img/Pasted%20image%2020230926184851.png)

# Recomendaciones: uso de modelos

![](./img/Pasted%20image%2020230926184926.png)

# Recomendaciones: obtención

![](./img/Pasted%20image%2020230926185003.png)

# Final de la obtención

![](./img/Pasted%20image%2020230926185026.png)

---