..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


El tipo abstracto de datos Cola
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

El tipo abstracto de datos Cola está definido por la siguiente estructura y operaciones. Una cola está estructurada, como se dijo antes, como una colección ordenada de ítems que son agregados en un extremo llamado “final” y removidos del otro, denominado “frente”. Las colas obedecen un ordenamiento FIFO. Las operaciones de cola están dadas a continuación.

.. The queue abstract data type is defined by the following structure and operations. A queue is structured, as described above, as an ordered collection of items which are added at one end, called the “rear,” and removed from the other end, called the “front.” Queues maintain a FIFO ordering property. The queue operations are given below.

-  ``Cola()`` crea una nueva cola que está vacía. No requiere parámetros y devuelve una cola vacía.

-  ``agregar(item)`` agrega un nuevo ítem al final de la cola. Requiere el ítem y no devuelve valor.

-  ``avanzar()`` elimina el ítem del frente de la cola. No require parámetros y devuelve el ítem que se eliminó. La cola es modificada.

-  ``estaVacia()`` verifica si la cola está vacía. No requiere parámetros y devuelve un valor booleano.

-  ``tamano()`` devuelve el número de ítems en la cola. No requiere parámetros y devuelve un entero.

Por ejemplo, si asumimos que ``c`` es una cola que se ha creado y está vacía, entonces la :ref:`Tabla 1 <tbl_queueoperations>` muestra los resultados de una secuencia de operaciones de cola. El contenido de la cola se muestra de tal manera que el frente está a la derecha. 4 fue el primer elemento agregado a la cola por lo que es el primer elemento devuelto por ``avanzar``.

.. As an example, if we assume that ``q`` is a queue that has been created and is currently empty, then :ref:`Table 1 <tbl_queueoperations>` shows the results of a sequence of queue operations. The queue contents are shown such that the front is on the right. 4 was the first item enqueued so it is the first item returned by dequeue.

.. _tbl_queueoperations:

.. table:: **Tabla 1: Ejemplo de operaciones de Cola**

    ============================ ======================== ================== 
           **Operación de Cola** **Contenido de la cola** **Valor devuelto** 
    ============================ ======================== ================== 
               ``c.estaVacia()``                   ``[]``           ``True`` 
                ``c.agregar(4)``                  ``[4]``                    
          ``c.agregar('perro')``          ``['perro',4]``                    
             ``c.agregar(True)``     ``[True,'perro',4]``                    
                  ``c.tamano()``     ``[True,'perro',4]``              ``3`` 
               ``c.estaVacia()``     ``[True,'perro',4]``          ``False`` 
              ``c.agregar(8.4)`` ``[8.4,True,'perro',4]``                    
                 ``c.avanzar()``   ``[8.4,True,'perro']``              ``4`` 
                 ``c.avanzar()``           ``[8.4,True]``        ``'perro'`` 
                  ``c.tamano()``           ``[8.4,True]``              ``2`` 
    ============================ ======================== ================== 


