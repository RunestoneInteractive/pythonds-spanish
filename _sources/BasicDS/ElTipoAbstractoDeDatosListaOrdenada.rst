..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


El tipo abstracto de datos Lista Ordenada
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ahora consideraremos un tipo de lista conocida como lista ordenada. Por ejemplo, si la lista de enteros mostrada arriba era una lista ordenada (orden ascendente), entonces podría escribirse como 17, 26, 31, 54, 77 y 93. Dado que 17 es el ítem más pequeño, ocupa la primera posición en la lista. Asimismo, puesto que 93 es el más grande, ocupa la última posición.

.. We will now consider a type of list known as an ordered list. For example, if the list of integers shown above were an ordered list (ascending order), then it could be written as 17, 26, 31, 54, 77, and 93. Since 17 is the smallest item, it occupies the first position in the list. Likewise, since 93 is the largest, it occupies the last position.

La estructura de una lista ordenada es una colección de ítems en los que cada uno contiene una posición relativa que se basa en alguna característica subyacente del ítem. El orden es típicamente ascendente o descendente y asumimos que los ítems de la lista tienen una operación de comparación significativa que ya está definida. Muchas de las operaciones de lista ordenada son las mismas que las de la lista no ordenada.

.. The structure of an ordered list is a collection of items where each item holds a relative position that is based upon some underlying characteristic of the item. The ordering is typically either ascending or descending and we assume that list items have a meaningful comparison operation that is already defined. Many of the ordered list operations are the same as those of the unordered list.

-  ``ListaOrdenada()`` crea una nueva lista ordenada que está vacía. No necesita parámetros y devuelve una lista vacía.

-  ``agregar(item)`` agrega un nuevo ítem a la lista, asegurando que el orden se preserve. Necesita el ítem y no devuelve nada. Asume que el ítem aún no está en la lista.

-  ``remover(item)`` elimina el ítem de la lista. Necesita el ítem y modifica la lista. Asume que el ítem está presente en la lista.

-  ``buscar(item)`` busca el ítem en la lista. Necesita el ítem y devuelve un valor booleano.

-  ``estaVacia()`` comprueba si la lista está vacía. No necesita parámetros y devuelve un valor booleano.

-  ``tamano()`` devuelve el número de ítems en la lista. No necesita parámetros y devuelve un entero.

-  ``indice(item)`` devuelve la posición del ítem en la lista. Necesita el ítem y devuelve el índice. Asume que el ítem está en la lista.

-  ``extraer()`` elimina y devuelve el último ítem de la lista. No necesita nada y devuelve un ítem. Asume que la lista tiene al menos un ítem.

-  ``extraer(pos)`` elimina y devuelve el ítem en la posición pos. Necesita la posición y devuelve el ítem. Asume que el ítem está en la lista.
