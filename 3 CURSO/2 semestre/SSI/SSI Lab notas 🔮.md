# 3 Febrero 2023 - Lab1 ⚱️

- Crear un usuario en Linux: `sudo adduser <user>`
- Para generar múltiples usuarios: `sudo useradd`
- Agregar un usuario al grupo sudo: `sudo usermod -aG sudo <user>`
- Cambiar entre usuarios: `su -user`
- Los datos de un usuario se guardan en: `/etc/passwd`
- Comprobar que ssh (o un servicio) funciona: `sudo service ssh status`
- Para cerrar las terminales usar Ctrl+D para conservar los logouts de los .log
- Para ver todo el contenido oculto: `ls -a`
- Para hacer una conexión desde linux: `su - <user>`
- Ctrl+R para ver el histórico
- Para poder ejecutar aplicaciones de otro usuario desde un ssh remoto: `ssh user@ip_addr -X `
- Para ver el estado del cortafuegos: `sudo ufw status`
- Para habilitar el cortafuegos: `sudo ufw enable`
- Para habilitar servicios ssh (o cualquier otro): `sudo ufw allow ssh`
- Para evaluar la configuración de seguridad de la máquina virtual **tool Lynis**: 
	- Descargar el proveedor de software:
	  `sudo wget -O - https://packages.cisofy.com/keys/cisofy-software-public.key | sudo apt-key add -`
	  - Agregar el repositorio de Lynis al SO:
	  `echo "deb https://packages.cisofy.com/community/lynis/deb/ stable main" | sudo tee /etc/apt/sources.list.d/cisofy-lynis.list`
	  - Actualiza la base de datos de paquetes justo después para poder usar los paquetes recién añadidos: `sudo apt update`
	  - Instala el software `sudo apt install lynis` y verifica la versión `lynis show version`
	  - Ejecuta: `lynis audit system` para validar tu máquina virtual
- Nmap cheatsheet:
![[Pasted image 20230204113531.png]]
- Para comprobar que una contraseña es segura visitar: https://password.kaspersky.com/
- Habilitar el software de escaneo de malware / rootkits:
	- Intalar el **tool Chkrootkit** (rootkits): `sudo apt install chkroot`
		- Para comprobar archivos: `sudo chkrootkit -r <file>`
	- Instalar el **tool Rkhunter** (rootkits): `sudo apt install rkhunter`
		- Ejecutar `sudo rkhunter -c` para comprobar que todo está correcto. (NOTA: los resultados se guardan en `(/var/log/rkhunter.log)`)
	- Instalar el **tool ClamAV** (malware): `sudo apt install clamav`
		- Actualizar las firmas del software anti malware: `sudo freshclam` (si no deja, parar el servicio con `sudo service clamav-freshclam stop` y ejecutar `sudo freshclam` de nuevo)
		- Para escanear un directorio usar: `sudo clamscan -r -i <dir>`
  - Para crear un informe de seguridad de una máquina usando Lynis y enviar los resultados a un HTML con formato: 
	  - Instalar el paquete:  `sudo apt install kbtin`
	  - Ejecutar: `sudo lynis audit system | ansi2html > report.html` y visualizar el resultado en cualquier navegador
- Para analizar URL sospechosas para ver si apuntan a una web maliciosa conocida usar el **tool VirusTotal**: https://www.virustotal.com/gui/home/upload
- Para saber si una página web está identificada como maliciosa usar: https://transparencyreport.google.com/safe-browsing/search
- ¿Cómo saber si una página web está ejecutando productos/frameworks con vulnerabilidades conocidas?. Esta info está contenida en las cabeceras http (producto, versión...)
	- Usar el propio navegador:
	 ![[Pasted image 20230204121149.png]]
- Para ver las rutas que siguen los paquetes que mandas por la red usar el **tool traceroute**:
	- Instalación: `sudo apt install tcptraceroute`
	- Uso: `tcptraceroute www.domain.com`
