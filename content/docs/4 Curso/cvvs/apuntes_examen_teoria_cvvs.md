---
title: Apuntes Examen Teoría CVVS 🧄
---
# Conceptos

- **Calidad**: conseguir calidad implica:
	- El producto satisface los requisitos funcionales y de rendimiento (explícitos) y de calidad
	- Los requisitos corresponden a las necesidades del usuario
	- Habilidad de un producto de satisfacer las necesidades del u/c, expectativas o requisitos
- **Verificación**: confirmación de si se satisfacen los requisitos especificados
- **Validación**: se comprueba si la especificación se corresponde con las necesidades de clientes y usuarios finales

- Prueba: proceso de ejecutar un programa con intención de encontrar fallos. Conjunto de actividades que facilitan el descubrimiento y/o la evaluación de propiedades de test items. las pruebas pueden ser:
	- Según su ejecución:
		- Estáticas (no se ejecuta)
		- Dinámicas (se ejecuta)
	- Según su visibilidad de la estructura interna:
		- Caja negra (no visible)
		- Caja blanca (visible)

- **Error**: acción humana que produce un resultado incorrecto
- **Defecto**: manifestación de un error. Desperfecto en un componente/sistema que puede causar que el software no realice su función requerida
- **Fallo**: desviación en un componente o sistema respecto de su comportamiento esperado

![](img/Pasted%20image%2020240101153753.png)

- **Clase de equivalencia**: representa un conjunto de datos para los que se supone que el programa tiene un comportamiento similar

# Técnicas basadas en la Especificación. Parte 1

## Clases de equivalencia

- **Identificación de clases de equivalencia**:
	- Se examina cada condición de entrada (derivadas de las entradas)
	- Cada condición de entrada se divide en clases de equivalencia
		- Enumeraciones
		- Rangos
		- Valores lógicos
	- Si los elementos de una clase no se tratarán de la misma forma, dividir la clase en otra más pequeña (jerarquía de clases)

## Ejemplo de problema. Clases de equivalencia

*Un sistema determina el tipo de interés aplicable a un crédito en función del importe del principal. Para valores menores de 10.000 euros se aplica el 4%, para valores mayores de 50.000 euros se aplica el 1%, en el resto de casos se aplica el 2%. Si el titular de la inversión es menor de 21 años se le añade medio punto porcentual adicional.*

- **Condiciones de entrada**: importe del principal y edad
- **Clases de equivalencia**:
	- Importe del principal
		- Hasta 10.000
		- Entre 10.000 y 50.000
		- Más de 50.000
		- Importe negativo (inválido)
	- Edad
		- Menor de 21
		- Mayor o igual de 21
		- Negativa (inválida)

## Derivación de casos de prueba

- **Derivación de casos de prueba**:
	- Estrategia típica: *minimized approach* (minimizada)
		- Consiste en crear el menor número de casos que cubran las clases válidas
		- Habitualmente uno por cada una de las clases inválidas (para evitar enmascaramiento, *one-to-one approach*)
	- En el ejemplo anterior los casos de prueba son:
	 ![](img/Pasted%20image%2020240101155834.png)

- **Clases de equivalencia de las salidas**:
	- Complementan el análisis respecto de las entradas
	- Para el problema anterior serían: 1%, 1.5%, 2%, 2.5%, 4%, 4.5%
	- Si deseásemos más exhaustividad en los casos de prueba, habría que añadir esto

- Las condiciones de entrada **no son necesariamente los parámetros de un programa**
	- Las condiciones de entrada, y por tanto, las clases de equivalencia, vienen muchas veces determinadas por situaciones derivadas de **relaciones entre variables o parámetros**
	- *Ejemplo*: determinar si la posición de un objeto (dado por sus coordenadas) está dentro de u círculo determinado por su radio y centro (coordenadas)
		- Condiciones de entrada (clases válidas)  
			- Distancia del objeto al centro del círculo
		- Clases de equivalencia 
			- Distancia...
				- Menor que el radio (interior).
				- Mayor que el radio (exterior).

## Análisis de valores límite

- **Análisis de valores límite**
	- Utilizando valores límite se sitúan las pruebas en los extremos de las clases de equivalencia (denominado *2-way/2-value*)
	
	  ![](img/Pasted%20image%2020240101160844.png)
	  
	- Existe asimismo el 3-way, que establece 3 valores (el que marca la frontera, uno más y uno menos)
		- *Ejemplo*: 49.999,99; 10.000,00; 10.000,01
	- Se pueden incluir valores típicos que no estén en los extremos

## Estrategia de combinaciones de clases

- **Estrategia de combinaciones de clases**
	- Un paso más allá de la estrategia minimizada
	- Si tenemos las clases de equivalencia:
		- Modo
			- Toque
			- Mouse
		- Tipo de dispositivo de entrada
			- Con panel táctil
			- Sin panel táctil
	- Con la estrategia minimizada, se forman dos casos de prueba. Pero si no son suficientes (queremos probar todas las combinaciones modo-tipo), podemos optar por la combinada. Transformamos el diseño original en uno “jerárquico”. Clases de eq. combinadas:
		- Combinación tipo-modo.
			- Con panel táctil.
			     - Modo toque.
			    - Modo Mouse.      
			- Sin panel táctil.
			    - Modo toque.
			    - Modo Mouse.
	- De aquí se extraen 4 casos de prueba

![](img/Pasted%20image%2020240101161554.png)

