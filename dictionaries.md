# Dictionaries


Un tipo de datos útiles integrados en Python es el diccionario.
A diferencia de las secuencias, que están indexadas por un rango de números, los diccionarios están 
indexados por claves, que pueden ser de cualquier tipo inmutable; strings, int,float, booleans siempre
pueden ser claves. Las tuplas se pueden usar como claves si contienen solo cadenas, números o tuplas;
si una tupla contiene cualquier objeto mutable, ya sea directa o indirectamente, no se puede usar 
como clave. No puede usar listas como claves, ya que las listas se pueden modificar en su lugar 
mediante asignaciones de índice, asignaciones de sectores o métodos como append () y extend ().

Lo mejor es pensar en un diccionario como un conjunto desordenado de pares clave: valor, 
con el requisito de que las claves sean únicas (dentro de un diccionario). Un par de llaves 
crea un diccionario vacío: {}. Al colocar una lista de pares clave-valor separados por comas,
dentro de las llaves se agregan los pares de clave:valor al diccionario.
Si almacena utilizando una clave que ya está en uso, se olvida el valor anterior
asociado con esa clave. Es un error extraer un valor con una clave que no existe.

Los diccionarios son buenas opciones cuando necesitemos una tabla de busqueda rapida (mas rapida
que las listas) con claves unicas por cada valor, donde el orden ni obtener grandes subconjuntos
de los datos es importante.

```python
# Ejemplo de diccionario
europe = {'spain':'madrid', 'france':'paris', 'germany':'berlin', 'norway':'oslo' }

# Si queremos obtener la capital de francia
europe['france']

# Para determinar las keys de un diccionario
europe.keys()
# Obtendriamos esto: dict_keys(['spain', 'norway', 'germany', 'france'])

# Agregar un nuevo par key:value
europe['argentina'] = 'buenos aires'

# Determinar si ya existe una key en nuestro dictionary
'argentina' in europe
# Nos retorna False

# Eliminar una par key:value
del(europe['argentina'])

# Diccionarios que contienen diccionarios como values.
europe = { 'spain': { 'capital':'madrid', 'population':46.77 },
           'france': { 'capital':'paris', 'population':66.03 },
           'germany': { 'capital':'berlin', 'population':80.62 },
           'norway': { 'capital':'oslo', 'population':5.084 } }
           
# Una forma de seleccionar mas simple
europe['spain']['capital'] # nos retorna la capital

# Anadir un nuevo key:value 

# Create sub-dictionary data
data = {
    'capital':'rome',
    'population':59.83
}

# Add data to europe under key 'italy'
europe['italy'] = data

```













