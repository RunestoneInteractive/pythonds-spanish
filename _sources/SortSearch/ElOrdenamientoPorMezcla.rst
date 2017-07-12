..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


El ordenamiento por mezcla
~~~~~~~~~~~~~~~~~~~~~~~~~~

Ahora dirigimos nuestra atención a usar una estrategia de dividir y conquistar como una forma de mejorar el desempeño de los algoritmos de ordenamiento. El primer algoritmo que estudiaremos es el **ordenamiento por mezcla**. El ordenamiento por mezcla es un algoritmo recursivo que divide continuamente una lista por la mitad. Si la lista está vacía o tiene un solo ítem, se ordena por definición (el caso base). Si la lista tiene más de un ítem, dividimos la lista e invocamos recursivamente un ordenamiento por mezcla para ambas mitades. Una vez que las dos mitades están ordenadas, se realiza la operación fundamental, denominada **mezcla**. La mezcla es el proceso de tomar dos listas ordenadas más pequeñas y combinarlas en una sola lista nueva y ordenada. La :ref:`Figura 10 <fig_mergesortA>` muestra nuestra lista de ejemplo familiar a medida que está siendo dividida por ``ordenamientoPorMezcla``. La :ref:`Figura 11 <fig_mergesortB>` muestra las listas simples, ahora ordenadas, a medida que se fusionan de nuevo.

.. We now turn our attention to using a divide and conquer strategy as a way to improve the performance of sorting algorithms. The first algorithm we will study is the **merge sort**. Merge sort is a recursive algorithm that continually splits a list in half. If the list is empty or has one item, it is sorted by definition (the base case). If the list has more than one item, we split the list and recursively invoke a merge sort on both halves. Once the two halves are sorted, the fundamental operation, called a **merge**, is performed. Merging is the process of taking two smaller sorted lists and combining them together into a single, sorted, new list. :ref:`Figure 10 <fig_mergesortA>` shows our familiar example list as it is being split by ``ordenamientoPorMezcla``. :ref:`Figure 11 <fig_mergesortB>` shows the simple lists, now sorted, as they are merged back together.


.. _fig_mergesortA:

.. figure:: Figures/mergesortA.png
   :align: center

   Figura 10: División de la lista en un ordenamiento por mezcla

   Figura 10: División de la lista en un ordenamiento por mezcla


.. _fig_mergesortB:

.. figure:: Figures/mergesortB.png
   :align: center

   Figura 11: Listas a medida que se fusionan de nuevo

   Figura 11: Listas a medida que se fusionan de nuevo

La función ``ordenamientoPorMezcla`` mostrada en el :ref:`ActiveCode 1 <lst_mergeSort>` comienza preguntando por el caso base. Si la longitud de la lista es menor o igual a uno, entonces ya tenemos una lista ordenada y no es necesario más procesamiento. Si, por otro lado, la longitud es mayor que uno, entonces usamos la operación ``slice`` de Python para extraer las mitades izquierda y derecha. Es importante tener en cuenta que la lista podría no tener un número par de ítems. Eso no importa, ya que las longitudes serán diferentes a lo sumo en uno.

.. The ``ordenamientoPorMezcla`` function shown in :ref:`ActiveCode 1 <lst_mergeSort>` begins by asking the base case question. If the length of the list is less than or equal to one, then we already have a sorted list and no more processing is necessary. If, on the other hand, the length is greater than one, then we use the Python ``slice`` operation to extract the left and right halves. It is important to note that the list may not have an even number of items. That does not matter, as the lengths will differ by at most one.

.. _lst_merge:

.. activecode:: lst_mergeSort
    :caption: Ordenamiendo por mezcla

    def ordenamientoPorMezcla(unaLista):
        print("Dividir ",unaLista)
        if len(unaLista)>1:
            mitad = len(unaLista)//2
            mitadIzquierda = unaLista[:mitad]
            mitadDerecha = unaLista[mitad:]

            ordenamientoPorMezcla(mitadIzquierda)
            ordenamientoPorMezcla(mitadDerecha)

            i=0
            j=0
            k=0
            while i < len(mitadIzquierda) and j < len(mitadDerecha):
                if mitadIzquierda[i] < mitadDerecha[j]:
                    unaLista[k]=mitadIzquierda[i]
                    i=i+1
                else:
                    unaLista[k]=mitadDerecha[j]
                    j=j+1
                k=k+1

            while i < len(mitadIzquierda):
                unaLista[k]=mitadIzquierda[i]
                i=i+1
                k=k+1

            while j < len(mitadDerecha):
                unaLista[k]=mitadDerecha[j]
                j=j+1
                k=k+1
        print("Mezclar ",unaLista)
        
    unaLista = [54,26,93,17,77,31,44,55,20]
    ordenamientoPorMezcla(unaLista)
    print(unaLista)


