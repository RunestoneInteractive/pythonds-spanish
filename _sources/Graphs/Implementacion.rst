..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementación
~~~~~~~~~~~~~~

Utilizando diccionarios, es fácil implementar la lista de adyacencia en Python. En nuestra implementación del tipo abstracto de datos Grafo, crearemos dos clases (ver el :ref:`Programa 1 <lst_vertex>` y el :ref:`Programa 2 <lst_graph>`), ``Grafo``, que contiene la lista maestra de vértices, y ``Vertice``, que representará cada vértice en el grafo.

.. Using dictionaries, it is easy to implement the adjacency list in Python. In our implementation of the Graph abstract data type we will create two classes (see :ref:`Listing 1 <lst_vertex>` and :ref:`Listing 2 <lst_graph>`), ``Grafo``, which holds the master list of vertices, and ``Vertice``, which will represent each vertex in the graph.

Cada ``Vertice`` utiliza un diccionario para realizar un seguimiento de los vértices a los que está conectado, y la ponderación de cada arista. Este diccionario se llama ``conectadoA``. El programa mostrado a continuación corresponde al código de la clase ``Vertice``. El constructor simplemente inicializa el ``id``, que normalmente será una cadena, y el  diccionario ``conectadoA``. El método ``agregarVecino`` se utiliza para agregar una conexión desde este vértice a otro. El método ``obtenerConexiones`` devuelve todos los vértices de la lista de adyacencia, representados por la variable ``conectadoA``. El método ``obtenerPonderacion`` devuelve la ponderación de la arista de este vértice al vértice pasado como parámetro.

.. Each ``Vertice`` uses a dictionary to keep track of the vertices to which it is connected, and the weight of each edge. This dictionary is called ``conectadoA``. The listing below shows the code for the ``Vertice`` class. The constructor simply initializes the ``id``, which will typically be a string, and the ``conectadoA`` dictionary. The ``agregarVecino`` method is used add a connection from this vertex to another. The ``obtenerConexiones`` method returns all of the vertices in the adjacency list, as represented by the ``conectadoA`` instance variable. The ``obtenerPonderacion`` method returns the weight of the edge from this vertex to the vertex passed as a parameter.

.. _lst_vertex:

**Programa 1**

::

    class Vertice:
        def __init__(self,clave):
            self.id = clave
            self.conectadoA = {}

        def agregarVecino(self,vecino,ponderacion=0):
            self.conectadoA[vecino] = ponderacion

        def __str__(self):
            return str(self.id) + ' conectadoA: ' + str([x.id for x in self.conectadoA])

        def obtenerConexiones(self):
            return self.conectadoA.keys()

        def obtenerId(self):
            return self.id

        def obtenerPonderacion(self,vecino):
            return self.conectadoA[vecino]

La clase ``Grafo``, mostrada en el siguiente programa, contiene un diccionario que asigna nombres de vértices a objetos vértice. En la :ref:`Figura 4 <fig_adjlist>` este objeto diccionario está representado por el recuadro sombreado de gris. ``Grafo`` también proporciona métodos para agregar vértices a un grafo y conectar un vértice a otro. El método ``obtenerVertices`` devuelve los nombres de todos los vértices del grafo. Además, hemos implementado el método ``__iter__`` para facilitar la iteración sobre todos los objetos vértice de un grafo en particular. Juntos, los dos métodos permiten iterar sobre los vértices de un grafo por nombre, o por los objetos mismos.

.. The ``Grafo`` class, shown in the next listing, contains a dictionary that maps vertex names to vertex objects. In :ref:`Figure 4 <fig_adjlist>` this dictionary object is represented by the shaded gray box. ``Grafo`` also provides methods for adding vertices to a graph and connecting one vertex to another. The ``obtenerVertices`` method returns the names of all of the vertices in the graph. In addition, we have implemented the ``__iter__`` method to make it easy to iterate over all the vertex objects in a particular graph. Together, the two methods allow you to iterate over the vertices in a graph by name, or by the objects themselves.

.. _lst_graph:

**Programa 2**

::

    class Grafo:
        def __init__(self):
            self.listaVertices = {}
            self.numVertices = 0
            
        def agregarVertice(self,clave):
            self.numVertices = self.numVertices + 1
            nuevoVertice = Vertice(clave)
            self.listaVertices[clave] = nuevoVertice
            return nuevoVertice
        
        def obtenerVertice(self,n):
            if n in self.listaVertices:
                return self.listaVertices[n]
            else:
                return None

        def __contains__(self,n):
            return n in self.listaVertices
        
        def agregarArista(self,de,a,costo=0):
            if de not in self.listaVertices:
                nv = self.agregarVertice(de)
            if a not in self.listaVertices:
                nv = self.agregarVertice(a)
            self.listaVertices[de].agregarVecino(self.listaVertices[a], costo)
        
        def obtenerVertices(self):
            return self.listaVertices.keys()
            
        def __iter__(self):
            return iter(self.listaVertices.values())

Utilizando las clases ``Grafo`` y ``Vertice`` que acabamos de definir, la siguiente sesión de Python crea el grafo de la :ref:`Figura 2 <fig_dgsimple>`. Primero creamos seis vértices numerados de 0 a 5. Luego mostramos el diccionario de vértices. Observe que para cada clave de 0 a 5 hemos creado una instancia de ``Vertice``. A continuación, agregamos las aristas que conectan los vértices entre sí. Finalmente, un ciclo anidado verifica que cada arista en el grafo esté almacenada correctamente. Compruebe la salida de la lista de aristas al final de esta sesión comparándola con la :ref:`Figura 2 <fig_dgsimple>`.

.. Using the ``Grafo`` and ``Vertice`` classes just defined, the following Python session creates the graph in :ref:`Figure 2 <fig_dgsimple>`. First we create six vertices numbered 0 through 5. Then we display the vertex dictionary. Notice that for each key 0 through 5 we have created an instance of a ``Vertice``. Next, we add the edges that connect the vertices together. Finally, a nested loop verifies that each edge in the graph is properly stored. You should check the output of the edge list at the end of this session against :ref:`Figure 2 <fig_dgsimple>`.

::

    >>> g = Grafo()
    >>> for i in range(6):
    ...    g.agregarVertice(i)
    >>> g.listaVertices
    {0: <__main__.Vertice object>, 
     1: <__main__.Vertice object>, 
     2: <__main__.Vertice object>, 
     3: <__main__.Vertice object>, 
     4: <__main__.Vertice object>, 
     5: <__main__.Vertice object>}
    >>> g.agregarArista(0,1,5)
    >>> g.agregarArista(0,5,2)
    >>> g.agregarArista(1,2,4)
    >>> g.agregarArista(2,3,9)
    >>> g.agregarArista(3,4,7)
    >>> g.agregarArista(3,5,3)
    >>> g.agregarArista(4,0,1)
    >>> g.agregarArista(5,4,8)
    >>> g.agregarArista(5,2,1)
    >>> for v in g:
    ...    for w in v.obtenerConexiones(): 
    ...        print("( %s , %s )" % (v.obtenerId(), w.obtenerId()))
    ... 
    ( 0 , 1 )
    ( 0 , 5 )
    ( 1 , 2 )
    ( 2 , 3 )
    ( 3 , 5 )
    ( 3 , 4 )
    ( 4 , 0 )
    ( 5 , 2 )
    ( 5 , 4 )
