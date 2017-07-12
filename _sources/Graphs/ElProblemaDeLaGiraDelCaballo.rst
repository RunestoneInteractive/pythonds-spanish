..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


El problema de la gira del caballo
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Otro problema clásico que podemos usar para ilustrar un segundo algoritmo de grafos común es el llamado “gira del caballo”. El rompecabezas de la gira del caballo se juega en un tablero de ajedrez con una sola pieza de ajedrez, el caballo. El objetivo del rompecabezas es encontrar una secuencia de movimientos que permitan al caballo visitar cada cuadrado del tablero exactamente una vez. Una de esas secuencias se llama “gira”. El rompecabezas de la gira del caballo ha fascinado a los jugadores de ajedrez, matemáticos y científicos por igual durante muchos años. Se sabe que la cota superior del número de giras legales posibles para un tablero de ajedrez de ocho por ocho es :math:`1.305 \times 10^{35}`; sin embargo, hay incluso un número mayor de posibles callejones sin salida. Claramente éste es un problema que requiere algo de buen seso, algo de verdadera potencia computacional, o ambos.

.. Another classic problem that we can use to illustrate a second common graph algorithm is called the “knight’s tour.” The knight’s tour puzzle is played on a chess board with a single chess piece, the knight. The object of the puzzle is to find a sequence of moves that allow the knight to visit every square on the board exactly once. One such sequence is called a “tour.” The knight’s tour puzzle has fascinated chess players, mathematicians and computer scientists alike for many years. The upper bound on the number of possible legal tours for an eight-by-eight chessboard is known to be :math:`1.305 \times 10^{35}`; however, there are even more possible dead ends. Clearly this is a problem that requires some real brains, some real computing power, or both.

Aunque los investigadores han estudiado muchos algoritmos diferentes para resolver el problema de la gira del caballo, una búsqueda de grafos es uno de los más fáciles de entender y programar. Una vez más vamos a resolver el problema utilizando dos pasos principales:

.. Although researchers have studied many different algorithms to solve the knight’s tour problem, a graph search is one of the easiest to understand and program. Once again we will solve the problem using two main steps:

-  Representar como un grafo los movimientos legales de un caballo en un tablero de ajedrez.

-  Usar un algoritmo de grafos para encontrar una ruta de longitud :math:`filas \times columnas - 1` donde cada vértice del grafo se visite exactamente una vez.
