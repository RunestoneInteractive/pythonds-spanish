..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Análisis de árboles de búsqueda
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Con la implementación de un árbol binario de búsqueda ahora completo, haremos un análisis rápido de los métodos que hemos implementado. Veamos primero el método ``agregar``. El factor limitante en su rendimiento es la altura del árbol binario. Recuerde de la sección de vocabulario que la altura de un árbol es el número de aristas entre la raíz y el nodo hoja más profundo. La altura es el factor limitante porque cuando estamos buscando el lugar apropiado para insertar un nodo en el árbol, tendremos que hacer como máximo una comparación en cada nivel del árbol.

.. With the implementation of a binary search tree now complete, we will do a quick analysis of the methods we have implemented. Let’s first look at the ``put`` method. The limiting factor on its performance is the height of the binary tree. Recall from the vocabulary section that the height of a tree is the number of edges between the root and the deepest leaf node. The height is the limiting factor because when we are searching for the appropriate place to insert a node into the tree, we will need to do at most one comparison at each level of the tree.

¿Cuál será la probable altura de un árbol binario? La respuesta a esta pregunta depende de cómo se agregan las claves al árbol. Si las claves se agregan en un orden aleatorio, la altura del árbol estará alrededor de :math:`\log_2{n}` donde :math:`n` es el número de nodos en el árbol. Esto se debe a que si las claves están distribuidas aleatoriamente, aproximadamente la mitad de ellas serán menores que la raíz y la otra mitad será mayor que la raíz. Recuerde que en un árbol binario hay un nodo en la raíz, dos nodos en el siguiente nivel y cuatro en el siguiente. El número de nodos en cualquier nivel es :math:`2^d` donde :math:`d` es la profundidad del nivel. El número total de nodos en un árbol binario perfectamente equilibrado es :math:`2^{h+1}-1`, donde :math:`h` representa la altura del árbol.

.. What is the height of a binary tree likely to be? The answer to this question depends on how the keys are added to the tree. If the keys are added in a random order, the height of the tree is going to be around :math:`\log_2{n}` where :math:`n` is the number of nodes in the tree. This is because if the keys are randomly distributed, about half of them will be less than the root and half will be greater than the root. Remember that in a binary tree there is one node at the root, two nodes in the next level, and four at the next. The number of nodes at any particular level is :math:`2^d` where :math:`d` is the depth of the level. The total number of nodes in a perfectly balanced binary tree is :math:`2^{h+1}-1`, where :math:`h` represents the height of the tree.

Un árbol perfectamente equilibrado tiene el mismo número de nodos en el subárbol izquierdo que en el subárbol derecho. En un árbol binario equilibrado, el peor desempeño de ``agregar`` es :math:`O(\log_2{n})`, donde :math:`n` es el número de nodos en el árbol. Note que ésta es la relación inversa respecto al cálculo del párrafo anterior. Así que :math:`\log_2{n}` nos da la altura del árbol, y representa el número máximo de comparaciones que ``agregar`` necesitará hacer mientras busca el lugar apropiado para insertar un nodo nuevo.

.. A perfectly balanced tree has the same number of nodes in the left subtree as the right subtree. In a balanced binary tree, the worst-case performance of ``put`` is :math:`O(\log_2{n})`, where :math:`n` is the number of nodes in the tree. Notice that this is the inverse relationship to the calculation in the previous paragraph. So :math:`\log_2{n}` gives us the height of the tree, and represents the maximum number of comparisons that ``put`` will need to do as it searches for the proper place to insert a new node.

Infortunadamente, ¡es posible construir un árbol de búsqueda que tenga una altura :math:`n` insertando simplemente las claves ordenadas! Un ejemplo de tal árbol se muestra en la :ref:`Figura 6 <fig_skewedtree_analysis>`. En este caso, el rendimiento del método ``agregar`` es :math:`O(n)`.

.. Unfortunately it is possible to construct a search tree that has height :math:`n` simply by inserting the keys in sorted order! An example of such a tree is shown in :ref:`Figure 6 <fig_skewedtree_analysis>`. In this case the performance of the ``put`` method is :math:`O(n)`.

.. _fig_skewedtree_analysis:

.. figure:: Figures/skewedTree.png
   :align: center

   Figura 6: Un árbol binario de búsqueda sesgado daría un desempeño pobre

   Figura 6: Un árbol binario de búsqueda sesgado daría un desempeño pobre

Ahora que usted entiende que el desempeño del método ``agregar`` está limitado por la altura del árbol, probablemente supondrá que otros métodos, ``obtener``, ``in`` y ``del``, también están limitados. Dado que ``obtener`` busca en el árbol para encontrar la clave, en el peor de los casos se busca hasta el fondo del árbol y no se encuentra ninguna clave. A primera vista ``del`` parecería más complicado, ya que podría necesitar buscar el sucesor antes de que la operación de eliminación pueda completarse. Pero recuerde que el peor de los casos para encontrar el sucesor es también la altura del árbol, lo que significa que  el trabajo simplemente se duplica. Dado que la duplicación es un factor constante, no cambia el análisis del peor caso de :math:`O(n)` para un árbol no equilibrado.

.. Now that you understand that the performance of the ``put`` method is limited by the height of the tree, you can probably guess that other methods, ``get, in,`` and ``del``, are limited as well. Since ``get`` searches the tree to find the key, in the worst case the tree is searched all the way to the bottom and no key is found. At first glance ``del`` might seem more complicated, since it may need to search for the successor before the deletion operation can complete. But remember that the worst-case scenario to find the successor is also just the height of the tree which means that you would simply double the work. Since doubling is a constant factor it does not change worst case analysis of :math:`O(n)` for an unbalanced tree. 
