En este tema se verá como mediante envenenamiento ARP se puede conseguir realizar un _man-in-the-middle_ entre la comunicación de un cliente con un servidor.

### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1721/#laboratorio)Laboratorio

La primera comprobación será comprobar si se tiene acceso a la miniweb desde el cliente y desde el atacante.

```
http://172.16.1.129:8000
```

A través del comando `arp -a` se puede ver en la máquina Windows _(Servidor)_ cómo reconoce a las máquinas del cliente y atacante:

```
...
172.16.1.128        00-0C-29-26-BE-91    (atacante)
172.16.1.130        00-50-56-22-FD-60    (cliente)
...
```

De la misma forma el cliente reconoce al servidor como:

```
172.16.1.129        00-0C-29-4A-9D-4D    (servidor)
```

**Nota:** Para que las pruebas que se van a realizar a continuación tengan sentido y realmente simulen el tráfico en una red interconectada, se debe desactivar en Wireshark la escucha de tráfico en modo promiscuo. Así, solo se debería escuchar la información que fuera destinada a la máquina en concreto y no la que mantienen dos terceros.

Si se presta atención al esquema final, el atacante va a quedar como intercomunicador entre cliente y servidor. Para que esto se produzca de forma transparente y tanto el servidor como el cliente no se percaten de la presencia del atacante, éste deberá poder reenviar los paquetes entre ambos. Para ello, en el Kali atacante se deberá habilitar el _forward_:

```
echo “1” >> /proc/sys/net/ipv4/ip_forward
```

Una vez arrancado el Wireshark en la máquina atacante, el cliente puede acceder al servidor y no queda nada reflejado en el equipo del atacante.

Para llevar a cabo el ataque se le indicará al servidor (`129`) que nosotros somos el cliente (`130`) con MAC `00-0C-29-26-BE-91` (MAC del atacante), y de esta forma el servidor enviará los mensajes, cuyo destinatario real es el cliente, al atacante. Se hará uso del comando `arpspoof`:

```
arpspoof -i eth0 -t 172.16.1.129 172.16.1.130
```

Y el sentido contrario también:

```
arpspoof -i eth0 -t 172.16.1.130 172.16.1.129
```

Si se vuelve a realizar la comprobación de las MACs tanto en el servidor como en el cliente, ambos han cambiado la MAC del contrario a `00-0C-29-26-BE-91` que es la del atacante.

Si se vuelve a ejecutar el Wireshark para que escuche y el cliente vuelve a acceder al servidor, se puede comprobar que el cliente es capaz de captar toda la comunicación entre ambos y es completamente transparente tanto para el servidor como para el cliente.

Se ve la petición `GET` del cliente al servidor y la respuesta `HTTP` en sentido contrario.

El peligro recae si esto se aplica sobre la MAC del router de la organización y que todos los equipos piensen que no ocurre absolutamente nada pero el atacante se ha colocado entre ellos y el router analizando y capturando todas las comunicaciones entre ambos.