- Para preguntarle a tu servidor DNS cierta información de cualquier nombre de dominio remoto usar el comando `dig`. Tutorial:  https://www.hostinger.es/tutoriales/comando-dig-linux/
	- Usar el comando: `dig @8.8.8.8 domain.com +trace` para ver la ruta 

## RESULTADOS LAB1
 
| Lab 1. Configuración del Sistema |                                                                                                                                                                                                                                     |       |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| Nivel de la insignia             | Debloqueada cuando                                                                                                                                                                                                                  | Notas |
| Bronce                           | Puedes desplegar máquinas virtuales en VirtualBox                                                                                                                                                                                   |    ✅   |
| Bronce                           | Puedes actualizar un sistema Ubuntu                                                                                                                                                                                                 |   ✅   |
| Bronce                           | Puedes crear un usuario en un sistema Ubuntu y ponerlo en el grupo sudo                                                                                                                                                             |     ✅  |
| Bronce                           | Puedes cambiar una contraseña de usuario                                                                                                                                                                                            |     ✅  |
| Bronce                           | Puedes comprobar si una contraseña es segura                                                                                                                                                                                        |     ✅  |
| Bronce                           | Puedes responder a esta pregunta: ¿Cuáles son las ventajas de tener una contraseña fuerte, no predeterminada y no conocida?                                                                                                         |     ✅  |
| Bronce                           | Puedes cambiar correctamente entre los usuarios en un sistema Ubuntu                                                                                                                                                                |      ✅ |
| Bronce                           | Puedes instalar un servidor OpenSSH operativo                                                                                                                                                                                       |      ✅ |
| Bronce                           | Puedes activar el firewall ufw y restringir todos los puertos, excepto el ssh                                                                                                                                                       |   ✅    |
| Bronce                           | Entiendes por qué nmap es mucha mejor forma de localizar hosts “vivos” que ping                                                                                                                                                     |   ✅    |
| Bronce                           | Puedes rastrear la ruta de los paquetes enviados a cualquier sistema remoto, e identificar si los nodos por los que viajan están en la red de tu casa o en otras redes (si la red lo permite)                                       |   ✅    |
| Plata                            | Puedes probar si hay una conexión entre el host y la máquina virtual base operativa                                                                                                                                                 |    ✅   |
| Plata                            | Puedes habilitar y utilizar software de análisis de malware y rootkits                                                                                                                                                              |     ✅  |
| Plata                            | Puedes habilitar la actualización de firmas y ejecutar el antivirus ClamAV                                                                                                                                                          |      ✅ |
| Plata                            | Puedes habilitar la última versión de Lynis y evaluar la configuración de seguridad actual de tu sistema base                                                                                                                       |   ✅    |
| Plata                            | Puedes crear informes de seguridad en una máquina Ubuntu con Lynis en HTML                                                                                                                                                          |  ✅     |
| Plata                            | Puedes responder a esta pregunta: ¿la puntuación Lynis de la máquina mejora una vez que se instale software de detección de malware y rootkits?                                                                                     |   ✅    |
| Plata                            | Debido a la anterior, conoces el procedimiento general para agregar repositorios externos de software a Ubuntu de proveedores externos.                                                                                             |   ✅    |
| Plata                            | Puedes responder a esta pregunta: Según el informe Lynis, ¿crees que una instalación de Ubuntu actualizada base es lo suficientemente segura? ¿por qué?                                                                             |   ✅    |
| Plata                            | Puedes realizar un escaneo con ping a un servidor remoto                                                                                                                                                                            |   ✅    |
| Plata                            | Puedes analizar un ejecutable con Virustotal e interpretar sus resultados                                                                                                                                                           |   ✅    |
| Plata                            | Puedes analizar una URL con Virustotal y Google Safe Browsing e interpretar sus resultados                                                                                                                                          |   ✅    |
| Oro                              | Puedes comprobar las vulnerabilidades conocidas de cualquier producto inspeccionando sus CVEs. En particular, puedes hacerlo a partir de la información que un servidor web puede proporcionar sobre los productos software que usa |   ✅    |
| Oro                              | Puedes responder a la siguiente pregunta: ¿qué se debe esperar del estado general de la seguridad de una página web que proporciona tipos de productos y versiones en sus encabezados HTTP?                                         |   ✅    |
| Oro                              | Puede utilizar dig para ver las conversiones de IP <-> DNS y para realizar un seguimiento de la jerarquía DNS de los servidores DNS que se utilizan para resolver un nombre.                                                        |    ✅   |
| ==Platino==                          | Puedo hacer esto todo el día: Puedes desplegar una máquina virtual base, evaluar su seguridad y realizar algunas operaciones iniciales relacionadas con la seguridad que te permiten comprender mejor los conceptos de teoría       |   ✅    |

