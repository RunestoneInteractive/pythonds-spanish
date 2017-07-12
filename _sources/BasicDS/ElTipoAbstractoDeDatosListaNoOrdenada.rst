..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


El tipo abstracto de datos Lista No Ordenada
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La estructura de una lista no ordenada, como se ha descrito anteriormente, es una colección de ítems en la que cada ítem mantiene una posición relativa con respecto a los demás. A continuación se indican algunas posibles operaciones para las listas no ordenadas.

.. The structure of an unordered list, as described above, is a collection of items where each item holds a relative position with respect to the others. Some possible unordered list operations are given below.

-  ``Lista()`` crea una nueva lista que está vacía. No necesita parámetros y devuelve una lista vacía.

-  ``agregar(item)`` agrega un nuevo ítem a la lista. Necesita el ítem y no devuelve nada. Asume que el ítem aún no está en la lista.

-  ``remover(item)`` elimina el ítem de la lista. Necesita el ítem y modifica la lista. Asume que el ítem está presente en la lista.

-  ``buscar(item)`` busca el ítem en la lista. Necesita el ítem y devuelve un valor booleano.

-  ``estaVacia()`` comprueba si la lista está vacía. No necesita parámetros y devuelve un valor booleano.

-  ``tamano()`` devuelve el número de ítems en la lista. No necesita parámetros y devuelve un entero.

-  ``anexar(item)`` agrega un nuevo ítem al final de la lista, convirtiéndolo en el último ítem de la colección. Necesita el ítem y no devuelve nada. Asume que el ítem aún no está en la lista.

-  ``indice(item)`` devuelve la posición del ítem en la lista. Necesita el ítem y devuelve el índice. Asume que el ítem está en la lista.

-  ``insertar(pos,item)`` agrega un nuevo ítem a la lista en la posición pos. Necesita el ítem y no devuelve nada. Asume que el ítem aún no está en la lista y que hay suficientes elementos existentes para tener la posición pos.

-  ``extraer()`` elimina y devuelve el último ítem de la lista. No necesita nada y devuelve un ítem. Asume que la lista tiene al menos un ítem.

-  ``extraer(pos)`` elimina y devuelve el ítem en la posición pos. Necesita la posición y devuelve el ítem. Asume que el ítem está en la lista.
