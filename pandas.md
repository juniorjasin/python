# Pandas

pandas is an open source, BSD-licensed library providing high-performance, easy-to-use data 
structures and data analysis tools for the Python programming language. Built on numpy.

pandas es una biblioteca de código abierto con licencia de BSD que proporciona estructuras
de datos y herramientas de análisis de datos de alto rendimiento y fácil de usar para el 
lenguaje de programación Python.

¿Qué problema resuelven los pandas?
Python siempre ha sido excelente para la eliminación y preparación de datos,
pero no tanto para el análisis y el modelado de datos. pandas ayuda a llenar este
vacío, lo que le permite llevar a cabo todo su flujo de trabajo de análisis de 
datos en Python sin tener que cambiar a un lenguaje más específico de dominio como R.

## Aspectos destacados de la biblioteca

- Un objeto **DataFrame** rápido y eficiente para la manipulación de datos con indexación integrada.

- Herramientas para leer y escribir datos entre estructuras de datos en memoria y diferentes formatos:
  CSV y archivos de texto, Microsoft Excel, bases de datos SQL y el rápido formato HDF5.
  
- Alineación inteligente de datos y manejo integrado de datos faltantes: obtenga una alineación automática
  basada en etiquetas en los cálculos y manipule fácilmente los datos desordenados en una forma ordenada.
  
- Reestructuración y rotación flexible de conjuntos de datos.

- etiquetado inteligente de slicing, indexación sofisticada y subconjunto de grandes conjuntos de datos.

- Las columnas pueden insertarse y eliminarse de estructuras de datos para la mutabilidad de tamaño.

- Agregando o transformando datos con un poderoso group by engine que permite dividir-aplicar-combinar
  operaciones en conjuntos de datos.

- merging and joining de conjuntos de datos de alta performance.

- La indexación jerárquica del eje proporciona una forma intuitiva de trabajar con datos de alta 
  dimensión en una estructura de datos de menor dimensión.

- Time series-functionality: generación de rango de fechas y conversión de frecuencia, 
  estadísticas de ventanas en movimiento, regresiones lineales de ventanas móviles, cambio de 
  fecha y retardo. Incluso crea compensaciones de tiempo específicas de dominio y únete a 
  series de tiempo sin perder datos.


- Muy optimizado para el rendimiento, con rutas de código críticas escritas en Cython o C.

- Python con pandas está en uso en una amplia variedad de dominios académicos y comerciales, 
  que incluyen finanzas, neurociencia, economía, estadística, publicidad, análisis web y más.
  

Instalacion:
```
pip install pandas
```

### Uso de pandas

```python
# Pre-defined lists
names = ['United States', 'Australia', 'Japan', 'India', 'Russia', 'Morocco', 'Egypt']
dr =  [True, False, False, False, True, True, True]
cpc = [809, 731, 588, 18, 200, 70, 45]

# Import pandas 
import pandas as pd

# Create dictionary my_dict with three key:value pairs: my_dict
my_dict = {
    'country':names,
    'drivers_right':dr,
    'cars_per_cap':cpc
}

# Build a DataFrame cars from my_dict: cars
cars = pd.DataFrame(my_dict)

print(cars)

# Obtendriamos la siguiente salida
'''
   cars_per_cap        country drivers_right
0           809  United States          True
1           731      Australia         False
2           588          Japan         False
3            18          India         False
4           200         Russia          True
5            70        Morocco          True
6            45          Egypt          True
'''

# La primera columna automaticamente se llena con integers del 0-6
# Ahora para poner nuestro propio label a cada fila hacemos

# Definition of row_labels
row_labels = ['US', 'AUS', 'JAP', 'IN', 'RU', 'MOR', 'EG']

# Specify row labels of cars
cars.index = row_labels

''' Ahora observamos la tabla asi
cars_per_cap        country drives_right
US            809  United States         True
AUS           731      Australia        False
JAP           588          Japan        False
IN             18          India        False
RU            200         Russia         True
MOR            70        Morocco         True
EG             45          Egypt         True
'''
```

