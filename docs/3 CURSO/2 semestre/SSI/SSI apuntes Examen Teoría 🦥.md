# Nota para la gente que lea esto:
*Hay muchos conocimientos que ya tengo muy de la mano, por lo que los más básicos o aquellos que ya conozca demasiado simplemente los omitiré y no aparecerán aquí (ej: **no voy a decir lo que es un exploit o un backdoor**). Estos apuntes deberían servir sólo como repaso o recordatorio (hay cosas que pongo meramente para hacer un pequeño esquema). Mirar los apuntes de Redondo antes que los míos.*
# Tema 1 Introducción
- Un sistema informático es seguro cuando responde según lo previsto
	- Permite que los usuarios realicen operaciones para las que tienen acceso y evita que realicen las que no lo tienen. 
	- También garantiza 3 cosas:
		- **Confidencialidad**: los datos solo son **visibles** para sus legítimos propietarios
		- **Integridad**: los datos solo pueden ser **modificados** por sus legítimos propietarios
		- **Disponibilidad**: los datos son siempre **accesibles** para sus legítimos propietarios
- Ataques contra la **CONFIDENCIALIDAD**:
	- **Hardening**: mejora de la seguridad de los sistemas informáticos
	- **Suplantación**: acceso a datos o software restringidos
	- **Sniffing**: acceso a los datos que el objetivo envía y/o recibe
	- Acceso **físico** a un pc
	- Acceso a las copias de seguridad
	- Acceso a datos/software restringido o privado
- Ataques contra la **INTEGRIDAD**:
	- Los mismos que contra la confidencialidad pero no se limitan exclusivamente a a cceder a la información/software
- Ataques contra la **DISPONIBILIDAD**:
	- Saturación
	- Dejar al sistema sin recursos
	- Eliminar o dañar deliberadamente el hardware existente
	- Apagar el sistema

- ¿Qué es un **CVE**?
	- (Common Vulnerabilities and Exposures) es información de vulnerabilidades de seguridad conocidas públicamente de cualquier software

- **Malware**: software para obtener accesos no autorizados (también llamado código malicioso)
	- Efectos comunes:
		- **Causar fallos**: virus, gusanos, troyanos
		- **Robar información personal/privada**: spyware, keyloggers, stealers
		- **Ataques distribuidos/coordinados**: botnets
		- **Insertar anuncios**: adware, hijackers
		- **Extorsión/daño financiero**: ransomware
		- **Otros**: rogue software, rootkits
- Técnicas de evasión del Malware:
	- Identificar su entorno cuando se ejecuta
	- Confundir a los métodos de detección de las herramientas de seguridad
	- Evasión basada en el tiempo
	- Ofuscación de datos internos (**droppers**: el código malicioso real se descarga cuando se ejecuta un programa)
	- Uso de certificados robados de fuentes acreditadas
	- Técnicas de ocultación de información de información (**stegomalware**)

Tipos de malware:
- **Propagadores**:
	- **Virus**: doble propósito, dañar y propagarse
	- **Gusanos**: se replican en un equipo para aumentar el uso de recursos
- **Wabbits**:
	- DDOS: se replica para agotar los recursos o ralentizar (**bombas fork**)
- **Troyano**:
	- Malware disfrazado de software legítimo
- **Robo de información**:
	- **Spyware**: obtiene información sobre individuos. Recopilan datos en segundo plano
	- **Keylogger**: roban información monitorizando pulsaciones de teclado
- **Anuncios molestos / maliciosos:**
	- **Adware**: software que muestra anuncios en navegadores/aplicaciones
	- **Browser hijackers**: bloquean o dificultan el uso del browser 
- **Daño finaciero/extorsión**:
	- Ransomware: bloquean el uso del ordenador y/o sus datos y piden un rescate por ellos (bloqueadores de pantalla)
- **Rootkit**:
	- Software no solicitado y no autorizado que se instala con privilegios de superusuario con el objetivo de robar información o crear una puerta trasera
- **Rogue software**:
	- Programas falsos que afirman implementar funcionalidades que no implementan (antivirus falsos, herramientas de limpieza de malware, optimizadores de SSOO)
- **Crimeware:**
	- Cualquier software especialmente creado para cometer delitos. Pueden replicarse a sí mismos. Se pueden crear para ser vendidos a delicuentes (RaaS - Ransomware as a Service)

¿Qué es el bug bounty?
- Es un trabajo ofrecido por muchas empresas y organizaciones que consiste en compensaciones a cambio de descubrirles vulnerabilidades o reportarles bugs

Redes Ip:
![[Pasted image 20230316171107.png]]

- **CIDR**: es un estándar basado en bits que utiliza prefijos para mostrar direcciones ip con sus propiedades de enrutamiento, es decir, es una forma de representar múltiples IPs con el mismo identificador. Estos grupos se denominan **bloques CIDR**:
![[Pasted image 20230316171457.png]]

- Las LAN más usadas son la /28 y la /24 (hasta 256 máquinas en la red)
- Los /31 se usan para crear enlaces punto a punto entre dispositivos

- En una red de máquinas puedes comunicarte con todos los dispositivos que tengan una IP compatible con la tuya (dispositivos cuya IP encaja en el mismo CIDR)
- También puedes comunicar máquinas en diferentes redes mediante puentes (bridges) o pasarelas (gateways)
- Normalmente un router asigna una IP privada a cada dispositivo conectado a él y envía todas las conexiones fuera de su LAN privada a través de una IP única. Este mecanismo de traducción se llama NAT.

