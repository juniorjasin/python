# Iterables vs. Iterators

Los iterables y los iteradores.
- Un iterable es un objeto que puede devolver un iterator, 
- Mientras que un iterator es un objeto que conserva el estado y produce el siguiente valor cuando llama a `next()` en él.



Iterating over iterables (2)
One of the things you learned about in this chapter is that not all iterables are actual lists. A couple of examples that we looked at are strings and the use of the range() function. In this exercise, we will focus on the range() function.

You can use range() in a for loop as if it's a list to be iterated over:

Recall that range() doesn't actually create the list; instead, it creates a range object with an iterator
that produces the values until it reaches the limit (in the example, until the value 4). If range() 
created the actual list, calling it with a value of 10100 may not work, especially since a number as big
as that may go over a regular computer's memory. The value 10100 is actually what's called a Googol which 
is a 1 followed by a hundred 0s. That's a huge number!


No todos los iterables son listas.
Un par de ejemplos son cadenas y el uso de la función `range()`. 
Puede usar `range()` en un ciclo for como si fuera una lista para iterar:

'''python
for i in range(5):
    print(i)
'''

`range()` en realidad no crea la lista; en su lugar, crea un objeto de range con un 
iterador que produce los valores hasta que alcanza el límite (en el ejemplo, hasta el valor 4). 
Si `range()` creara una lista real, llamarla con un valor de 10^100 puede no funcionar, especialmente
porque un número tan grande como ese puede pasar por la memoria de una computadora normal. El valor
10^100 es en realidad lo que se llama Googol que es un 1 seguido de cien 0s.

Ejemplo de como crear un iterator a traves de un iterable

'''python
# Create a list of strings: flash
flash = ['jay garrick', 'barry allen']

# Create an iterator for flash: superspeed
superspeed = iter(flash)

# Print each item from the iterator
print(next(superspeed))
print(next(superspeed))
# print(next(superspeed)) si hago este print obtenemos un error, porque la lista solo tiene dos strings
'''

### Another ways to iterate

- `enumerate()`

`enumerate()` devuelve un objeto de enumerar que produce una secuencia de tuplas, y cada una
de las tuplas es un par index-value. 


'''python
# Create a list of strings: mutants
mutants = ['charles xavier', 
            'bobby drake', 
            'kurt wagner', 
            'max eisenhardt', 
            'kitty pride']

# Create a list of tuples: mutant_list
mutant_list = list(enumerate(mutants))

# Print the list of tuples
print(mutant_list)

# Una forma de iterar la lista donde en cada posicion hay una tupla de dos elementos es esta.
for index1, value1 in mutant_list:
    print(index1, value1)

# Ahora podriamos directamente llamar enumerate() aca y decirle que comience a crear las tuplas con 1.
for index2, value2 in enumerate(mutants, 1):
    print(index2, value2)
'''

- `zip()`

`zip ()` toma cualquier número de iterables y devuelve un objeto zip que es un iterator de tuplas.
Si desea imprimir los valores de un objeto zip, se puede convertir en una lista y luego imprimirlo. 
Imprimir solo un objeto zip no devolverá los valores a menos que lo desempaquete primero.


'''python
mutants = ['charles xavier', 'bobby drake', 'kurt wagner', 'max eisenhardt', 'kitty pride']
aliases = ['prof x', 'iceman', 'nightcrawler', 'magneto', 'shadowcat']
powers = ['telepathy','thermokinesis','teleportation','magnetokinesis','intangibility']
 
# Create a list of tuples: mutant_data
mutant_data = list(zip(mutants, aliases, powers))

# Print the list of tuples
print(mutant_data)

# Create a zip object using the three lists: mutant_zip
mutant_zip = zip(mutants, aliases, powers)

# Print the zip object
print(mutant_zip)

# Unpack the zip object and print the tuple values
for value1, value2, value3 in mutant_zip:
    print(value1, value2, value3)
'''

### Using * and zip to 'unzip'

No hay función de unzip para hacer lo contrario de lo que hace zip (). Sin embargo, podemos 
revertir lo que se ha "zippeado" usando `zip()` con un poco de ayuda de `*`. `*` desempaqueta un iterable 
como una lista o una tupla en argumentos posicionales en una llamada de función.


'''python
# Re-create a zip object from mutants and powers: z1
z1 = zip(mutants, powers)

# 'Unzip' the tuples in z1 by unpacking with * and zip(): result1, result2
result1, result2 = zip(*z1)

# Check if unpacked tuples are equivalent to original tuples
print(result1 == mutants)
print(result2 == powers)
'''
