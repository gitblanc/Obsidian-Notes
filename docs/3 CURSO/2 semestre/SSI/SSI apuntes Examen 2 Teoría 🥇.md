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

## Principios de diseño general de redes seguras
### Ataques actuales de red
- Escenario de tipo traiga su propio dispositivo
- Teletrabajo
- Aplicaciones en la nube
- Ahora se atacan dispositivos finales (endpoints) de usuarios/empleados

## Zero Trust
- Sistema de seguridad que sólo admite dispositivos que cumplen con unas condiciones
- Comprueba los dispositivos continuamente
![[Pasted image 20230509143544.png|500]]

## ¿Qué hacer contra los ataques de hoy?
- Detección de endpoints
- Aislar el navegador
- Proteger el acceso a los servicios a través de cortafuegos u otros medios
- Controlar el acceso remoto (nunca usar RDP)

## Diseños de red inadecuados
- Soluciones basadas en un servidor con todos los servicios (front, back, SGBD...) son inadecuadas

## Secure Network Infraestructure (SNI)
- Una configuración de base segura para todos los servidores
- Firewall de red y de aplicaciones (WAF) externo
- Dos DMZ con 2 firewalls SPI/NGFW
- Dos LAN internas con doble cortafuegos SPI/NGFW
- Una política común de ubicación de los puertos de servicios
- Todos los puertos que no se usen deben estar cerrados
![[Pasted image 20230509144215.png]]

## HoneyPot
- Captura intentos de ataque de usuarios o herramientas de ataque automatizadas, bloqueando sus IPs
- Podemos derivar intentos de conexión al honeypot
- Más recursos sobre honeypots: https://github.com/paralax/awesome-honeypots
![[Pasted image 20230509144315.png]]

## IDS & IPS
- Intrusion Detection System
- Intrusion Prevention System
![[Pasted image 20230509144617.png]]

## Security Operations Center (SOC)
![[Pasted image 20230509144854.png]]

## Introducción al Pentesting de red

## The MITRE ATT&CK
- Base de conocimientos internacional libre y accesible de tácticas y técnicas de adversarios basadas en observaciones del mundo real

## Active Scanning
- El adversario sonde la infraestructura de la vísctima a través del tráfico de red: https://attack.mitre.org/techniques/T1595/
- Herramienta popular: **Nmap**
- Estas técnicas tienen dos objetivos:
	- Localizar sistemas "vivos"
	- Crear un perfil de cada sistema "vivo" para investigarlo
- Tras un escaneo de Nmap deberíamos saber
	- Puertos abiertos
	- Servicios que se ejecutan tras esos puertos
	- Información extendida de ese servicio
Cheat Sheet:
![[Pasted image 20230509145554.png]]
Puertos comunes:
![[Pasted image 20230509145732.png]]
Interpretando los resultados de Nmap:
![[Pasted image 20230509145903.png]]
Si el objetivo tiene servicios HTTPS en ejecución, hay una serie de **tools** que podemos usar para enumerarlos:
- Proxy Burp
- dirb
- dirbuster
- Gobuster
- Wpscan
- Droopescan
- Joomscan

## Fichero robots.txt
- Parte del Robot Exclusion Standard
- A veces se usa para evitar que los motores de búsqueda indexen contenido privado

## Listado de directorios
![[Pasted image 20230509150646.png]]

# Tema 6 Introducción a la seguridad de aplicaciones

## Principios de diseño de software seguro
- Mínimo privilegio
- Valores por defecto a prueba de fallos
- Mediación completa
- Separación
- Confianza mínima
- Economía de mecanismos
- Minimizar mecanismos comunes
- Menor asombro/sorpresa
- Diseño abierto
- Capas (principio de separación)
- Abstracción
- Modularidad
- Vinculación completa
- Diseño por iteraciones

## Filosofía pushing left
- Cuanto más tarde se descubra un problea de seguridad, más caro será solucionarlo
![[Pasted image 20230509162944.png]]

## Requisitos de cifrado
- Las claves y la información sensible nunca se guardan en texto plano
- Se usan técnicas de hashing para claves
- Para el resto de clases, usaremos algoritmos de cifrado/descifrado fuertes
- Esto garantizará la integridad y confidencialidad de la información (no la disponibilidad)

## Requisitos de manejo de datos
- Nunca confíes en la entrada del usuario (toda entrada debe ser validada)
- Privacidad de datos
- Clasificación de datos

***Posibles puntos de entrada de datos**:*
- Cualquier entrada de usuario, cabeceras HTTP, campos hidden...
- Información que se reciba de 
	- SGBDs
	- APIs
	- Código incluído en la aplicación y compilado en ella
	- De otra aplicación
- Valores en la URL, en las cookies, en los ficheros de configuración...
- Datos o comandos que vengan de aplicaciones en la nube
- Imágenes que recibas de otros sitios

## MFA - Multi Factor Authentication
- Los esquemas MFA se basan en que los usuarios den 2 de 3 "algos":
	- Algo que **SABEN**, como una clave o PIN de una cuenta
	- Algo que **TIENEN**, como un dispositivo físico o una aplicación que genera OTPs
	- Algo que **SON**, una característica biológica única como una huella, la voz o la retina
![[Pasted image 20230509164357.png|500]]

## Cuentas de servicio
- Si una aplicación necesita acceder a un servicio externo, debe hacerlo a través de una cuenta de servicio (que no sea la de un usuario REAL capaz de hacer login)

## Threat modeling ("evil brainstorming")
- Identificación de potenciales amenazas para un negocio, sistema, producto o aplicación
- **Brainstorming** donde se piensan, buscan y definen los posibles peligros a los que nos podemos enfrentar

## Dark patterns
- Diseñar programas para engañar a los usuarios y que hagan cosas que no quieren hacer
![[Pasted image 20230509170415.png|500]]

## Web languages vulnerabilities
![[Pasted image 20230509171210.png]]

## Ataques típicos

## Reflected XSS
- Ocurre cuando un atacante inyecta código ejecutable en alguna parte de la petición HTTP
- No es persistente
- https://portswigger.net/web-security/cross-site-scripting/cheat-sheet
![[Pasted image 20230509171555.png]]

## Stored XSS
- Es persistente
- No tiene por qué conllevar una acción por parte de otros usuarios para afectarles
![[Pasted image 20230509171856.png]]

## SQL Injection
![[Pasted image 20230509171959.png|500]]

## CSRF (Cross Site Request Forgery)
- Ataque que obliga a usuarios autenticados a ejecutar acciones no deseadas
![[Pasted image 20230509172318.png|500]]

# Tema 7 Introducción a técnicas de Red Team

## Valid Accounts - CEWL
- Usar el tool **CEWL** para explorar una web y crear un diccionario de palabras de su contenido
- Útil para nombres de usuario o contraseñas
![[Pasted image 20230509172927.png]]