---
# 10 Febrero 2023 - Lab2 ⚱️

- Para descomprimir un zip en ubuntu: `unzip -d directory "file"`
- El comentario `#!/bin/bash` dice que un script se ejecuta con la shell de bash
- En docker las imágenes reutilizan código (en lugar de que cada máquina ocupe varios gigas)
- Requisitos previos para docker:
````bash
sudo apt install gnome-keyring gnupg2 pass
````
- Para ver las imagenes en docker: `docker images`
- Para ver los contenedores activos: `docker ps` y para ver los inactivos `docker ps -a`
- Para parar un proceso en Linux usar: Ctrl+Z
- Para usar un proceso en background escribir: `bg`
- Para parar un contenedor: `sudo docker stop id`
- Para parar todos los contenedores de golpe usar: `sudo docker stop $(sudo docker ps -q)`
- Para borrar todos los contenedores usar: `sudo docker rm $(sudo docker ps -qa)`
- Para ver los procesos parados usar: `jobs`
- Para devolver un proceso usar: `fg`
- Para salir de un contenedor usar: Ctrl+D
- Para saber si una web está reveleando rutas "secretas": visitar el fichero `robots.txt`
- Para saber si los documentos, imágenes, etc de una web están revelando mucha información de sus autores (*metadatos*) usar: **tool FOCA** o **tool Metashield Clean-up Online** -> https://metashieldclean-up.elevenpaths.com/, o la herramienta local **tool exiftool**
	 - Para instalarla: `sudo apt install exiftool`
	 - Para uso básico: `exiftools -s file`
	 - Más info: https://linuxopsys.com/topics/install-and-use-exiftool-on-linux?utm_content=cmp-true
- ¿Cómo usar Google Hacking? (búsquedas en Google combinadas con el operador **site:** que tienen como objetivo detectar vulnerabilidades, problemas de configuración o información que puedan provocar un ataque):
	- Google Hacking Database (GHDB): https://www.exploit-db.com/google-hacking-database
- Para ver la historia de una página web o de cualquier archivo consultar tool **The Wayback Machine**: https://archive.org/web/
	- Para más información: https://www.elladodelmal.com/2013/04/hacking-con-archivecom-wayback-machine.html
- Para descubrir subdominios registrados de un dominio usar:
	- **tool knockpy** -> https://github.com/guelfoweb/knock o `sudo apt install knockpy`
	- **tool dnsenum** -> https://github.com/fwaeytens/dnsenum
	- tools que son Sitios web:
		- https://dnsdumpster.com/
		- https://search.netcraft.com/
		- https://www.virustotal.com
		- https://crt.sh/
	- Podemos encontrarnos dominios abandonados (que pueden estar realmente **abandonados** o bien **no mantenidos** (siendo ahí donde puede haber más vulnerabilidades))
	- Para hacer un resumen de cada subdominio que encontremos está el **tool eyewitness** https://github.com/ChrisTruncer/EyeWitness
