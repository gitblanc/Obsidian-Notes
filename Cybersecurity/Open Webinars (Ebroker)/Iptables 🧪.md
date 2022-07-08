Las reglas en Iptables siguen la siguiente sintaxis:

```
iptables [-t table] COMANDO CADENA condición acción [opciones]
```

Existe una gran cantidad de opciones y parámetros a la hora de utilizar iptables (reglas y cadenas) que pueden encontrarse en la documentación oficial

```
http://ipset.netfilter.org/iptables.man.html
```

o con el comando:

```
iptables -h
```

A continuación se listarán y explicarán aquellas más comunes y que serán utilizadas posteriormente en el laboratorio.

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#manejo-de-reglas)Manejo de reglas

**_-L:_** Listar las reglas, se puede especificar la cadena.

```
iptables -L [CHAIN -v] [--line-numbers]
```

**_-A / -I i:_** Agregar una regla [final o posición].

```
iptables –A CHAIN… // -I i CHAIN…
```

**_-F / -D i:_** Eliminar reglas [todas o la i-ésima de una cadena].

```
iptables –F CHAIN // –D CHAIN i
```

**_-R i:_** Reemplazar la regla i-ésima por otra nueva especificada.

```
iptables –R CHAIN i _newRule_
```

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#manejo-de-cadenas)Manejo de cadenas

**_-E:_** Renombrar una cadena (solo cambia apariencia).

```
iptables –E old-chain new-chain
```

**_-N name:_** Crear una nueva cadena.

**_-X name:_** Borrar una cadena (debe estar vacía).

**_-R i:_** Reemplazar la regla i-ésima por otra nueva especificada.

```
iptables –-R CHAIN i _newRule_
```

**_-Z:_** Pone a cero los contadores de todas las reglas de una cadena.

**_-P:_** Cambia la política por defecto sobre una cadena, si no se produce ningún _match_ con ninguna regla, ¿qué hacer con ellos? `ACCEPT / DROP`.

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#operadores)Operadores

**_-p [ protocolo ]:_** Sobre qué protocolo se realiza la comprobación, posibilidades en /etc/protocols. _Ejemplo_: `-p tcp,udp`.

**_-s [ ip/máscara origen ]:_** IP o subred origen del paquete. _Ejemplo_: `-s 192.168.1.0/24`.

**_-d [ ip/máscara destino ]:_** IP o subred destino del paquete. _Ejemplo_: `-d 192.168.1.0/24`.

**_-i / -o [ interfaz ]:_** Especifica la interfaz de entrada o salida, solo se puede utilizar en las tablas nat o mangle. _Ejemplo_: `-i eth0, -o eth1`.

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#extensiones)Extensiones

Hay distintos operadores que disponen de más funcionalidades gracias a algunas extensiones que se le pueden añadir. Gracias a ellas se pueden hacer mejores y más específicas condiciones. Por ejemplo, para el caso del operador _-p [protocolo]_ se pueden encontrar las siguientes:

**_—sport, —dport:_** Puerto origen o destino para _tcp_ o _udp_. _Ejemplos_: `-p tcp --sport 0:1024` // `-p tcp,udp --dport 80`

**_—icmp-type:_** Selecciona los paquetes ICMP y comprueba de qué tipo de mensaje se trata. _Ejemplo_: `-p icmp --icmp-type echo-reply` // `-p icmp --icmp-type time-exceded`

**Nota:** Todos los operadores / extensiones tienen la posibilidad de negarlos añadiendo justo delante una negación `!`.

### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#[](#iptables-rules-laboratorio)laboratorio)[](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#iptables-rules-laboratorio)LABORATORIO

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#preparación)Preparación

Lo primero que se va a realizar será configurar el escenario en el que se va a trabajar este ejemplo. Incluye dos subredes:

-   172.16.2.0/24 (_INTERNET_)
-   172.16.1.0/24 (_RED PRIVADA_)

**Nota:** Para habilitar el ping en Windows7:

