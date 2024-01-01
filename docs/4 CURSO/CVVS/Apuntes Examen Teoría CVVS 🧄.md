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

![](./img/Pasted%20image%2020240101153753.png)

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
	 ![](./img/Pasted%20image%2020240101155834.png)

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
	
	  ![](./img/Pasted%20image%2020240101160844.png)
	  
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

![](./img/Pasted%20image%2020240101161554.png)

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

![](./img/Pasted%20image%2020240101162747.png)

## Función con Base de Datos

*Problema 3b: Se tiene un informe que muestra los clientes en la base de datos a los que se aplica algún descuento en las compras mediante tarjeta y el valor de éste. Los descuentos se determinan como se indica a continuación y son acumulables. Si el cliente acaba de abrir una cuenta de crédito obtiene el 15% de descuento en todas sus compras de hoy, si es un cliente habitual con tarjeta de fidelización obtiene un 10% de descuento. Si el cliente tiene un cupón de descuento obtiene el 20% de descuento (no acumulable con el descuento de nuevo cliente).*

- **Diseño**: igual que el anterior
- **Implementación**: esta vez sólo tenemos un caso de prueba (una tabla). De las clases de equivalencia se derivan filas de la BD, y no casos. El informe es la salida

![](./img/Pasted%20image%2020240101163121.png)

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

![](./img/Pasted%20image%2020240101163526.png)

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

![](./img/Pasted%20image%2020240101164406.png)

- Cuando hay interfaz de usuario
	- Probar las acciones que realiza
	- Que causan CAMBIOS en lo visualizado
	- Y posiblemente en la BD
- Muchas veces esto da lugar a casos de prueba compuestos de una serie de pasos relacionados unos con otros
- Script para ejecución manual:

![](./img/Pasted%20image%2020240101164612.png)

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

![](./img/Pasted%20image%2020240101165016.png)

![](./img/Pasted%20image%2020240101165118.png)

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

![](./img/Pasted%20image%2020240101165557.png)

- Expandiendo la Implementación y más concretamente los Casos de Prueba. Pueden clasificarse en:
	- **CP Lógico**: Describe en términos lógicos las circunstancias en las que se probará el comportamiento del sistema, incluyendo las situaciones a cubrir.
	- **CP Físico**: Elaboración concreta del caso lógico con todos los valores de las entradas, salidas y configuración del entorno.

- A partir de los CP se puede generar:
	- **Script para ejecución manual**: Descripción detallada de los CP para poder ejecutarlos de forma eficiente y simple: Documento, Excel...
	- **Script para ejecución automática**: Implementación en un programa o configuración de casos de prueba para ejecución utilizando una herramienta.

![](./img/Pasted%20image%2020240101165803.png)

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

