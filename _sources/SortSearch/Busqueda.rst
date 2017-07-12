..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Búsqueda
--------

Ahora nos centraremos en algunos de los problemas más comunes que surgen en la computación, los de búsqueda y ordenamiento. En esta sección estudiaremos la búsqueda. Regresaremos al ordenamiento más adelante en el capítulo. La búsqueda es el proceso algorítmico de encontrar un ítem particular en una colección de ítems. Una búsqueda normalmente devuelve ``True`` o ``False`` según el ítem esté o no presente, respectivamente. En ocasiones, el algoritmo se puede modificar para devolver la posición donde se encuentre el ítem. Para nuestros propósitos, simplemente nos ocuparemos de la pregunta sobre la membresía.

.. We will now turn our attention to some of the most common problems that arise in computing, those of searching and sorting. In this section we will study searching. We will return to sorting later in the chapter. Searching is the algorithmic process of finding a particular item in a collection of items. A search typically answers either ``True`` or ``False`` as to whether the item is present. On occasion it may be modified to return where the item is found. For our purposes here, we will simply concern ourselves with the question of membership.

En Python, hay una manera muy fácil de preguntar si un ítem está en una lista de ítems. Utilizamos el operador ``in``.

.. In Python, there is a very easy way to ask whether an item is in a list of items. We use the ``in`` operator.

::

    >>> 15 in [3,5,2,4,1]
    False
    >>> 3 in [3,5,2,4,1]
    True
    >>> 

A pesar de que esto es fácil de escribir, un proceso subyacente debe llevarse a cabo para responder a la pregunta. Resulta que hay muchas maneras diferentes de buscar el ítem. Lo que nos interesa aquí es cómo funcionan estos algoritmos y compararlos entre sí.

.. Even though this is easy to write, an underlying process must be carried out to answer the question. It turns out that there are many different ways to search for the item. What we are interested in here is how these algorithms work and how they compare to one another.