### CSV a DataFrame
Poner datos en un diccionario y luego construir un DataFrame funciona, pero no es muy eficiente.
¿Qué pasa si estás lidiando con millones de observaciones? En esos casos, los datos generalmente
están disponibles como archivos con una estructura regular. Uno de esos tipos de archivos es el
archivo CSV, que es la abreviatura de "valores separados por comas".

Para importar desde un archivo csv:

```python
path_to_file = 'cars.csv'
cars = pd.read_csv(path_to_file)

''' y obtenemos:
Unnamed: 0  cars_per_cap        country drives_right
0         US           809  United States         True
1        AUS           731      Australia        False
2        JAP           588          Japan        False
'''

# Pero la primera columna no tiene label, entonces le agregamos diciendo cual columna es el indice:
cars = pd.read_csv('cars.csv', index_col=0)

'''
     cars_per_cap        country drives_right
US            809  United States         True
AUS           731      Australia        False
JAP           588          Japan        False
'''
```

## Index and Select Data

### Square brackets
puede indexar y seleccionar Pandas DataFrames de muchas maneras diferentes. La forma más simple,
pero no la más poderosa, es usar corchetes.

Ejemplo:
```python
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Imprimir la columna 'country'
print(cars['country'])

''' Nos imprime algo asi, con una linea al final, agregando un label, pero no es un objeto DataFrame.
    Es un objeto 'pandas.core.series.Series', los objetos del tipo series agregan un label y con 
    varios series podemos obtener un DataFrame.
    
US     United States
AUS        Australia
JAP            Japan
Name: country, dtype: object
'''


# Print out country column as Pandas DataFrame
print(cars[['country']])
''' Ahora nos da un objeto DataFrame y nos saca el label del final.
           country
US   United States
AUS      Australia
JAP          Japan
IN           India
'''

# Print out DataFrame with country and drives_right columns
print(cars[['country','drives_right']])

''' Veriamos algo asi:
           country drives_right
US   United States         True
AUS      Australia        False
JAP          Japan        False
'''
```

Los corchetes pueden hacer más que simplemente seleccionar columnas. También puede usarlos para
obtener filas u observaciones de un DataFrame. La siguiente llamada selecciona las primeras cinco 
filas del DataFrame de cars:

```python
cars[0: 5]
```

El resultado es otro DataFrame que contiene solo las filas que especificó.

```python
# Print out first 3 observations
print(cars[0:3])

''' Vamos a ver esto:
     cars_per_cap        country drives_right
US            809  United States         True
AUS           731      Australia        False
JAP           588          Japan        False
'''
```



## Advanced methods

### loc & iloc

Con `loc` e `iloc` puede realizar prácticamente cualquier operación de selección de datos en DataFrames
que pueda imaginar. 
- `loc` está basado en etiquetas, lo que significa que debe especificar filas y 
   columnas en función de sus etiquetas de fila y columna. 
-  `iloc` está basado en índices enteros, por lo que debe especificar filas y columnas por su índice carentero.
    
```python
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Print out observation for Japan
print(cars.loc['JAP'])
'''
    cars_per_cap      588
    country         Japan
    drives_right    False
    Name: JAP, dtype: object
'''

# Print out observations for Australia and Egypt
print(cars.iloc[[1,6]]) 

'''
     cars_per_cap    country drives_right
AUS           731  Australia        False
EG             45      Egypt         True
'''

# Print out the drives_right value of the row corresponding to Morocco (its row label is MOR)
print(cars.loc[['MOR'],['drives_right']])

'''
    drives_right
MOR         True
'''

# Print out a sub-DataFrame, containing the observations for Russia and Morocco and the columns country and drives_right
print(cars.loc[ ['RU', 'MOR'], ['country', 'drives_right'] ])

'''
     country drives_right
RU    Russia         True
MOR  Morocco         True
'''

# It's also possible to select only columns with loc and iloc
cars.loc[:, 'country']
cars.iloc[:, 1]

cars.loc[:, ['country','drives_right']]
cars.iloc[:, [1, 2]]

# Print out drives_right column as DataFrame
print(cars.iloc[:, [2] ])
# or
print(cars.loc[:, ['drives_right'] ])
```


