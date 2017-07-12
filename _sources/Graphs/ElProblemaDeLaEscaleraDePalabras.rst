..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


El problema de la escalera de palabras
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Para comenzar nuestro estudio de los algoritmos de grafos, consideremos el siguiente rompecabezas llamado escalera de palabras. Transforme la palabra “FOOL” (tonto, en inglés) en la palabra “SAGE” (sabio, en inglés). En un rompecabezas de escalera de palabras usted debe hacer que el cambio se produzca gradualmente mediante el cambio de una letra a la vez. En cada paso usted debe transformar una palabra en otra palabra, no se le permite transformar una palabra en una cadena que no sea una palabra. El rompecabezas de escalera de palabras fue inventado en 1878 por Lewis Carroll, el autor de *Alicia en el País de las Maravillas*. La siguiente secuencia de palabras en inglés muestra una posible solución al problema planteado anteriormente.

.. To begin our study of graph algorithms let’s consider the following puzzle called a word ladder. Transform the word “FOOL” into the word “SAGE”. In a word ladder puzzle you must make the change occur gradually by changing one letter at a time. At each step you must transform one word into another word, you are not allowed to transform a word into a non-word. The word ladder puzzle was invented in 1878 by Lewis Carroll, the author of *Alice in Wonderland*. The following sequence of words shows one possible solution to the problem posed above.

::

 FOOL
 POOL
 POLL
 POLE
 PALE
 SALE
 SAGE        
 
Hay muchas variantes del rompecabezas de escalera de palabras. Por ejemplo, podrían darle a usted un número determinado de pasos en los que se debe realizar la transformación, o podría tener que utilizar una palabra en particular. En esta sección nos interesa averiguar el menor número de transformaciones necesarias para convertir la palabra inicial en la palabra final.

.. There are many variations of the word ladder puzzle. For example you might be given a particular number of steps in which to accomplish the transformation, or you might need to use a particular word. In this section we are interested in figuring out the smallest number of transformations needed to turn the starting word into the ending word.

No es de extrañar, ya que este capítulo trata sobre grafos, que podamos resolver este problema usando un algoritmo de grafos. El siguiente es un esquema de hacia dónde vamos:

.. Not surprisingly, since this chapter is on graphs, we can solve this problem using a graph algorithm. Here is an outline of where we are going:

-  Representar las relaciones entre las palabras como un grafo.

-  Usar el algoritmo de grafos conocido como búsqueda en anchura para encontrar una ruta eficiente desde la palabra inicial hasta la palabra final.
