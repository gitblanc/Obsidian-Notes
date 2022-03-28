# 21 Marzo 2022 🍓 
---
 ![[database system internals.png |300]]
- Para poder usar una biblioteca necesitamos una API.

#### _Técnicas de despliegue de servidores_:
---
1. **Biblioteca nativa:** las instruciones que usa por defecto están impuestas por el fabricante.
2. **Biblioteca genérica (JDBC):** la biblioteca no conecta directamente con el producto. Tiene dos partes, el equivalente a la API fija, el frontal(habla con el cliente), y tiene la posibilidad de plugins. Es la más habitual.
3. **SQL inmerso (embedded):** consiste en programar sin usar bibliotecas. En lugar de hacer los accesos a una base de datos de forma indirecta, se escriben directamente en el código. El código en sql lo pasas por un preprocesador que lo convierte al código utilizado.
    ````c
	Tu ves y haces -> 2+3
	La librería hace -> add(2,3)
	````
4. **Lenguajes 4G (de cuarta generación):** lenguaje de programación cuyas sentencias del manejo de datos son parte del lenguaje. Un ejemplo sería PLSQL. Están pensados para realizar aplicaciones de gestión de los 1990-2000. De fábrica manejan menús. El lenguaje maneja formularios de fábrica.
- Todos estos mecanismos se basan en cursores.
- Ejemplo de código:
http://di002.edv.uniovi.es/~darioa/bdatos/mysql/Ejemplo_programa_MySQL_C_API.htm

---
*¿En qué se diferencia un create table frente a una búsqueda?*
El create sólo se hace una vez, la búsqueda la puedes realizar de forma ilimitada.

---
### **ENTRA:**
- *MODELO RELACIONAL:* relacion -> tabla, 
											   atributos -> columna, 
											   valores de atribs. en: dominio -> tipo de datos, 
											   dominios son: atómicos
											   tuplas -> fila
1. Una base de datos relacional tiene **integridad de entidad**, es decir, tiene clave primaria. Impide que haya datos repetidos.
2. Una base de datos mantiene la **integridad referencial**, es decir, tiene claves externas. Los valores de la clave externa tienen que existir donde son clave primaria.
---
♻️ Segunda parte -> [[BD Segunda parte 🚀]]