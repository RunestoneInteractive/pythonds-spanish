..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementación de un árbol de búsqueda
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Un árbol binario de búsqueda (abb) se basa en la propiedad de que las claves que son menores que el padre se encuentran en el subárbol izquierdo, y las claves que son mayores que el padre se encuentran en el subárbol derecho. Llamaremos esto la **propiedad abb**. A medida que implementemos la interfaz de Vector Asociativo como se describió anteriormente, la propiedad abb guiará nuestra implementación. La :ref:`Figura 1 <fig_simpleBST>` ilustra esta propiedad de un árbol binario de búsqueda, mostrando las claves sin ningún valor asociado. Observe que la propiedad es válida para cada padre e hijo. Todas las claves del subárbol izquierdo son menores que la clave de la raíz. Todas las claves en el subárbol derecho son mayores que la raíz.

.. A binary search tree relies on the property that keys that are less than the parent are found in the left subtree, and keys that are greater than the parent are found in the right subtree. We will call this the **bst property**. As we implement the Map interface as described above, the bst property will guide our implementation. :ref:`Figure 1 <fig_simpleBST>` illustrates this property of a binary search tree, showing the keys without any associated values. Notice that the property holds for each parent and child. All of the keys in the left subtree are less than the key in the root. All of the keys in the right subtree are greater than the root.

   
.. _fig_simpleBST:

.. figure:: Figures/simpleBST.png
   :align: center

   Figura 1: Un árbol binario de búsqueda simple

   Figura 1: Un árbol binario de búsqueda simple
    
Ahora que usted ya sabe lo que es un árbol binario de búsqueda, veremos cómo se construye. El árbol de búsqueda de la :ref:`Figura 1 <fig_simpleBST>` representa los nodos que existen después de haber insertado las siguientes claves en el orden mostrado: :math:`70,31,93,94,14,23,73`. Dado que 70 fue la primera clave insertada en el árbol, es la raíz. A continuación, 31 es menor que 70, por lo que se convierte en el hijo izquierdo de 70. Luego, 93 es mayor que 70, por lo que se convierte en el hijo derecho de 70. Ahora tenemos dos niveles del árbol llenos, así que la siguiente clave va a ser el hijo izquierdo o derecho de 31 o 93. Dado que 94 es mayor que 70 y 93, se convierte en el hijo derecho de 93. Similarmente 14 es menor que 70 y 31, por lo que se convierte en el hijo izquierdo de 31. 23 es también menor que 31, por lo que debe estar en el subárbol izquierdo de 31. Sin embargo, es mayor que 14, por lo que se convierte en el hijo derecho de 14.

.. Now that you know what a binary search tree is, we will look at how a binary search tree is constructed. The search tree in :ref:`Figure 1 <fig_simpleBST>` represents the nodes that exist after we have inserted the following keys in the order shown: :math:`70,31,93,94,14,23,73`. Since 70 was the first key inserted into the tree, it is the root. Next, 31 is less than 70, so it becomes the left child of 70. Next, 93 is greater than 70, so it becomes the right child of 70. Now we have two levels of the tree filled, so the next key is going to be the left or right child of either 31 or 93. Since 94 is greater than 70 and 93, it becomes the right child of 93. Similarly 14 is less than 70 and 31, so it becomes the left child of 31. 23 is also less than 31, so it must be in the left subtree of 31. However, it is greater than 14, so it becomes the right child of 14.

Para implementar el árbol binario de búsqueda, utilizaremos un enfoque de nodos y referencias similar al que utilizamos para implementar la lista enlazada y el árbol de expresiones. Sin embargo, puesto que debemos ser capaces de crear y trabajar con un árbol binario de búsqueda que esté vacío, nuestra implementación utilizará dos clases. A la primera clase la llamaremos ``ArbolBinarioBusqueda`` y a la segunda clase la llamaremos ``NodoArbol``. La clase ``ArbolBinarioBusqueda`` tiene una referencia a ``NodoArbol`` que es la raíz del árbol binario de búsqueda. En la mayoría de los casos, los métodos externos definidos en la clase externa simplemente comprueban si el árbol está vacío. Si hay nodos en el árbol, la petición simplemente se pasa a un método privado definido en la clase ``ArbolBinarioBusqueda`` que recibe la raíz como parámetro. En caso que el árbol esté vacío o queramos borrar la clave en la raíz del árbol, debemos tomar medidas especiales. El código para el constructor de la clase ``ArbolBinarioBusqueda`` junto con algunas otras funciones misceláneas se muestra en el :ref:`Programa 1 <lst_bst1>`.

.. To implement the binary search tree, we will use the nodes and references approach similar to the one we used to implement the linked list, and the expression tree. However, because we must be able create and work with a binary search tree that is empty, our implementation will use two classes. The first class we will call ``ArbolBinarioBusqueda``, and the second class we will call ``NodoArbol``. The ``ArbolBinarioBusqueda`` class has a reference to the ``NodoArbol`` that is the root of the binary search tree. In most cases the external methods defined in the outer class simply check to see if the tree is empty. If there are nodes in the tree, the request is just passed on to a private method defined in the ``ArbolBinarioBusqueda`` class that takes the root as a parameter. In the case where the tree is empty or we want to delete the key at the root of the tree, we must take special action. The code for the ``ArbolBinarioBusqueda`` class constructor along with a few other miscellaneous functions is shown in :ref:`Listing 1 <lst_bst1>`.

.. _lst_bst1:

**Programa 1**