# Técnicas basadas en la Especificación. Clases de Equivalencia. Parte 2

## Función Independiente. Ejemplo

*Problema 3a: Se tiene una función que determina el descuento a aplicar en las compras mediante tarjeta. Los descuentos se determinan como se indica a continuación y son acumulables: Si el cliente acaba de abrir una cuenta de crédito obtiene el 15% de descuento en todas sus compras de hoy, si es un cliente habitual con tarjeta de fidelización obtiene un 10% de descuento. Si el cliente tiene un cupón de descuento obtiene el 20% de descuento (no acumulable con el descuento de nuevo cliente).*

- **Diseño**
	- Entradas
		- Tipo de cliente
			- Nuevo
			- Existente
		- Cupón descuento
			- Si
			- No
		- Tarjeta de fidelización
			- Si
			- No
	- Salidas
		- Acumulación de descuentos
			- Se acumulan
			- No se acumulan
		- Descuento aplicado (%)
			- 0, 10, 15, 20

	- Con la estrategia combinada (combinaciones parciales), el diseño pasa a ser:
		- Nuevo cliente
			- Sin cupón ni tarjeta
			- Cupón de descuento
			- Tarjeta de fidelización (inválido)
		- Cliente existente
			- Sin cupón ni tarjeta
			- Cupón de descuento
			- Tarjeta de fidelización
- **Implementación**
	- Incluye casos de prueba y trazabilidad

![](img/Pasted%20image%2020240101162747.png)

## Función con Base de Datos

*Problema 3b: Se tiene un informe que muestra los clientes en la base de datos a los que se aplica algún descuento en las compras mediante tarjeta y el valor de éste. Los descuentos se determinan como se indica a continuación y son acumulables. Si el cliente acaba de abrir una cuenta de crédito obtiene el 15% de descuento en todas sus compras de hoy, si es un cliente habitual con tarjeta de fidelización obtiene un 10% de descuento. Si el cliente tiene un cupón de descuento obtiene el 20% de descuento (no acumulable con el descuento de nuevo cliente).*

- **Diseño**: igual que el anterior
- **Implementación**: esta vez sólo tenemos un caso de prueba (una tabla). De las clases de equivalencia se derivan filas de la BD, y no casos. El informe es la salida

![](img/Pasted%20image%2020240101163121.png)

## Función con Base de Datos y Parámetros

*Problema 3c: Se tiene un informe que muestra los clientes en la base de datos a los que se aplica algún descuento en las compras mediante tarjeta y el valor de éste. Los descuentos se determinan como se indica a continuación y son acumulables. Si el cliente acaba de abrir una cuenta de crédito obtiene el 15% de descuento en todas sus compras de hoy, si es un cliente habitual con tarjeta de fidelización obtiene un 10% de descuento. Si el cliente tiene un cupón de descuento obtiene el 20% de descuento (no acumulable con el descuento de nuevo cliente). El informe tiene un parámetro opcional (edad) que si está presente, oculta los resultados de aquellos con edad menor que la especificada*

- Diseño
	- Entradas.
		- Tipo de cliente. 
			- Nuevo.
			- Existente.
		- Cupón descuento.
			- Sí.
			- No.
		- Tarjeta de fidelización.
			- Sí.
			- No.
	- Entradas adicionales.
		- Filtro de Edad
			- No especificado.
			- Cliente filtrado.
			- Cliente no filtrado.
	- Salidas.
		- Acumulación de descuentos.
			- Se acumulan.
			- No se acumulan.
		- Descuento aplicado.
			- 0, 10, 15, 20.
- Implementación

![](img/Pasted%20image%2020240101163526.png)

Los parámetros que afectan a la salida generan ahora más de un caso de prueba. Concretamente, dos: uno sin especificar el parámetro: salida original; y otro con una edad indicada: aquellos clientes que superan el corte.

## Datos de prueba en Bases de datos

- Datos de prueba en Bases de datos
	- Cuando el programa procesa datos en una base de datos, los datos almacenados en ésta también se deben considerar como entrada (y salida)
		- Las situaciones a probar se representan:
			- Como filas en tablas de la base de datos
			- Como entradas adicionales (parámetros) -> Caso de Prueba
			- Varios casos de prueba pueden compartir la misma base de datos
		- Con frecuencia nos referimos a los datos de la base de datos como Datos de Prueba (Test Data), formando parte del estado inicial de las pruebas
		- Se reserva la palabra entrada para las entradas adicionales

## Prueba del interfaz de usuario. Ejercicio

*Problema 3d: Se tiene un informe que muestra los clientes en la base de datos a los que se aplica algún descuento en las compras mediante tarjeta y el valor de éste. Los descuentos se determinan como se indica a continuación y son acumulables. Si el cliente acaba de abrir una cuenta de crédito obtiene el 15% de descuento en todas sus compras de hoy, si es un cliente habitual con tarjeta de fidelización obtiene un 10% de descuento. Si el cliente tiene un cupón de descuento obtiene el 20% de descuento (no acumulable con el descuento de nuevo cliente). El informe tiene un parámetro opcional (edad) que si está presente, oculta los resultados de aquellos con edad menor que la especificada. Este parámetro es indicado desde la pantalla del usuario (se supone que ya está validado el formulario).*

Al diseño de las pruebas hemos de añadir una (condición de prueba?): 
- Acciones de Usuario.
	- Cambio Filtro Edad.
		- Se pone.
		- Se cambia valor.
		- Se quita.

