..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Árboles binarios de búsqueda equilibrados
-----------------------------------------

En la sección anterior estudiamos la construcción de un árbol binario de búsqueda. Como aprendimos, el desempeño del árbol binario de búsqueda puede degradarse a :math:`O(n)` para operaciones como ``obtener`` y ``agregar`` cuando el árbol se desequilibra. En esta sección examinaremos un tipo especial de árbol binario de búsqueda que garantiza automáticamente que el árbol permanezca equilibrado en todo momento. Este árbol se llama un **árbol AVL** en razón a sus inventores: G.M. Adelson-Velskii y E.M. Landis.

.. In the previous section we looked at building a binary search tree. As we learned, the performance of the binary search tree can degrade to :math:`O(n)` for operations like ``get`` and ``put`` when the tree becomes unbalanced. In this section we will look at a special kind of binary search tree that automatically makes sure that the tree remains balanced at all times. This tree is called an **AVL tree** and is named for its inventors: G.M. Adelson-Velskii and E.M. Landis.

Un árbol AVL implementa el tipo abstracto de datos Vector Asociativo al igual que un árbol binario de búsqueda regular, la única diferencia está en cómo el árbol se desempeña. Para implementar nuestro árbol AVL necesitamos hacer seguimiento de un **factor de equilibrio** para cada nodo en el árbol. Hacemos esto observando las alturas de los subárboles izquierdo y derecho para cada nodo. Más formalmente, definimos el factor de equilibrio para un nodo como la diferencia entre la altura del subárbol izquierdo y la altura del subárbol derecho.

.. An AVL tree implements the Map abstract data type just like a regular binary search tree, the only difference is in how the tree performs. To implement our AVL tree we need to keep track of a **balance factor** for each node in the tree. We do this by looking at the heights of the left and right subtrees for each node. More formally, we define the balance factor for a node as the difference between the height of the left subtree and the height of the right subtree.

.. math::

   factorEquilibrio = altura(subarbolIzquierdo) - altura(subarbolDerecho)

Utilizando la definición de factor de equilibrio dada anteriormente, decimos que un subárbol es pesado a la izquierda si el factor de equilibrio es mayor que cero. Si el factor de equilibrio es menor que cero, entonces el subárbol es pesado a la derecha. Si el factor de equilibrio es cero entonces el árbol está perfectamente equilibrado. Para propósitos de implementar un árbol AVL y obtener el beneficio de tener un árbol equilibrado, definiremos que un árbol estará en equilibrio si el factor de equilibrio es -1, 0 ó 1. Una vez que el factor de equilibrio de un nodo en un árbol esté fuera de este rango necesitaremos un procedimiento para reequilibrar el árbol nuevamente. La :ref:`Figura 1 <fig_unbal>` muestra un ejemplo de un árbol desequilibrado y pesado a la derecha y los factores de equilibrio de cada nodo.

.. Using the definition for balance factor given above we say that a subtree is left-heavy if the balance factor is greater than zero. If the balance factor is less than zero then the subtree is right heavy. If the balance factor is zero then the tree is perfectly in balance. For purposes of implementing an AVL tree, and gaining the benefit of having a balanced tree we will define a tree to be in balance if the balance factor is -1, 0, or 1. Once the balance factor of a node in a tree is outside this range we will need to have a procedure to bring the tree back into balance. :ref:`Figure 1 <fig_unbal>` shows an example of an unbalanced, right-heavy tree and the balance factors of each node.


.. _fig_unbal:

.. figure:: Figures/unbalanced.png
   :align: center

   Figura 1: Un árbol desequilibrado y pesado a la derecha con factores de equilibrio

   Figura 1: Un árbol desequilibrado y pesado a la derecha con factores de equilibrio