::

    class ArbolBinarioBusqueda:

        def __init__(self):
    	    self.raiz = None
    	    self.tamano = 0
	
        def longitud(self):
    	    return self.tamano

        def __len__(self):
    	    return self.tamano

        def __iter__(self):
    	    return self.raiz.__iter__()
	    

La clase ``NodoArbol`` proporciona muchas funciones auxiliares que hacen que el trabajo realizado en los métodos de la clase ``ArbolBinarioBusqueda`` sea mucho más fácil. El constructor de un ``NodoArbol``, junto con estas funciones auxiliares, se muestra en el :ref:`Programa 2 <lst_bst2>`. Como se puede ver en el programa, muchas de estas funciones auxiliares ayudan a clasificar un nodo según su propia posición como hijo, (izquierdo o derecho) y el tipo de hijos que tiene el nodo. La clase ``NodoArbol`` también mantendrá explícitamente un seguimiento del padre como un atributo de cada nodo. Usted verá por qué esto es importante cuando discutamos la implementación del operador ``del``.

.. The ``NodoArbol`` class provides many helper functions that make the work done in the ``ArbolBinarioBusqueda`` class methods much easier. The constructor for a ``NodoArbol``, along with these helper functions, is shown in :ref:`Listing 2 <lst_bst2>`. As you can see in the listing many of these helper functions help to classify a node according to its own position as a child, (left or right) and the kind of children the node has. The ``NodoArbol`` class will also explicitly keep track of the parent as an attribute of each node. You will see why this is important when we discuss the implementation for the ``del`` operator.

Otro aspecto interesante de la implementación de ``NodoArbol`` en el :ref:`Programa 2 <lst_bst2>` es que usamos parámetros opcionales de Python. Los parámetros opcionales facilitan la creación de un ``NodoArbol`` bajo diferentes circunstancias. A veces queremos construir un nuevo ``NodoArbol`` que ya tenga ``padre`` e ``hijo``. Con un padre y un hijo existentes, podemos pasar padres e hijos como parámetros. En otras ocasiones, simplemente crearemos un ``NodoArbol`` con la pareja clave-valor, y no pasaremos ningún parámetro ``padre`` o ``hijo``. En este caso, se utilizan los valores por defecto de los parámetros opcionales.

.. Another interesting aspect of the implementation of ``NodoArbol`` in :ref:`Listing 2 <lst_bst2>` is that we use Python’s optional parameters. Optional parameters make it easy for us to create a ``NodoArbol`` under several different circumstances. Sometimes we will want to construct a new ``NodoArbol`` that already has both a ``padre`` and a ``hijo``. With an existing parent and child, we can pass parent and child as parameters. At other times we will just create a ``NodoArbol`` with the key value pair, and we will not pass any parameters for ``padre`` or ``hijo``. In this case, the default values of the optional parameters are used.

.. _lst_bst2:

**Programa 2**

::

    class NodoArbol:
       def __init__(self,clave,valor,izquierdo=None,derecho=None,
					   padre=None):
	    self.clave = clave
	    self.cargaUtil = valor
	    self.hijoIzquierdo = izquierdo
	    self.hijoDerecho = derecho
	    self.padre = padre

	def tieneHijoIzquierdo(self):
	    return self.hijoIzquierdo

	def tieneHijoDerecho(self):
	    return self.hijoDerecho
	
	def esHijoIzquierdo(self):
	    return self.padre and self.padre.hijoIzquierdo == self

	def esHijoDerecho(self):
	    return self.padre and self.padre.hijoDerecho == self

	def esRaiz(self):
	    return not self.padre

	def esHoja(self):
	    return not (self.hijoDerecho or self.hijoIzquierdo)

	def tieneAlgunHijo(self):
	    return self.hijoDerecho or self.hijoIzquierdo

	def tieneAmbosHijos(self):
	    return self.hijoDerecho and self.hijoIzquierdo
	
	def reemplazarDatoDeNodo(self,clave,valor,hizq,hder):
	    self.clave = clave
	    self.cargaUtil = valor
	    self.hijoIzquierdo = hizq
	    self.hijoDerecho = hder
	    if self.tieneHijoIzquierdo():
		self.hijoIzquierdo.padre = self
	    if self.tieneHijoDerecho():
		self.hijoDerecho.padre = self
		
Ahora que tenemos el armazón de ``ArbolBinarioBusqueda`` y la clase ``NodoArbol``, es hora de escribir el método ``agregar`` que nos permitirá construir nuestro árbol binario de búsqueda. El método ``agregar`` es un método de la clase ``ArbolBinarioBusqueda``. Este método comprobará si el árbol ya tiene una raíz. Si no hay una raíz entonces ``agregar`` creará un nuevo ``NodoArbol`` y lo instalará como la raíz del árbol. Si ya existe un nodo raíz, entonces ``agregar`` llama a la función auxiliar, privada y recursiva, ``_agregar`` para buscar en el árbol de acuerdo con el siguiente algoritmo:

.. Now that we have the ``ArbolBinarioBusqueda`` shell and the ``NodoArbol`` it is time to write the ``agregar`` method that will allow us to build our binary search tree. The ``agregar`` method is a method of the ``ArbolBinarioBusqueda`` class. This method will check to see if the tree already has a root. If there is not a root then ``agregar`` will create a new ``NodoArbol`` and install it as the root of the tree. If a root node is already in place then ``agregar`` calls the private, recursive, helper function ``_agregar`` to search the tree according to the following algorithm:

-  Comenzando en la raíz del árbol, buscar en el árbol binario comparando la nueva clave con la clave del nodo actual. Si la nueva clave es menor que el nodo actual, buscar en el subárbol izquierdo. Si la nueva clave es mayor que el nodo actual, buscar en el subárbol derecho.