![](img/Pasted%20image%2020240101164406.png)

- Cuando hay interfaz de usuario
	- Probar las acciones que realiza
	- Que causan CAMBIOS en lo visualizado
	- Y posiblemente en la BD
- Muchas veces esto da lugar a casos de prueba compuestos de una serie de pasos relacionados unos con otros
- Script para ejecución manual:

![](img/Pasted%20image%2020240101164612.png)

- No abusar de casos de prueba con demasiados pasos

## Automatización con Spring Boot

## Prueba Unitaria del Repositorio

Se prueba realizar operaciones en un repo cuyo contenido cargamos automáticamente, tales como consultas sin o con parámetros; cuyo resultado comparamos con el contenido esperado. Los test parametrizados indican los valores esperados como un parámetro (etiqueta JPA), en lugar de en el equals.

## Prueba Unitaria con Mocks

- Se emplea en dos casos típicos:
	- El servicio externo todavía no está implementado.
	- Como parte de la funcionalidad está en un servicio externo, queremos independizarnos de éste y probar la lógica de negocio de forma unitaria.
- Como ejemplo, supongamos una funcionalidad adicional:
	- Mostrar la lista de *clientes que tienen alguna promoción aplicable*, junto con el código.
		- Las promociones dependen del país (atributo del cliente).
		- Los códigos de promociones aplicables a cada país se almacenan y gestionan en un microservicio externo al que se accede mediante un API REST.

![](img/Pasted%20image%2020240101165016.png)

![](img/Pasted%20image%2020240101165118.png)

## Prueba de un servicio REST

Accede directamente a la dirección del API, indicando que los datos son JSON. Hay distintas formas de comprobar los datos devueltos: Status devuelto (200), comprobaciones de tamaño o de contenido en fragmentos... O comparar directamente el contenido del JSON devuelto.

## Prueba unitaria de un controlador web

Probar un controlador de forma independiente si tiene una lógica compleja que no se probará desde IU Emplea una configuración similar al REST, pero sin especificar contexto (sólo se prueba el controlador) y sin TestPropertySource (se prueba sin BD). Comprueba el contenido de todos los objetos usando matchers. Se prueban GET y POST.

## Prueba de integración con el IU

Se emplea Selenium. Se despliega un servidor Tomcat. Se crea una BD limpia y se abre el navegador. Tras finalizar las pruebas, se cierra el navegador y se finaliza sesión del driver (quit).

La inicialización consiste siempre en obtener instancia del driver (iniciar sesión) y navegar a la página. Dado que los pasos son similares, se implementa un método común (doStep). Se puede asimismo realizar capturas de pantalla o leer todo el contenido de una tabla.

## Resumen

1. **Definir lo que hay que probar**: Condiciones de prueba de entrada/salida. Se derivan sus Clases de Equivalencia y Valores Límite (si es aplicable).
2. Posible transformación mediante **estrategia de combinación**. Puede haberse pensado así directamente.
3. **Diseño**: definir lo que se va a probar. Estructura jerárquica con las situaciones a cubrir.
4. **Implementación**: de qué forma se organizará la prueba. Derivar casos de prueba -los menos posibles- para cubrir todas las situaciones.
5. **Trazabilidad**: qué situaciones son ejercitadas por cada caso de prueba.

![](img/Pasted%20image%2020240101165557.png)

- Expandiendo la Implementación y más concretamente los Casos de Prueba. Pueden clasificarse en:
	- **CP Lógico**: Describe en términos lógicos las circunstancias en las que se probará el comportamiento del sistema, incluyendo las situaciones a cubrir.
	- **CP Físico**: Elaboración concreta del caso lógico con todos los valores de las entradas, salidas y configuración del entorno.

- A partir de los CP se puede generar:
	- **Script para ejecución manual**: Descripción detallada de los CP para poder ejecutarlos de forma eficiente y simple: Documento, Excel...
	- **Script para ejecución automática**: Implementación en un programa o configuración de casos de prueba para ejecución utilizando una herramienta.

![](img/Pasted%20image%2020240101165803.png)

- Técnicas básicas e intuitivas. Proceso:
	- Determinar las condiciones de prueba para entradas. Completar con salidas.
	- Determinar y aplicar técnicas para determinar las situaciones a cubrir (test coverage items).
	- Decidir si algunas situaciones a cubrir se han de combinar. Compromiso coste/beneficio.
	- Partiendo de las situaciones, derivar los casos de prueba.  
	- Al ejecutar los CP, comparar lo que cambia y lo que no debería cambiar (incluyendo actualizaciones de BD). 
- Notas:
	- Cuando hay BD, algunas situaciones a probar se representan como filas en la BD.
	- Cuando hay IU puede haber CP compuestos por varios pasos (no abusar).  
	- En general, No situaciones > no casos > no BD.

# Técnicas basadas en la estructura. Condiciones

- Utiliza la estructura de las decisiones lógicas que se definen explícita o implícitamente en la especificación
	- Elementos básicos:
		- Condición: Expresión lógica primitiva, sin operadores lógicos (A>B).
		- Decisión: Expresión lógica compuesta por varias (o una) condiciones (ej. A>B AND C>D)

## Ejemplo de Prueba de Decisiones y Prueba de Condiciones

*Problema 1: La remuneración especial de las cuentas corrientes (que ofrece un tipo de interés superior al habitual) se aplica solamente cuando se ha mantenido la cuenta abierta al menos dos años a los clientes menores de 21 años y a los que han mantenido un saldo medio anual como mínimo de 50K euros durante el último año*

