# Comprehensions & Generators

Ahora vamos a ver los list y dictionaries comprehensions y los generators en python.

## List comprehension

Las list comprehensions son formas mas eficientes y acotadas de crear listas a partir de cualquier objeto
iterable. Las caracteristicas que tienen son:

- Colapsar for loops para crear listas en una sola línea de codigo
- Se componen:
    - Iterable
    - Variable Iterator (representa miembros de iterable)
    - Output expression

Ejemplo:

'''python
squares = [i ** 2 for i in range(10)]
print(squares)
#[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
'''

Para aclarar, la sintaxis en forma general seria algo asi:

`[output expression for iterator variable in iterable]`


Let's step aside for a while from strings. One of the ways in which lists can be used are in representing
multi-dimension objects such as matrices. Matrices can be represented as a list of lists in Python. 
For example a 5 x 5 matrix with values 0 to 4 in each row can be written as:

Una de las formas en que se pueden usar las listas es en la representación objetos multidimensionales como matrices.
Las matrices se pueden representar como una lista de listas en Python.
Por ejemplo, una matriz de 5 x 5 con valores de 0 a 4 en cada fila se puede escribir como:

'''python
#Create a 5 x 5 matrix using a list of lists: matrix
matrix = [[col for col in range(5)] for row in range(5)]

""" Lo que nos da la matriz que queriamos
matrix = [[0, 1, 2, 3, 4],
          [0, 1, 2, 3, 4],
          [0, 1, 2, 3, 4],
          [0, 1, 2, 3, 4],
          [0, 1, 2, 3, 4]]
"""
'''

### Conditionals in comprehensions

Podemos agregar una condicion simple `if` a la hora de crear una lista.
El `if` se realiza sobre el *iterable*, va al final en este caso.

'''python
[num ** 2 for num in range(10) if num % 2 == 0]
#[0, 4, 16, 36, 64] obtenemos esto
'''

Tambien, podemos agrear conditional `if-else` en la parte del output expression
El `if-else` se realiza sobre el *output expresion* por eso va antes del for loop.

'''python
[num ** 2 if num % 2 == 0 else 0 for num in range(10)]
#[0, 0, 4, 0, 16, 0, 36, 0, 64, 0] obtenemos esto
'''

### Resumen de la sintaxis

- Basic:
`[output expression for iterator variable in iterable]`

- Advanced:
`[output expression + conditional on output for iterator variable in iterable + conditional on iterable]`

### Dict comprehension

Ahora creamos dictionaries. La sintaxis es la misma excepto que usamos `{}` en vez de `[]` y tambien
separamos los key-values con `:`.

Ejemplo:

'''python
pos_neg = {num: -num for num in range(9)}
print(pos_neg)
{0: 0, 1: -1, 2: -2, 3: -3, 4: -4, 5: -5, 6: -6, 7: -7, 8: -8}
print(type(pos_neg))
<class 'dict'>
'''


## Diference between Comprehension & Generators

Las list comprehension generan listas, es decir, objetos que se cargan en memoria. Sin embargo,
hay casos donde no es deseable intentar crear estas listas, porque pueden ser demasiado
grandes y sobrepasar el tamaño de la memoria. Aca entran los generators.
Los generators no almacenan la lista en memoria, porque ni siquiera la contruye, pero 
si nos devuelve objetos del tipo `generator` que podemos iterar estos objetos al igual que cualquier otro iterable.
Esto que sucede con los generators es algo que se llama lazy evaluation, donde la evaluacion de 
la expresion es postergada hasta que realmente se necesita.
Cuando usamos `.items()` en diccionarios, o la función `range()`, Python crea generadores para usted detrás de las escenas.

### Generator expresion

La sintaxis es igual a las list comprehension, solo que reemplazamos los `[]` con `()`


Ejemplo:

'''python
#List of strings
fellowship = ['frodo', 'samwise', 'merry', 'aragorn', 'legolas', 'boromir', 'gimli']

#List comprehension
fellow1 = [member for member in fellowship if len(member) >= 7]

#Generator expression
fellow2 = (member for member in fellowship if len(member) >= 7)

#Esto crea una lista que sobrepasa el tamaño de la memoria y no termina hasta el overflow
>>> [num for num in range(10 ** 10000000)]

#Esto nos devuelve un generator, sin alojar la lista en memoria.
>>> res = (num for num in range(10 ** 10000000))
>>> <generator object <genexpr> at 0x7f9f36fe8bf8>
>>> next(res)
0
'''

### Generator functions

Las funciones del generador son funciones que, al igual que las expresiones generadoras, producen una
serie de valores, en lugar de devolver un solo valor. Una función de generador se define como una función normal,
pero cada vez que genera un valor, utiliza la palabra clave `yield` en lugar de `return`.

En resumen:

- Son funciones que cuando son llamdas producen generator objects
- Estan definidas como cualquier otra funcion
- Otorga una secuencia de valores en lugar de devolver un solo valor
- Genera un valor con la palabra clave `yield` en vez de `return`

'''python
#Create a list of strings
lannister = ['cersei', 'jaime', 'tywin', 'tyrion', 'joffrey']

#Define generator function get_lengths
def get_lengths(input_list):
    """Generator function that yields the
    length of the strings in input_list."""

    # Yield the length of a string
    for person in input_list:
        yield len(person)

#Print the values generated by get_lengths()
for value in get_lengths(lannister):
    print(value)
'''
