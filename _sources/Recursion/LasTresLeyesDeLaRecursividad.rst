..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Las tres leyes de la recursividad
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Al igual que los robots de Asimov, todos los algoritmos recursivos deben obedecer tres leyes importantes:

.. Like the robots of Asimov, all recursive algorithms must obey three important laws:

#. Un algoritmo recursivo debe tener un **caso base**.

#. Un algoritmo recursivo debe cambiar su estado y moverse hacia el caso base.

#. Un algoritmo recursivo debe llamarse a sí mismo, recursivamente.

Echemos un vistazo a cada una de estas leyes con más detalle y veamos cómo se usó en el algoritmo ``sumalista``. En primer lugar, un caso base es la condición que permite que el algoritmo detenga la recursividad. Un caso base es típicamente un problema que es lo suficientemente pequeño como para resolverlo directamente. En el algoritmo ``sumalista`` el caso base es una lista de longitud 1.

.. Let’s look at each one of these laws in more detail and see how it was used in the ``sumalista`` algorithm. First, a base case is the condition that allows the algorithm to stop recursing. A base case is typically a problem that is small enough to solve directly. In the ``sumalista`` algorithm the base case is a list of length 1.

Para obedecer la segunda ley, debemos organizar un cambio de estado que mueva el algoritmo hacia el caso base. Un cambio de estado significa que se modifican algunos datos que el algoritmo está usando. Por lo general, los datos que representan nuestro problema se hacen más pequeños de alguna manera. En el algoritmo ``sumalista`` nuestra estructura de datos primaria es una lista, así que debemos centrar nuestros esfuerzos de cambio de estado en la lista. Dado que el caso base es una lista de longitud 1, una progresión natural hacia el caso base es acortar la lista. Esto es exactamente lo que ocurre en la línea 5 del :ref:`ActiveCode 2 <lst_recsum>` cuando llamamos a ``sumalista`` con una lista más corta.

.. To obey the second law, we must arrange for a change of state that moves the algorithm toward the base case. A change of state means that some data that the algorithm is using is modified. Usually the data that represents our problem gets smaller in some way. In the ``sumalista`` algorithm our primary data structure is a list, so we must focus our state-changing efforts on the list. Since the base case is a list of length 1, a natural progression toward the base case is to shorten the list. This is exactly what happens on line 5 of :ref:`ActiveCode 2 <lst_recsum>` when we call ``sumalista`` with a shorter list.

La última ley es que el algoritmo debe llamarse a sí mismo. Esta es la definición misma de la recursividad. La recursividad es un concepto confuso para muchos programadores principiantes. Como programador principiante, usted ha aprendido que las funciones son buenas porque usted puede tomar un problema grande y descomponerlo en problemas más pequeños. Los problemas más pequeños pueden resolverse escribiendo una función para resolver cada problema. Cuando hablamos de recursividad, puede parecer que estamos hablando en círculos. Tenemos un problema que resolver con una función, ¡pero esa función resuelve el problema llamándose a sí misma! Pero la lógica no es circular en absoluto; la lógica de la recursividad es una expresión elegante de resolver un problema al descomponerlo en problemas más pequeños y más fáciles.

.. The final law is that the algorithm must call itself. This is the very definition of recursion. Recursion is a confusing concept to many beginning programmers. As a novice programmer, you have learned that functions are good because you can take a large problem and break it up into smaller problems. The smaller problems can be solved by writing a function to solve each problem. When we talk about recursion it may seem that we are talking ourselves in circles. We have a problem to solve with a function, but that function solves the problem by calling itself! But the logic is not circular at all; the logic of recursion is an elegant expression of solving a problem by breaking it down into a smaller and easier problems.

En lo restante de este capítulo veremos más ejemplos de recursividad. En cada caso nos centraremos en diseñar una solución a un problema usando las tres leyes de la recursividad.

.. In the remainder of this chapter we will look at more examples of recursion. In each case we will focus on designing a solution to a problem by using the three laws of recursion.


.. admonition:: Autoevaluación

   .. mchoice:: question_recsimp_1
      :correct: c
      :answer_a: 6
      :answer_b: 5
      :answer_c: 4
      :answer_d: 3
      :feedback_a: Sólo hay cinco números en la lista, el número de llamadas recursivas no será mayor que el tamaño de la lista.
      :feedback_b: La llamada inicial a sumalista no es una llamada recursiva.
      :feedback_c: La primera llamada recursiva pasa la lista [4,6,8,10], la segunda [6,8,10] y así sucesivamente hasta [10].
      :feedback_d: Esta no sería una cantidad suficiente de llamadas para cubrir todos los números de la lista

      ¿Cuántas llamadas recursivas se realizan al calcular la sumatoria de la lista [2,4,6,8,10]?

   .. mchoice:: question_recsimp_2
      :correct: d
      :answer_a: n == 0
      :answer_b: n == 1
      :answer_c: n &gt;= 0
      :answer_d: n &lt;= 1
      :feedback_a:  Aunque esto funcionaría hay opciones mejores y un poco más eficientes. Dado que fact(1) y fact(0) valen lo mismo.
      :feedback_b: Una buena opción, pero ¿qué pasa si usted llama a fact(0)?
      :feedback_c: Este caso base sería verdadero para todos los números mayores que cero, así que el factorial de cualquier número positivo sería 1.
      :feedback_d: Bien, éste es el más eficiente, e incluso previene que su programa colapse si se intenta calcular el factorial de un número negativo.

      Suponga que usted va a escribir una función recusiva para calcular el factorial de un número. fact(n) devuelve n * n-1 * n-2 * ... , donde el factorial de cero está definido como 1. ¿Cuál sería el caso base más apropiado?