- Para analizar un rango de IPs asociados a un dominio de Internet usar los tools:
	- Para dominios **.com** usar el **tool https://whois.arin.net 
	- Para dominios **.es** usar el **tool https://www.nic.es
- Para hacer escaneos de servicios en un puerto concreto en todo Internet se pueden usar:
	- **tool Zmap**: es más rápido pero por defecto no funciona en redes locales
	- **tool Nmap**: se usa para escaneos LAN en busca de máquinas "vivas"
	- Cheat Sheet Zmap:
![[Pasted image 20230210162031.png]]
 - Cheat Sheet Nmap:
![[Pasted image 20230210162202.png]]
- Para saber cómo cualquier sitio web usa tus datos de navegación para su propio provecho usar el **tool BlackLight** -> http://themarkup.org/blacklight
- ¿Cómo crear un entorno de navegación más seguro?
	- Para tratar con extensiones maliciosas: usar el **tool de navegador uBlock Origin**
	- Para bloquear scripts: usar el **tool de navegador NoScript**
	- Para evitar rastreadores: usar el **tool de navegador Privacy Badger**
- Para comprobar si una de tus cuentas ha sido comprometida: usar la página https://haveibeenpwned.com/
- Para geolocalizar al remitente de un correo electrónico: usar la página https://www.iplocation.net/
	- Podemos obtener la ip de un correo para obtener de manera aproximada el remitente obtenido del campo `x-originating-ip`
![[Pasted image 20230210165124.png]]
![[Pasted image 20230210165144.png]]
![[Pasted image 20230210165202.png]]
## RESULTADOS LAB2

