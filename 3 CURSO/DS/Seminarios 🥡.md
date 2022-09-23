# 23 Sept 2022 🍮
---
## Herencia

### Ejercicio 1
**¿Una pila es un vector (ArrayList)?**
- No porque si heredamos, en este caso se hereda todo, y puede no servirnos la implementación. Se podrían insertar elementos en cualquier lugar de la pila, cosa que no se puede hacer.

- Hay que evitar que al modificar código afecte al cliente. Nuestro código ha de ser transparente para él.

- No sirve el criterio **Es-un**. No sirve que nos suene bien. No es un criterio válido para aplicar la herencia: ¿un dibujo **es una** figura? -> NO tiene por que

**Criterio para decidir si algo es subtipo de otro** -> ***criterio de pertenecia***: un objeto pertenecerá a una jerarquía si se quiere poder conectar a un cliente para que éste lo use como a uno más de la misma

¡Nunca debe surgir una jerarquía como una manera de clasificación!


### Ejercicio 3
No es correcto porque si existiese un método double getValor(), ¿qué devolvería?. Que compile es una cosa, y que tenga sentido es otra muy distinta.

- **Las interfaces surgen por la necesidad de declarar unas responsabilidades que un objeto ha delegado**
- **La jerarquía surge con alternativas de implementación de dichas responsabilidades**

### Ejercicio 4
**¿Un cuadrado es un rectángulo?**
- No es lo mismo redimensionar un rectángulo que un cuadrado
- Hay que razonarlo todo siempre en función de los clientes
- Para el cliente, un cuadrado no es un rectángulo

---
