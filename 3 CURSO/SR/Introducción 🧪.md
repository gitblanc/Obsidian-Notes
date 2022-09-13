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