En el anterior tema se analizó un equipo con un servicio BadBlue que tenía una vulnerabilidad. Ésta fue aprovechada para conseguir una sesión meterpreter en dicha máquina.

Los _payloads_ son muy importantes en post-explotación. Una vez realizada la explotación dependerá del payload elegido para ver qué va a realizarse.

Existen 3 tipos de payloads:

-   **_Single:_** Payloads independientes y autónomos que ejecutan una tarea concreta.
-   **_Stagers:_** Su misión es establecer la conexión con la víctima. Suelen ocupar poco espacio y se encargan de descargar los payloads de tipo _staged_.
-   **_Staged:_** Descargados y ejecutados por los _stagers_. Ocupan más memoria pues ejecutan tareas más complejas. Por ejemplo, _meterpreter_.

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1725/#módulos-auxiliares)Módulos auxiliares

No requieren interacción por parte del usuario. Pueden, por ejemplo:

```
Ser capaces de obtener una shell...
Provocar una DoS en una máquina...
...
```

Uno de los ejemplos es un DoS (pantallazo azul) en el servicio RDP de Microsoft con código _MS12_020_.

Es difícil poder explotar esta vulnerabilidad ya que se tiene que dar que el antivirus esté desactivado y que se permitan las conexiones desde equipos que ejecutan cualquier versión de Escritorio remoto (no recomendadas ninguna de las dos acciones).

Para este ejemplo en concreto se utilizará el módulo auxiliar y, al igual que en el anterior ejemplo, solo deberá establecerse el parámetro del host remoto:

```
msf > use auxiliary/dos/windows/rdp/ms12_020_maxchannelids
msf auxiliary(ms12_020_maxchannelids)> set RHOST 172.16.1.129
msf auxiliary(ms12_020_maxchannelids)> show options
msf auxiliary(ms12_020_maxchannelids)> run
```

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1725/#comandos-meterpreter)Comandos Meterpreter

-   Comando **_bgrun_**, igual que run pero en 2º plano.
    
    `bgrun keylogrecorder`
    
-   Comando **_bglist_**, lista tareas en 2º plano.
    
-   Comando **_bgkill_**, mata tareas en 2º plano.
    
-   Comando **_background_**, se deja la sesión meterpreter en segundo plano volviendo a la consola metasploit (_sessions -i para volver_).
    
-   Comando **_migrate_**, migra el proceso a otro más estable (explorer.exe).
    

### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1725/#laboratorio)LABORATORIO

Uno de los scripts más populares es **_winenum_**, el cual realiza gran cantidad de tareas: _listado de programas instalados, volcado de hashes, obtención de información de sus redes…_.

Se ejecuta con el comando `run`.

```
meterpreter > run winenum
```

Y, una vez ejecutado el script, se habrá creado un directorio donde se encuentra la salida de todos los comandos. Esa información es muy relevante ya que aporta una visión completa, no solo del equipo, sino de su red, routing, arp… Puede que haya otro objetivo mejor detrás de este **_(pivoting)_**.

Por último, se puede obtener una línea de comandos en el equipo comprometido ejecutando en el meterpreter:

```
meterpreter > shell
```