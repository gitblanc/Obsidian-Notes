- Soy del grupo 1

- Me toca: **Escenario de matrícula ordinaria y generación de lotes**

- Hay que realizar una combinación entre **clases de equivalencia** y **valores límite**

# Matrícula ordinaria

**Objetivo**: matricular a un alumno en un curso académico en una o más asignaturas

## Esquema

- **Criterio de selección de curso**
	- Restringir desde dos años antes
	- Restringir hasta dos años después
- **Hacer matrícula**
	- No puede hacerla
		- Criterio de matriculación en el mismo curso (¿Se matriculó antes?)
			- Si
			- No
		- Criterio de comprobación de si es moroso (En los últimos 5 cursos anteriores)
			- La fecha está entre los 5 años atrás (si lo es)
			- La fecha de morosidad es anterior a 5 años (no lo es)
			- Nunca lo fue
		- Criterio de evaluación de asignaturas de matrículas de cursos anteriores
			- Aprobadas
			- Suspensas
			- No presentadas
			- Anuladas
		- Criterio de matrícula de este curso ya realizada
			- Si está hecha, no se puede modificar
				- Muestra info de asignaturas matriculadas y de sus recibos
			- No está hecha, se puede modificar
	- Puede hacerla
		- Muestra la lista de asignaturas de las que no se ha matriculado o las que no ha aprobado previamente
- **Tipos de pago**
	- Único
		- Se genera 1 recibo domiciliado 'D' en estado emitido 'E' 
		- fecha 
			- Octubre-Año
			- importe total
	- Fraccionado
		- Se generan 4 recibos de tipo domiciliado 'D' en estado emitido 'E' 
		- Fechas
			- Octubre-Año
				- importe al 30%
			- Enero-Año
				- importe al 30%
			- Marzo-Año
				- importe al 20%
			- Mayo-Año
				- importe al 20%
	- Solicitud de beca
		- Se generan 2 recibos de tipo beca 'B' en estado emitido 'E'
		- fecha
			- Octubre-Año importe 0 para alumno y total para entidad concesora de la beca

- El importe es una salida

# Generación de lotes