-  Cuando no hay hijo izquierdo (o derecho) para buscar, hemos encontrado la posición en el árbol donde se debe instalar el nuevo nodo.

-  Para agregar un nodo al árbol, crear un nuevo objeto ``NodoArbol`` e insertar el objeto en el punto descubierto en el paso anterior.

El :ref:`Programa 3 <lst_bst3>` muestra el código en Python para insertar un nuevo nodo en el árbol. La función ``_agregar`` se escribe recursivamente siguiendo los pasos descritos anteriormente. Note que cuando se inserta un nuevo hijo en el árbol, el ``nodoActual`` se pasa al nuevo árbol como padre.

.. :ref:`Listing 3 <lst_bst3>` shows the Python code for inserting a new node in the tree. The ``_agregar`` function is written recursively following the steps outlined above. Notice that when a new child is inserted into the tree, the ``nodoActual`` is passed to the new tree as the parent.

Un problema importante con nuestra implementación de insertar es que las claves duplicadas no se manejan correctamente. A medida que se implementa nuestro árbol, una clave duplicada creará un nuevo nodo con el mismo valor clave en el subárbol derecho del nodo que tenga la clave original. El resultado de esto es que el nodo con la nueva clave nunca será encontrado durante una búsqueda. Una mejor manera de manejar la inserción de una clave duplicada es que el valor asociado con la nueva clave reemplace al valor antiguo. Dejamos que usted arregle este error como ejercicio.

.. One important problem with our implementation of insert is that duplicate keys are not handled properly. As our tree is implemented a duplicate key will create a new node with the same key value in the right subtree of the node having the original key. The result of this is that the node with the new key will never be found during a search. A better way to handle the insertion of a duplicate key is for the value associated with the new key to replace the old value. We leave fixing this bug as an exercise for you.

.. _lst_bst3:

**Programa 3**

::

    def agregar(self,clave,valor):
    	if self.raiz:
    	    self._agregar(clave,valor,self.raiz)
    	else:
    	    self.raiz = NodoArbol(clave,valor)
    	self.tamano = self.tamano + 1

    def _agregar(self,clave,valor,nodoActual):
    	if clave < nodoActual.clave:
    	    if nodoActual.tieneHijoIzquierdo():
    		   self._agregar(clave,valor,nodoActual.hijoIzquierdo)
    	    else:
    		   nodoActual.hijoIzquierdo = NodoArbol(clave,valor,padre=nodoActual)
    	else:
    	    if nodoActual.tieneHijoDerecho():
    		   self._agregar(clave,valor,nodoActual.hijoDerecho)
    	    else:
    		   nodoActual.hijoDerecho = NodoArbol(clave,valor,padre=nodoActual)

Con el método ``agregar`` definido, podemos sobrecargar fácilmente el operador ``[]`` para asignación gracias a que hacemos que el método ``__setitem__`` (ver :ref:`Programa 4 <lst_bst4>`) llame al método ``agregar``. Esto nos permite escribir instrucciones con el estilo de Python como ``miArbolCodigosPostales['Plymouth'] = 55446``, tal como un diccionario de Python.

.. With the ``agregar`` method defined, we can easily overload the ``[]`` operator for assignment by having the ``__setitem__`` method call (see :ref:`Listing 4 <lst_bst4>`) the put method. This allows us to write Python statements like ``miArbolCodigosPostales['Plymouth'] = 55446``, just like a Python dictionary.


.. _lst_bst4:

**Programa 4**

::

	def __setitem__(self,c,v):
	    self.agregar(c,v)
	    
La :ref:`Figura 2 <fig_bstput>` ilustra el proceso para insertar un nuevo nodo en un árbol binario de búsqueda. Los nodos ligeramente sombreados indican los nodos que fueron visitados durante el proceso de inserción.

.. :ref:`Figure 2 <fig_bstput>` illustrates the process for inserting a new node into a binary search tree. The lightly shaded nodes indicate the nodes that were visited during the insertion process.

.. _fig_bstput:

.. figure:: Figures/bstput.png
   :align: center

   Figura 2: Inserción de un nodo con clave = 19

   Figura 2: Inserción de un nodo con clave = 19

.. admonition:: Autoevaluación

    .. mchoice:: bst_1
       :correct: b
       :answer_a: <img src="../_static/bintree_a.png">
       :feedback_a: Recuerde que, a partir de la raíz, las claves menores que la raíz deben estar en el subárbol izquierdo, mientras que las claves mayores que la raíz van en el subárbol derecho.
       :answer_b: <img src="../_static/bintree_b.png">
       :feedback_b: Bien hecho.
       :answer_c: <img src="../_static/bintree_c.png">       
       :feedback_c: Este árbol luce como un árbol binario que satisface la propiedad de árbol completo que es necesaria para un montículo.

       ¿Cuál de los siguientes árboles muestra un árbol binario de búsqueda correcto dado que las claves fueron insertadas en el siguiente orden 5, 30, 2, 40, 25, 4?

Una vez que el árbol está construido, la siguiente tarea es implementar la consulta de un valor para una clave dada. El método ``obtener`` es aún más fácil que el método ``agregar`` porque simplemente busca el árbol de forma recursiva hasta que llega a un nodo hoja no coincidente o encuentra una clave coincidente. Cuando se encuentra una clave coincidente, se devuelve el valor almacenado en la carga útil del nodo.

.. Once the tree is constructed, the next task is to implement the retrieval of a value for a given key. The ``obtener`` method is even easier than the ``agregar`` method because it simply searches the tree recursively until it gets to a non-matching leaf node or finds a matching key. When a matching key is found, the value stored in the payload of the node is returned.