- Cuál es la decisión y las condiciones?

- **Prueba de decisiones**
	- Derivamos situaciones a cubrir de modo que cada decisión tome valores V y F

![](img/Pasted%20image%2020240101174054.png)

- **Prueba de condiciones**
	- Derivamos situaciones a cubrir de forma que cada condición tome los valores V y F

![](img/Pasted%20image%2020240101174305.png)

- Prueba de Decisión/Condición
	- Derivamos pruebas de modo que cada decisión y condición tome los valores V y F

![](img/Pasted%20image%2020240101174616.png)

## Prueba de múltiple condición

Derivamos pruebas de modo que se ejercite cada una de las combinaciones lógicas de las condiciones. Tiene un crecimiento exponencial: 8 combinaciones para 3 condiciones, 16, 32...

## Prueba de Condición/Decisión Modificada (MCDC)

Derivamos situaciones a cubrir de forma que cada condición afecta de forma independiente al resultado de la decisión. *Variar cada condición manteniendo inalteradas al resto*

![](img/Pasted%20image%2020240101174854.png)

## Variantes de MCDC

Habitualmente, de n condiciones resultan n+1 combinaciones. Pero a veces, si existen variables que estén en varias condiciones, es difícil de conseguir.
- Unique Cause MCDC. Ejemplo anterior. 1 y 4 mantienen los valores de las 2 primeras condiciones, la salida cambia al cambiar la tercera condición.
- Masking MCDC. Relaja el requisito, sólo requiere que las subexpresiones mantengan el valor. Ej: 1 con 4, 4’, 4’’ cumplen Masking; en todas e<21 OR s>=50 es TRUE.

![](img/Pasted%20image%2020240101175429.png)

## Masking MCDC

Usar cuando no es posible mantener Unique Cause. Por defecto, al hablar de MCDC nos referimos a Unique-Cause.

![](img/Pasted%20image%2020240101175533.png)

## Pruebas Negativas

Ver si hace lo que no debería hacer. Ejercitar la funcionalidad que trata con fallos/rechazo de entradas, excepciones, etc. Incluir pruebas/valores/condiciones para determinar valores que NO influyen en la salida.

![](img/Pasted%20image%2020240101175650.png)

## Resumen

-  Aplicar valores límite en las condiciones cuando sea posible.
- Grandes grupos de técnicas de prueba.
	- Basadas en la especificación. (P.e. partición en clases de eq.)
	-  Basadas en la estructura. (P.e. basadas en condiciones).
- Tradicionalmente denominadas como:
	- Basadas en la estructura. Técnicas de caja blanca. INCORRECTO.
	- Basadas en la especificación. Técnicas de caja negra.
	- Conceptos ortogonales. Tipo de técnica vs caja blanca/negra.
- Independientemente de la técnica, lo habitual será partir de la especificación.
- La prueba se realiza ejecutando casos de prueba (test cases).
- Hay que determinar qué es lo que hay que probar (test conditions) y qué situaciones se probarán (test coverage items) apoyándose en el uso de técnicas de prueba.
- La cobertura es el porcentaje de situaciones cubiertas por los CP.

![](img/Pasted%20image%2020240101175900.png)

# Técnicas basadas en la Especificación. Caminos y transiciones

## State Transition Testing

*Problema 1: En un sistema de compra online cuando un cliente selecciona un item para añadir al carrito de la compra, se debe comprobar si existe ya un carrito asociado al cliente, creándose uno nuevo en caso contrario. En cualquier caso se añadirá el nuevo item al carrito. A continuación el cliente decidirá si acepta éste, en cuyo caso el proceso de compra continuará, o si cancela la operación.*

- Qué decisiones o clases de equivalencia se pueden determinar? 
- Qué casos de prueba se pueden realizar?

## Pruebas de Caminos Simples

![](img/Pasted%20image%2020240101211722.png)

![](img/Pasted%20image%2020240101211827.png)

## Pruebas de Caminos Pares

![](img/Pasted%20image%2020240101211929.png)

![](img/Pasted%20image%2020240101211947.png)

## Modelo

- Diferentes formas de modelar la especificación
	- Estados
	- Actividades
	- Diagrama de flujo
- Aplicable en ámbitos diferentes
	- Formularios y navegación
	- Sistemas de control
	- Procesos de negocio
- En cualquier caso, el modelo identificará:
	- Estados/actividades
	- Transiciones/caminos/flujos
	- Condiciones/acciones (si aplicable)

## Combinaciones con otras técnicas

![](img/Pasted%20image%2020240101212218.png)

![](img/Pasted%20image%2020240101212240.png)

## Pruebas negativas

![](img/Pasted%20image%2020240101212344.png)

![](img/Pasted%20image%2020240101212404.png)

![](img/Pasted%20image%2020240101212440.png)

![](img/Pasted%20image%2020240101212502.png)

## Pruebas basadas en escenarios

- Modelo de las secuencias de interacciones del objeto de prueba y otros sistemas o usuarios
	- Escenario principal: secuencia típica
	- Escenarios alternativos
- Forma típica de prueba de escenarios: prueba de casos de uso

## Pruebas del interfaz de usuario

- El interfaz o parte se puede modelar como estados y transiciones
	- En una única pantalla
	- En la navegación entre varias pantallas
- En el problema anterior

![](img/Pasted%20image%2020240101212829.png)

![](img/Pasted%20image%2020240101212850.png)

