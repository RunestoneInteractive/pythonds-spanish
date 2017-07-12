..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Vocabulario y definiciones
--------------------------

Ahora que hemos visto algunos ejemplos de grafos, definiremos más formalmente un grafo y sus componentes. Ya conocemos algunos de estos términos desde nuestra discusión sobre los árboles.

.. Now that we have looked at some examples of graphs, we will more formally define a graph and its components. We already know some of these terms from our discussion of trees.

Vértice
    Un vértice (también llamado “nodo”) es una parte fundamental de un grafo. Puede tener un nombre, que llamaremos “clave”. Un vértice también puede tener información adicional. A esta información adicional la llamaremos “carga útil”.

Arista
    Una arista (también llamada “arco”) es otra parte fundamental de un grafo. Una arista conecta dos vértices para mostrar que hay una relación entre ellos. Las aristas pueden ser unidireccionales o bidireccionales. Si las aristas de un grafo son todas unidireccionales, decimos que el grafo es un **grafo dirigido** o un **digrafo**. El grafo de prerrequisitos de asignaturas que se muestra arriba es claramente un digrafo ya que se deben tomar algunas asignaturas antes que otras.

Ponderación
    Las aristas pueden ponderarse para mostrar que hay un costo para ir de un vértice a otro. Por ejemplo, en un grafo de carreteras que conectan una ciudad con otra, la ponderación en la arista puede representar la distancia entre las dos ciudades.

Con esas definiciones a mano podemos definir formalmente un grafo. Un grafo puede ser representado por :math:`G` donde :math:`G=(V,E)`. Para el grafo :math:`G`, :math:`V` es un conjunto de vértices y :math:`E` es un conjunto de aristas. Cada arista es una tupla :math:`(v,w)` donde :math:`w,v \in V`. Podemos añadir un tercer componente a la tupla de la arista para representar una ponderación. Un subgrafo :math:`s` es un conjunto de aristas :math:`e` y de vértices :math:`v` tales que :math:`e \subset E` y :math:`v \subset V`.

.. With those definitions in hand we can formally define a graph. A graph can be represented by :math:`G` where :math:`G =(V,E)`. For the graph :math:`G`, :math:`V` is a set of vertices and :math:`E` is a set of edges. Each edge is a tuple :math:`(v,w)` where :math:`w,v \in V`. We can add a third component to the edge tuple to represent a weight. A subgraph :math:`s` is a set of edges :math:`e` and vertices :math:`v` such that :math:`e \subset E` and :math:`v \subset V`.

La :ref:`Figura 2 <fig_dgsimple>` muestra otro ejemplo de un digrafo ponderado simple. Formalmente podemos representar este grafo como el conjunto de seis vértices:

.. :ref:`Figure  2 <fig_dgsimple>` shows another example of a simple weighted digraph. Formally we can represent this graph as the set of six vertices:

.. math::

   V = \left\{ V0,V1,V2,V3,V4,V5 \right\}

y el conjunto de nueve aristas:

.. math::

   E = \left\{ \begin{array}{l}(v0,v1,5), (v1,v2,4), (v2,v3,9), (v3,v4,7), (v4,v0,1), \\
                (v0,v5,2),(v5,v4,8),(v3,v5,3),(v5,v2,1)
                \end{array} \right\}

..  _fig_dgsimple:

.. figure:: Figures/digraph.png
   :align: center

   Figura 2: Un ejemplo simple de un grafo dirigido

   Figura 2: Un ejemplo simple de un grafo dirigido

El grafo de ejemplo en la :ref:`Figura 2 <fig_dgsimple>` ayuda a ilustrar otros dos términos clave de los grafos:

.. The example graph in :ref:`Figure 2 <fig_dgsimple>` helps illustrate two other key graph terms:

Ruta
    Una ruta en un grafo es una secuencia de vértices que están conectados por las aristas. Formalmente definiríamos una ruta como :math:`w_1, w_2, ..., w_n` tal que :math:`(w_i, w_{i+1}) \in E` para todo :math:`1 \le i \le n-1`. La longitud de la ruta no ponderada es el número de aristas en la ruta, específicamente :math:`n-1`. La longitud ponderada de la ruta es la suma de las ponderaciones de todos las aristas en la trayectoria. Por ejemplo, en la :ref:`Figura 2 <fig_dgsimple>` la ruta desde :math:`V3` hasta :math:`V1` es la secuencia de vértices :math:`(V3,V4,V0,V1)`. Las aristas son :math:`\left\{(v3,v4,7),(v4,v0,1),(v0,v1,5) \right\}`.

Ciclo
    Un ciclo en un grafo dirigido es una ruta que comienza y termina en el mismo vértice. Por ejemplo, en la :ref:`Figura 2 <fig_dgsimple>` la ruta :math:`(V5,V2,V3,V5)` es un ciclo. Un grafo sin ciclos se denomina **grafo acíclico**. Un grafo dirigido sin ciclos se denomina **grafo acíclico dirigido** o **GAD**. Veremos que podemos resolver varios problemas importantes si el problema se puede representar como un GAD.
