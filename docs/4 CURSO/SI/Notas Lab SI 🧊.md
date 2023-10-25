# 1. Bloque de búsqueda

# Lab 1

## Guía para instalar aima-python

- [Descargarlo de aquí como .zip](https://github.com/aimacode/aima-python)
- Descomprimirlo
- Dentro de la carpeta pegar el fichero `search4e-Busqueda_2023_2024.ipynb` del campus
- Meterlo en la carpeta del aima descargada
- Darle doble click
- Seleccionar el kernel (Python 3.9.10)
- Ejecutar

![](./img/Pasted%20image%2020230920165329.png)

## Ejercicio 2

![](./img/Pasted%20image%2020230920165026.png)

![](./img/Pasted%20image%2020230920165055.png)

- Comprobar que el coste es el indicado en el Word

- Para cambiar si usa el h0, el h1 o el h2 modificar aquí:

![](./img/Pasted%20image%2020230920165644.png)

- Modificamos el h2:

````python
# Mi solución
sum = 0;

for i in range(9):

	if node.state[i] != 0:
	
	sum += abs(i//3 - self.goal.index(node.state[i])//3) + abs(i%3 - self.goal.index(node.state[i])%3)

return sum

#------------------------------------------------------------

# Solución del profe
sum = 0;

for i in range(9):

	if (i!=0):
	
	X1, Y1 = (node.state.index(i)%3, node.state.index(i)//3) #board positions of the i tilde in node.state
	
	Xg, Yg = (self.goal.index(i)%3, self.goal.index(i)//3) #board positions of the i tilde in goal.state
	
	sum += abs(X1-Xg) + abs(Y1-Yg)

return sum
````

- h2 es el más eficiente en tiempo

## Ejercicio 4

![](./img/Pasted%20image%2020230920173558.png)

- Hay que modificar esta función:

![](./img/Pasted%20image%2020230920172003.png)

- Solución:
````python
ok = False

  

while not ok:

	node = frontier.pop()
	
	if node.path_cost > reached[node.state].path_cost:
	
		DUMMY_NODES += 1
	
	else:
	
		ok = True
````

## Ejercicio 5

- Solución
````python
# Reexpansion control, number of states reexpanded

if node.state in expanded:

	STATES_REEXPANDED += 1

else:

	expanded[node.state] = True

# counting expansions

NODES_EXPANDED += 1
````

## Ejercicio 6

![](./img/Pasted%20image%2020230920174343.png)

![](./img/Pasted%20image%2020230920174527.png)

- Para ejecutar el PA* usamos la función weighted_astar_search

![](./img/Pasted%20image%2020230920175226.png)

# Lab 2

![](./img/Pasted%20image%2020230927170000.png)
# Lab 3

- El elitismo consiste en conservar los mejores que tengamos (no perder una mejor solución, sino mantenerla)
	- Lo que pretende conseguir es que las diferencias entre los buenos y los malos sean más grandes
	- Para escalar el fitness podemos elevar dos números a una potencia muy grande, para que su diferencia sea mayor (por ejemplo)

# Lab 4

# Lab 5 

## Ejercicio 1

- La probabilidad de que tenga cáncer de pulmón es 48,87%
- Como ha viajado al extranjero, ahora la probabilidad es un 37,15%
	- Se ha decrementado porque ha aumentado la probabilidad de que tenga tuberculosis debido a su viaje en el extranjero