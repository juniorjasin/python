# Importing data into python


### context manager

La forma sencilla de abrir un archivo en python es con la funcion `open()` y al finalizar hay que recordar hacer
un `close()`. Existe una forma con la cual no es necesario acordarse de esto, utilizando el context manager,
el cual te permite tener una conexion con un archivo dentro de un contexto:

```python
with open('huck_finn.txt') as file:
    # While still within this construct, the variable file will be bound to open('huck_finn.txt')
    print(file.text())
    print(file.readline())
```

## The importance of flat files in data science

Los flat files son archivos que representan una tabla, y contienen records que es una fila con campos o
atributos y columnas que representan caracteristicas o atributos. Estos archivos pueden o no tener un header
de las columnas. Estas tablas NO son relacionales.
Algunas extensiones de estos archivos pueden contener tablas con strings y numeros, campos que querramos visualizar como una
tabla similar a una planilla de calculo. Pero otros archivos pueden contener numeros que representen una imagen.
Dependiendo de como lo querramos visualizar y trabajar con ellos podemos optar por utilizar  `pandas` para el primero
caso o `numpy` para el segudo. 


## Using NumPy to import flat files

Porque numpy?

- Arrays NumPy: estándar para almacenar datos numéricos
- Esencial para otros paquetes: p. scikit-learn

Usaremos las funciones: `loadtxt()` `genfromtxt()`

Ejemplo de uso:

```python
import numpy as np
filename = 'MNIST.txt'

# almacenamos en data y decimos que el separador es el caracter `,`
data = np.loadtxt(filename, delimiter=',') 

# Si la primera fila es un header con los nombres de las columnas la evitamos
data = np.loadtxt(filename, delimiter=',', skiprows=1) 

# Si solo queremos la 1ra o 3ra columna
data = np.loadtxt(filename, delimiter=',', skiprows=1, usecols=[0, 2]) 
```

### Trabajando con tipos de datos mixtos

Gran parte del tiempo necesitará importar conjuntos de datos que tengan diferentes tipos de datos en diferentes columnas;
una columna puede contener cadenas y otras carrozas, por ejemplo. La función `np.loadtxt()` no es util en este caso.
Hay otra función, `np.genfromtxt()`, que puede manejar tales estructuras.
Si pasamos `dtype = None` a él, descubrirá qué tipos debe ser cada columna.

Importe `'titanic.csv'` utilizando la función `np.genfromtxt()` de la siguiente manera:

```python
data = np.genfromtxt('titanic.csv', delimiter=',', names=True, dtype=None)
```

Aquí, el primer argumento es el nombre del archivo, el segundo especifica el delimitador y el tercer argumento
los nombres nos dicen que hay un encabezado. Debido a que los datos son de diferentes tipos, los datos son un 
objeto llamado structured array. Porque los numpy arrays deben contener elementos del mismo tipo, 
la structured array resuelve esto al ser una array 1D, donde cada elemento del array es una fila del archivo 
plano importado.

Acceder a filas y columnas de los structured array es superintuitivo: para obtener la fila i, simplemente ejecute
`data[i]` y para obtener la columna con el nombre 'Fare', ejecute `data['Fare']`.

Para importar archivos del tipo `.csv` existe una funcion que nos resulve el trabajo.
tiene los valores predeterminados `delimiter = ','` y `names = True` además de `dtype = None`!
```python
d = np.recfromcsv('titanic.csv')
```

## Importing flat files using pandas

Lo que un Data Scientist necesita:
- Estructura (s) de datos etiquetadas bidimensionales
- Columnas de tipos potencialmente diferentes
- Manipulate, slice, reshape, groupby, join, merge
- Realizar estadísticas
- Trabajar con time series data



### Manipulating pandas DataFrames
Algunas de las ventajas de trabajar con DataFrames son:

