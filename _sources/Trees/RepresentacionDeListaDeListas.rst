..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Representación de lista de listas
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

En un árbol representado por una lista de listas, comenzaremos con la estructura de datos de las listas de Python y escribiremos las funciones definidas anteriormente. Aunque escribir la interfaz como un conjunto de operaciones sobre una lista es un poco diferente de los otros tipos abstractos de datos que hemos implementado, es interesante hacerlo porque nos proporciona una estructura de datos recursiva simple que podemos mirar y examinar directamente . En un árbol representado como una lista de listas, almacenaremos el valor del nodo raíz como el primer elemento de la lista. El segundo elemento de la lista será en sí mismo una lista que represente el subárbol izquierdo. El tercer elemento de la lista será otra lista que represente el subárbol derecho. Veamos un ejemplo para ilustrar esta técnica de almacenamiento. La :ref:`Figura 1 <fig_smalltree>` muestra un árbol simple y su correspondiente implementación como una lista.

.. In a tree represented by a list of lists, we will begin with Python’s list data structure and write the functions defined above. Although writing the interface as a set of operations on a list is a bit different from the other abstract data types we have implemented, it is interesting to do so because it provides us with a simple recursive data structure that we can look at and examine directly. In a list of lists tree, we will store the value of the root node as the first element of the list. The second element of the list will itself be a list that represents the left subtree. The third element of the list will be another list that represents the right subtree. To illustrate this storage technique, let’s look at an example. :ref:`Figure 1 <fig_smalltree>` shows a simple tree and the corresponding list implementation.

.. _fig_smalltree:

.. figure:: Figures/smalltree.png
   :align: center
           
   Figura 1: Un pequeño árbol

   Figura 1: Un pequeño árbol

::

        miArbol = ['a',   #raíz
              ['b',  #subárbol izquierdo
               ['d', [], []],
               ['e', [], []] ],
              ['c',  #subárbol derecho
               ['f', [], []],
               [] ]  
             ]           
                  


Note que podemos acceder a los subárboles de la lista mediante la indización estándar para listas. La raíz del árbol es ``miArbol[0]``, el subárbol izquierdo de la raíz es ``miArbol[1]``, y el subárbol derecho es ``miArbol[2]``. El :ref:`ActiveCode 1 <lst_treelist1>` ilustra la creación de un árbol simple usando una lista. Una vez construido el árbol, podemos acceder a la raíz y a los subárboles izquierdo y derecho. Una propiedad muy conveniente de este enfoque de lista de listas es que la estructura de una lista que representa un subárbol se ajusta a la estructura definida para un árbol; ¡la estructura en sí misma es recursiva! Un subárbol que tiene un valor raíz y dos listas vacías es un nodo hoja. Otra buena característica del enfoque de lista de listas es que es generalizable a un árbol que tiene muchos subárboles. En caso que el árbol sea mayor que un árbol binario, otro subárbol será simplemente otra lista.

.. Notice that we can access subtrees of the list using standard list indexing. The root of the tree is ``miArbol[0]``, the left subtree of the root is ``miArbol[1]``, and the right subtree is ``miArbol[2]``. :ref:`ActiveCode 1 <lst_treelist1>` illustrates creating a simple tree using a list. Once the tree is constructed, we can access the root and the left and right subtrees. One very nice property of this list of lists approach is that the structure of a list representing a subtree adheres to the structure defined for a tree; the structure itself is recursive! A subtree that has a root value and two empty lists is a leaf node. Another nice feature of the list of lists approach is that it generalizes to a tree that has many subtrees. In the case where the tree is more than a binary tree, another subtree is just another list.

.. _lst_treelist1:

.. activecode:: tree_list1
    :caption: Uso de indización para acceder a los subárboles

    miArbol = ['a', ['b', ['d',[],[]], ['e',[],[]] ], ['c', ['f',[],[]], []] ]
    print(miArbol)
    print('subárbol izquierdo = ', miArbol[1])
    print('raíz = ', miArbol[0])
    print('subárbol derecho = ', miArbol[2])