## Resumen

- Diferentes intensidades (Test completion criteria) según ISO 29119:
	- Estados: Cubrir todos los del modelo.
	- Transiciones (0switch-coverage): Cubrir todas las transiciones válidas.
	- Pares de transiciones (1switch-coverage): Cubrir todos los pares de transiciones secuenciales válidas en el modelo.
	 - N-switch coverage: cubrir N+1 transiciones secuenciales válidas.
	- All transitions: Cubrir toda transición, válida e inválida.
- Caso de prueba contiene:
	- Estado inicial: Carrito con 1 producto.
	- Secuencia de pasos: Entradas + salidas esperadas.
- Múltiples denominaciones: caminos/transición de estados.
	- Múltiples formas de modelar: Diagramas de flujo, de procesos, transiciones...
	- Diferentes niveles de detalle: Proceso negocio, caso de uso, estados de objeto...
- Combinable con otras técnicas (condiciones).
- Incluir también pruebas negativas.

# Técnicas basadas en la Especificación: Clases de Equivalencia. Parte 3. Otras técnicas y combinatoria

## Each Choice

![](img/Pasted%20image%2020240102125334.png)

## Multiple Combination

![](img/Pasted%20image%2020240102125403.png)

## Base Choice

![](img/Pasted%20image%2020240102125437.png)

## Combinaciones parciales

![](img/Pasted%20image%2020240102125513.png)

## Combinaciones con Tablas de Decisión

![](img/Pasted%20image%2020240102125636.png)

- Útiles para probar reglas de negocio complejas en función de combinaciones de diferentes valores
- Cada regla será una situación a cubrir (test coverage item)
- Tabla de decisión para el problema anterior:

![](img/Pasted%20image%2020240102125911.png)

- Cada condición no es necesariamente binaria: En problema 1b de parte 1 (interés crédito-importe ppal.+edad) si contemplamos clases para entradas y salidas
- Realizamos una combinación completa de las clases para entradas
- Tabla de decisión (incluyendo sólo clases válidas)

![](img/Pasted%20image%2020240102130215.png)

## Árbol de clasificación

- El problema de las tablas de decisiones es que se hacen muy grandes cuando hay muchas reglas
- Elementos de un Classification Tree Method (CT):
	- Clasificaciones
	- Clases
	- Casos (Test Coverage Items)
	- Cómo combinar
		- Mínima
		- Máxima (foto de abajo)
- Es muy útil cuando hay muchas entradas

![](img/Pasted%20image%2020240102130525.png)

- Ejemplo reserva de vuelos

![](img/Pasted%20image%2020240102130654.png)

![](img/Pasted%20image%2020240102130722.png)

![](img/Pasted%20image%2020240102130848.png)

**Técnicas combinatorias**  
- En general tenemos pares P-V (Parámetro condición, clasificación; valor clase, VL)
	- Each Choice/1-wise (mínima): cada V es probado al menos una vez.
	- Base Choice: para cada P se elige un V (base). Formar combinaciones donde todos los P - 1 permanecen en su valor base.
	- Pair-wise: para cada par de condiciones, deben aparecer todas las posibles combinaciones de sus valores. Reduce significativamente las combinaciones.
	- N-wise: generalización.
	-  All combinations: cada combinación P-V es probada.

![](img/Pasted%20image%2020240102131054.png)

## Combinaciones Pair-Wise

- Cada valor de cada parámetro se ha combinado con todos los valores del resto de parámetro.
- Combinación muy compleja, detecta problemas debidos a influencia de parejas de parámetro.

![](img/Pasted%20image%2020240102131220.png)

![](img/Pasted%20image%2020240102131251.png)

## Resumen

- Técnica básica: clases de equivalencia. Derivadas:
	- Valores Límite. Tablas de decisión.
	- Árbol de clasificación: jerarquizar lo anterior.
	- Combinatorias: cómo combinar lo anterior.
- Test Conditions: condiciones de entrada/salida, lo que hay que probar.
- Test Coverage Items: situaciones a cubrir, lo que se va a probar.
	- Clases o valores límite.
	- Si combinamos dentro de la jerarquía, dichas combinaciones. 
- Cobertura.
	- Cuántas de las situaciones definidas se han probado. 
- Habilidad del Tester.
	- Determinar las test conditions, técnicas y método de combinación a aplicar en el contexto de cada problema (coste/beneficio).

## Validación de Datos

- Clave: separar el proceso de negocio del interfaz.
	- Pruebas para el procesamiento. 
		- Tener en cuenta valores límite.
	- Pruebas para la validación de datos. 
		- Típicamente se usarán clases de equivalencia.
- Algunas clases de equivalencia típicas para la validación.
	- Presencia/ausencia de valor.
	- Contenido.
		- Rangos permitidos/no permitidos
		- Formatos inválidos.
	- Datos/opciones visibles/invisibles según estado de formulario.
	- Cambios en listas de selección.

Por ejemplo:  
- Importe (numérico)
	- Campo vacío (inválida).
	- Negativo/Cero/Valor muy grande (inválido)
	- Sin/con decimales...
	- Separador de millares convenio inglés (inválido)
	- Texto (inválida)
- Fecha
	- Campo vacío.
	- Muy antigua/futura (inválida)
	- Separadores de fecha.
	- Fechas tipo dd-mm y mm-dd.
	- Valores alfabéticos válidos e inválidos.
	- Número, texto (inválida).

# Pruebas en el Contexto de un Proyecto

