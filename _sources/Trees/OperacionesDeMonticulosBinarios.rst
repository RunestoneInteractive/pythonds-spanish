..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Operaciones de montículos binarios
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Las operaciones básicas que implementaremos para nuestro montículo binario son las siguientes:

.. The basic operations we will implement for our binary heap are as follows:

-  ``MonticuloBinario()`` crea un nuevo montículo binario vacío.

-  ``insertar(k)`` agrega un nuevo ítem al montículo.

-  ``buscarMin()`` devuelve el ítem con el menor valor clave, dejándolo en el montículo.

-  ``eliminarMin()`` devuelve el ítem con el menor valor clave, eliminándolo del montículo.

-  ``estaVacio()`` devuelve True si el montículo está vacío, o False de lo contrario.

-  ``tamano()`` devuelve el número de ítems en el montículo.

-  ``construirMonticulo(lista)`` construye un montículo nuevo a partir de una lista de claves.

El :ref:`ActiveCode 1 <lst_heap1>` ilustra el uso de algunos de los métodos de MontículoBinario. Observe que no importa el orden en que agregamos ítems al montículo, el menor es cada vez eliminado. Ahora nos concentraremos en la creación de una implementación para esta idea.

.. :ref:`ActiveCode 1 <lst_heap1>` demonstrates the use of some of the binary heap methods. Notice that no matter the order that we add items to the heap, the smallest is removed each time. We will now turn our attention to creating an implementation for this idea.

.. _lst_heap1:


.. activecode:: heap1
    :caption: Uso de un montículo binario
    :nocodelens:
    
    from pythoned.arboles.monticuloBinario import MonticuloBinario
    
    miMonticulo = MonticuloBinario()
    miMonticulo.insertar(5)
    miMonticulo.insertar(7)
    miMonticulo.insertar(3)
    miMonticulo.insertar(11)
    
    print(miMonticulo.eliminarMin())

    print(miMonticulo.eliminarMin())

    print(miMonticulo.eliminarMin())

    print(miMonticulo.eliminarMin())
