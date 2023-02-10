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
# 10 Febrero 2023 - Lab1 ⚱️