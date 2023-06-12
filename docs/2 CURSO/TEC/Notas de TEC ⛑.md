# Comparativas CMOS vs TTL

- Los **CMOS** son más baratos que los **TTL**
- Los **CMOS** tienen una mayor capacidad de integración que **TTL**
- Una puerta **CMOS** puede consistir en 2 transistores MOSFET, mientras que una **TTL** usa un número mayor de transistores bipolares
- Los **CMOS** son menos complejos que los **TTL**
- Los TTL requieren componentes adicionales (resistencias)
- Los **CMOS** consumen menos que los **TTL**, aunque el consumo del **CMOS** se incrementa con la frecuencia
- Los **CMOS** tienen mayor inmunidad al ruido que los **TTL**
- El margen de ruido de una puerta **CMOS** es prácticamente nulo (muy reducido)
- **CMOS** es más susceptible al daño por descarga electrostática que **TTL**
- Los retardos de propagación en **TTL** son menores que en **CMOS**
- **CMOS** tiene un FAN-OUT de 50, mientras que **TTL** de 10

# Convertidor

## ¿Qué ocurre si no adapto la salida del sensor a la entrada del convertidor?
- Pierdo resolución en la medida al no usar todos los códigos disponibles del A/D
![[convertidor.png]]

- Fórmula: (HIGH-LOW)/2^bits

# Transistores

![[transistores.png]]

## Estructura del MOSFET

![[mosfet.png]]


## Física del MOSFET

- No existe corriente de puerta al estar aislada del canal I = 0
- Id = Is, sólo existe una corriente
- La mínima tensión Vgs para que exista el canal es Vt
- Hay que aplicar una Vds positiva (Canal N) para que se produzca Id
- En el MOS de canal P todas las I y V son de signo contrario

## MOSFET Característica V-I ideal

![[vi.png]]

## ¿Cómo modelo el MOSFET ?

![[vi ideal.png]]

## Preguntas sobre MOSFET

![[p1.png]]
![[p2.png]]


# Niveles lógicos de tensión

![[tension.png]]

- FAN-OUT: número de puertas lógicas que puedo conectar a la salida de otra puerta

![[fan out.png]]

## Preguntas de puertas lógicas

![[p1 l.png]]
![[p2 l.png]]

# Amplificadores operacionales

![[amplificadores.png]]


---

# Algunas definiciones

## Fototransistor
- Transistor sensible a la luz. La luz incide sobre la región de base y genera portadores en ella. El fototransistor es más sensible que el fotodiodo por la ganancia en corriente del transistor.

## Optoacoplador
- Combina un diodo LED y un fototransistor. El dispositivo funciona como un interruptor activado mediante la luz emitida por el diodo LED. Si el LED emite luz,  satura (cortocircuita) el fototransistor. Se utiliza para aislar eléctricamente dos circuitos pues la conexión entre ambos es óptica. Se encapsula como un circuito integrado DIP.

## Puertas lógicas
![[Pasted image 20230612115145.png]]

## Propiedades de los sistemas digitales
- Circuitos electrónicos que manejan señales discretas
- Las entradas y salidas toman valores binarios y se representan físicamente por magnitudes eléctricas dentro de un margen de valores
- La salida binaria es función de las entradas binarias (función lógica)
- Los valores de tensión a las entradas se regeneran a la salida
- Los cambios en las salidas no deben afectar a las entradas (unidireccional)
- La salida de una puerta debe ser capaz de excitar a otras puertas del mismo tipo

---

