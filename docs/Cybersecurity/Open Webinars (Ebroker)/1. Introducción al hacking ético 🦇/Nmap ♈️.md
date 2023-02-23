Se utilizará la herramienta NMAP en la parte de obtención de información. Con ella se podrán escanear puertos, servicios, versiones de dichos servicios, de qué sistema operativo se trata… para un uso posterior de toda dicha información que se verá en el módulo de Metasploit.

La descarga de esta herramienta (Multiplataforma) se puede llevar a cabo desde el siguiente enlace:

```
https://nmap.org/download.html
```

Si se decide realizar la compilación de la misma de forma manual se debe hacer con los siguientes comandos:

```
bzip2 -cd nmap-7.40.tar.bz2 | tar xvf -
cd nmap-7.40
./configure
make
su root
make install
```

Se pueden realizar escaneos tanto a nivel de equipo como de red:

```
nmap 172.16.1.129    (equipo)
nmap 172.16.1.0/24    (red)
```

### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1713/#respuestas-en-nmap)Respuestas en Nmap

A continuación se van a simular las tres posibilidades que se pueden encontrar al realizar un escaneo con Nmap viendo el tránsito de paquetes entre ambas máquinas.

El escaneo se va a realizar al puerto 80 únicamente para poder analizar bien los paquetes. Se usarán los siguientes comandos para escanear en una máquina y para escuchar las conexiones en la otra:

```
nmap -sS -p 80 172.16.2.128
tcpdump -i eth0 'host 172.16.2.129'
```

De esta forma se está realizando un escaneo TCP SYN (_-sS_) y se intercambian los paquetes SYN, la conexión no queda establecida porque no se manda el ACK del SYNC que manda el servidor destino sino que se envía un RESET.

En el _FILTERED_ no se recibe respuesta alguna. Para provocarlo se puede introducir la siguiente regla.

```
iptables -A INPUT -i eth0 -p tcp -m tcp --dport 80 -j DROP
```

En el _CLOSED_ devuelve un RESET y deberá realizarse con la siguiente regla.

```
iptables -A INPUT -i eth0 -p tcp -m tcp --dport 80 -j REJECT --reject-with tcp-reset
```

El borrado de reglas se puede hacer con `iptables -F` para realizar las distintas pruebas.

### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1713/#filtrado-de-puertos)Filtrado de puertos

Por defecto Nmap escanea los 1000 puertos más usados, aunque se pueden seleccionar los puertos que se quieren escanear o un rango de los mismos.

**_Puertos concretos (-p i,j)_**

```
nmap -p 21,22,80 172.16.2.128
```

**_Rango de puertos (-p min-max)_**

```
nmap -p 20-100 172.16.2.128
```

**_Escaneos UDP (-sU)_**

```
nmap -p 53,123 -sU 172.16.2.128
```

### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1713/#otras-opciones)Otras opciones

Existen muchas opciones para distintos escenarios y necesidades:

**_No usar Ping (-PN)_**

```
nmap -PN 172.16.2.128
```

**_Deshabilitar la resolución inversa de nombres (-n)_**

```
nmap -n 172.16.2.128
```

**_Debug (-v/-vv…)_**

```
nmap -vv 172.16.2.128
```

### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1713/#descubrimiento-de-servicios)Descubrimiento de servicios

Para conocer qué servicio se encuentra escuchando detrás de un puerto:

**_Versión del servicio usando banners de respuesta (-sV)_**

```
nmap -sV 172.16.2.128
```

**_Intensidad del escaneo (-version-intensity X)_**

Mientras mayor intensidad se indique, se realizarán más pruebas pero provocará ser más _ruidosos_ (más visibles).

```
nmap --version-intensity 9 172.16.2.128
```

**_Sistemas Operativos (-O)_**

```
nmap -O 172.16.2.128
```