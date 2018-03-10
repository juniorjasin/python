# numpy

Es un package de python, que provee una alternativa a las python list que provee el lenguaje, los numpy arrays, 
se utilizan para tener una mejor performance que las listas que vienen implementadas en python, y nos facilita 
hacer calculos sin tener que recorrer cada lista.

``` python
import numpy as np
```

### numpy arrays
estos arrays contienen un solo tipo de valor y si ponemos valores de diferentes tipos los castea a un mismo tipo,
esto se denomina type coercion.

```python
np.array([1,2,3])
array([1, 2, 3])

np.array([1,'a',True])
array(['1', 'a', 'True'], dtype='<U21')
```

### numpy subsetting
Si queremos un subconjunto de un numpy array poniendo una condicion podemos hacer lo siguiente:

```python 
# Creamos nuestro array bmi de ejemplo
>>> bmi = np.array([21.852, 20.975, 21.75, 24.747, 21.441])

# Accedemos a un indice al igual que las listas
>>> bmi[1]
20.975

# si queremos saber en que posiciones los valores son mayores a 21
# Veamos que nos devuelve un array de booleans y True cuando se cumple la condicion
>>> bmi > 21
array([  True,   False,  True,  True,  True])
# array([21.852, 20.975, 21.75, 24.747, 21.441])

# Ahora si queremos un array con los valores donde se cumple la condicion.
# Es como decir, selecciona los elementos en bmi, donde cada bmi es mayor a 21.
>>> bmi[bmi > 21]
array([21.852, 21.75 , 24.747, 21.441])

# Tambien podemos ponerlo en una variable
>> condicion = bmi > 21
>>> bmi[condicion]
array([21.852, 21.75 , 24.747, 21.441])
```

### 2D Numpy Arrays

Los numpy arrays son del tipo ndarray, que es N-dimensional array, esto quiere decir que podemos tener arrays
de la dimension que querramos. 
Podemos crear un array 2D a partir de una lista de listas en python.

```python
>>> np_2d = np.array([[10,11,12,13,14],[20,21,22,23,24]])
>>> np_2d
array([[10, 11, 12, 13, 14],
       [20, 21, 22, 23, 24]])
# shape es un atributo del array, y nos dice la forma de nuestro array, con 2 filas y 3 columnas.
>>> np_2d.shape
(2, 5)
```
Numpy nos permite hacer un subsetting mas avanzado y simple.

```python
# Tenemos nuestro array 2D
>>> np_2d
array([[10, 11, 12, 13, 14],
       [20, 21, 22, 23, 24]])
       
# Para seleccionar una fila completa
>>> np_2d[0]
array([10, 11, 12, 13, 14])

# Para seleccionar un solo elemento de nuestro array 2D
>>> np_2d[1][3]
23

# Pero existe una notacion mas conveniente
>>> np_2d[1,3]
23

# Y nos permite usar nuestro operador ':' dentro de los corchetes
>>> np_2d[:,1:3]
array([[11, 12],
       [21, 22]])
       
# Esto nos devuelve de todas las filas, los elementos en las posiciones uno inclusive hasta la tercera posicion
# sin incluirla, algo asi [1,3).
# Lo interesante es que esto a su vez es un array 2D bastante simple de extraer.
```

### Basic Statistics

Numpy provee herramientas para el calculo de valores estadisticos de manera sencilla. Muchas veces se
utilizan estas funciones para determinar si nuestros datos poseen valores aceptables.

```python
# Si queremos calcular el promedio en un array 2D 
# np_city contiene 2 columnas, una con la altura de las personas y otra con su peso.

# altura promedio de las personas
np.mean(np_city[:,0]) 

# mediana de la altura
np.median(np_city[:,0])

# correlacion entre altura y peso
np.corrcoef(np_city[:,0],np_city[:,1])

# desvio estandar
np.std(np_city[:,0])
```

### generando datos

Numpy tambien nos da la posibilidad de generar nuestras propias muestras de forma realistica.
Veamos como podemos generar valores para altura y peso de 5000 personas.

```python
avg = 1.75 # promedio de altura
dsd = 0.20 # distribution standard deviation
samples = 5000 # cantidad de muestras que quiero generar

height = np.round(np.random.normal(avg, dsd, samples), 2)
weight = np.round(np.random.normal(60.32, 15, samples), 2)

# ahora unimos el peso y la altura en un array 2D de dos columnas
np_city = np.column_stack((height, weight))
```

## Boolean Operators

Antes, los operadores como < y >= funcionaban con Numpy arrays. 
Desafortunadamente, esto no es cierto para los operadores booleanos and, or, y not.

Para usar estos operadores con Numpy, necesitará np.logical_and(), np.logical_or() y np.logical_not()

```python
import numpy as np
my_house = np.array([18.0, 20.0, 10.75, 9.50])
your_house = np.array([14.0, 24.0, 14.25, 9.0])

# my_house greater than 18.5 or smaller than 10
print(np.logical_or(my_house > 18.5, my_house < 10))

```