| Lab 2. Descubrimiento de información y OSINT |                                                                                                                                                                                                                                                                                                                                                                                 |       |
|----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| Nivel de Insignia                            | Debloqueada cuando                                                                                                                                                                                                                                                                                                                                                              | Notas |
| Bronce                                       | Puedes encontrar y analizar cualquier archivo robots.txt                                                                                                                                                                                                                                                                                                                        |   ✅    |
| Bronce                                       | Responde a esta pregunta: ¿Cuáles crees que serán los problemas de seguridad que un robots.txt mal escrito podría provocar?                                                                                                                                                                                                                                                     |   ✅    |
| Bronce                                       | Puedes analizar los metadatos de cualquier archivo individual de un tipo adecuado que encuentres. Puedes responder a esta pregunta: ¿Por qué los metadatos pueden ser una amenaza para la seguridad?                                                                                                                                                                            |   ✅    |
| Bronce                                       | Puedes analizar una única URL o IP utilizando Shodan e interpretar los resultados. También puedes responder a esta pregunta: ¿qué parte de los resultados enlaza con algo que vimos en el laboratorio anterior, y puede indicar un problema grave con la página web?                                                                                                            |   ✅    |
| Bronce                                       | Puedes buscar todas las direcciones URL históricas de un dominio.                                                                                                                                                                                                                                                                                                               |   ✅    |
| Bronce                                       | Puedes responder a esta pregunta: ¿qué problemas de seguridad pueden aparecer si tenemos un archivo histórico de los diferentes contenidos de un archivo robots.txt?                                                                                                                                                                                                            |    ✅   |
| Bronce                                       | Puedes responder a esta pregunta: ¿por qué los subdominios son interesantes desde el punto de vista de la seguridad? ¿Qué podría suceder si un subdominio (y su contenido) ha sido olvidado durante mucho tiempo?                                                                                                                                                               |   ✅    |
| Bronce                                       | Puedes analizar cómo un sitio web recopila datos de usuario y trata la privacidad mediante Blacklight.                                                                                                                                                                                                                                                                          |   ✅    |
| Bronce                                       | Puedes comprobar si una contraseña ha sido potencialmente comprometida en una fuga de datos y responder a esta pregunta: ¿qué debes hacer si encuentras tu email en una de estas intrusiones documentadas?                                                                                                                                                                      |   ✅    |
| Plata                                        | Puedes utilizar Censys para analizar los hosts de una red e interpretar los resultados, tanto de una red como de cualquier host individual. También puedes responder a esta pregunta: ¿puedes encontrar los servicios que se ejecutan en los hosts? ¿Cómo puedes encontrar si algunos son vulnerables?                                                                          |    ✅   |
| Plata                                        | Sabes cómo utilizar la base de datos de Google Hacking contra un objetivo concreto.                                                                                                                                                                                                                                                                                             |     ✅  |
| Plata                                        | Responde a esta pregunta: ¿Qué tipo de problema de seguridad crees que encontrar contenido que estaba alojado en el pasado podría suponer en un sitio web?                                                                                                                                                                                                                      |    ✅   |
| Plata                                        | Puedes localizar subdominios de cualquier dominio mediante una de las herramientas proporcionadas y analizar la información del dominio que muestran.                                                                                                                                                                                                                           |   ✅    |
| Plata                                        | Puedes localizar las redes IP de cualquier dominio .com o .es                                                                                                                                                                                                                                                                                                                   |   ✅    |
| Plata                                        | Puede localizar servicios activos en rangos de redes públicas utilizando zmap                                                                                                                                                                                                                                                                                                   |   ✅    |
| Plata                                        | Puedes localizar hosts activos en redes LAN                                                                                                                                                                                                                                                                                                                                     |   ✅    |
| Plata                                        | Puedes configurar un entorno de navegación privado y seguro                                                                                                                                                                                                                                                                                                                     |   ✅    |
| Plata                                        | Puedes geolocalizar una IP (y, en particular, el remitente de un correo electrónico). Puedes responder a esta pregunta: después de ver la precisión de la ubicación IP que tiene, ¿cuál es, en tu opinión, la utilidad de la geolocalización IP?                                                                                                                                |   ✅    |
| Oro                                          | Puedes responder a esta pregunta: ¿Qué sucede si en lugar de un correo electrónico tuyo, decides investigar correos electrónicos de otras personas? ¿Qué sucede si el correo electrónico se notifica como comprometido?                                                                                                                                                         |   ✅    |
| Oro                                          | Puedes responder a esta pregunta: Si soy capaz de encontrar cualquier imagen o documento que está (o estaba) en cualquier sitio web, ¿qué podemos hacer con estos archivos que pueda revelarme más información? ¿Qué sucede si puedo encontrar el historial de versiones de cualquiera de estos archivos? ¿Qué tipo de información puede proporcionar?                          |   ✅    |
| Oro                                          | Puedes responder a esta pregunta: Si soy capaz de encontrar cualquier versión de cualquier página web de que una vez fue parte de un sitio web, ¿qué podemos hacer con estos archivos que pueda revelarme más información? ¿Crees que esto podría permitir localizar posibles vulnerabilidades?                                                                                 |   ✅    |
| Oro                                          | Puedes responder a esta pregunta: Imagina que por error dejo en una página web un comentario comprometedor (por ejemplo, indicando un nombre de producto y / o versión, parte del código de servidor en un comentario ...). ¿Qué debemos hacer para eliminar realmente el problema de seguridad que esto podría suponer?                                                        |   ✅    |
| Oro                                          | Puedes responder a esta pregunta: Es un hecho que los escaneos UDP son muy lentos, especialmente en WAN / Internet. También se sabe que nmap generalmente escanea por defecto sólo los puertos más utilizados en todo el mundo (una lista finita de puertos conocidos). Sabiendo esto, si quieres crear un servicio UDP "oculto" que sea muy difícil de localizar, ¿qué harías? |   ✅    |
| ==Platino==                                      | He visto cosas que no creerías: Conoces múltiples técnicas de enumeración y OSINT para extraer mucha información sobre máquinas, empresas y personas que puedes utilizar para investigarlas.                                                                                                                                                                                    |   ✅    |

---