El :ref:`Programa 5 <lst_bst5>` muestra el código de ``obtener``, ``_obtener`` y ``__getitem__``. El código de búsqueda del método ``_obtener`` utiliza la misma lógica para elegir el hijo izquierdo o el derecho que el método ``_agregar``. Note que el método ``_obtener`` devuelve un ``NodoArbol`` a ``obtener``, esto permite que ``_obtener`` sea usado como un método flexible de ayuda para otros métodos de ``ArbolBinarioBusqueda`` que puedan necesitar hacer uso de otros datos de ``NodoArbol`` además de la carga útil.

.. :ref:`Listing 5 <lst_bst5>` shows the code for ``obtener``, ``_obtener`` and ``__getitem__``. The search code in the ``_obtener`` method uses the same logic for choosing the left or right child as the ``_agregar`` method. Notice that the ``_obtener`` method returns a ``NodoArbol`` to ``obtener``, this allows ``_obtener`` to be used as a flexible helper method for other ``ArbolBinarioBusqueda`` methods that may need to make use of other data from the ``NodoArbol`` besides the payload.

Al implementar el método ``__getitem__`` podemos escribir una instrucción de Python que se vea como si accediéramos a un diccionario, cuando de hecho estamos utilizando un árbol de búsqueda binario, por ejemplo ``z = miArbolCodigosPostales['Fargo']`` . Como se puede ver, todo lo que hace el método ``__getitem__`` es llamar a ``obtener``.

.. By implementing the ``__getitem__`` method we can write a Python statement that looks just like we are accessing a dictionary, when in fact we are using a binary search tree, for example ``z = miArbolCodigosPostales['Fargo']``.  As you can see, all the ``__getitem__`` method does is call ``obtener``.


.. _lst_bst5:




**Programa 5**

::

    def obtener(self,clave):
    	if self.raiz:
    	    res = self._obtener(clave,self.raiz)
    	    if res:
                return res.cargaUtil
    	    else:
                return None
    	else:
    	    return None

    def _obtener(self,clave,nodoActual):
    	if not nodoActual:
    	    return None
    	elif nodoActual.clave == clave:
    	    return nodoActual
    	elif clave < nodoActual.clave:
    	    return self._obtener(clave,nodoActual.hijoIzquierdo)
    	else:
    	    return self._obtener(clave,nodoActual.hijoDerecho)

    def __getitem__(self,clave):
    	return self.obtener(clave) 

Utilizando ``obtener``, podemos implementar la operación ``in`` escribiendo un método ``__contains__`` para  ``ArbolBinarioBusqueda``. El método ``__contains__`` llamará simplemente a ``obtener`` y devolverá ``True`` si ``obtener`` devuelve un valor o ``False`` si devuelve ``None``. El código para ``__contains__`` se muestra en el :ref:`Programa 6 <lst_bst6>`.

.. Using ``obtener``, we can implement the ``in`` operation by writing a ``__contains__`` method for the ``ArbolBinarioBusqueda``. The ``__contains__`` method will simply call ``obtener`` and return ``True`` if ``obtener`` returns a value, or ``False`` if it returns ``None``. The code for ``__contains__`` is shown in :ref:`Listing 6 <lst_bst6>`.

.. _lst_bst6:

**Programa 6**

::

    def __contains__(self,clave):
    	if self._obtener(clave,self.raiz):
    	    return True
    	else:
    	    return False

Recuerde que ``__contains__`` sobrecarga el operador ``in`` y nos permite escribir instrucciones como:

.. Recall that ``__contains__`` overloads the ``in`` operator and allows us to write statements such as:

::

	if 'Northfield' in miArbolCodigosPostales:
	    print("Sí está en el árbol")

Por último, fijémonos en el método más difícil en el árbol binario de búsqueda, la eliminación de una clave (ver el :ref:`Programa 7 <lst_bst7>`). La primera tarea es encontrar el nodo que se va a eliminar buscándolo en el árbol. Si el árbol tiene más de un nodo, buscamos usando el método ``_obtener`` para encontrar el ``NodoArbol`` que debe ser eliminado. Si el árbol tiene un solo nodo, significa que estamos eliminando la raíz del árbol, pero debemos comprobar que la clave de la raíz coincida con la clave que se va a eliminar. En cualquier caso, si no se encuentra la clave, el operador ``del`` genera un error.

.. Finally, we turn our attention to the most challenging method in the binary search tree, the deletion of a key (see :ref:`Listing 7 <lst_bst7>`). The first task is to find the node to delete by searching the tree. If the tree has more than one node we search using the ``_obtener`` method to find the ``NodoArbol`` that needs to be removed. If the tree only has a single node, that means we are removing the root of the tree, but we still must check to make sure the key of the root matches the key that is to be deleted. In either case if the key is not found the ``del`` operator raises an error.

.. _lst_bst7:

**Programa 7**

::

    def eliminar(self,clave):
       if self.tamano > 1:
          nodoAEliminar = self._obtener(clave,self.raiz)
    	  if nodoAEliminar:
    	      self.remover(nodoAEliminar)
    	      self.tamano = self.tamano-1
    	  else:
    	      raise KeyError('Error, la clave no está en el árbol')
       elif self.tamano == 1 and self.raiz.clave == clave:
    	  self.raiz = None
    	  self.tamano = self.tamano - 1
       else:
    	  raise KeyError('Error, la clave no está en el árbol')

    def __delitem__(self,clave):
    	self.eliminar(clave)

