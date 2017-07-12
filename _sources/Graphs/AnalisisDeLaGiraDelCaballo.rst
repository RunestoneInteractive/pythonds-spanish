..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Análisis de la gira del caballo
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hay un último tema interesante sobre el problema de la gira del caballo, luego pasaremos a la versión general de la búsqueda en profundidad. El tema es el desempeño. En particular, ``giraCaballo`` es muy sensible al método que usted use para seleccionar el siguiente vértice a visitar. Por ejemplo, en un tablero de cinco por cinco usted puede producir una ruta en aproximadamente 1.5 segundos en una computadora razonablemente rápida. Pero, ¿qué ocurre si usted intenta hacerlo con un tablero de ocho por ocho? En este caso, dependiendo de la velocidad de su computadora, ¡usted podría tener que esperar hasta media hora para obtener los resultados! La razón de esto es que el problema de la gira del caballo, como lo hemos implementado hasta ahora, es un algoritmo exponencial de tamaño :math:`O(k^N)`, donde N es el número de cuadrados en el tablero de ajedrez, y k es una constante pequeña. La :ref:`Figura 12 <fig_8array>` puede ayudarnos a visualizar por qué esto es así. La raíz del árbol representa el punto de partida de la búsqueda. A partir de ahí el algoritmo genera y comprueba cada uno de los movimientos posibles que el caballo puede hacer. Como hemos notado antes, el número de movimientos posibles depende de la posición del caballo en el tablero. En las esquinas hay sólo dos movimientos legales, en los cuadrados adyacentes a las esquinas hay tres y en el centro del tablero hay ocho. La :ref:`Figura 13 <fig_numMoves>` muestra el número de movimientos posibles para cada posición en un tablero. En el siguiente nivel del árbol hay otra vez entre 2 y 8 movimientos siguientes posibles desde la posición que estamos explorando actualmente. El número de posiciones posibles por examinar corresponde al número de nodos en el árbol de búsqueda.

.. There is one last interesting topic regarding the knight’s tour problem, then we will move on to the general version of the depth first search. The topic is performance. In particular, ``giraCaballo`` is very sensitive to the method you use to select the next vertex to visit. For example, on a five-by-five board you can produce a path in about 1.5 seconds on a reasonably fast computer. But what happens if you try an eight-by-eight board? In this case, depending on the speed of your computer, you may have to wait up to a half hour to get the results! The reason for this is that the knight’s tour problem as we have implemented it so far is an exponential algorithm of size :math:`O(k^N)`, where N is the number of squares on the chess board, and k is a small constant. :ref:`Figure 12 <fig_8array>` can help us visualize why this is so. The root of the tree represents the starting point of the search. From there the algorithm generates and checks each of the possible moves the knight can make. As we have noted before the number of moves possible depends on the position of the knight on the board. In the corners there are only two legal moves, on the squares adjacent to the corners there are three and in the middle of the board there are eight. :ref:`Figure 13 <fig_numMoves>` shows the number of moves possible for each position on a board. At the next level of the tree there are once again between 2 and 8 possible next moves from the position we are currently exploring. The number of possible positions to examine corresponds to the number of nodes in the search tree.

.. _fig_8array:  

.. figure:: Figures/8arrayTree.png
   :align: center

   Figura 12: Un árbol de búsqueda para la gira del caballo

   Figura 12: Un árbol de búsqueda para la gira del caballo

.. _fig_numMoves:

.. figure:: Figures/moveCount.png
   :align: center

   Figura 13: Número de movimientos posibles para cada cuadrado

   Figura 13: Número de movimientos posibles para cada cuadrado


Ya hemos visto que el número de nodos en un árbol binario de altura N es :math:`2^{N+1}-1`. Para un árbol con nodos que pueden tener hasta ocho hijos en lugar de dos, el número de nodos es mucho mayor. Debido a que el factor de ramificación de cada nodo es variable, podríamos estimar el número de nodos usando un factor de ramificación promedio. Lo importante a destacar es que este algoritmo es exponencial: :math:`k^{N+1}-1`, donde :math:`k` es el factor de ramificación promedio para el tablero. ¡Veamos cuán rápidamente crece esto! Para un tablero de tamaño 5x5, el árbol será de 25 niveles de profundidad, o N = 24 contando el primer nivel como nivel 0. El factor de ramificación promedio es :math:`k = 3.8`; así que el número de nodos en el árbol de búsqueda es :math:`3.8^{25}-1` ó :math:`3.12 \times 10^{14}`. Para un tablero de tamaño 6x6, :math:`k = 4.4`, hay :math:`1.5 \times 10^{23}` nodos, y para un tablero de ajedrez regular de 8x8, :math:`k = 5.25`, hay :math:`1.3 \times 10^{46}`. Por supuesto, dado que existen múltiples soluciones al problema, no tendremos que explorar cada uno de los nodos, pero la parte fraccional de los nodos que tenemos que explorar es simplemente un multiplicador constante que no cambia la naturaleza exponencial del problema. Dejaremos que usted vea, como ejercicio, si puede expresar :math:`k` en función del tamaño del tablero.

