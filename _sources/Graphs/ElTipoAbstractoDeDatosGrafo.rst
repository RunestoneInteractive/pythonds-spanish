..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


El tipo abstracto de datos grafo
--------------------------------

El tipo abstracto de datos (TAD) grafo está definido como sigue:

-  ``Grafo()`` crea un grafo nuevo y vacío.

-  ``agregarVertice(vert)`` agrega una instancia de ``Vertice`` al grafo.

-  ``agregarArista(deVertice, aVertice)`` agrega al grafo  una nueva arista dirigida que conecta dos vértices.

-  ``agregarArista(deVertice, aVertice, ponderacion)`` agrega al grafo una nueva arista ponderada y dirigida que conecta dos vértices.

-  ``obtenerVertice(claveVert)`` encuentra el vértice en el grafo con nombre ``claveVert``.

-  ``obtenerVertices()`` devuelve la lista de todos los vértices en el grafo.

-  ``in`` devuelve ``True`` para una instrucción de la forma ``vertice in grafo``, si el vértice dado está en el grafo, ``False`` de lo contrario.

A partir de la definición formal de un grafo, hay varias maneras de implementar el TAD grafo en Python. Veremos que hay concesiones mutuas en el uso de diferentes representaciones para implementar el TAD descrito anteriormente. Hay dos implementaciones bien conocidas de un grafo, la **matriz de adyacencia** y la **lista de adyacencia**. Explicaremos ambas opciones y luego implementaremos una como una clase en Python.

.. Beginning with the formal definition for a graph there are several ways we can implement the graph ADT in Python. We will see that there are trade-offs in using different representations to implement the ADT described above. There are two well-known implementations of a graph, the **adjacency matrix** and the **adjacency list**. We will explain both of these options, and then implement one as a Python class.