Una vez que hemos encontrado el nodo que contiene la clave que queremos eliminar, hay tres casos que debemos considerar:

.. Once we’ve found the node containing the key we want to delete, there are three cases that we must consider:

#. El nodo a eliminar no tiene hijos (ver la :ref:`Figura 3 <fig_bstdel1>`).

#. El nodo a eliminar tiene un solo hijo (ver la :ref:`Figura 4 <fig_bstdel2>`).

#. El nodo a eliminar tiene dos hijos (ver la :ref:`Figura 5 <fig_bstdel3>`).

El primer caso es sencillo (ver el :ref:`Programa 8 <lst_bst8>`). Si el nodo actual no tiene hijos, todo lo que debemos hacer es borrar el nodo y eliminar la referencia a ese nodo en el padre. El código para este caso se muestra a continuación.

.. The first case is straightforward (see :ref:`Listing 8 <lst_bst8>`). If the current node has no children all we need to do is delete the node and remove the reference to this node in the parent. The code for this case is shown in here.


.. _lst_bst8:

**Programa 8**


::

    if nodoActual.esHoja():
    	if nodoActual == nodoActual.padre.hijoIzquierdo:
    	    nodoActual.padre.hijoIzquierdo = None
    	else:
    	    nodoActual.padre.hijoDerecho = None


.. _fig_bstdel1:

.. figure:: Figures/bstdel1.png
   :align: center

   Figura 3: Eliminación del nodo 16, un nodo sin hijos

   Figura 3: Eliminación del nodo 16, un nodo sin hijos

El segundo caso es sólo un poco más complicado (vea el :ref:`Programa 9 <lst_bst9>`). Si un nodo tiene un solo hijo, entonces podemos simplemente promover al hijo para que tome el lugar de su padre. El código para este caso se muestra en el programa siguiente. Al examinar este código verá que hay seis casos a considerar. Dado que los casos son simétricos con respecto a tener un hijo izquierdo o un hijo derecho, simplemente discutiremos el caso en que el nodo actual tiene un hijo izquierdo. La decisión se hace de la siguiente manera:

.. The second case is only slightly more complicated (see :ref:`Listing 9 <lst_bst9>`). If a node has only a single child, then we can simply promote the child to take the place of its parent. The code for this case is shown in the next listing. As you look at this code you will see that there are six cases to consider. Since the cases are symmetric with respect to either having a left or right child we will just discuss the case where the current node has a left child. The decision proceeds as follows:

#. Si el nodo actual es un hijo izquierdo, solo necesitamos actualizar la referencia al padre del hijo izquierdo para que apunte al padre del nodo actual y luego actualizar la referencia al hijo izquierdo del padre para que apunte al nodo izquierdo del nodo actual.

#. Si el nodo actual es un hijo derecho, solo necesitamos actualizar la referencia al padre del hijo izquierdo para que apunte al padre del nodo actual y luego actualizar la referencia al hijo derecho del padre para que apunte al hijo izquierdo del nodo actual.

#. Si el nodo actual no tiene padre, debe ser la raíz. En este caso, solo reemplazaremos los datos ``clave``, ``cargaUtil``, ``hijoIzquierdo`` e ``hijoDerecho`` llamando al método ``reemplazarDatoDeNodo`` aplicado a la raíz.

.. _lst_bst9:

**Programa 9**

::

    else: # este nodo tiene un (1) hijo
       if nodoActual.tieneHijoIzquierdo():
    	  if nodoActual.esHijoIzquierdo():
    	      nodoActual.hijoIzquierdo.padre = nodoActual.padre
    	      nodoActual.padre.hijoIzquierdo = nodoActual.hijoIzquierdo
    	  elif nodoActual.esHijoDerecho():
    	      nodoActual.hijoIzquierdo.padre = nodoActual.padre
    	      nodoActual.padre.hijoDerecho = nodoActual.hijoIzquierdo
    	  else:
    	      nodoActual.reemplazarDatoDeNodo(nodoActual.hijoIzquierdo.clave,
    				 nodoActual.hijoIzquierdo.cargaUtil,
    				 nodoActual.hijoIzquierdo.hijoIzquierdo,
    				 nodoActual.hijoIzquierdo.hijoDerecho)
       else:
    	  if nodoActual.esHijoIzquierdo():
    	      nodoActual.hijoDerecho.padre = nodoActual.padre
    	      nodoActual.padre.hijoIzquierdo = nodoActual.hijoDerecho
    	  elif nodoActual.esHijoDerecho():
    	      nodoActual.hijoDerecho.padre = nodoActual.padre
    	      nodoActual.padre.hijoDerecho = nodoActual.hijoDerecho
    	  else:
    	      nodoActual.reemplazarDatoDeNodo(nodoActual.hijoDerecho.clave,
    				 nodoActual.hijoDerecho.cargaUtil,
    				 nodoActual.hijoDerecho.hijoIzquierdo,
    				 nodoActual.hijoDerecho.hijoDerecho)

.. _fig_bstdel2:

.. figure:: Figures/bstdel2.png
   :align: center

   Figura 4: Eliminación del nodo 25, un nodo que tiene un solo hijo

   Figura 4: Eliminación del nodo 25, un nodo que tiene un solo hijo

