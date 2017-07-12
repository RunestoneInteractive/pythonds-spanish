..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Ejercicios de programación
--------------------------

#. Amplíe la función ``construirArbolAnalisis`` para que pueda manejar expresiones matemáticas que no tienen espacios entre cada carácter.

#. Modifique las funciones ``construirArbolAnalisis`` y ``evaluar`` para que puedan manejar las sentencias booleanas (and, or, y not). Recuerde que “not” es un operador unitario, por lo que esto complicará un poco su código.

#. Utilizando el método ``encontrarSucesor``, escriba un recorrido inorden no recursivo para un árbol binario de búsqueda.

#. Modifique el código de un árbol binario de búsqueda para que sea hilado. Escriba un método de recorrido inorden no recursivo para el árbol binario de búsqueda hilado. Un árbol binario hilado mantiene una referencia de cada nodo a su sucesor.

#. Modifique nuestra implementación de árbol binario de búsqueda para que maneje correctamente claves duplicadas. Es decir, si una clave ya está en el árbol, entonces la nueva carga útil debería sustituir a la antigua en lugar de agregar otro nodo con la misma clave.

#. Cree un montículo binario con un tamaño de montículo limitado. En otras palabras, el montículo sólo realizará un seguimiento de los ``n`` ítems más importantes. Si el montículo crece en tamaño a más de ``n`` ítems, se eliminará el ítem menos importante.

#. Modifique la función ``imprimirExpresion`` para que no incluya un par de paréntesis ‘extra’ alrededor de cada número.

#. Utilizando el método ``constructionMonticulo``, escriba una función de ordenamiento que pueda ordenar una lista en tiempo :math:`O(n\log{n})`.

#. Escriba una función que tome un árbol de análisis para una expresión matemática y calcule la derivada de la expresión con respecto a alguna variable.

#. Implemente un montículo binario como un montículo máx.

#. Utilizando la clase ``MonticuloBinario``, implemente una nueva clase llamada ``ColaPrioridad``. Su clase ``ColaPrioridad`` debe implementar el constructor, además de los métodos ``agregar`` y ``avanzar``.
