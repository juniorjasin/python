# Generatin Randon Numbers

### Caso practico

El juego consiste en determinar las chances que tenes de subir al 60 escalones del Empire State 
si tiras un dado 100 veces y
- Si sale 1 o 2 bajas un escalon (no se puede bajar menos que cero)
- Si sale 3, 4 o 5 subis un escalon
- si sale 6, volves a tiara y el numero que sale es la cantidad de escalones que subis

Ademas tenes un 0.1% de chances de caerte por las escaleras y empezar de cero.

### Resolucion
El problema se ataca desde un punto estadistico, haciendo una simulacion de 500 juegos.

Primero se resuelve el problema de un solo juego, con 100 tiradas de dado (el dado es simulado
con la funcion rand() de numpy), con la logica en if-elif-else.
Tambien se utiliza rand() para obtener un numero aleatorio y si es menor 0.001 el jugador
comienza de cero, simulando la probabilidad de caida del mismo.
Se almacenan el avance de los escalones(step) en una lista random_walk.

Esto se encapsula en una simulacion de 500 veces jugadas este juego, Y al final de cada juego
almacenando el progreso del jugador en las 100 tiradas de dados.

Al finalizar en all_walks tenemos una lista de listas, con todos las 500 jugadas hechas y su progreso
en cada indice.
Ahora, convertimos all_wallks en un numpy array para poder aplicarle la transpuesta a este array 2D.
Lo que nos facilita la extraccion en la ultima fila, de como terminaron todas las jugadas, es decir,
en que escalon finalizo el jugador despues de las 100 tiradas de dados en los 500 intentos.

Con esta ultima fila descrita, armamos un numpy array, para poder graficar un histograma
que nos muestre una distribucion de todas las finalizaciones del juego.
Se observa graficamente que la mayoria de las veces, el jugador finaliza el juego por encima
de los 60 escalones, por lo que tiene mas chances de ganar que de perder.

Al final se realiza el calculo de que porcentaje de simulaciones gano el jugador,
nos da que un 78.4% de las veces gano (finalizo en 60 escalones o mas).

```python
import matplotlib.pyplot as plt
import numpy as np
np.random.seed(123)
all_walks = []

# Simulate random walk 500 times
for i in range(500) :
    random_walk = [0]
    for x in range(100) :
        step = random_walk[-1]
        dice = np.random.randint(1,7)
        if dice <= 2:
            step = max(0, step - 1)
        elif dice <= 5:
            step = step + 1
        else:
            step = step + np.random.randint(1,7)
        if np.random.rand() <= 0.001 :
            step = 0
        random_walk.append(step)
    all_walks.append(random_walk)

# Create and plot np_aw_t
np_aw_t = np.transpose(np.array(all_walks))

# Select last row from np_aw_t: ends
ends = np_aw_t[-1]

# Plot histogram of ends, display plot
plt.hist(ends)
plt.show()

# Calculo % simulaciones ganadas
count = 0
for e in ends:
    if e >= 60:
        count = count + 1

print('porcentaje de simulaciones ganadas:' + str( c / 500 ) )
```
