♻️ Primera parte -> [[BD Primera parte 💿]]

---
# 28 Marzo 2022
---
- **El modelo relacional** fue inventado por E.F. Codel.
- De los 70-80 se utilizaba el modelo de datos en red.
- De los 80-90 llega el **modelo relacional**, que se sigue utilizando a día de hoy.

---
### Lenguajes de datos
 - TIPOS
	- **Procedimental:** tenemos un conjunto de operaciones y las combinamos para llegar a un resultado final (Ej: C).
	- **Declarativos:** no hay que decirle al sistema los pasos que ha de dar para llegar al resultado, sino que das el resultado y el sistema realiza las operaciones necesarias para llegar a él (Ej: lenguaje matemático).
	-----Complementables con-----
	- **Formales:** se basa en principios matemáticos de forma directa y la sintaxis es más matemática/formal.
	- **Comerciales:** coge los fundamentos de loslenguajes formales y les adjudica una sintaxis más bonita (entendible).
---
# Álgebra relacional, operaciones 🎨
NOTA: En todas las operaciones se eliminan los elementos duplicados.
#### Unarias
- **Selección:** usa el símbolo sigma "σ". Equivale al from.
- **Proyección:** permite quedarse con los elementos de la colección que interesan, usa el símbolo "П". Equivale al select.
- **Renombrar:** equivalente al as, usa el símbolo  ro "ρ".
#### Binarias
- **Producto cartesiano:** usa el símbolo "x". El resultado es otro conjunto, los elementos del resultado concatenan los datos con el del primer conjunto. Genera todas las posibles combinaciones de tuplas del conjunto "a" con las del conjunto "b". Es una operación asociativa, da igual el orden, no necesita paréntesis
- **Unión:** usa el símbolo "U". Devuelve el conjunto que resulta de unir las tuplas del primer conjunto con las tuplas del segundo conjunto. Las relaciones han de ser compatibles.
- **Diferencia:** al primer conjunto le quitamos el segundo, usa el símbolo "-".
#### Derivadas
- **Intersección:** usa el símbolo "∩".
- **Producto natural:** igualamos clave primaria con clave externa.
- **Esquema:** es el conjunto de atributos, se representa dentro de dos paréntesis "(x)".
---
# 18 Abril 2022 📍:)
---
## Restricciones de integridad
- Son un predicado "p", algo que siempre tiene que ser verdadero en la base de datos.
- Reciben el nombre de **restricciones genéricas**.
- Se usan las cláusulas check -> check(p).
- A veces trabajamos con casos particulares llamados **restricciones específicas**.
- Los dominios, las claves (super, candidato), claves externas son restricciones específicas. 
- Las **restricciones específicas** se usan porque suele haber una forma más eficiente de comprobarlas.
![[especificas.png||600]]
![[restricciones1.png||500]]
![[restricciones 2.png||500]]

---
## Dominios
- Tipos de datos base.
![[dominios 1.png||500]]
![[dominios 2.png||500]]

---
## Restricciones de integridad referencial
![[referencial.png||500]]
- Los problemas surgen al borrar la entidad r1.

**Alternativas para mantener la integridad referencial** (Cosas que puedo hacer en la r2 cuando se borra la tabla r1):
- Restringir -> **NO ACTION**
- Propagar en cascada: todas las cuentas a nombre de dni 1 pasan a ser del dni 2
- Poner a nulo -> **SET NULL**
- Poner como default -> **SET DEFAULT**
---
## Asertos
![[asertos.png||500]]

---
## Dependencias funcionales
![[funcionales.png||500]]
- Como deducir dependencias
	- Ir aplicando la definición
	- Usando reglas de inferencia (**Reglas de Armstrong**)

### Reglas de Armstrong
*Fundamentales*
1. **Reflexividad**: genera las dependencias triviales x->y x 
2. **Aumentación**: x->y, wx->wy
3. **Transitividad**: x->y, y->z, x->z
*Derivadas*
4. **Unión**: x->y, x->yz, x->z
5. **Descomposición**: x->yz, x->z, x->y
6. **Pseudotransitividad**: x->y, wy->z, wx->z
---