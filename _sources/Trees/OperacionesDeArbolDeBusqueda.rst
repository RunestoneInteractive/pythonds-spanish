..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Operaciones de un árbol de búsqueda
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Antes de examinar la implementación, revisemos la interfaz proporcionada por el TAD Vector Asociativo. Usted notará que esta interfaz es muy similar a un diccionario en Python.

.. Before we look at the implementation, let’s review the interface provided by the map ADT. You will notice that this interface is very similar to the Python dictionary.

-  ``VectorAsociativo()`` Crea un vector asociativo nuevo y vacío.

-  ``agregar(clave,valor)`` Agrega una nueva pareja clave-valor al vector asociativo. Si la clave ya está en el vector asociativo, reemplaza el valor anterior por el nuevo.

-  ``obtener(clave)`` Dada una clave, devuelva el valor almacenado en el vector asociativo o ``None`` de lo contrario.

-  ``del`` Elimina la pareja clave-valor del vector asociativo utilizando una instrucción de la forma ``del VectorAsociativo[clave]``.

-  ``len()`` Devuelve el número de parejas clave-valor almacenadas en el vector asociativo.

-  ``in`` Devuelve ``True`` para una instrucción de la forma ``clave in VectorAsociativo``, si la clave dada está en el vector asociativo.