Una vez que se invoca la función ``ordenamientoPorMezcla`` en la mitad izquierda y la mitad derecha (líneas 8-9), se asume que están ordenadas. El resto de la función (líneas 11-31) es responsable de mezclar las dos listas ordenadas más pequeñas en una lista ordenada más grande. Observe que la operación de mezcla ubica los ítems de nuevo en la lista original (``unaLista``) uno a la vez tomando repetidamente el ítem menor de las listas ordenadas.

.. Once the ``ordenamientoPorMezcla`` function is invoked on the left half and the right half (lines 8–9), it is assumed they are sorted. The rest of the function (lines 11–31) is responsible for merging the two smaller sorted lists into a larger sorted list. Notice that the merge operation places the items back into the original list (``unaLista``) one at a time by repeatedly taking the smallest item from the sorted lists.

La función ``ordenamientoPorMezcla`` se ha aumentado con una instrucción ``print`` (línea 2) para mostrar el contenido de la lista que se está ordenando al inicio de cada invocación. También hay una instrucción ``print`` (línea 32) para mostrar el proceso de mezcla. La impresión muestra el resultado de la ejecución de la función con nuestra lista de ejemplo. Note que la lista con los ítems 44, 55 y 20 no se dividirá en partes iguales. La primera división da [44] y la segunda da [55,20]. Es fácil ver cómo el proceso de división eventualmente produce una lista que se puede mezclar inmediatamente con otras listas ordenadas.

.. The ``ordenamientoPorMezcla`` function has been augmented with a ``print`` statement (line 2) to show the contents of the list being sorted at the start of each invocation. There is also a ``print`` statement (line 32) to show the merging process. The transcript shows the result of executing the function on our example list. Note that the list with 44, 55, and 20 will not divide evenly. The first split gives [44] and the second gives [55,20]. It is easy to see how the splitting process eventually yields a list that can be immediately merged with other sorted lists.


.. animation:: merge_anim
   :modelfile: sortmodels.js
   :viewerfile: sortviewers.js
   :model: MergeSortModel
   :viewer: BarViewer
  
  
.. Para mayores detalles, el CodeLens 6 le permite a usted ejecutar el algoritmo paso a paso.
..
..
.. .. codelens:: mergetrace
..     :caption: Seguimiento del ordenamiento por mezcla
..
..     def ordenamientoPorMezcla(unaLista):
..         print("Dividir ",unaLista)
..         if len(unaLista)>1:
..             mitad = len(unaLista)//2
..             mitadIzquierda = unaLista[:mitad]
..             mitadDerecha = unaLista[mitad:]
..
..             ordenamientoPorMezcla(mitadIzquierda)
..             ordenamientoPorMezcla(mitadDerecha)
..
..             i=0
..             j=0
..             k=0
..             while i<len(mitadIzquierda) and j<len(mitadDerecha):
..                 if mitadIzquierda[i]<mitadDerecha[j]:
..                     unaLista[k]=mitadIzquierda[i]
..                     i=i+1
..                 else:
..                     unaLista[k]=mitadDerecha[j]
..                     j=j+1
..                 k=k+1
..
..             while i<len(mitadIzquierda):
..                 unaLista[k]=mitadIzquierda[i]
..                 i=i+1
..                 k=k+1
..
..             while j<len(mitadDerecha):
..                 unaLista[k]=mitadDerecha[j]
..                 j=j+1
..                 k=k+1
..         print("Mezclar ",unaLista)
..
..     unaLista = [54,26,93,17,77,31,44,55,20]
..     ordenamientoPorMezcla(unaLista)
..     print(unaLista)


