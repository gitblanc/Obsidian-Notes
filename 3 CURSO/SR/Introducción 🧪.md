# 13 Sept 2022 🔫
---
## Objetivos
- Diseño de sistemas robóticos
- Introducción al modelado de piezas 3D
- Robots manipuladores y biorobots
- Robots móviles y planificación de rutas
- Internet de las cosas
	- Smart Objects, sensores y actuadores
	- Objetos heterogéneos y ubicuos
	- Campos de Internet de las cosas
	- Control remoto, integración entre dispositivos
	- Investigaciones y líneas de trabajo

## Componentes de un robot
- **Sensores**: donde perciben la información del mundo real
- **Actuadores**: emiten respuestas (señal, movimiento), ejecutan una acción (un led)
- **Controladores**: toma las decisiones
- **Mecanismos** y estructura**

## Comportamientos
- Percepción
- Procesamiento de la lógica de negocio
- Acción (con los actuadores)
- Desencadenadores

**Ley de Ohm** -> I = V/R (cuidado con los problemas de las resistencias)

## Programación en Arduino
- Funciones básicas:
	- **Setup**: sólo se usa una vez (inicialización)
	- **Loop**: se ejecuta continuamente (es igual que un while true y representa la funcionalidad continua a ejecutar)
- Pines
	- **Digitales**: detectan sensores digitales (0 o 1, true o false) (funcionalidad: encender o apagar leds, saber si está activo o no, etc)
		- **PWM** (~): emulan la salida de un analógico mediante pulsos.
	- **Analógicos**: del A0 al A5, da valores entre 0 y 1023 (fucionalidad: cuánta cantidad está detectando, ej: sensor de temperatura)
---
# 20 Sept 2022 🎾
---
- **Actuador**: dispositivo capaz de transformar energía en un proceso (motores, bombas de aire, ...). Se conectan mediante una fuente de alimentación eléctrica. Dependiendo del tipo se manejan de diferentes formas:
	- Pin de escritura en el actuador
	- Relés u otros componentes
- **Drivers**: permiten un mejor control para los motores.
- **Relé**: es un interruptor controlado por un circuito eléctrico. Encender o apagar programáticamente un componente.
- **Servomotores**: similar a los motores de corriente continua, pero permiten controlar con precisión la rotación/ángulo/aceleración. Cuentan con la capacidad de ubicarse en cualquier posición. Permiten controlar la orientación.
- **Steppers**: motores muy precisos (los que usan las impresoras 3d).
- **Sensores**: son capaces de detectar magnitudes físicas o químicas y transformarlas en variables eléctricas.

## Conceptos generales
- Un **robot** es un sistema físico reprogramable con diferentes sensores y actuadores. Pueden ser autónomos, totalmente manejados o híbridos.
- Son capaces de recoger datos sistemáticos, coherentes y repetitivos de una forma que permiten su comparación, realizar análisis, ...
- Si están bien programados, pueden trabajar sin ningún fallo a escala milimétrica.
- Lo más importante de un robot es su autonomía y que un ser humano no deba controlarlo.

## Áreas de la robótica
- Robots manipuladores
- Robots móviles
- Robots inspirados en la biología o biorobots

## Las tres reglas de la robótica
0. Un robot no hará daño a la humanidad o permitir que esta sufra daño
1. Un robot no puede hacer daño a un ser humano
2. Un robot debe obedecer las órdenes dadas por un ser humano
3. Un robot debe proteger su propia existencia

---

