..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementación de una cola en Python
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Es de nuevo apropiado crear una nueva clase para la implementación del tipo abstracto de datos Cola. Como antes, vamos a utilizar la potencia y la simplicidad de las listas para construir la representación interna de la cola.

.. It is again appropriate to create a new class for the implementation of the abstract data type queue. As before, we will use the power and simplicity of the list collection to build the internal representation of the queue.

Tenemos que decidir qué extremo de la lista utilizar como el final y cuál utilizar como el frente. La implementación mostrada en el :ref:`Programa 1 <lst_queuecode>` supone que el final está en la posición 0 en la lista. Esto nos permite usar la función ``insert`` en las listas para agregar nuevos elementos al final de la cola. La operación ``pop`` puede utilizarse para eliminar el elemento del frente (el último elemento de la lista). Recuerde que esto también significa que ``agregar`` será O(n) y ``avanzar`` será O(1).

.. We need to decide which end of the list to use as the rear and which to use as the front. The implementation shown in :ref:`Listing 1 <lst_queuecode>` assumes that the rear is at position 0 in the list. This allows us to use the ``insert`` function on lists to add new elements to the rear of the queue. The ``pop`` operation can be used to remove the front element (the last element of the list). Recall that this also means that enqueue will be O(n) and dequeue will be O(1). 

.. _lst_queuecode:

**Programa 1**

::

    class Cola:
        def __init__(self):
            self.items = []

        def estaVacia(self):
            return self.items == []

        def agregar(self, item):
            self.items.insert(0,item)

        def avanzar(self):
            return self.items.pop()

        def tamano(self):
            return len(self.items)

El CodeLens 1 muestra la clase ``Cola`` en acción a medida que realizamos la secuencia de operaciones de la :ref:`Tabla 1 <tbl_queueoperations>`.

.. El CodeLens 1 shows the ``Queue`` class in action as we perform the sequence of operations from :ref:`Table 1 <tbl_queueoperations>`.

.. codelens:: ququeuetest
   :caption: Ejemplo de operaciones de Cola

   class Cola:
       def __init__(self):
           self.items = []

       def estaVacia(self):
           return self.items == []

       def agregar(self, item):
           self.items.insert(0,item)

       def avanzar(self):
           return self.items.pop()

       def tamano(self):
           return len(self.items)

   c=Cola()
   
   c.agregar(4)
   c.agregar('perro')
   c.agregar(True)
   print(c.tamano())


Una manipulación adicional de esta cola daría los siguientes resultados:

.. Further manipulation of this queue would give the following results:


::

    >>> c.tamano()
    3
    >>> c.estaVacia()
    False
    >>> c.agregar(8.4)
    >>> c.avanzar()
    4
    >>> c.avanzar()
    'perro'
    >>> c.tamano()
    2

.. admonition:: Autoevaluación

   .. mchoice:: queue_1
      :correct: b
      :answer_a: 'hola', 'perro'
      :answer_b: 'perro', 3
      :answer_c: 'hola', 3
      :answer_d: 'hola', 'perro', 3
      :feedback_a: Recuerde que lo primero que se agrega a la cola es lo primero que se elimina. FIFO
      :feedback_b: S&iacute;, first-in-first-out significa que hola se ha eliminado
      :feedback_c: Colas y pilas son estructuras de datos en las que s&oacute;lo se puede acceder al primero y al &uacute;ltimo &iacute;tem.
      :feedback_d: Tal vez usted pas&oacute; por alto el llamado a avanzar al final

      Suponga que usted tiene la siguiente serie de operaciones para colas.

      ::
      
          c = Cola()
          c.agregar('hola')
          c.agregar('perro')
          c.agregar(3)
          c.avanzar()

      ¿Qué ítems quedan en la cola?

