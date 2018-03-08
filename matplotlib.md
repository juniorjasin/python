# Basic plots with matplotlib

Matplotlib es una biblioteca para la generación de gráficos a partir de datos contenidos
en listas o arrays en el lenguaje de programación Python.

### Data Visualizacion 

Esta herramienta es util para la visualizacion de datos, como explorar los mismos, hallar patrones 
y relaciones entre variables

```python
# En general los graficos siguen esta forma:
import matplotlib.pyplot as plt
plt.plot(x,y)
plt.show()

# Para graficar poblacion a traves de los a años
year = [1950, 1970, 1990, 2010]
population = [2.519, 3.692, 5.263, 6.972]

# muestra un grafico donde se unen los puntos con lineas
plt.plot(year, population) # primer arg es eje X, segundo eje y.
plt.show()

# muestra un grafico donde figuran solo los puntos
plt.scatter(year, population)
plt.show()

# Para escalar nuestro grafico a escala logaritmica
plt.xscale('log')
```


### Histogramas

Utiles para explorar los data sets, y tener una idea de la distribucion de los datos.

```python
values = [0,0.6,1.4,1.6,2.2,2.5,2.6,3.2,3.5,3.9,4.2,6]
# hist recibe muchos argumentos, pero con bins indicamos cuantas barras queremos en nuestr histograma
plt.hist(values, bins = 3)
plt.show()
```


### Customization

Existen diferentes tipos de graficos, y tambien existen diferentes formas de parametrizar cada uno.
Vamos a elegir la forma apropiada segun:
- Los datos que tengamos
- Lo que querramos resaltar

```python
import matplotlib.pyplot as plt
year = [1950, 1951, 1952, ..., 2100]
pop = [2.538, 2.57, 2.62, ..., 10.85]

# Add more data
year = [1800, 1850, 1900] + year
pop = [1.0, 1.262, 1.650] + pop

plt.plot(year, pop)

# le ponemos un nombre a nuestros ejes
plt.xlabel('Year') 
plt.ylabel('Population')

# titulo del grafico
plt.title('World Population Projections')

# Con la primera lista sola, en el eje y cambiamos los valores para que vayan de a dos
# Si agregamos la segunda lista opcional, reemplazamos cada valor con un nombre,
# en este caso '2B' indica 2 billions.
# Las listas tienen que ser del mismo tamaño.
plt.yticks([0, 2, 4, 6, 8, 10],
 ['0', '2B', '4B', '6B', '8B', '10B'])
 

# Si queremos modificar el tamaño de cada punto segun el valor de la lista o array en un grafico scatter,
# dependiendo de la cantidad de poblacion en cada pais:
plt.scatter(x = gdp_cap, y = life_exp, s = np.array(pop) * 2)

# Especificamos el color de cada pais, si tenemos una lista 'col' donde por cada pais, posee un color,
# respetando el orden los paises.
# Con alpha, decimos que tan transparentes queremos que sean nuestros puntos, va de [0,...,1]
plt.scatter(x = gdp_cap, y = life_exp, s = np.array(pop) * 2, c = col, alpha = 0.8)

plt.show()
```