Diseño típico de una red doméstica:
![[Pasted image 20230316172436.png]]
![[Pasted image 20230316172550.png]]

- El servicio DNS traduce IPs en nombres y viceversa
- URL cheat sheet:
![[Pasted image 20230316173251.png]]
- ¿Cómo funciona un DNS?
![[Pasted image 20230316173418.png]]

- ¡No se pueden abrir puertos bajo CG-NAT!
- Un mal ejemplo sobre puertos:
![[Pasted image 20230316173833.png]]

¿Qué pasa con las redes WIFI?
- Todos los datos que viajan por tu WIFI podrían ser leídos por la una persona que esté conectada a tu wifi (hay que evitar el wifi gratuito, no me seas *lerdo*, y si lo haces usa un vpn al menos)

- En un sistema operativo normalmente hay estos tipos de cuentas:
	- **Root/Administrador**: admin del sistema
	- **Cuentas del sistema:** con el id de un usuario conocido
	- **Cuentas de servicio**: ejecutan aplicaciones/procesos

- Recuerda que cuando algo es gratuito ¡tus datos son el pago!. No hay duros a 4 pelas. Estos datos posiblemente salgan de tu historial de búsqueda.

- **Hoaxes**: mensajes o publicaciones no deseados con información falsa / sesgada de varios tipos
- **APT** (Advanced Persistent Threat): actores de amenazas ocultos de redes informáticas que obtienen acceso no autorizado a una red y permanecen sin ser detectados durante mucho tiempo
- **OSINT**: conjunto de datos recopilados de fuentes públicas para ser utilizados en el estudio de un objetivo. Es un conjunto de información legalmente accesible

# Tema 2 Criptografía
- **Criptografía:** oculta el **significado** de la información transformándola en una versión no legible (cifrada/encriptada) por medio de algoritmos de encriptación.
- **Esteganografía**: oculta la **existencia** de la información (que está incrustada en otra información distinta). Usarla exclusivamente no es muy aconsejable

- Objetivos de la criptografía:
	- Confidencialidad
	- Integridad
	- Autenticación

- Los **algoritmos de descifrado** son funciones que transforman la información
- Los **algoritmos de cifrado** se pueden clasificar en:
	- **Cifrado por bloques**: IDEA, AES, RSA
	- **Cifrados de flujo**: A5, RC4, SEAL
	- **Cifrados sin clave**: ROT13, ROT47
	- **Cifrados con clave criptográfica** (los más seguros)
		- **Algoritmos de clave simétrica**: el emisor y el receptor comparten la misma clave privada
		- **Algorimtos asimétricos**: el emisor y el receptor tienen dos claves cada uno (una es pública y otra privada)

- Principios de Kerchkoffs (pautas para crear un algoritmo de cifrado basado en claves irrompible)
	- La efectividad no debe depender de que el diseño del algoritmo sea secreto
	- Las claves deben ser fáciles de recordar

¿Los algoritmos con tamaños de clave más grandes son más fuertes que los que usan claves más cortas?
- No, el algoritmo en sí es más importante

**Algoritmo Diffie-Hellman:**
- Establece una clave simétrica entre 2 máquinas para cifrar las comunicaciones
- Pasos:
	- Una máquina elige dos números (p y g) y los envía a otra máquina de manera pública
	- Cada uno elige otro número secreto < p
	- Usando una fórmula matemática cada máquina realiza una serie de operaciones con los números público y secreto
	- Esta es la clave secreta usada para cifrar el mensaje
![[Pasted image 20230316182047.png]]

**Aplicaciones prácticas de los algoritmos de clave simétrica: **
- **Cifrado de discos**
![[Pasted image 20230316182200.png]]
- **Autenticación de plataforma**: 
![[Pasted image 20230316182317.png]]
- **Onion routing**: los nodos de Tor intercambian claves simétricas usando Diffie-Hellman:
![[Pasted image 20230316182525.png]]

- Algoritmos asimétricos (o de clave pública):
![[Pasted image 20230316182647.png]]

- **GNUPG** es una herramienta de cifrado simétrico / asimétrico y firma digital

- **Aplicaciones prácticas de los algoritmos asimétricos:**
	- Cifrado de archivos y directorios
	- Cifrado de extremo a extremo (WhatsApp)

- Algoritmos de HASH: SHA-1, SHA-3, MD5, BLAKE2

- **Aplicaciones de los algoritmos hash**: aumenta la dificultad de averiguar contraseñas

- Técnicas típicas para adivinar contraseñas a partir de datos almacenados
	- Fuerza bruta pura
	- Diccionarios
	- Tablas rainbow
- Para resistir a estos ataques hay que usar KDF (Key Derivation Function):
![[Pasted image 20230316183553.png]]

- Firmas digitales: son el resultado de una operación criptográfica que une un documento firmado a un elemento personal, el Certificado Digital. Son el resultado de firmar criptográficamente el hash de un archivo con la clave privada de su autor (las firmas pueden ser .sig o .asc).
- Objetivos de las firmas digitales:
	- Autenticación del origen
	- Integridad
	- No repudiar (el autor no lo puede negar)

- Procedimiento de firma de mensajes:
![[Pasted image 20230316184021.png]]
- Cuando se pierde una clave privada, cualquiera que la tenga puede firmar como otra persona o entidad suplantándola.

---