Formalicemos esta definición de la estructura de datos árbol proporcionando algunas funciones que nos faciliten usar las listas como árboles. Tenga en cuenta que no vamos a definir una clase Arbol Binario. Las funciones que escribiremos solo nos ayudarán a manipular una lista estándar como si estuviéramos trabajando con un árbol.

.. Let’s formalize this definition of the tree data structure by providing some functions that make it easy for us to use lists as trees. Note that we are not going to define a binary tree class. The functions we will write will just help us manipulate a standard list as though we are working with a tree.

::


    def ArbolBinario(r):
        return [r, [], []]    

La función ``ArbolBinario`` simplemente construye una lista con un nodo raíz y dos sublistas vacías para los hijos. Para agregar un subárbol izquierdo a la raíz de un árbol, necesitamos insertar una nueva lista en la segunda posición de la lista raíz. Debemos ser cuidadosos. Si la lista ya tiene algún contenido en la segunda posición, necesitamos rastrearlo y empujarlo hacia abajo en el árbol para que sea el hijo izquierdo de la lista que estamos agregando. El :ref:`Programa 1 <lst_linsleft>` muestra el código en Python para insertar un hijo izquierdo.

.. The ``ArbolBinario`` function simply constructs a list with a root node and two empty sublists for the children. To add a left subtree to the root of a tree, we need to insert a new list into the second position of the root list. We must be careful. If the list already has something in the second position, we need to keep track of it and push it down the tree as the left child of the list we are adding. :ref:`Listing 1 <lst_linsleft>` shows the Python code for inserting a left child.

.. _lst_linsleft:

**Programa 1**

::

    def insertarIzquierdo(raiz,nuevaRama):
        t = raiz.pop(1)
        if len(t) > 1:
            raiz.insert(1,[nuevaRama,t,[]])
        else:
            raiz.insert(1,[nuevaRama, [], []])
        return raiz


Note que para insertar un hijo izquierdo, primero obtendremos la lista (posiblemente vacía) que corresponde al hijo izquierdo actual. A continuación, agregamos el nuevo hijo izquierdo, instalando el antiguo hijo izquierdo como hijo izquierdo del nuevo. Esto nos permite empalmar un nuevo nodo en el árbol en cualquier posición. El código de ``insertarDerecho`` es similar al de ``inserttarIzquierdo`` y se muestra en el :ref:`Programa 2 <lst_linsright>`.

.. Notice that to insert a left child, we first obtain the (possibly empty) list that corresponds to the current left child. We then add the new left child, installing the old left child as the left child of the new one. This allows us to splice a new node into the tree at any position. The code for ``insertarDerecho`` is similar to ``insertarIzquierdo`` and is shown in :ref:`Listing 2 <lst_linsright>`.

.. _lst_linsright:

**Programa 2**

::

    def insertarDerecho(raiz,nuevaRama):
        t = raiz.pop(2)
        if len(t) > 1:
            raiz.insert(2,[nuevaRama,[],t])
        else:
            raiz.insert(2,[nuevaRama,[],[]])
        return raiz

Para redondear este conjunto de funciones de creación de árboles (ver el :ref:`Programa 3 <lst_treeacc>`), vamos a escribir un par de funciones de acceso para obtener y establecer el valor raíz, así como para obtener los subárboles izquierdo o derecho.

.. To round out this set of tree-making functions(see :ref:`Listing 3 <lst_treeacc>`), let’s write a couple of access functions for getting and setting the root value, as well as getting the left or right subtrees.

.. _lst_treeacc:

**Programa 3**

::


    def obtenerValorRaiz(raiz):
        return raiz[0]
    
    def asignarValorRaiz(raiz,nuevoValor):
        raiz[0] = nuevoValor
    
    def obtenerHijoIzquierdo(raiz):
        return raiz[1]
    
    def obtenerHijoDerecho(raiz):
        return raiz[2]