El tercer caso es el más difícil de manejar (ver el :ref:`Programa 10 <lst_bst10>`). Si un nodo tiene dos hijos, entonces es improbable que podamos simplemente promover uno de ellos para que tome el lugar del nodo. Sin embargo, podemos buscar en el árbol un nodo que se pueda usar para reemplazar el que está agendado para ser eliminado. Lo que necesitamos es un nodo que preserve las relaciones binarias del árbol de búsqueda para ambos subárboles izquierdo y derecho existentes. El nodo que cumple con esto es el nodo que tiene la segunda clave más grande del árbol. Llamamos a este nodo el **sucesor**, y buscaremos una manera de encontrar al sucesor rápidamente. Está garantizado que el sucesor no tendrá más de un hijo, por lo que sabemos cómo eliminarlo utilizando los dos casos de eliminación que ya hemos implementado. Una vez que se ha eliminado el sucesor, simplemente lo colocamos en el árbol en lugar del nodo que se va a eliminar.

.. The third case is the most difficult case to handle (see :ref:`Listing 10 <lst_bst10>`). If a node has two children, then it is unlikely that we can simply promote one of them to take the node’s place. We can, however, search the tree for a node that can be used to replace the one scheduled for deletion. What we need is a node that will preserve the binary search tree relationships for both of the existing left and right subtrees. The node that will do this is the node that has the next-largest key in the tree. We call this node the **successor**, and we will look at a way to find the successor shortly. The successor is guaranteed to have no more than one child, so we know how to remove it using the two cases for deletion that we have already implemented. Once the successor has been removed, we simply put it in the tree in place of the node to be deleted.

.. _fig_bstdel3:

.. figure:: Figures/bstdel3.png
    :align: center

    Figura 5: Eliminación del nodo 5, un nodo con dos hijos

    Figura 5: Eliminación del nodo 5, un nodo con dos hijos

El código para manejar el tercer caso se muestra en el programa a continuación. Observe que hacemos uso de los métodos auxiliares ``encontrarSucesor`` y ``encontrarMin`` para encontrar el sucesor. Para eliminar el sucesor, hacemos uso del método ``empalmar``. La razón por la que usamos ``empalmar`` es que él va directamente al nodo que queremos empalmar y hace los cambios correctos. Podríamos llamar a ``eliminar`` recursivamente, pero luego perderíamos el tiempo buscando nuevamente el nodo clave.

.. The code to handle the third case is shown in the next listing. Notice that we make use of the helper methods ``encontrarSucesor`` and ``encontrarMin`` to find the successor. To remove the successor, we make use of the method ``empalmar``. The reason we use ``empalmar`` is that it goes directly to the node we want to splice out and makes the right changes. We could call ``delete`` recursively, but then we would waste time re-searching for the key node.

.. _lst_bst10:

**Programa 10**

::

   elif nodoActual.tieneAmbosHijos(): #interior
	   suc = nodoActual.encontrarSucesor()
	   suc.empalmar()
	   nodoActual.clave = suc.clave
	   nodoActual.cargaUtil = suc.cargaUtil

El código para encontrar el sucesor se muestra a continuación (ver el :ref:`Programa 11 <lst_bst11>`) y, como se puede ver, es un método de la clase ``NodoArbol``. Este código hace uso de las mismas propiedades de los árboles binarios de búsqueda que hacen que un recorrido inorden imprima los nodos en el árbol de menor a mayor. Hay tres casos a considerar cuando se busca el sucesor:

.. The code to find the successor is shown below (see :ref:`Listing 11 <lst_bst11>`) and as you can see is a method of the ``NodoArbol`` class. This code makes use of the same properties of binary search trees that cause an inorder traversal to print out the nodes in the tree from smallest to largest. There are three cases to consider when looking for the successor:

#. Si el nodo tiene un hijo derecho, entonces el sucesor es la clave más pequeña en el subárbol derecho.

#. Si el nodo no tiene hijo derecho y es el hijo izquierdo de su padre, entonces el padre es el sucesor.

#. Si el nodo es el hijo derecho de su padre, y no tiene hijo derecho, entonces el sucesor de este nodo es el sucesor de su padre, excluyendo este nodo.

La primera condición es la única que nos importa al eliminar un nodo de un árbol binario de búsqueda. Sin embargo, el método ``encontrarSucesor`` tiene otros usos que exploraremos en los ejercicios al final de este capítulo.

.. The first condition is the only one that matters for us when deleting a node from a binary search tree. However, the ``encontrarSucesor`` method has other uses that we will explore in the exercises at the end of this chapter.

El método ``encontrarMin`` se invoca para encontrar la clave mínima en un subárbol. Convénzase de que la clave de valor mínimo en cualquier árbol binario de búsqueda es el hijo más a la izquierda del árbol. Por lo tanto, el método ``encontrarMin`` simplemente sigue las referencias ``hijoIzquierdo`` en cada nodo del subárbol hasta que alcanza un nodo que no tiene un hijo izquierdo.

.. The ``encontrarMin`` method is called to find the minimum key in a subtree. You should convince yourself that the minimum valued key in any binary search tree is the leftmost child of the tree. Therefore the ``encontrarMin`` method simply follows the ``hijoIzquierdo`` references in each node of the subtree until it reaches a node that does not have a left child.

.. _lst_bst11:

**Programa 11**