## Filtering Pandas DataFrame

Vamos a ver como filtrar datos de un DataFrame con operadores booleanos.

Recordemos la tabla original

```python
     cars_per_cap        country drives_right
US            809  United States         True
AUS           731      Australia        False
JAP           588          Japan        False
IN             18          India        False
RU            200         Russia         True
MOR            70        Morocco         True
EG             45          Egypt         True
```


```python
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Extract drives_right column as Series: dr
# NOTA: tiene que ser como Series sino no funciona.

dr = cars['drives_right']
print(dr)

''' Obtenemos la columna de tipo Series, con los valores booleanos
US      True
AUS    False
JAP    False
IN     False
RU      True
MOR     True
EG      True
Name: drives_right, dtype: bool
'''

#  Ahora usamos dr, para subdividir cars.
# Como dr es una columna de valores booleanos, esta operacion, nos va a devolver
# un DataFrame donde cada fila donde 'drives_right' sea True solamente.
sel = cars[dr]

# Print sel
print(sel)
'''
     cars_per_cap        country drives_right
US            809  United States         True
RU            200         Russia         True
MOR            70        Morocco         True
EG             45          Egypt         True
'''

# Ahora queremos determinar los paises donde hay mas de 500 autos per capita

# Create car_maniac: observations that have a cars_per_cap over 500
cpc = cars['cars_per_cap'] # Panda series de autos por capita
many_cars = cpc > 500 # Creamos boolean Series con los que tienen mas de 500 per capita
car_maniac = cars[many_cars] # Le pasamos el boolean Series a cars, y nos devuelve las filas
                             # de los paises que cumplen la condicion

# Print car_maniac
print(car_maniac)
'''
     cars_per_cap        country drives_right
US            809  United States         True
AUS           731      Australia        False
JAP           588          Japan        False
'''
```

Recuerde acerca de np.logical_and (), np.logical_or () y np.logical_not (), También se pueden usar
en Pandas Series para realizar operaciones de filtrado más avanzadas.

```python
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Vamos a necesitar numpy (porque Pandas esta basado en numpy)
import numpy as np

cpc = cars['cars_per_cap']
between = np.logical_and(cpc > 10, cpc < 80)
medium = cars[between]

''' Obtenemos
     cars_per_cap  country drives_right
IN             18    India        False
MOR            70  Morocco         True
EG             45    Egypt         True

'''
```

### Loop over DataFrame
    
La iteración sobre un Pandas DataFrame normalmente se hace con el método `iterrows()`. Usado en un bucle for,
cada observación se repite y en cada iteración están disponibles la row label y el contenido real de la fila:

```python
para lab, row en brics.iterrows ():
     ...
```

Los datos de fila generados por `iterrows()` en cada ejecución son un Pandas Series. 
Se puede seleccionar fácilmente variables de la serie Pandas usando corchetes:

```python
for lab, row in brics.iterrows() :
    print(row['country'])
```

### Add column
Agregar la columna que indique el largo del nombre de cada pais al DataFrame brics:

```python
for lab, row in brics.iterrows() :
    brics.loc[lab, "name_length"] = len(row["country"])
```

Usar `iterrows()` para iterar sobre cada observación de un Pandas DataFrame es fácil de entender,
pero no muy eficiente. En cada iteración, estás creando una nueva Pandas Series.

Si queremos agregar una columna a un DataFrame llamando a una función en otra columna, el método `iterrows()`
en combinación con un bucle for no es la forma preferida de hacerlo. En cambio, usamos `apply()`.

Compare la versión de `terrows()` con la versión de `apply()` para obtener el mismo resultado en el DataFrame brics:

Compare the `iterrows()` version with the `apply()` version to get the same result in the brics DataFrame:

```python
for lab, row in brics.iterrows() :
    brics.loc[lab, "name_length"] = len(row["country"])

brics["name_length"] = brics["country"].apply(len)
```
