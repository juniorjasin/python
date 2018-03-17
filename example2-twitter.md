# Processing large amounts of Twitter data

A veces, los datos que tenemos que procesar alcanzan un tamaño que es demasiado para que lo maneje la
memoria de una computadora. Este es un problema común que enfrentan los científicos de datos. 
Una solución para esto es procesar una fuente de datos completa pedazo por pedazo, en lugar de un solo ir a la vez.

En este ejercicio, se procesará un gran archivo csv de datos de Twitter 'tweets.csv', ahora
trabajaremos en trozos de 10 entradas a la vez.


'''python
# Define count_entries()

import pandas as pd

def count_entries(csv_file, c_size, colname):
    """Return a dictionary with counts of
    occurrences as value for each key."""
    
    # Initialize an empty dictionary: counts_dict
    counts_dict = {}

    # Iterate over the file chunk by chunk
    for chunk in pd.read_csv(csv_file, chunksize=c_size):

        # Iterate over the column in DataFrame
        for entry in chunk[colname]:
            if entry in counts_dict.keys():
                counts_dict[entry] += 1
            else:
                counts_dict[entry] = 1

    # Return counts_dict
    return counts_dict

# Call count_entries(): result_counts
result_counts = count_entries('tweets.csv', 10, 'lang')

# Print result_counts
print(result_counts)
'''