::

    def encontrarSucesor(self):
    	suc = None
    	if self.tieneHijoDerecho():
    	    suc = self.hijoDerecho.encontrarMin()
    	else:
    	    if self.padre:
    		   if self.esHijoIzquierdo():
    		       suc = self.padre
    		   else:
    		       self.padre.hijoDerecho = None
    		       suc = self.padre.encontrarSucesor()
    		       self.padre.hijoDerecho = self
    	return suc

    def encontrarMin(self):
    	actual = self
    	while actual.tieneHijoIzquierdo():
    	    actual = actual.hijoIzquierdo
    	return actual

    def empalmar(self):
    	if self.esHoja():
    	    if self.esHijoIzquierdo():
    		   self.padre.hijoIzquierdo = None
    	    else:
    		   self.padre.hijoDerecho = None
    	elif self.tieneAlgunHijo():
    	    if self.tieneHijoIzquierdo():
    		   if self.esHijoIzquierdo():
    		      self.padre.hijoIzquierdo = self.hijoIzquierdo
    		   else:
    		      self.padre.hijoDerecho = self.hijoIzquierdo
    		   self.hijoIzquierdo.padre = self.padre
    	    else:
    		   if self.esHijoIzquierdo():
    		      self.padre.hijoIzquierdo = self.hijoDerecho
    		   else:
    		      self.padre.hijoDerecho = self.hijoDerecho
    		   self.hijoDerecho.padre = self.padre


Tenemos que mirar un último método de interfaz para el árbol binario de búsqueda. Supongamos que nos gustaría simplemente iterar en orden sobre todas las claves del árbol. Esto es definitivamente algo que hemos hecho con los diccionarios, así que ¿por qué no con los árboles? Usted ya sabe cómo recorrer un árbol binario en orden, usando el algoritmo de recorrido ``inorden``. Sin embargo, escribir un iterador requiere un poco más de trabajo, ya que un iterador debe devolver sólo un nodo cada vez que se llama al iterador.

.. We need to look at one last interface method for the binary search tree. Suppose that we would like to simply iterate over all the keys in the tree in order. This is definitely something we have done with dictionaries, so why not trees? You already know how to traverse a binary tree in order, using the ``inorder`` traversal algorithm. However, writing an iterator requires a bit more work, since an iterator should return only one node each time the iterator is called.

Python nos proporciona una función muy potente para usar cuando creamos un iterador. La función se llama ``yield``. ``yield`` es similar a ``return``, ya que devuelve un valor a quien haya hecho el llamado. Sin embargo, ``yield`` también toma el paso adicional de congelar el estado de la función para que la próxima vez que se llame a la función continúe ejecutándose desde el punto exacto donde quedó antes. Las funciones que crean objetos que se pueden iterar se llaman funciones generadoras.

.. Python provides us with a very powerful function to use when creating an iterator. The function is called ``yield``. ``yield`` is similar to ``return`` in that it returns a value to the caller. However, ``yield`` also takes the additional step of freezing the state of the function so that the next time the function is called it continues executing from the exact point it left off earlier. Functions that create objects that can be iterated are called generator functions.

El código para un iterador ``inorden`` de un árbol binario se muestra en el programa siguiente. Mire este código cuidadosamente; a primera vista se podría pensar que el código no es recursivo. Sin embargo, recuerde que ``__iter__`` anula la operación ``for x in`` para la iteración, ¡así que realmente es recursivo! Debido a que es recursivo sobre las instancias de ``NodoArbol``, el método ``__iter__`` se define en la clase ``NodoArbol``.

.. The code for an ``inorder`` iterator of a binary tree is shown in the next listing. Look at this code carefully; at first glance you might think that the code is not recursive. However, remember that ``__iter__`` overrides the ``for x in`` operation for iteration, so it really is recursive! Because it is recursive over ``NodoArbol`` instances the ``__iter__`` method is defined in the ``NodoArbol`` class.

::

    def __iter__(self):
       if self:
    	  if self.tieneHijoIzquierdo():
    	  	 for elem in self.hijoIzquierdo:
    		    yield elem
          yield self.clave
    	  if self.tieneHijoDerecho():
    		 for elem in self.hijoDerecho:
    		    yield elem

En este punto usted podría querer descargar todo el archivo que contiene la versión completa de las clases ``ArbolBinarioBusqueda`` y ``NodoArbol``.

.. At this point you may want to download the entire file containing the full version of the ``ArbolBinarioBusqueda`` and ``NodoArbol`` classes.