## Técnicas estáticas

- El testing puede ser:
	- Dinámico: requiere la ejecución del software
	- Estático: no requiere la ejecución del software
		- Pueden realizarse muy pronto
		- Detección temprana de defectos: reducción coste
- Dos grandes grupos de testing estático
	- Revisiones
	- Análisis estático

## Técnicas estáticas. Revisiones

- Tipos de revisiones
	- **Revisión de gestión** (Management Review): monitorización de progreso, estado de planes, etc
	- **Recorrido** (Walkthrough): presentación del documento por parte del autor para obtener un conocimiento común, comentarios...
	- **Revisión técnica** (Technical Review): discusión detallada para determinar consenso/discrepancias en los contenidos técnicos
	- **Inspección** (Inspection): la más formal, con un procedimiento muy definido para detectar defectos
	- **Auditoría** (Audit): independiente, para determinar conformidad con especificaciones, estándares u otros criterios
- **Peer review** (revisión por pares): revisión por pares
- **Revisión formal**, actividades típicas:
	- Planificación. Asignación de moderador, chequeo inicial.
	- Kick-off meeting. Introducir objetivos de la revisión y objeto a revisar.
	- Preparación. Individual: detección de defectos, preguntas...
	- Reunión de revisión. Exposición de defectos encontrados y clasificación.
	- Rework. Mejorar el objeto de revisión.
	- Follow up. Confirmación de que las acciones a tomar lo han sido.
- **Herramientas**
	- Proceso manual, soportado por procesadores de texto
	- Para la revisión de código, típicamente los Pull Requests de repositorios

## Técnicas estáticas. Revisiones en Pull Request con forked repo

## Análisis estático

- Analizar artefactos para buscar defectos 
	- Mediante herramientas automáticas 
	- Muchas veces antes de las revisiones realizadas manualmente 
	- Comprobación de requisitos y trazabilidad, estándares de codificación, métricas de código o estructura de código, vulnerabilidades… 
- Ejemplos de herramientas: 
	- Calidad del Código: SonarQube 
	- Vulnerabilidades en dependencias: OWASP Dependency Check 
	- Herramientas incluidas en los repositorios Git

## Modelo en V

![](img/Pasted%20image%2020240102134909.png)

## Niveles y Tipos de Prueba

- **Nivel de prueba**: grupo de actividades de prueba organizadas y gestionadas en conjunto
	- *Ej: integración, sistema, aceptación*
- **Tipo de prueba**: grupo de actividades de prueba para un componente o sistema enfocadas en un objetivo específico de prueba
	- Un tipo de prueba puede usarse en uno o más niveles de prueba
	- Característica de calidad. *Ej: funcional, rendimiento...*
	- Relativo a cambios. Ej: *regresión*

![](img/Pasted%20image%2020240102135234.png)

## Niveles de prueba

- **Componentes**: por separado, principalmente funcionalidad
- **Integración**: interfaces entre componentes, interacciones con otras partes del sistema
	- A nivel de componentes
	- A nivel de sistema
- **Sistema**: comportamiento del sistema/producto global, funcional y no funcional, suele ser el último paso de verificación
- **Aceptación**: determinar si el sistema está listo para ser liberado (validación)
	- Aceptación de usuario: principalmente funcional
	- Aceptación operacional: recuperación de desastres, tareas de mantenimiento...
	- FAT (Factory Acceptance Testing) y SAT (Site Acceptance Testing)
	- En COTS: alpha/beta

## Tipos de prueba

-  Funcionales.
- No funcionales. Otros atributos de calidad.
	-  Interoperabilidad.
	-  Seguridad.
	-  Rendimiento. Carga esperada, estrés del sistema.
	- Usabilidad, Accesibilidad.
	- Fiabilidad.
	- Eficiencia.
	- Portabilidad.
- Relativas a cambios.
	- Confirmación. Retest. Defectos han sido solucionados.
	- Regresión. Los cambios no han afectado a otras partes.

## Pirámide de test

Concepto de Mike Cohn, referido a los tests automatizados: *es una metáfora que nos indica agrupar pruebas de software en cubos de diferente granularidad. Da una idea del no de pruebas en cada grupo.*

![](img/Pasted%20image%2020240102140011.png)

Diferentes formas, mezclando en cada capa de la pirámide:
- Niveles de prueba.
- Tipos de prueba.
- Grado de automatización.
No olvidar que tipo, nivel, grado de automatización son conceptos ortogonales.

![](img/Pasted%20image%2020240102140107.png)

Cuando la pirámide no se aplica correctamente. Se entiende como un concepto físico: no se prueba nada en una capa hasta que la anterior esté completa.

## Pruebas de rendimiento

- Planificación y Análisis
	- Infraestructura (sistema y herramientas) y objetivos de la prueba:
		- Límites del sistema (aumentar usuarios hasta saturación/fallo)
		- Carga (a porcentajes dados del límite)
		- Estrés (ej: aumento muy rápido de usuarios)
	- Determinar principales funcionalidades y escenarios a probar
- Diseño e implementación
	- Definir número de Usuarios, ritmo de entrada, tiempo de espera entre cada acción 
	- Establecer escenarios combinados con los parámetros anteriores
	- Registrar sesiones con un usuario
	- Crear scripts para ejecución automática para varios usuarios y carga
- Ejecución
	- Introducir carga en el sistema, no olvidar volumen de datos
	- Medir: tiempos de respuesta, memoria, cursores abiertos y errores producidos

