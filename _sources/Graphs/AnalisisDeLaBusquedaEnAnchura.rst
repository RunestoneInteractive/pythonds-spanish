..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Análisis de la búsqueda en anchura
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Antes de continuar con otros algoritmos de grafos vamos a analizar el desempeño de tiempo de ejecución del algoritmo de búsqueda en anchura. Lo primero que debemos observar es que el ciclo while se ejecuta, como máximo, una vez para cada vértice del grafo :math:`|V|`. Usted puede verificar que esto es cierto porque un vértice debe ser blanco antes de que pueda ser examinado y agregado a la cola. Esto nos da :math:`O(V)` para el ciclo while. El ciclo for, que está anidado dentro del while, se ejecuta como máximo una vez para cada arista del grafo, :math:`|E|`. La razón es que cada vértice sale de la cola a lo sumo una vez  y que examinamos una arista del nodo :math:`u` al nodo :math:`v` únicamente cuando el nodo :math:`u` sale de la cola. Esto nos da :math:`O(E)` para el ciclo for. Combinando los dos ciclos nos da :math:`O(V + E)`.

.. Before we continue with other graph algorithms let us analyze the run time performance of the breadth first search algorithm. The first thing to observe is that the while loop is executed, at most, one time for each vertex in the graph :math:`|V|`. You can see that this is true because a vertex must be white before it can be examined and added to the queue. This gives us :math:`O(V)` for the while loop. The for loop, which is nested inside the while is executed at most once for each edge in the graph, :math:`|E|`. The reason is that every vertex is dequeued at most once and we examine an edge from node :math:`u` to node :math:`v` only when node :math:`u` is dequeued. This gives us :math:`O(E)` for the for loop. combining the two loops gives us :math:`O(V + E)`.

Por supuesto, hacer la búsqueda en anchura es sólo una parte de la tarea. Seguir los enlaces desde el nodo inicial hasta el nodo objetivo es la otra parte de la tarea. El peor caso para esto sería que el grafo fuera una única cadena larga. En ese caso, recorrer todos los vértices sería :math:`O(V)`. El caso normal será alguna fracción de :math:`|V|` pero en todo caso escribiríamos :math:`O(V)`.

.. Of course doing the breadth first search is only part of the task. Following the links from the starting node to the goal node is the other part of the task. The worst case for this would be if the graph was a single long chain. In this case traversing through all of the vertices would be :math:`O(V)`. The normal case is going to be some fraction of :math:`|V|` but we would still write :math:`O(V)`.

Finalmente, al menos para este problema, también está el tiempo requerido para construir el grafo inicial. Dejamos el análisis de la función ``construirGrafo`` como ejercicio para usted.

.. Finally, at least for this problem, there is the time required to build the initial graph. We leave the analysis of the ``buildGraph`` function as an exercise for you.
