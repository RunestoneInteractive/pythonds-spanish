..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Análisis del algoritmo de Dijkstra
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Finalmente, veamos el tiempo de ejecución del algoritmo de Dijkstra. Notamos en primer lugar que construir la cola de prioridad toma un tiempo :math:`O(V)` ya que inicialmente agregamos cada vértice del grafo a la cola de prioridad. Una vez construida la cola, el ciclo ``while`` se ejecuta una vez para cada vértice, ya que los vértices son todos agregados al principio y sólo se eliminan después. Dentro de ese ciclo, cada llamada a ``eliminarMin`` toma un tiempo :math:`O(\log V)`. En conjunto, esa parte del ciclo y las llamadas a ``eliminarMin`` toman un tiempo :math:`O(V \log(V))`. El ciclo ``for`` se ejecuta una vez por cada arista en el grafo, y dentro del ciclo ``for`` la llamada a ``decrementarClave`` toma un tiempo :math:`O (E\log(V))`. Así que el tiempo de ejecución combinado es :math:`O((V+E) \log(V))`.

.. Finally, let us look at the running time of Dijkstra’s algorithm. We first note that building the priority queue takes :math:`O(V)` time since we initially add every vertex in the graph to the priority queue. Once the queue is constructed the ``while`` loop is executed once for every vertex since vertices are all added at the beginning and only removed after that. Within that loop each call to ``delMin``, takes :math:`O(\log V)` time. Taken together that part of the loop and the calls to delMin take :math:`O(V \log(V))`. The ``for`` loop is executed once for each edge in the graph, and within the ``for`` loop the call to ``decreaseKey`` takes time :math:`O(E\log(V)).` So the combined running time is :math:`O((V+E) \log(V)).`
