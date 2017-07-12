..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Desempeño de un árbol AVL
~~~~~~~~~~~~~~~~~~~~~~~~~

Antes de continuar, analicemos el resultado de aplicar este nuevo requisito de factor de equilibrio. Nuestra afirmación es que al garantizar que un árbol tenga siempre un factor de equilibrio de -1, 0 ó 1, podremos obtener un mejor desempeño de las operaciones clave. Comencemos por pensar en cómo esta condición de equilibrio cambia al árbol del peor de los casos. Hay dos posibilidades a considerar, un árbol pesado a la izquierda y un árbol pesado a la derecha. Si consideramos árboles de alturas 0, 1, 2 y 3, la :ref:`Figura 2 <fig_worstAVL>` ilustra el árbol más desequilibrado y pesado a la izquierda posible bajo las nuevas reglas.

.. Before we proceed any further let's look at the result of enforcing this new balance factor requirement. Our claim is that by ensuring that a tree always has a balance factor of -1, 0, or 1 we can get better Big-O performance of key operations. Let us start by thinking about how this balance condition changes the worst-case tree. There are two possibilities to consider, a left-heavy tree and a right heavy tree. If we consider trees of heights 0, 1, 2, and 3, :ref:`Figure 2 <fig_worstAVL>` illustrates the most unbalanced left-heavy tree possible under the new rules.

.. _fig_worstAVL:

.. figure:: Figures/worstAVL.png
   :align: center

   Figura 2: Árboles AVL pesados a la izquierda del peor caso

   Figura 2: Árboles AVL pesados a la izquierda del peor caso
   
Observando el número total de nodos en el árbol vemos que para un árbol de altura 0 hay 1 nodo, para un árbol de altura 1 hay :math:`1 + 1 = 2` nodos, para un árbol de altura 2 hay :math:`1 + 1 + 2 = 4` y para un árbol de altura 3 hay :math:`1 + 2 + 4 = 7` nodos. Más en general, el patrón que vemos para el número de nodos en un árbol de altura h (:math:`N_h`) es:

.. Looking at the total number of nodes in the tree we see that for a tree of height 0 there is 1 node, for a tree of height 1 there is :math:`1+1 = 2` nodes, for a tree of height 2 there are :math:`1+1+2 = 4` and for a tree of height 3 there are :math:`1 + 2 + 4 = 7`. More generally the pattern we see for the number of nodes in a tree of height h (:math:`N_h`) is:

.. math::

   N_h = 1 + N_{h-1} + N_{h-2}  

Esta recurrencia quizás le parezca familiar porque es muy similar a la secuencia de Fibonacci. Podemos utilizar este hecho para derivar una fórmula para la altura de un árbol AVL dado el número de nodos en el árbol. Recordemos que, para la secuencia de Fibonacci, el :math:`i_{ésimo}` número de Fibonacci está dado por:

.. This recurrence may look familiar to you because it is very similar to the Fibonacci sequence. We can use this fact to derive a formula for the height of an AVL tree given the number of nodes in the tree. Recall that for the Fibonacci sequence the :math:`i_{th}` Fibonacci number is given by:

.. math::

   F_0 = 0 \\
   F_1 = 1 \\
   F_i = F_{i-1} + F_{i-2}  \text{ para todo } i \ge 2


Un resultado matemático importante es que a medida que los números de la secuencia de Fibonacci se hacen más y más grandes, la relación de :math:`F_i / F_{i-1}` se aproxima cada vez más a la proporción áurea :math:`\Phi` que se define como :math:`\Phi = \frac{1 + \sqrt {5}}{2}`. Usted puede consultar un texto de matemáticas si desea examinar una derivación de la ecuación anterior. Simplemente utilizaremos esta ecuación para aproximar :math:`F_i` como :math:`F_i = \Phi^i /\sqrt{5}`. Si hacemos uso de esta aproximación podemos reescribir la ecuación para :math:`N_h` como:

.. An important mathematical result is that as the numbers of the Fibonacci sequence get larger and larger the ratio of :math:`F_i / F_{i-1}` becomes closer and closer to approximating the golden ratio :math:`\Phi` which is defined as :math:`\Phi = \frac{1 + \sqrt{5}}{2}`. You can consult a math text if you want to see a derivation of the previous equation. We will simply use this equation to approximate :math:`F_i` as :math:`F_i = \Phi^i/\sqrt{5}`. If we make use of this approximation we can rewrite the equation for :math:`N_h` as:

.. math::

   N_h = F_{h+2} - 1, h \ge 1


Al reemplazar la referencia de Fibonacci por su aproximación de la proporción áurea obtenemos:

.. By replacing the Fibonacci reference with its golden ratio approximation we get: 

.. math::

   N_h = \frac{\Phi^{h+2}}{\sqrt{5}} - 1


Si reordenamos los términos y tomamos el logaritmo en base 2 de ambos lados y luego despejamos :math:`h` obtenemos la siguiente derivación:

.. If we rearrange the terms, and take the base 2 log of both sides and then solve for :math:`h` we get the following derivation:

.. math::

   \log{N_h+1} = (H+2)\log{\Phi} - \frac{1}{2} \log{5} \\
   h = \frac{\log{N_h+1} - 2 \log{\Phi} + \frac{1}{2} \log{5}}{\log{\Phi}} \\
   h = 1.44 \log{N_h}

Esta derivación nos muestra que en cualquier momento la altura de nuestro árbol AVL es igual a una constante (1.44) veces el logaritmo del número de nodos en el árbol. Ésta es una gran noticia para buscar en nuestro árbol AVL porque limita la búsqueda a :math:`O(\log{N})`.

.. This derivation shows us that at any time the height of our AVL tree is equal to a constant(1.44) times the log of the number of nodes in the tree. This is great news for searching our AVL tree because it limits the search to :math:`O(\log{N})`.