- Análisis de datos exploratorios
- disputa de datos
- Preprocesamiento de datos
- Construcción de modelos
- Visualización
- Es un estándar y best practice usar pandas


```python
# Import pandas as pd
import pandas as pd

# Assign the filename: file
file = 'titanic.csv'

# Read the file into a DataFrame: df
df = pd.read_csv(file)

# Read the first 5 rows of the file into a DataFrame: data
data = pd.read_csv(file, nrows=5, header=None)

""" Tab-delimited, anula los comentarios (lo que este despues de '#' y reemplaza los valores de la lista,
en este caso 'Nothing' por NA o NaN."""
data = pd.read_csv(file, sep='\t' , comment='#', na_values=['Nothing'])
```

## Loading a pickled file

There are a number of datatypes that cannot be saved easily to flat files, such as lists and dictionaries. 
If you want your files to be human readable, you may want to save them as text files in a clever manner. 
JSONs, which you will see in a later chapter, are appropriate for Python dictionaries.

However, if you merely want to be able to import them into Python, you can serialize them. 
All this means is converting the object into a sequence of bytes, or a bytestream.

Hay varios tipos de datos que no se pueden guardar fácilmente en archivos planos, como listas y diccionarios.
Si queremos que nuestros archivos sean legibles, se pueden guardar al igual archivos de texto pero 
de una manera inteligente. Los JSON, son apropiados para los diccionarios de Python.

Sin embargo, si simplemente desea poder importarlos a Python, puede [serializarlos](https://en.wikipedia.org/wiki/Serialization), es decir,
que se puede convertir el objeto en una secuencia de bytes, o un bytestream.

El módulo `pickle` de python implementa un algoritmo fundamental pero poderoso para serializar y deserializar un
Python object structure. "Pickling" es el proceso mediante el cual una jerarquía de objetos de Python se convierte en
una secuencia de bytes, y "unpickling" es la operación inversa, mediante la cual una secuencia de bytes se convierte 
de nuevo en una jerarquía de objetos.

Ejemplo:
```python
# Import pickle package
import pickle

# Open pickle file and load data: d
with open('data.pkl', 'rb') as file:
    d = pickle.load(file)

# Print d
print(d)

# Print datatype of d
print(type(d)) # <class 'dict'>
```

## Loading Excels files

Los archivos de Excel son muy utilizados en todo tipo de areas, por lo que es conveniente tener una forma
de importarlos.

Vamos a utilizar `pandas` para importar estos archivos de extension `.xlsx`, asi poder extraer cada una de las
hojas de calculo y dentro de cada una poder explorar las cabeceras de las tablas.

Ejemplo de como ver las hojas de un archivo de excel

```python
# Import pandas
import pandas as pd

# Assign spreadsheet filename: file
file = 'battledeath.xlsx'

# Load spreadsheet: xl
xl = pd.ExcelFile(file)

# Print sheet names 
print(xl.sheet_names)
```

Ahora que ya cargamos el archivo, para acceder a una hoja de calculo podemos acceder con el index o con
el nombre y obtenemos un `DataFrame`:
```python
# Load a sheet into a DataFrame by name: df1
df1 = xl.parse('2004')

# Load a sheet into a DataFrame by index: df2
df2 = xl.parse(0)
```

- Ahora vamos a personalizar la carga del archivo `.xlxs`

Vamos a usar los argumentos adicionales `skiprows`, `names` y `parse_cols`. Para omitir filas, 
nombrar las columnas y designe qué columnas analizar, respectivamente. Todos estos argumentos se pueden asignar 
a listas que contienen los números de fila específicos, cadenas y números de columna, según corresponda.

```python
"""Parse the second sheet by index. In doing so, parse only the first column with the parse_cols parameter,
skip the first row and rename the column 'Country'. The argument passed to parse_cols, names, skiprows needs to be of type list."""
df2 = xl.parse(1, parse_cols=[0], skiprows=[0], names=['Country'])
```