.. We have already seen that the number of nodes in a binary tree of height N is :math:`2^{N+1}-1`. For a tree with nodes that may have up to eight children instead of two the number of nodes is much larger. Because the branching factor of each node is variable, we could estimate the number of nodes using an average branching factor. The important thing to note is that this algorithm is exponential: :math:`k^{N+1}-1`, where :math:`k` is the average branching factor for the board. Let’s look at how rapidly this grows! For a board that is 5x5 the tree will be 25 levels deep, or N = 24 counting the first level as level 0. The average branching factor is :math:`k = 3.8` So the number of nodes in the search tree is :math:`3.8^{25}-1` or :math:`3.12 \times 10^{14}`. For a 6x6 board, :math:`k = 4.4`, there are :math:`1.5 \times 10^{23}` nodes, and for a regular 8x8 chess board, :math:`k = 5.25`, there are :math:`1.3 \times 10^{46}`. Of course, since there are multiple solutions to the problem we won’t have to explore every single node, but the fractional part of the nodes we do have to explore is just a constant multiplier which does not change the exponential nature of the problem. We will leave it as an exercise for you to see if you can express :math:`k` as a function of the board size.

Por suerte hay una manera de acelerar el caso de un tablero ocho por ocho para que funcione en menos de un segundo. En el programa siguiente mostramos el código que acelera ``giraCaballo``. Esta función (ver el :ref:`Programa 4 <lst_avail>`), llamada ``ordenPorDisp`` se utilizará en lugar de la llamada a ``u.obtenerConexiones`` en el código mostrado anteriormente. La línea crítica en la función ``ordenPorDisp`` es la línea 10. Esta línea asegura que seleccionemos, para ir a continuación, el vértice que tenga el menor número de movimientos disponibles. Usted podría pensar que esto es realmente contraproducente; ¿por qué no seleccionar el nodo que tiene la mayor cantidad de movimientos disponibles? Usted puede probar ese enfoque fácilmente ejecutando el programa usted mismo e insertando la línea ``listaRes.reverse()`` justo después del ordenamiento.

.. Luckily there is a way to speed up the eight-by-eight case so that it runs in under one second. In the listing below we show the code that speeds up the ``giraCaballo``. This function (see :ref:`Listing 4 <lst_avail>`), called ``ordenPorDisp`` will be used in place of the call to ``u.obtenerConexiones`` in the code previously shown above. The critical line in the ``ordenPorDisp`` function is line 10. This line ensures that we select the vertex to go next that has the fewest available moves. You might think this is really counter productive; why not select the node that has the most available moves? You can try that approach easily by running the program yourself and inserting the line ``listaRes.reverse()`` right after the sort.

El problema de usar el vértice con la mayor cantidad de movimientos disponibles como siguiente vértice en la ruta es que tiende a que el caballo tenga que visitar los cuadrados del medio anticipadamente durante la gira. Cuando esto sucede, es factible que el caballo se quede varado en un lado del tablero donde no puede alcanzar cuadrados no visitados en el otro lado del tablero. Por otro lado, visitar primero los cuadrados con el menor número de movimientos disponibles obliga al caballo a visitar primero los cuadrados alrededor de los bordes del tablero. Esto asegura que el caballo visite temprano las esquinas difíciles de alcanzar y pueda usar los cuadrados del medio para saltar a través del tablero solamente cuando sea necesario. Utilizar este tipo de conocimiento para acelerar un algoritmo se denomina heurística. Los seres humanos usan la heurística todos los días para ayudar a tomar decisiones, las búsquedas heurísticas se utilizan a menudo en el campo de la inteligencia artificial. Esta heurística particular se llama el algoritmo de Warnsdorff, nombrado en honor a H. C. Warnsdorff que publicó su idea en 1823.

.. The problem with using the vertex with the most available moves as your next vertex on the path is that it tends to have the knight visit the middle squares early on in the tour. When this happens it is easy for the knight to get stranded on one side of the board where it cannot reach unvisited squares on the other side of the board. On the other hand, visiting the squares with the fewest available moves first pushes the knight to visit the squares around the edges of the board first. This ensures that the knight will visit the hard-to-reach corners early and can use the middle squares to hop across the board only when necessary. Utilizing this kind of knowledge to speed up an algorithm is called a heuristic. Humans use heuristics every day to help make decisions, heuristic searches are often used in the field of artificial intelligence. This particular heuristic is called Warnsdorff’s algorithm, named after H. C. Warnsdorff who published his idea in 1823.

.. _lst_avail:

**Programa 4**

.. highlight:: python
    :linenothreshold: 5

::

    def ordenPorDisp(n):
        listaRes = []
        for v in n.obtenerConexiones():
            if v.obtenerColor() == 'blanco':
                c = 0
                for w in v.obtenerConexiones():
                    if w.obtenerColor() == 'blanco':
                        c = c + 1
                listaRes.append((c,v))
        listaRes.sort(key=lambda x: x[0])
        return [y[1] for y in listaRes]   


.. highlight:: python
    :linenothreshold: 500    


