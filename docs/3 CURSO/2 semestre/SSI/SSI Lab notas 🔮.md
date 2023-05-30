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