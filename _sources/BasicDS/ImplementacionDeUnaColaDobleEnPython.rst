..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementación de una cola doble en Python
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Como hemos hecho en las secciones anteriores, crearemos una nueva clase para la implementación del tipo abstracto de datos Cola Doble. Una vez más, las listas de Python proporcionan un muy buen conjunto de métodos sobre los cuales se pueden construir los detalles de la cola doble. Nuestra implementación (el :ref:`Programa 1 <lst_dequecode>`) asumirá que el final de la cola doble está en la posición 0 de la lista.

.. As we have done in previous sections, we will create a new class for the implementation of the abstract data type deque. Again, the Python list will provide a very nice set of methods upon which to build the details of the deque. Our implementation (:ref:`Listing 1 <lst_dequecode>`) will assume that the rear of the deque is at position 0 in the list.

.. _lst_dequecode:

.. highlight:: python
   :linenothreshold: 5

**Programa 1**

::

    class ColaDoble:
        def __init__(self):
            self.items = []

        def estaVacia(self):
            return self.items == []

        def agregarFrente(self, item):
            self.items.append(item)

        def agregarFinal(self, item):
            self.items.insert(0,item)

        def removerFrente(self):
            return self.items.pop()

        def removerFinal(self):
            return self.items.pop(0)

        def tamano(self):
            return len(self.items)

.. highlight:: python
   :linenothreshold: 500

En ``removerFrente`` utilizamos el método ``pop`` para eliminar el último elemento de la lista. Sin embargo, en ``removerFinal``, el método ``pop(0)`` debe eliminar el primer elemento de la lista. Del mismo modo, necesitamos usar el método ``insert`` (línea 12) en ``agregarFinal``, ya que el método ``append`` asume la adición de un nuevo ítem al final de la lista.

.. In ``removeFront`` we use the ``pop`` method to remove the last element from the list. However, in ``removeRear``, the ``pop(0)`` method must remove the first element of the list. Likewise, we need to use the ``insert`` method (line 12) in ``addRear`` since the ``append`` method assumes the addition of a new element to the end of the list.

El CodeLens 1 muestra la clase ``ColaDoble`` en acción a medida que realizamos la secuencia de operaciones de la :ref:`Tabla 1 <tbl_dequeoperations>`.

.. CodeLens 1 shows the ``Deque`` class in action as we perform the sequence of operations from :ref:`Table 1 <tbl_dequeoperations>`.

.. codelens:: deqtest
   :caption: Ejemplo de operaciones sobre colas dobles

   class ColaDoble:
       def __init__(self):
           self.items = []

       def estaVacia(self):
           return self.items == []

       def agregarFrente(self, item):
           self.items.append(item)

       def agregarFinal(self, item):
           self.items.insert(0,item)

       def removerFrente(self):
           return self.items.pop()

       def removerFinal(self):
           return self.items.pop(0)

       def tamano(self):
           return len(self.items)

   d = ColaDoble()
   print(d.estaVacia())
   d.agregarFinal(4)
   d.agregarFinal('perro')
   d.agregarFrente('gato')
   d.agregarFrente(True)
   print(d.tamano())
   print(d.estaVacia())
   d.agregarFinal(8.4)
   print(d.removerFinal())
   print(d.removerFrente())
   print d.tamano()
   
Pueden verse muchas similitudes con el código de Python ya descrito para pilas y colas. También es probable que usted observe que, en esta implementación, agregar y remover ítems desde el frente es O(1) mientras que agregar y remover del final es O(n). Esto es esperable dadas las operaciones comunes que aparecen para agregar y remover ítems. Una vez más, lo importante es estar seguros de que sabemos dónde se asignan el frente y el final en la implementación.

.. You can see many similarities to Python code already described for stacks and queues. You are also likely to observe that in this implementation adding and removing items from the front is O(1) whereas adding and removing from the rear is O(n). This is to be expected given the common operations that appear for adding and removing items. Again, the important thing is to be certain that we know where the front and rear are assigned in the implementation.
