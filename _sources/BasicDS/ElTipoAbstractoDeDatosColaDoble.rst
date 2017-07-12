..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


El tipo abstracto de datos Cola Doble
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

El tipo abstracto de datos Cola Doble se define por la siguiente estructura y las siguientes operaciones. Una cola doble está estructurada, como se describió anteriormente, como una colección ordenada de ítems en la que se añaden y se retiran ítems de cualquier extremo, ya sea por el frente o por el final. Las operaciones de la cola doble se dan a continuación.

.. The deque abstract data type is defined by the following structure and operations. A deque is structured, as described above, as an ordered collection of items where items are added and removed from either end, either front or rear. The deque operations are given below.

-  ``ColaDoble()`` Crea una cola doble nueva que está vacía. No necesita parámetros y devuelve una cola doble vacía.

-  ``agregarFrente(item)`` añade un nuevo ítem al frente de la cola doble. Necesita el ítem y no devuelve nada.

-  ``agregarFinal(item)`` añade un nuevo ítem en el final de la cola doble. Necesita el ítem y no devuelve nada.

-  ``removerFrente()`` elimina el ítem que está en el frente de la cola doble. No necesita parámetros y devuelve el ítem. La cola doble se modifica.

-  ``removerFinal()`` elimina el ítem que está al final de la cola doble. No necesita parámetros y devuelve el ítem. La cola doble se modifica.

-  ``estaVacia()`` comprueba si la cola doble está vacía. No necesita parámetros y devuelve un valor booleano.

-  ``tamano()`` devuelve el número de ítems en la cola doble. No necesita parámetros y devuelve un entero.

A modo de ejemplo, si asumimos que ``d`` es una cola doble que se ha creado y que está actualmente vacía, entonces la :ref:`Tabla 1 <tbl_dequeoperations>` muestra los resultados de una secuencia de operaciones sobre la cola doble. Tenga en cuenta que el contenido que está en el frente aparece listado a la derecha. Es muy importante hacer un seguimiento de los dos extremos, frente y final, a medida que se ingresan y retiran ítems de la colección ya que las cosas pueden tornarse un poco confusas.

.. As an example, if we assume that ``d`` is a deque that has been created and is currently empty, then Table {dequeoperations} shows the results of a sequence of deque operations. Note that the contents in front are listed on the right. It is very important to keep track of the front and the rear as you move items in and out of the collection as things can get a bit confusing.

.. _tbl_dequeoperations:

.. table:: **Tabla 1: Ejemplos de operaciones sobre colas dobles**

    ============================ =============================== ================== 
     **Operación de cola doble**  **Contenido de la cola doble** **Valor devuelto** 
    ============================ =============================== ================== 
               ``d.estaVacia()``                          ``[]``           ``True`` 
           ``d.agregarFinal(4)``                         ``[4]``                    
     ``d.agregarFinal('perro')``                ``['perro',4,]``                    
     ``d.agregarFrente('gato')``          ``['perro',4,'gato']``                    
       ``d.agregarFrente(True)``     ``['perro',4,'gato',True]``                    
                  ``d.tamano()``     ``['perro',4,'gato',True]``              ``4`` 
               ``d.estaVacia()``     ``['perro',4,'gato',True]``          ``False`` 
         ``d.agregarFinal(8.4)`` ``[8.4,'perro',4,'gato',True]``                    
            ``d.removerFinal()``     ``['perro',4,'gato',True]``            ``8.4`` 
           ``d.removerFrente()``          ``['perro',4,'gato']``           ``True`` 
    ============================ =============================== ================== 