## Procesos genéricos

- Planificación
	- Priorizar y estimar
	- Realizar plan
- Preparación
	- Diseño e implementación
- Realización
	- Ejecución
	- Reporting
- Monitorización y Control
	- Medir
	- Aplicar acciones

## Plan de pruebas

- Resumen:
	- Contexto de la prueba: identificar el proyecto y las partes interesadas, test ítems y características a ser probadas
	- Comunicación entre testing y resto de organización
	- Riesgos (de producto y de proyecto)
	- Estrategia de prueba
		- Niveles y tipos de prueba que realizarán, entregables, técnicas a utilizar, criterios de finalización, métricas
		- Requisitos del entorno de test y de los datos
		- Pruebas de regresión y retest. Criterios de suspensión/reanudación
	- Actividades de prueba, estimaciones, personal, necesidades de formación y contratación
	- Planificación temporal

## Reporting - Proceso

- Para cada problema detectado:
	- Ejecutar y anotar resultado provisional (pasa, falla y lo que se observa)
	- Verificar qué es realmente un fallo, reproducir, aislar
	- Incorporar información útil para resolución
	- Comprobar duplicados. No perder credibilidad
	- Determinar causa probable (aplicación, especificación, entorno de prueba)
	- Determinar severidad provisional, título (impacto sobre todo el sistema)
- Otras pruebas
	- Anotar fallos no buscados explícitamente
	- Explorar con más detalle las zonas problemáticas
- Revisar resultados (completitud y precisión) e informar (reporting)

- El reporte incluye:
	- Su último objetivo es que los problemas se solucionen. Hay que vender el report (Bug advocacy)
	- Título corto
	- Resumen conciso del problema
	- Detalles sobre el proceso llevado a cabo para reproducir el problema y lo que se observa  frente a lo que debería.
	- Máxima información con mínimas palabras
	- Información adicional (configuración, datos para reproducción, volcados...)
	- Nunca usar genericidades como "no funciona", porque podemos obtener respuestas como "a mí si"

## Ejemplo Reporting

![](img/Pasted%20image%2020240104170153.png)

## Medición

- Monitorizar el progreso de las actividades de prueba
	- Realimentación de lo que está ocurriendo
	- Visibilidad sobre los resultados de pruebas
	- Obtener información para estimaciones futuras
- Mediciones
	- Progreso de las actividades de pruebas
	- Progreso de la cobertura de los requisitos por las pruebas
	- Evolución de los resultados de las pruebas
	- Defectos encontrados/solucionados
	- Casos de prueba planificados/ejecutados con sus resultados
- Cobertura es siempre RELATIVO a algo (requisitos, situaciones a cubrir, líneas de código...)

## Notas sobre documentación

- El plan de pruebas no es una lista de casos de prueba
	- Hay que decidir qué es lo más prioritario
	- Incluir los objetos de la prueba con niveles y tipos aplicables
	- Indicar qué pruebas se automatizarán y con qué herramientas
	- No se trata de teorizar sobre las pruebas, sino describir las pruebas que se han realizado
- No dejar las pruebas para el final
	- En pruebas funcionales, es más importante un diseño de las situaciones a cubrir/probar que una lista de casos de prueba inefectivos
	- Las pruebas automatizadas con JUnit deben autodocumentarse, salvo casos excepcionales

# El nuevo estándar internacional para pruebas de software

## Estándares

Conjunto de requisitos de obligado cumplimiento establecidos por consenso y
mantenido por un organismo reconocido para prescribir un uniforme disciplinado
abordar o especificar un producto, es decir, convenciones obligatorias y
prácticas

## Problemas de los estándares

- Definiciones en conflicto, procesos y procedimientos

## ¿Qué estándar seguir?

- ISO/IEC/IEEE 29119

![](img/Pasted%20image%2020240104171838.png)

## Modelo de Procesos de pruebas

![](img/Pasted%20image%2020240104171929.png)

## Especificación pruebas de la organización

![](img/Pasted%20image%2020240104172022.png)

## Procesos de Gestión

![](img/Pasted%20image%2020240104172048.png)

## Documentación

- Define plantillas que pueden ser utilizadas para generar documentación
- Versiones diferentes para proyectos ágiles y tradicionales
- Mapeo a otros estándares

## Clasificación de las técnicas de diseño de las pruebas

![](img/Pasted%20image%2020240104172249.png)

![](img/Pasted%20image%2020240104172329.png)

## Medición de la cobertura alcanzada

![](img/Pasted%20image%2020240104172357.png)

# Pruebas en entornos ágiles

## Proceso general

![](img/Pasted%20image%2020240104174415.png)

![](img/Pasted%20image%2020240104174434.png)

## Múltiples dimensiones

![](img/Pasted%20image%2020240104174519.png)

## Niveles de prueba

- Organizadas y gestionadas en conjunto
	- **Unitarias/componentes**: por separado, principalmente funcionalidad
	- **Integración**: interfaces entre componentes, interacciones con otras partes del sistema
	- **Sistema**: comportamiento del sistema/producto global, funcional y no funcional
	- **Aceptación**: determinar si el sistema está listo para ser liberado

## Tipos de pruebas

- **Funcionales**
- **No funcionales**
	- Interoperabilidad
	- Seguridad
	- Rendimiento
	- ...
- **Relativas a cambios**
	- Confirmación (retest): defectos han sido solucionados
	- Regresión: los cambios no han afectado a otras partes

