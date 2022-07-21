A continuación se presenta un resumen de los principales comandos de la consola de Metasploit a través de _msfconsole_.

**Help:** Lista los comandos disponibles clasificados en comandos de core y de ddbb.

**Search:** Para realizar búsquedas de módulos teniendo en cuenta la gran cantidad que existen.

**Use:** Permite usar el exploit que se quiere ejecutar. Será necesario escribir la ruta hasta el exploit en cuestión.

**Info:** Proporciona información acerca del módulo que se está ejecutando.

**Show:** Muestra los módulos de un determinado tipo o todos (Payloads, Encoders, Post, Options).

**Back:** Para salirse del módulo que se está ejecutando.

**Set & Setg:** Comandos para configurar los parámetros de los módulos. Set asigna el valor al parámetro de ese determinado módulo mientras que setg lo asigna de forma global.

**Unset & Unsetg:** Usado para desasignar los valores establecidos con los comandos set y setg vistos anteriormente.

**Run:** Comando para ejecutar un módulo auxiliar.

**Exploit:** Similar a _run_, se usa para ejecutar un exploit. Si la ejecución es exitosa se establece una conexión con la máquina conocida como sesión.

**Check:** permite saber si el exploit tendrá éxito sin lanzar el script (para aquellos intrusivos).

**Sessions:** Permite interactuar con las sesiones obtenidas después de la ejecución del exploit. Funciones como -l: listar, -i: interactuar con alguna sesión, -k: terminar con una sesión.

### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1724/#explotando-vulnerabilidades)EXPLOTANDO VULNERABILIDADES

El laboratorio que se va a realizar consistirá en una máquina Windows 7 con el servicio `BadBlue` en su versión 2.7, la cual tiene vulnerabilidades reconocidas.

El primero de los pasos vistos en este temario será una fase de escaneo en el que se muestren los puertos abiertos y servicios (con sus respectivas versiones) que están funcionando en la posible víctima.

```
nmap 172.16.1.129/32 -sV
```

La respuesta es que efectivamente en el puerto 80 (HTTP) está funcionando un servidor **BadBlue 2.7**. El siguiente paso será buscar si existen vulnerabilidades para dicha versión de ese servicio.

```
https://www.cvedetails.com/vulnerability-list/vendor_id-7535/Badblue.html
```

Según lo mostrado en la web existen vulnerabilidades, pero es necesario saber si están creados los exploits para dichas vulnerabilidades. Esto se puede realizar con el comando _search_ mostrado en la parte superior.

```
msfconsole
msf > search badblue
```

Con suerte están publicados. En este caso existe con una buena valoración y es un `passthru`por lo que se usará para pasar a través de él y ejecutar un payload que, por ejemplo, pueda dar una sesión en la máquina.

Se lanzará y se verán las opciones para ver cuáles hay que introducir.

```
msf > use exploit/windows/http/badblue_passthru
msf exploit(badblue_passthru) > show options
```

Los dos campos requeridos son la IP y Puerto de la víctima, donde se encuentra el servicio en cuestión. Por defecto, ya se encuentra establecido el puerto al 80, por lo que solo será necesario incluir la IP con el comando `set`.

```
msf exploit(badblue_passthru) > set RHOST 172.16.1.129
```

Teniendo preparado el exploit solo será necesario elegir el _payload_, se suele buscar obtener una sesión meterpreter que puede ser directa _(bind)_ o indirecta _(reverse)_.

```
msf exploit(badblue_passthru) > set payload windows/meterpreter/bind_tcp
```

Por último, solo faltará ejecutarlo:

```
msf exploit(badblue_passthru) > exploit
```

Se ejecuta correctamente y devuelve la sesión **meterpreter** con la que se trabajará en el siguiente tema.