..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


El ordenamiento por selección
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

El **ordenamiento por selección** mejora el ordenamiento burbuja haciendo un sólo intercambio por cada pasada a través de la lista. Para hacer esto, un ordenamiento por selección busca el valor mayor a medida que hace una pasada y, después de completar la pasada, lo pone en la ubicación correcta. Al igual que con un ordenamiento burbuja, después de la primera pasada, el ítem mayor está en la ubicación correcta. Después de la segunda pasada, el siguiente mayor está en su ubicación. Este proceso continúa y requiere :math:`n-1` pasadas para ordenar los *n* ítems, ya que el ítem final debe estar en su lugar después de la :math:`(n-1)`-ésima pasada.

.. The **selection sort** improves on the bubble sort by making only one exchange for every pass through the list. In order to do this, a selection sort looks for the largest value as it makes a pass and, after completing the pass, places it in the proper location. As with a bubble sort, after the first pass, the largest item is in the correct place. After the second pass, the next largest is in place. This process continues and requires :math:`n-1` passes to sort *n* items, since the final item must be in place after the :math:`(n-1)` st pass.

La :ref:`Figura 3 <fig_selectionsort>` muestra todo el proceso de ordenamiento. En cada paso, el ítem mayor restante se selecciona y luego se pone en su ubicación correcta. La primera pasada ubica el 93, la segunda pasada ubica el 77, la tercera ubica el 55, y así sucesivamente. La función se muestra en el :ref:`ActiveCode 1 <lst_selectionsortcode>`.

.. :ref:`Figure 3 <fig_selectionsort>` shows the entire sorting process. On each pass, the largest remaining item is selected and then placed in its proper location. The first pass places 93, the second pass places 77, the third places 55, and so on. The function is shown in :ref:`ActiveCode 1 <lst_selectionsortcode>`.

.. _fig_selectionsort:

.. figure:: Figures/selectionsortnew.png
   :align: center

   
   Figura 3: ``ordenamientoPorSeleccion``

   Figura 3: ``ordenamientoPorSeleccion``



.. activecode:: lst_selectionsortcode
    :caption: Ordenamiento por selección

    def ordenamientoPorSeleccion(unaLista):
       for llenarRanura in range(len(unaLista)-1,0,-1):
           posicionDelMayor=0
           for ubicacion in range(1,llenarRanura+1):
               if unaLista[ubicacion]>unaLista[posicionDelMayor]:
                   posicionDelMayor = ubicacion

           temp = unaLista[llenarRanura]
           unaLista[llenarRanura] = unaLista[posicionDelMayor]
           unaLista[posicionDelMayor] = temp

    unaLista = [54,26,93,17,77,31,44,55,20]
    ordenamientoPorSeleccion(unaLista)
    print(unaLista)

.. animation:: selection_anim
   :modelfile: sortmodels.js
   :viewerfile: sortviewers.js
   :model: SelectionSortModel
   :viewer: BarViewer
   

.. Con el fin de tener una ilustración más detallada, el CodeLens 3 le permite a usted ejecutar el algoritmo paso a paso.
..
..
.. .. codelens:: selectionsortcodetrace
..     :caption: Seguimiento al ordenamiento por selección
..
..     def ordenamientoPorSeleccion(unaLista):
..        for llenarRanura in range(len(unaLista)-1,0,-1):
..            posicionDelMayor=0
..            for ubicacion in range(1,llenarRanura+1):
..                if unaLista[ubicacion]>unaLista[posicionDelMayor]:
..                    posicionDelMayor = ubicacion
..
..            temp = unaLista[llenarRanura]
..            unaLista[llenarRanura] = unaLista[posicionDelMayor]
..            unaLista[posicionDelMayor] = temp
..
..     unaLista = [54,26,93,17,77,31,44,55,20]
..     ordenamientoPorSeleccion(unaLista)
..     print(unaLista)

Usted habrá notado que el ordenamiento por selección hace el mismo número de comparaciones que el ordenamiento burbuja y por lo tanto también es :math:`O(n^{2})`. Sin embargo, debido a la reducción en el número de intercambios, el ordenamiento por selección normalmente se ejecuta más rápidamente en pruebas de referencia. De hecho, para nuestra lista, el ordenamiento burbuja hace 20 intercambios, mientras que el ordenamiento por selección hace sólo 8.

.. You may see that the selection sort makes the same number of comparisons as the bubble sort and is therefore also :math:`O(n^{2})`. However, due to the reduction in the number of exchanges, the selection sort typically executes faster in benchmark studies. In fact, for our list, the bubble sort makes 20 exchanges, while the selection sort makes only 8.


.. admonition:: Autoevaluación

   .. mchoice:: question_sort_2
      :correct: d
      :answer_a: [7, 11, 12, 1, 6, 14, 8, 18, 19, 20]
      :answer_b: [7, 11, 12, 14, 19, 1, 6, 18, 8, 20]
      :answer_c: [11, 7, 12, 14, 1, 6, 8, 18, 19, 20]
      :answer_d: [11, 7, 12, 14, 8, 1, 6, 18, 19, 20]
      :feedback_a: El ordenamiento por selección es similar al ordenamiento burbuja (el cual parece que usted usó) pero usa menos intercambios
      :feedback_b: Este resultado parece de un ordenamiento por inserción.
      :feedback_c: Este resultado se parece a la respuesta correcta pero en lugar de intercambiar los números, estos se han desplazado a la izquierda para dar cabida a los números correctos.
      :feedback_d: El ordenamiento por selección mejora el ordenamiento burbuja ya que hace menos intercambios.

      Suponga que usted tiene que ordenar la siguiente lista de números: [11, 7, 12, 14, 19, 1, 6, 18, 8, 20] ¿Cuál de las siguientes listas representa la lista parcialmente ordenada tras tres pasadas completas del ordenamiento por selección?
