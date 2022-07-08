Netfilter es un framework de linux que permite interceptar y manipular paquetes de red. Iptables es su componente más popular y actúa como cortafuegos.

```
https://www.netfilter.org
```

Las cadenas son agrupaciones de reglas que se aplican a los paquetes en momentos concretos.

```
PREROUTING: Justo antes de que entre al sistema
INPUT: Entrada de la interfaz
FORWARD: Reenvío
OUTPUT: Salida de la interfaz
POSTROUTING: Justo antes de enviar el paquete a la interfaz destino
```

Las tablas se pueden definir como el tipo de procesamiento que se debe aplicar a los paquetes.

```
FILTER: Filtrado de paquetes
NAT: Traducción de direcciones
MANGLE: Etiquetado de paquetes
```