.. activecode:: completebstcode

    class NodoArbol:
        def __init__(self,clave,valor,izquierdo=None,derecho=None,padre=None):
            self.clave = clave
            self.cargaUtil = valor
            self.hijoIzquierdo = izquierdo
            self.hijoDerecho = derecho
            self.padre = padre

        def tieneHijoIzquierdo(self):
            return self.hijoIzquierdo

        def tieneHijoDerecho(self):
            return self.hijoDerecho

        def esHijoIzquierdo(self):
            return self.padre and self.padre.hijoIzquierdo == self

        def esHijoDerecho(self):
            return self.padre and self.padre.hijoDerecho == self

        def esRaiz(self):
            return not self.padre

        def esHoja(self):
            return not (self.hijoDerecho or self.hijoIzquierdo)

        def tieneAlgunHijo(self):
            return self.hijoDerecho or self.hijoIzquierdo

        def tieneAmbosHijos(self):
            return self.hijoDerecho and self.hijoIzquierdo

        def reemplazarDatoDeNodo(self,clave,valor,hizq,hder):
            self.clave = clave
            self.cargaUtil = valor
            self.hijoIzquierdo = hizq
            self.hijoDerecho = hder
            if self.tieneHijoIzquierdo():
                self.hijoIzquierdo.padre = self
            if self.tieneHijoDerecho():
                self.hijoDerecho.padre = self
            

    class ArbolBinarioBusqueda:

        def __init__(self):
            self.raiz = None
            self.tamano = 0

        def longitud(self):
            return self.tamano

        def __len__(self):
            return self.tamano

        def agregar(self,clave,valor):
            if self.raiz:
                self._agregar(clave,valor,self.raiz)
            else:
                self.raiz = NodoArbol(clave,valor)
            self.tamano = self.tamano + 1

        def _agregar(self,clave,valor,nodoActual):
            if clave < nodoActual.clave:
                if nodoActual.tieneHijoIzquierdo():
                       self._agregar(clave,valor,nodoActual.hijoIzquierdo)
                else:
                       nodoActual.hijoIzquierdo = NodoArbol(clave,valor,padre=nodoActual)
            else:
                if nodoActual.tieneHijoDerecho():
                       self._agregar(clave,valor,nodoActual.hijoDerecho)
                else:
                       nodoActual.hijoDerecho = NodoArbol(clave,valor,padre=nodoActual)

        def __setitem__(self,c,v):
           self.agregar(c,v)

        def obtener(self,clave):
           if self.raiz:
               res = self._obtener(clave,self.raiz)
               if res:
                      return res.cargaUtil
               else:
                      return None
           else:
               return None

        def _obtener(self,clave,nodoActual):
           if not nodoActual:
               return None
           elif nodoActual.clave == clave:
               return nodoActual
           elif clave < nodoActual.clave:
               return self._obtener(clave,nodoActual.hijoIzquierdo)
           else:
               return self._obtener(clave,nodoActual.hijoDerecho)

        def __getitem__(self,clave):
           return self.obtener(clave)

        def __contains__(self,clave):
           if self._obtener(clave,self.raiz):
               return True
           else:
               return False

        def eliminar(self,clave):
          if self.tamano > 1:
             nodoAEliminar = self._obtener(clave,self.raiz)
             if nodoAEliminar:
                 self.remover(nodoAEliminar)
                 self.tamano = self.tamano-1
             else:
                 raise KeyError('Error, la clave no está en el árbol')
          elif self.tamano == 1 and self.raiz.clave == clave:
             self.raiz = None
             self.tamano = self.tamano - 1
          else:
             raise KeyError('Error, la clave no está en el árbol')

        def __delitem__(self,clave):
           self.eliminar(clave)

        def empalmar(self):
           if self.esHoja():
               if self.esHijoIzquierdo():
                      self.padre.hijoIzquierdo = None
               else:
                      self.padre.hijoDerecho = None
           elif self.tieneAlgunHijo():
               if self.tieneHijoIzquierdo():
                      if self.esHijoIzquierdo():
                         self.padre.hijoIzquierdo = self.hijoIzquierdo
                      else:
                         self.padre.hijoDerecho = self.hijoIzquierdo
                      self.hijoIzquierdo.padre = self.padre
               else:
                      if self.esHijoIzquierdo():
                         self.padre.hijoIzquierdo = self.hijoDerecho
                      else:
                         self.padre.hijoDerecho = self.hijoDerecho
                      self.hijoDerecho.padre = self.padre

        def encontrarSucesor(self):
          suc = None
          if self.tieneHijoDerecho():
              suc = self.hijoDerecho.encontrarMin()
          else:
              if self.padre:
                     if self.esHijoIzquierdo():
                         suc = self.padre
                     else:
                         self.padre.hijoDerecho = None
                         suc = self.padre.encontrarSucesor()
                         self.padre.hijoDerecho = self
          return suc

        def encontrarMin(self):
          actual = self
          while actual.tieneHijoIzquierdo():
              actual = actual.hijoIzquierdo
          return actual

        def remover(self,nodoActual):
             if nodoActual.esHoja(): #hoja
               if nodoActual == nodoActual.padre.hijoIzquierdo:
                   nodoActual.padre.hijoIzquierdo = None
               else:
                   nodoActual.padre.hijoDerecho = None
             elif nodoActual.tieneAmbosHijos(): #interior
               suc = nodoActual.encontrarSucesor()
               suc.empalmar()
               nodoActual.clave = suc.clave
               nodoActual.cargaUtil = suc.cargaUtil

             else: # este nodo tiene un (1) hijo
               if nodoActual.tieneHijoIzquierdo():
                 if nodoActual.esHijoIzquierdo():
                     nodoActual.hijoIzquierdo.padre = nodoActual.padre
                     nodoActual.padre.hijoIzquierdo = nodoActual.hijoIzquierdo
                 elif nodoActual.esHijoDerecho():
                     nodoActual.hijoIzquierdo.padre = nodoActual.padre
                     nodoActual.padre.hijoDerecho = nodoActual.hijoIzquierdo
                 else:
                     nodoActual.reemplazarDatoDeNodo(nodoActual.hijoIzquierdo.clave,
                                        nodoActual.hijoIzquierdo.cargaUtil,
                                        nodoActual.hijoIzquierdo.hijoIzquierdo,
                                        nodoActual.hijoIzquierdo.hijoDerecho)
               else:
                 if nodoActual.esHijoIzquierdo():
                     nodoActual.hijoDerecho.padre = nodoActual.padre
                     nodoActual.padre.hijoIzquierdo = nodoActual.hijoDerecho
                 elif nodoActual.esHijoDerecho():
                     nodoActual.hijoDerecho.padre = nodoActual.padre
                     nodoActual.padre.hijoDerecho = nodoActual.hijoDerecho
                 else:
                     nodoActual.reemplazarDatoDeNodo(nodoActual.hijoDerecho.clave,
                                        nodoActual.hijoDerecho.cargaUtil,
                                        nodoActual.hijoDerecho.hijoIzquierdo,
                                        nodoActual.hijoDerecho.hijoDerecho)




    miArbol = ArbolBinarioBusqueda()
    miArbol[3]="rojo"
    miArbol[4]="azul"
    miArbol[6]="amarillo"
    miArbol[2]="en"

    print(miArbol[6])
    print(miArbol[2])