Para analizar la función ``ordenamientoPorMezcla``, debemos considerar los dos procesos distintos que conforman su implementación. En primer lugar, la lista se divide en mitades. Ya calculamos (en una búsqueda binaria) que podemos dividir una lista por la mitad en un tiempo :math:`\log n` donde *n* es la longitud de la lista. El segundo proceso es la mezcla. Cada ítem de la lista se procesará y se colocará en la lista ordenada. Así que la operación de mezcla que da lugar a una lista de tamaño *n* requiere *n* operaciones. El resultado de este análisis es que se hacen :math:`\log n` divisiones, cada una de las cuales cuesta :math:`n` para un total de :math:`n\log n` operaciones. Un ordenamiento por mezcla es un algoritmo :math:`O(n\log n)`.

.. In order to analyze the ``ordenamientoPorMezcla`` function, we need to consider the two distinct processes that make up its implementation. First, the list is split into halves. We already computed (in a binary search) that we can divide a list in half :math:`\log n` times where *n* is the length of the list. The second process is the merge. Each item in the list will eventually be processed and placed on the sorted list. So the merge operation which results in a list of size *n* requires *n* operations. The result of this analysis is that :math:`\log n` splits, each of which costs :math:`n` for a total of :math:`n\log n` operations. A merge sort is an :math:`O(n\log n)` algorithm.

Recuerde que el operador de partición es :math:`O(k)` donde *k* es el tamaño de la partición. Para garantizar que ``ordenamientoPorMezcla`` sea :math:`O(n\log n)` tendremos que quitar el operador de partición. Una vez más, esto es posible si simplemente pasamos los índices inicial y final junto con la lista cuando hacemos la llamada recursiva. Dejamos esto como ejercicio.

.. Recall that the slicing operator is :math:`O(k)` where *k* is the size of the slice. In order to guarantee that ``ordenamientoPorMezcla`` will be :math:`O(n\log n)` we will need to remove the slice operator. Again, this is possible if we simply pass the starting and ending indices along with the list when we make the recursive call. We leave this as an exercise.

Es importante notar que la función ``ordenamientoPorMezcla`` requiere espacio adicional para almacenar las dos mitades a medida que se extraen con las operaciones de partición. Este espacio adicional puede ser un factor crítico si la lista es grande y puede tornar problemático a este ordenamiento cuando se trabaja sobre grandes conjuntos de datos.

.. It is important to notice that the ``ordenamientoPorMezcla`` function requires extra space to hold the two halves as they are extracted with the slicing operations. This additional space can be a critical factor if the list is large and can make this sort problematic when working on large data sets.


.. admonition:: Autoevaluación

   .. mchoice:: question_sort_5
      :correct: b
      :answer_a: [16, 49, 39, 27, 43, 34, 46, 40]
      :answer_b: [21,1]
      :answer_c: [21, 1, 26, 45]
      :answer_d: [21]
      :feedback_a: Ésta es la segunda mitad de la lista.
      :feedback_b: Sí, ordenamientoPorMezcla continuará moviéndose recursivamente hacia el inicio de la lista hasta que se tope con el caso base.
      :feedback_c: Recuerde que ordenamientoPorMezcla no opera sobre la mitad derecha de la lista sino hasta que la mitad derecha esté completamente ordenada.
      :feedback_d: Ésta es la lista después de 4 llamadas recursivas

      Dada la siguiente lista de números: [21, 1, 26, 45, 29, 28, 2, 9, 16, 49, 39, 27, 43, 34, 46, 40] ¿Cuál de las siguientes respuestas corresponde a la lista que será ordenada después de 3 llamadas recursivas a ordenamientoPorMezcla?

   .. mchoice:: question_sort_6
      :correct: c
      :answer_a: [21, 1] y [26, 45]
      :answer_b: [[1, 2, 9, 21, 26, 28, 29, 45] y [16, 27, 34, 39, 40, 43, 46, 49]
      :answer_c: [21] y [1]
      :answer_d: [9] y [16]
      :feedback_a: Las primeras dos listas mezcladas serán listas de caso base, aún no hemos alcanzado un caso base.
      :feedback_b: Éstas serán las dos últimas listas mezcladas
      :feedback_c: Las listas [21] y [1] son los dos primeros casos base encontrados por ordenamientoPorMezcla y, por tanto, serán las dos primeras listas mezcladas.
      :feedback_d: Aunque 9 y 16 son valores vecinos, están en mitades diferentes de la lista desde la primera partición.

      Dada la siguiente lista de números: [21, 1, 26, 45, 29, 28, 2, 9, 16, 49, 39, 27, 43, 34, 46, 40] ¿Cuál de las siguientes respuestas corresponde a las primeras dos listadas que serán mezcladas?
