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
# 24 Febrero 2023 - Lab 3 ⚱️
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