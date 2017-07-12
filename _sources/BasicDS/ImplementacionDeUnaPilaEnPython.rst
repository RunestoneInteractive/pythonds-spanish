..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementación de una pila en Python
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ahora que hemos definido claramente la pila como un tipo abstracto de datos, centraremos nuestra atención en usar Python para implementar la pila. Recuerde que cuando a un tipo abstracto de datos se le da una implementación física, dicha implementación se denomina una estructura de datos.

.. Now that we have clearly defined the stack as an abstract data type we will turn our attention to using Python to implement the stack. Recall that when we give an abstract data type a physical implementation we refer to the implementation as a data structure.

Como hemos descrito en el Capítulo 1, en Python, como en cualquier lenguaje de programación orientado a objetos, la implementación elegida para un tipo abstracto de datos como por ejemplo una pila es la creación de una nueva clase. Las operaciones de la pila se implementarán como métodos de la clase. Además, para implementar una pila, que es una colección de elementos, tiene sentido usar el poder y la simplicidad de las colecciones primitivas suministradas por Python. Nosotros usaremos una lista.

.. As we described in Chapter 1, in Python, as in any object-oriented programming language, the implementation of choice for an abstract data type such as a stack is the creation of a new class. The stack operations are implemented as methods. Further, to implement a stack, which is a collection of elements, it makes sense to utilize the power and simplicity of the primitive collections provided by Python. We will use a list.

Recuerde que la clase ``List`` en Python proporciona un mecanismo de colección ordenada y un conjunto de métodos. Por ejemplo, si tenemos la lista [2,5,3,6,7,4], sólo tenemos que decidir qué extremo de la lista se considerará el tope de la pila y cuál será la base. Una vez que se toma esa decisión, las operaciones se pueden implementar usando los métodos de listas como ``append`` y ``pop``.

.. Recall that the list class in Python provides an ordered collection mechanism and a set of methods. For example, if we have the list [2,5,3,6,7,4], we need only to decide which end of the list will be considered the top of the stack and which will be the base. Once that decision is made, the operations can be implemented using the list methods such as ``append`` and ``pop``.

En la siguiente implementación de la pila (:ref:`ActiveCode 1 <lst_stackcode1>`) se asume que el final de la lista contendrá el elemento del tope de la pila. A medida que la pila crece (cuando se producen operaciones ``incluir``), se añadirán nuevos elementos al final de la lista. Las operaciones ``extraer`` manipularán ese mismo extremo.

.. The following stack implementation (:ref:`ActiveCode 1 <lst_stackcode1>`) assumes that the end of the list will hold the top element of the stack. As the stack grows (as ``push`` operations occur), new items will be added on the end of the list. ``pop`` operations will manipulate that same end.

.. _lst_stackcode1:


.. activecode:: stack_1ac
   :caption: Implementación de una clase Pila usando listas de Python
   :nocodelens:

   class Pila:
        def __init__(self):
            self.items = []

        def estaVacia(self):
            return self.items == []

        def incluir(self, item):
            self.items.append(item)

        def extraer(self):
            return self.items.pop()

        def inspeccionar(self):
            return self.items[len(self.items)-1]

        def tamano(self):
            return len(self.items)

Recuerde que cuando hacemos clic en el botón ``Run`` no ocurre nada más que la definición de la clase. Debemos crear un objeto ``Pila`` y luego usarlo. El :ref:`ActiveCode 2 <lst_stackcode1>` muestra la clase ``Pila`` en acción a medida que realizamos la secuencia de operaciones de la :ref:`Tabla 1 <tbl_stackops>`. Observe que la definición de la clase ``Pila`` se importa desde el módulo ``pythoned``.

.. Remember that nothing happens when we click the ``run`` button other than the definition of the class.  We must create a ``Stack`` object and then use it. :ref:`ActiveCode 2 <lst_stackcode1>` shows the ``Stack`` class in action as we perform the sequence of operations from :ref:`Table 1 <tbl_stackops>`.  Notice that the definition of the ``Stack`` class is imported from the ``pythonds`` module.

.. note:: 
    El módulo ``pythoned`` contiene las implementaciones de todas las estructuras de datos discutidas en este libro. Está estructurado de acuerdo con las secciones: básicas, árboles y grafos. El módulo se puede descargar de `pythonworks.org <http://www.pythonworks.org/pythonds>`_.
    

.. activecode:: stack_ex_1
   :nocodelens:

   from pythoned.basicas.pila import Pila

   p=Pila()
   
   print(p.estaVacia())
   p.incluir(4)
   p.incluir('perro')
   print(p.inspeccionar())
   p.incluir(True)
   print(p.tamano())
   print(p.estaVacia())
   p.incluir(8.4)
   print(p.extraer())
   print(p.extraer())
   print(p.tamano())