## Técnicas

![](img/Pasted%20image%2020240104175005.png)

## Scripted testing

- Las acciones a realizar por el tester son prescritas en el caso de prueba. Separación clara entre
	- Preparación (diseño e implementación)
	- Ejecución
- Requiere tener claros los requisitos/criterios de aceptación
- Diferencias en escala temporal
	- No Agile. Ejecución distante de preparación.
	- Agile. Ejecución cercana de preparación.
- Script
	- Para ejecución automática

## Pruebas exploratorias

- Diseño, ejecución y aprendizaje simultáneo
	- Planificación previa (test charter): declaración breve del alcance y objetivos para una prueba en una ventana de tiempo limitado
	- Diseño y ejecución se realizan en paralelo
		- Se profundiza en el conocimiento del sistema según se ejecuta
		- Se aplican técnicas, aunque no siempre se documenta
		- Se registra lo que se prueba y los problemas encontrados
	- Otros aspectos
		- No es test ad-hoc o improvisado
		- Necesita personal muy experimentado
		- Session-Based Testing: Más estructurado

## Desarrollo Dirigido por las Pruebas

- TDD (Test Driven Development)
	- Definir las pruebas antes de codificar
	- Incremental al extremo
- Características
	- Requiere disciplina
	- Requiere automatización
	- Muy útil para mejorar la calidad de los programas

## Desarrollo dirigido por el comportamiento

- BDD Behaviour Driven Development
	- Similar a TDD, pero las pruebas son de más alto nivel
	- Definir el comportamiento deseado que se traduce a pruebas ejecutables
	- Lenguaje cercano al cliente
		- Facilita colaboración
		- Casos de prueba autodocumentados
		- Dudosa efectividad si no se colabora con el cliente
	- Las pruebas siguen un patrón: Dado... Cuando... Entonces...
- Cucumber/Gherkin (herramientas)

## Cucumber. Herramienta BDD

![](img/Pasted%20image%2020240104180119.png)

![](img/Pasted%20image%2020240104180214.png)

## ¿Quién hace las pruebas?

- Papel del tester:
	- Habilidades diferentes de las del programador
	- Centrado en asegurar que se entrega el producto con la calidad que precisan los usuarios
	- Añadir valor al equipo
- Diferentes modelos
	- Solo programador + usuario/cliente
	- + Tester (a tiempo parcial)
	- + Tester(s) (a tiempo completo)
	- Equipo especializado
- Ideal: el tester es uno más del equipo de desarrollo

## "The Three Amigos"

- Son reuniones entre:
	- Analista de Negocio y/o Dueño del Producto
	- Desarrollador(es)
	- Tester(s)
- Objetivo relacionado con la planificación del sprint, pero grupo pequeño y bajo demanda. Más Kanban que Scrum
	- Discutir características nuevas y revisar la especificación
	- Entendimiento y vocabulario compartido
	- Identificación de requisitos no definidos y definición de pruebas
	- Antes de que la característica se considere lista para el desarrollo y asignada en un sprint

## ¿Cuándo se hacen las pruebas?

![](img/Pasted%20image%2020240104180813.png)

- **Release Planning**
	- Aunque no se pueda planificar con gran precisión, hay que dimensionar recursos y plazos
	- Preparar un plan de pruebas
		- Riesgos, estrategia (tipos y niveles, enfoques para mitigarlos), requisitos de documentación
		- Grado de automatización, entorno(s), datos, herramientas
		- Recursos, reporting, métricas
		- Story/task board: ej. por hacer, desarrollo, testing, hecho
		- Brevedad y concisión
- **Sprint Planning**:
	- Definir ejemplos y a escribir las historias con sus criterios de aceptación
	- Dimensionar las historias (no olvidar el esfuerzo necesario para las pruebas)
	- Otros aspectos: integración, impacto en el sistema
	- Y posiblemente comenzar a diseñar las pruebas de las historias
	- Nota: criterio de aceptación != test de aceptación
- **Dentro del Sprint (unitario, componente)**:
	- Test unitario
	- Test de historias
		- Confirmar el comportamiento del sistema a alto nivel
		- Tester ayuda o realiza
		- Automatizados si es posible, ejercitar lógica de negocio
		- No son los únicos test de aceptación
- **Dentro del sprint, más allá de una historia individual (sistema, integración, aceptación)**:
	- Test exploratorio: tester
	- Test de escenarios complejos, workflows
	- Aceptación de usuario: el usuario
	- Otros test de sistema, no funcionales: tester, equipo especializado
	- Tareas o historias "técnicas" específicas
- **Antes de la entrega de la release**:
	- Muchos test ya se han ejecutado (regresión)
	- Puede ser necesario incluir sprints adicionales
		- Test de sistema (funcionales y no funcionales)
		- Integraciones
		- Conversión/actualización de datos
		- Aceptación de Usuario
		- Rework y retest
	- Cuanto mejores pruebas se realicen en los sprints de desarrollo, menos será necesario aquí

## Conclusión

- Las pruebas son **parte integral** del proceso de desarrollo ágil
- Considerar las pruebas desde un **punto de vista global** (no solo unitarias y de componentes o historias)
- La inclusión de testers aporta gran **valor añadido** al integrarse en el equipo
- Automatizar la ejecución de pruebas valorando la relación **coste/beneficio**
- Adaptarse al **contexto**. Cada organización y proyecto tiene sus particularidades y necesidades
- Pruebas **efectivas** y **eficientes**

