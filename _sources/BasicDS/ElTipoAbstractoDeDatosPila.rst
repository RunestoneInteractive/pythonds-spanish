..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


El tipo abstracto de datos Pila
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

El tipo abstracto de datos Pila se define mediante las siguientes estructura y operaciones. Una pila está estructurada, como se ha descrito anteriormente, como una colección ordenada de ítems en la cual los ítems se pueden agregar y eliminar en el extremo llamado “tope”. Las pilas tienen un ordenamiento LIFO. A continuación se describen las operaciones de la pila.

.. The stack abstract data type is defined by the following structure and operations. A stack is structured, as described above, as an ordered collection of items where items are added to and removed from the end called the “top.” Stacks are ordered LIFO. The stack operations are given below.

-  ``Pila()`` crea una nueva pila que está vacía. No necesita parámetros y devuelve una pila vacía.

.. -  ``Stack()`` creates a new stack that is empty. It needs no parameters and returns an empty stack.

-  ``incluir(item)`` agrega un nuevo ítem en el tope de la pila. Requiere el ítem y no devuelve valor.

.. -  ``push(item)`` adds a new item to the top of the stack. It needs the item and returns nothing.

-  ``extraer()`` elimina el ítem en el tope de la pila. No requiere parámetros y devuelve el ítem. La pila se modifica.

.. -  ``pop()`` removes the top item from the stack. It needs no parameters and returns the item. The stack is modified.


-  ``inspeccionar()`` devuelve el ítem en el tope de la pila pero no lo elimina. No requiere parámetros. La pila no se modifica.

.. -  ``peek()`` returns the top item from the stack but does not remove it. It needs no parameters. The stack is not modified.

-  ``estaVacia()`` comprueba si la pila está vacía. No requiere parámetros y devuelve un valor booleano.

.. -  ``isEmpty()`` tests to see whether the stack is empty. It needs no parameters and returns a boolean value.

-  ``tamano()`` devuelve el número de ítems en la pila. No requiere parámetros y devuelve un entero.

.. -  ``size()`` returns the number of items on the stack. It needs no parameters and returns an integer.

Por ejemplo, si ``p`` es una pila que se ha creado y comienza vacía, entonces la :ref:`Tabla 1 <tbl_stackops>` muestra los resultados de una secuencia de operaciones de pila. En el contenido de la pila, el ítem del tope aparece en el extremo derecho.

.. For example, if ``s`` is a stack that has been created and starts out empty, then :ref:`Table 1 <tbl_stackops>` shows the results of a sequence of stack operations. Under stack contents, the top item is listed at the far right.

.. _tbl_stackops:

.. table:: **Table 1: Sample Stack Operations**

    ============================ ======================== ==================
           **Operación de pila** **Contenido de la pila** **Valor devuelto**
    ============================ ======================== ==================
               ``p.estaVacia()``                   ``[]``           ``True``
                ``p.incluir(4)``                  ``[4]``
          ``p.incluir('perro')``          ``[4,'perro']``
            ``p.inspeccionar()``          ``[4,'perro']``          ``'perro'``
             ``p.incluir(True)``     ``[4,'perro',True]``
                  ``p.tamano()``     ``[4,'perro',True]``              ``3``
               ``p.estaVacia()``     ``[4,'perro',True]``          ``False``
              ``p.incluir(8.4)`` ``[4,'perro',True,8.4]``
                 ``p.extraer()``     ``[4,'perro',True]``            ``8.4``
                 ``p.extraer()``          ``[4,'perro']``           ``True``
                  ``p.tamano()``          ``[4,'perro']``              ``2``
    ============================ ======================== ==================