Es importante tener en cuenta que podríamos haber elegido implementar la pila usando una lista donde el tope esté al principio en lugar de estar al final. En este caso, los métodos ``pop`` y ``append`` anteriores ya no funcionarían y tendríamos que indizar la posición 0 (el primer ítem de la lista) explícitamente usando ``pop`` e ``insert``. La implementación se muestra en :ref:`CodeLens 1 <lst_stackcode2>`.

.. It is important to note that we could have chosen to implement the stack using a list where the top is at the beginning instead of at the end. In this case, the previous ``pop`` and ``append`` methods would no longer work and we would have to index position 0 (the first item in the list) explicitly using ``pop`` and ``insert``. The implementation is shown in :ref:`CodeLens 1 <lst_stackcode2>`.

.. _lst_stackcode2:

.. codelens:: stack_cl_1
   :caption: Implementación alternativa de la clase Pila

   class Pila:
        def __init__(self):
            self.items = []

        def estaVacia(self):
            return self.items == []

        def incluir(self, item):
            self.items.insert(0,item)

        def extraer(self):
            return self.items.pop(0)

        def inspeccionar(self):
            return self.items[0]

        def tamano(self):
            return len(self.items)

   s = Pila()
   s.incluir('hola')
   s.incluir('verdadero')
   print(s.extraer())


Esta capacidad de cambiar la implementación física de un tipo abstracto de datos mientras se mantienen las características lógicas es un ejemplo de abstracción en funcionamiento. Sin embargo, aunque la pila funcionará en todo caso, si consideramos el desempeño de las dos implementaciones, definitivamente hay una diferencia. Recuerde que las operaciones ``append`` y ``pop()`` resultaron ser O(1). Esto significa que la primera implementación realizará las operaciones incluir y extraer en tiempo constante sin importar cuántos ítems están en la pila. El desempeño de la segunda implementación sufre en que las operaciones ``insert(0)`` y ``pop(0)`` requerirán un tiempo O(n) para una pila de tamaño n. Evidentemente, aunque las implementaciones son lógicamente equivalentes, tendrían tiempos muy diferentes al realizar las pruebas de referencia (*benchmark*).

.. This ability to change the physical implementation of an abstract data type while maintaining the logical characteristics is an example of abstraction at work. However, even though the stack will work either way, if we consider the performance of the two implementations, there is definitely a difference. Recall that the ``append`` and ``pop()`` operations were both O(1). This means that the first implementation will perform push and pop in constant time no matter how many items are on the stack. The performance of the second implementation suffers in that the ``insert(0)`` and ``pop(0)`` operations will both require O(n) for a stack of size n. Clearly, even though the implementations are logically equivalent, they would have very different timings when performing benchmark testing.

.. admonition:: Autoevaluación

   .. mchoice:: stack_1
      :answer_a: 'x'
      :answer_b: 'y'
      :answer_c: 'z'
      :answer_d: La pila está vacía
      :correct: c
      :feedback_a: Recuerde que una pila se construye de abajo hacia arriba.
      :feedback_b: Recuerde que una pila se construye de abajo hacia arriba.
      :feedback_c: ¡Bien hecho!
      :feedback_d: Recuerde que una pila se construye de abajo hacia arriba.

      Dada la siguiente secuencia de operaciones de pila, ¿cuál es el ítem en el tope de la pila cuando se completa la secuencia?
       
      .. code-block:: python
       
       m = Pila()
       m.incluir('x')
       m.incluir('y')
       m.extraer()
       m.incluir('z')
       m.inspeccionar()

   .. mchoice:: stack_2
      :answer_a: 'x'
      :answer_b: la pila está vacía
      :answer_c: ocurrirá un error
      :answer_d: 'z'
      :correct: c
      :feedback_a: Quizás usted desee comprobar la documentación para estaVacia
      :feedback_b: Hay un número impar de cosas en la pila, pero cada vez a través del ciclo se extraen 2 cosas
      :feedback_c: ¡Bien hecho!
      :feedback_d: Quizás usted desee comprobar la documentación para estaVacia

      Dada la siguiente secuencia de operaciones de pila, ¿cuál es el ítem en el tope de la pila cuando se completa la secuencia?

      .. code-block:: python
  
        m = Pila()
        m.incluir('x')
        m.incluir('y')
        m.incluir('z')
        while not m.estaVacia():
           m.extraer()
           m.extraer()

   Escriba una función `cadenaInversa(miCadena)` que utilice una pila para invertir los caracteres de una cadena.

   .. actex:: stack_stringrev
      :nocodelens:

      from test import testEqual

      class Pila:
           def __init__(self):
               self.items = []

           def estaVacia(self):
               return self.items == []

           def incluir(self, item):
               self.items.append(item)

           def extraer(self):
               return self.items.pop()

           def inspeccionar(self):
               return self.items[len(self.items)-1]

           def tamano(self):
               return len(self.items)


      def cadenaInversa(miCadena):
          # Escriba aquí su código

      testEqual(cadenaInversa('casa'),'asac')
      testEqual(cadenaInversa('x'),'x')
      testEqual(cadenaInversa('1234567890'),'0987654321')



