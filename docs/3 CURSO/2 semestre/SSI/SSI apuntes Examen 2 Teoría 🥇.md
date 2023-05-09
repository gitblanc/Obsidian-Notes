# Tema 5 Seguridad Perimetral y de Red

- **Protocolos de red**: definen las reglas de comunicación entre dos servicios (software)
- Los protocolos más importantes son: **IP** y **TCP**

## Firewalls
- Diseñados para bloquear acceso no autorizado, pero normalmente permitiendo el tráfico saliente
- Pueden ser de software, hardware o híbridos:
	- **Firewalls hardware**: máquinas personalizables con un harware especializado en el rendimiento de la red y la potencia de procesamiento de paquetes
	- **Firewalls híbridos**: firewalls basados en software que se ejecutan en hardware de PC estándar
	- **Firewalls de software**: sólo ejecutan un programa de firewall en su PC

- **Packet-filtering** (PF): examina datos de cada paquete de red recibido. Los paquetes se examinan uno por uno y se descartan si no cumplen las reglas
![[Pasted image 20230509134004.png|500]]
- **Stateful Packet Inspection** (SPI): firewalls de filtrado de paquetes dinámico con una tabla que rastrea todas las conexiones abiertas
![[Pasted image 20230509134259.png|500]]
- **Proxy firewall**: proporciona filtrado en la capa de aplicación
![[Pasted image 20230509134418.png|500]]
- **Next-Generation Firewalls** (NGFW): firewalls que usan un enfoque de varias capas. Un ejemplo es Fortinet
![[Pasted image 20230509134534.png|500]]

### Reglas de un Firewall
- **Permitidas** (ALLOW)
- **Rechazadas** (REJECT)
- **Descartadas** (DROP) - no avisan al cliente
![[Pasted image 20230509134725.png|500]]

- Las reglas de un firewall operan con tripletas (IP, puerto, protocolo)
![[Pasted image 20230509134832.png]]
- Cuando los firewalls pueden restringir las conexiones entre diferentes redes o zonas se denominan **firewalls perimetrales** (son una primera línea de defensa).

## Demilitarized Zones (DMZs)
- Son zonas de red aisladas dentro de la red interna de una empresa
- Deben contener todos los recursos que sean accesibles desde internet
- Se implementan con cortafuegos perimetrales
![[Pasted image 20230509135410.png|500]]
- Los firewalls son necesarios para implementar una DMZ
- Recomendaciones con el tráfico de red que proviene y va hacia los distintos segmentos de red:
![[Pasted image 20230509135552.png|500]]
![[Pasted image 20230509135612.png|500]]
- Se usan firewalls para aumentar la seguridad de las redes:
![[Pasted image 20230509140001.png|500]]

## Ficheros HOST
- Archivo local para la traducción de nombres de dominio a IPs
	- Todo lo que se pone en este archivo será consultado y resuelto primero
	- Bloqueador de URL maliciosas: https://github.com/StevenBlack/hosts
![[Pasted image 20230509140205.png|500]]

## Ataques en red: Man in the middle
![[Pasted image 20230509140343.png]]

## DNS Poisoning
![[Pasted image 20230509140822.png]]

## DDoS
- Lanzados habitualmente desde botnets
![[Pasted image 20230509140916.png]]

## Botnet
![[Pasted image 20230509140944.png]]