El :ref:`ActiveCode 2 <lst_bintreetry>` ejecuta las funciones que acabamos de escribir para árboles. Usted debe probarlo por sí mismo. Uno de los ejercicios le pide que dibuje la estructura de árbol resultante de este conjunto de llamadas.

.. :ref:`ActiveCode 2 <lst_bintreetry>` exercises the tree functions we have just written. You should try it out for yourself. One of the exercises asks you to draw the tree structure resulting from this set of calls.

.. _lst_bintreetry:


.. activecode:: bin_tree
    :caption: Una sesión en Python para ilustrar las funciones básicas para los árboles

    def ArbolBinario(r):
        return [r, [], []]    

    def insertarIzquierdo(raiz,nuevaRama):
        t = raiz.pop(1)
        if len(t) > 1:
            raiz.insert(1,[nuevaRama,t,[]])
        else:
            raiz.insert(1,[nuevaRama, [], []])
        return raiz

    def insertarDerecho(raiz,nuevaRama):
        t = raiz.pop(2)
        if len(t) > 1:
            raiz.insert(2,[nuevaRama,[],t])
        else:
            raiz.insert(2,[nuevaRama,[],[]])
        return raiz

    def obtenerValorRaiz(raiz):
        return raiz[0]
    
    def asignarValorRaiz(raiz,nuevoValor):
        raiz[0] = nuevoValor
    
    def obtenerHijoIzquierdo(raiz):
        return raiz[1]
    
    def obtenerHijoDerecho(raiz):
        return raiz[2]

    r = ArbolBinario(3)
    insertarIzquierdo(r,4)
    insertarIzquierdo(r,5)
    insertarDerecho(r,6)
    insertarDerecho(r,7)
    l = obtenerHijoIzquierdo(r)
    print(l)
    
    asignarValorRaiz(l,9)
    print(r)
    insertarIzquierdo(l,11)
    print(r)
    print(obtenerHijoDerecho(obtenerHijoDerecho(r)))
    

.. admonition:: Autoevaluación

   .. mchoice:: mctree_1
      :correct: c
      :answer_a: ['a', ['b', [], []], ['c', [], ['d', [], []]]]
      :answer_b: ['a', ['c', [], ['d', ['e', [], []], []]], ['b', [], []]]
      :answer_c: ['a', ['b', [], []], ['c', [], ['d', ['e', [], []], []]]]
      :answer_d: ['a', ['b', [], ['d', ['e', [], []], []]], ['c', [], []]]
      :feedback_a: No es así, este árbol no tiene el nodo 'e'.
      :feedback_b: Esto está cerca, pero si usted mira cuidadosamente verá que los hijos izquierdo y derecho de la raíz están intercambiados.
      :feedback_c: Muy bien
      :feedback_d: Esto está cerca, pero los nombres de los hijos izquierdo y derecho han sido intercambiados junto con las estructuras subyacentes.

      Dadas las siguientes instrucciones:

      .. sourcecode:: python
      
          x = ArbolBinario('a')
          insertarIzquierdo(x,'b')
          insertarDerecho(x,'c')
          insertarDerecho(obtenerHijoDerecho(x),'d')
          insertarIzquierdo(obtenerHijoDerecho(obtenerHijoDerecho(x)),'e')    

      ¿Cuál de las siguientes respuestas corresponde a la representación correcta del árbol?

   Escriba una función ``crearArbol`` que devuelva un árbol usando las funciones de lista de listas y que corresponda al siguiente árbol:

   .. image:: Figures/tree_ex.png

   .. actex:: mctree_2

      from test import testEqual
      
      def crearArbol():
          #Escriba su código aquí
          
      arbolDePrueba = crearArbol()
      testEqual(obtenerValorRaiz(obtenerHijoDerecho(arbolDePrueba)),'c')
      testEqual(obtenerValorRaiz(obtenerHijoDerecho(obtenerHijoIzquierdo(arbolDePrueba))),'d')      
      testEqual(obtenerValorRaiz(obtenerHijoDerecho(obtenerHijoDerecho(arbolDePrueba))),'f')            
      
