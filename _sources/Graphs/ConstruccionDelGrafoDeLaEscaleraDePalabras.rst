..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Construcción del grafo de la escalera de palabras
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nuestro primer problema es averiguar cómo convertir una gran colección de palabras en un grafo. Lo que nos gustaría es tener una arista de una palabra a otra si las dos palabras se diferencian por una sola letra. Si podemos crear tal grafo, entonces cualquier ruta de una palabra a otra es una solución al rompecabezas de la escalera de palabras. La :ref:`Figura 1 <fig_wordladder>` muestra un pequeño grafo de algunas palabras en inglés que resuelven el problema de la escalera de palabras de FOOL a SAGE. Observe que el grafo es un grafo no dirigido y que las aristas no están ponderadas.

.. Our first problem is to figure out how to turn a large collection of words into a graph. What we would like is to have an edge from one word to another if the two words are only different by a single letter. If we can create such a graph, then any path from one word to another is a solution to the word ladder puzzle. :ref:`Figure 1 <fig_wordladder>` shows a small graph of some words that solve the FOOL to SAGE word ladder problem. Notice that the graph is an undirected graph and that the edges are unweighted.

.. _fig_wordladder:

.. figure:: Figures/wordgraph.png
   :align: center

   Figura 1: Un pequeño grafo de una escalera de palabras

   Figura 1: Un pequeño grafo de una escalera de palabras

Podríamos utilizar varios enfoques diferentes para crear el grafo que necesitamos para resolver este problema. Comencemos con la suposición de que tenemos una lista de palabras que son todas de la misma longitud. Como punto de partida, podemos crear un vértice en el grafo por cada palabra de la lista. Para averiguar cómo conectar las palabras, podríamos comparar cada palabra en la lista con cada una de las otras. Cuando comparamos, miramos cuántas letras son diferentes. Si las dos palabras en cuestión son diferentes en una sola letra, podemos crear una arista entre ellas en el grafo. Para un pequeño conjunto de palabras, ese enfoque funcionaría bien; sin embargo supongamos que tenemos una lista de 5,110 palabras. A grandes rasgos, la comparación de una palabra con otra palabra en la lista es un algoritmo :math:`O(n^2)`. Para 5,110 palabras, :math:`n^2` son más de 26 millones de comparaciones.

.. We could use several different approaches to create the graph we need to solve this problem. Let’s start with the assumption that we have a list of words that are all the same length. As a starting point, we can create a vertex in the graph for every word in the list. To figure out how to connect the words, we could compare each word in the list with every other. When we compare we are looking to see how many letters are different. If the two words in question are different by only one letter, we can create an edge between them in the graph. For a small set of words that approach would work fine; however let’s suppose we have a list of 5,110 words. Roughly speaking, comparing one word to every other word on the list is an :math:`O(n^2)` algorithm. For 5,110 words, :math:`n^2` is more than 26 million comparisons.

Podemos hacerlo mucho mejor usando el siguiente enfoque. Supongamos que tenemos un gran número de baldes, cada uno de ellos con una palabra de cuatro letras en el exterior, excepto que una de las letras de la etiqueta ha sido sustituido por un guión bajo. Por ejemplo, considere la :ref:`Figura 2 <fig_wordbucket>`, podríamos tener un balde etiquetado como “pop\_”. A medida que procesamos cada palabra en nuestra lista comparamos la palabra con cada balde, usando el ‘\_’ como un comodín, de modo que tanto “pope” como “pops” coincidirían con “pop\_”. Cada vez que encontremos un balde coincidente, pondremos nuestra palabra en ese balde. Una vez que tengamos todas las palabras en los baldes apropiados sabremos que todas las palabras en el balde deben estar conectadas.

.. We can do much better by using the following approach. Suppose that we have a huge number of buckets, each of them with a four-letter word on the outside, except that one of the letters in the label has been replaced by an underscore. For example, consider :ref:`Figure 2 <fig_wordbucket>`, we might have a bucket labeled “pop\_.” As we process each word in our list we compare the word with each bucket, using the ‘\_’ as a wildcard, so both “pope” and “pops” would match “pop\_.” Every time we find a matching bucket, we put our word in that bucket. Once we have all the words in the appropriate buckets we know that all the words in the bucket must be connected.

.. _fig_wordbucket:
    
.. figure:: Figures/wordbuckets.png
   :align: center

   Figura 2: Baldes de palabras para palabras que se diferencian por una sola letra

   Figura 2: Baldes de palabras para palabras que se diferencian por una sola letra


En Python, podemos implementar el esquema que acabamos de describir usando un diccionario. Las etiquetas de los baldes que acabamos de describir son las claves de nuestro diccionario. El valor almacenado para esa clave es una lista de palabras. Una vez que tenemos el diccionario construido podemos crear el grafo. Iniciamos nuestro grafo creando un vértice para cada palabra en el grafo. Luego creamos aristas entre todos los vértices que encontramos para palabras encontradas bajo la misma clave en el diccionario. El :ref:`Programa 1 <lst_wordbucket1>` muestra el código en Python necesario para construir el grafo.

.. In Python, we can implement the scheme we have just described by using a dictionary. The labels on the buckets we have just described are the keys in our dictionary. The value stored for that key is a list of words. Once we have the dictionary built we can create the graph. We start our graph by creating a vertex for each word in the graph. Then we create edges between all the vertices we find for words found under the same key in the dictionary. :ref:`Listing 1 <lst_wordbucket1>` shows the Python code required to build the graph.

.. _lst_wordbucket1:

**Programa 1**

::

    from pythoned.grafos import Grafo
  
    def construirGrafo(archivoPalabras):
        d = {}
        g = Grafo()    
        archivo = open(archivoPalabras,'r')
        # crear baldes de palabras que se diferencian por una letra
        for linea in archivo:
            palabra = linea[:-1]
            for i in range(len(palabra)):
                balde = palabra[:i] + '_' + palabra[i+1:]
                if balde in d:
                    d[balde].append(palabra)
                else:
                    d[balde] = [palabra]
        # agregar vértices y aristas para palabras en el mismo balde
        for balde in d.keys():
            for palabra1 in d[balde]:
                for palabra2 in d[balde]:
                    if palabra1 != palabra2:
                        g.agregarArista(palabra1,palabra2)
        return g

Puesto que éste es nuestro primer problema de grafos de un caso real, usted podría preguntarse: ¿qué tan ralo es el grafo? La lista de palabras de cuatro letras que tenemos para este problema es de 5,110 palabras. Si tuviéramos que usar una matriz de adyacencia, la matriz tendría 5,110 \* 5,110 = 26,112,100 celdas. El grafo construido por la función ``construcciónGrafo`` tiene exactamente 53,286 aristas, por lo cual ¡la matriz tendría sólo el 0.20% de las celdas llenas! Ésa es una matriz muy rala.

.. Since this is our first real-world graph problem, you might be wondering how sparse is the graph? The list of four-letter words we have for this problem is 5,110 words long. If we were to use an adjacency matrix, the matrix would have 5,110 \* 5,110 = 26,112,100 cells. The graph constructed by the ``construirGrafo`` function has exactly 53,286 edges, so the matrix would have only 0.20% of the cells filled! That is a very sparse matrix indeed.