```
https://answers.microsoft.com/es-es/windows/forum/windows_7-networking/como-habilitar-el-ping-en-el-firewall-de-windows-7/69d287a2-873c-495b-980b-5c5495577152
```

Es necesario que se modifiquen las rutas por defectos de las tres máquinas que no son el firewall. Se configurarán de forma que si el paquete no va destinado a una IP de su subred lo redirija a la máquina Kali que va a realizar las funciones de interconexión.

Para ello será necesario realizar lo siguiente con los permisos necesarios (_root_):

-   **_Ubuntu:_** `route add default gw 172.16.1.128 ens33`
-   **_Kali2:_** `route add default gw 172.16.2.129 eth0`
-   **_Windows:_** `desde la configuración de red`

Por último, para permitir el reenvío de paquetes en la máquina que actuará como Firewall, habrá que activárselo ya que por defecto viene deshabilitado con el siguiente comando:

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

**Nota:** Añadir los nombres _windows_ y _ubuntu_ en `/etc/hosts` puede ayudar a no liarse mucho con las direcciones IP.

```
...
172.16.1.129    windows
172.16.1.130    ubuntu
...
```

Ya sería posible el envío de PINGs entre todas las máquinas del laboratorio ya que le Firewall (_iptables_) está permitiendo todo el tráfico por defecto y se ha habilitado el _forwarding_ en la máquina.

En las máquinas finales Kali y Ubuntu se levantará un servidor Web básico mediante el comando:

```
/etc/init.d/apache2 start
```

Y un SSH (_Secure SHell_) en la Ubuntu:

```
/etc/init.d/ssh start
```

Por último, se instalará un servidor miniWeb en la máquina Windows que puede descargarse desde internet y que por defecto escuchará en el puerto 8000.

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#test-1)TEST 1

_- Se requiere que no se tenga acceso desde el exterior hacia ningún servicio de ningún equipo de nuestra red._

```
iptables -L
iptables –P FORWARD DROP
```

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#test-2)TEST 2

_- Se requiere que solo se permita el tráfico al Windows pero no al Ubuntu._

```
iptables –A FORWARD –j DROP –d 172.16.1.130
```

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#test-3)TEST 3

_- Realmente nos damos cuenta de que lo crítico es el servidor SSH pero no la navegación web, por lo que se necesita que se acepte este último._

```
iptables –A FORWARD –p tcp --dport 80 –j ACCEPT (no hay acceso)
iptables –L --line-numbers
iptables –D FORWARD 1
iptables –A FORWARD –j DROP –d 172.16.1.130
```

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#test-4)TEST 4

_- Suponiendo que el cortafuegos fuera otra máquina que requiere tener acceso al servicio SSH pero no a la navegación web ni a ningún otro servicio._

```
iptables –A OUTPUT –p tcp --dport 22 -j ACCEPT
iptables -P OUTPUT DROP
```

Estas dos reglas no afectan en nada a las anteriormente insertadas debido a que dichos paquetes que se estaban reenviando no pasan por _OUTPUT_ sino por _POSTROUTING_.

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#test-5)TEST 5

_- Se requiere que cuando una máquina interna (Ubuntu) navege hacia el exterior (Kali) se enmascare la IP origen (SNAT) simulando el tráfico que existe detrás de un router._

```
iptables -A POSTROUTING -t nat -o eth1 -j MASQUERADE
iptables -t nat --list
Si nos equivocamos: iptables -t nat -F POSTROUTING
```

Lo anterior es lo mismo que:

```
iptables -A POSTROUTING -t nat -o eth1 -j SNAT --to-source 172.16.2.129
```

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1712/#test-6)TEST 6

_- Se necesita publicar hacia el exterior la máquina Windows ya que los clientes situados en internet no podrán acceder a la IP privada directamente por lo que se debe configurar un DNAT en el Firewall._

```
iptables -A PREROUTING -t nat -i eth1 -p tcp --dport 8080 -j DNAT --to-destination 172.16.1.129:8000
```