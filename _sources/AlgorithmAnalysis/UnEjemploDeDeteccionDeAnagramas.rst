..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Un ejemplo de detección de anagramas
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Un buen problema de ejemplo para mostrar algoritmos con diferentes órdenes de magnitud es el clásico problema de detección de anagramas para cadenas de caracteres. Una cadena es un anagrama de otra si la segunda es simplemente un reordenamiento de la primera. Por ejemplo, ``'fresa'`` y ``'frase'`` son anagramas. Las cadenas ``'caro'`` y ``'roca'`` son también anagramas. Por razones de simplicidad, asumiremos que las dos cadenas en cuestión son de la misma longitud y que están formadas por símbolos del conjunto de 26 caracteres alfabéticos en minúsculas. Nuestro objetivo es escribir una función booleana que tomará dos cadenas y devolverá una confirmación de si son o no anagramas.

.. A good example problem for showing algorithms with different orders of magnitude is the classic anagram detection problem for strings. One string is an anagram of another if the second is simply a rearrangement of the first. For example, ``'heart'`` and ``'earth'`` are anagrams. The strings ``'python'`` and ``'typhon'`` are anagrams as well. For the sake of simplicity, we will assume that the two strings in question are of equal length and that they are made up of symbols from the set of 26 lowercase alphabetic characters. Our goal is to write a boolean function that will take two strings and return whether they are anagrams.

Solución 1: Marcado de verificación
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Nuestra primera solución al problema de los anagramas verificará que cada carácter de la primera cadena realmente aparezca en la segunda. Si es posible “marcar” todos los caracteres, entonces las dos cadenas deben ser anagramas. El marcado de verificación de un carácter se realizará reemplazándolo con el valor especial de Python ``None``. No obstante, como las cadenas en Python son inmutables, el primer paso en el proceso será convertir la segunda cadena en una lista. Cada carácter de la primera cadena se puede verificar contra los caracteres de la lista y, si se encuentra, se marca mediante el reemplazo. El :ref:`ActiveCode 1 <lst_anagramSolution>` muestra esta función.

.. Our first solution to the anagram problem will check to see that each character in the first string actually occurs in the second. If it is possible to “checkoff” each character, then the two strings must be anagrams. Checking off a character will be accomplished by replacing it with the special Python value ``None``. However, since strings in Python are immutable, the first step in the process will be to convert the second string to a list. Each character from the first string can be checked against the characters in the list and if found, checked off by replacement. :ref:`ActiveCode 1 <lst_anagramSolution>` shows this function.

.. _lst_anagramSolution:

.. activecode:: active5
    :caption: Marcado de verificación

    def anagramaSolucion1(cadena1,cadena2):
        unaLista = list(cadena2)

        pos1 = 0
        aunOK = True

        while pos1 < len(cadena1) and aunOK:
            pos2 = 0
            encontrado = False
            while pos2 < len(unaLista) and not encontrado:
                if cadena1[pos1] == unaLista[pos2]:
                    encontrado = True
                else:
                    pos2 = pos2 + 1

            if encontrado:
                unaLista[pos2] = None
            else:
                aunOK = False

            pos1 = pos1 + 1

        return aunOK

    print(anagramaSolucion1('abcd','dcba'))

Para analizar este algoritmo, debemos tener en cuenta que por cada uno de los *n* caracteres en ``cadena1`` se causará una iteración a lo largo de hasta *n* caracteres en la lista de ``cadena2``. Cada una de las *n* posiciones de la lista se visitará una vez para compararla con un carácter de ``cadena1``. El número de visitas se convierte entonces en la suma de los enteros de 1 a *n*. Dijimos anteriormente que esto puede escribirse como

.. To analyze this algorithm, we need to note that each of the *n* characters in ``cadena1`` will cause an iteration through up to *n* characters in the list from ``cadena2``. Each of the *n* positions in the list will be visited once to match a character from ``cadena1``. The number of visits then becomes the sum of the integers from 1 to *n*. We stated earlier that this can be written as

.. math::

   \sum_{i=1}^{n} i &= \frac {n(n+1)}{2} \\
                    &= \frac {1}{2}n^{2} + \frac {1}{2}n

A medida que :math:`n` se hace más grande, el término :math:`n^{2}` dominará el término :math:`n` y el :math:`\frac {1} {2}` puede ignorarse. Por lo tanto, esta solución es :math:`O(n^{2})`.

.. As :math:`n` gets large, the :math:`n^{2}` term will dominate the :math:`n` term and the :math:`\frac {1}{2}` can be ignored. Therefore, this solution is :math:`O(n^{2})`.

Solución 2: Ordenar y comparar
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Otra solución al problema de los anagramas hará uso del hecho de que aunque ``cadena1`` y ``cadena2`` son diferentes, serán anagramas solamente si consisten exactamente de los mismos caracteres. Por lo tanto, si empezamos por clasificar cada cadena alfabéticamente, de la a a la z, terminaremos con la misma cadena si las dos originales son anagramas. El :ref:`ActiveCode 2 <lst_ana2>` muestra esta solución. De nuevo, en Python podemos aplicar el método incorporado ``sort`` sobre listas simplemente convirtiendo al principio cada cadena en una lista.

.. Another solution to the anagram problem will make use of the fact that even though ``cadena1`` and ``cadena2`` are different, they are anagrams only if they consist of exactly the same characters. So, if we begin by sorting each string alphabetically, from a to z, we will end up with the same string if the original two strings are anagrams. :ref:`ActiveCode 2 <lst_ana2>` shows this solution. Again, in Python we can use the built-in ``sort`` method on lists by simply converting each string to a list at the start.

.. _lst_ana2:

.. activecode:: active6
    :caption: Ordenar y comparar

    def anagramaSolucion2(cadena1,cadena2):
        unaLista1 = list(cadena1)
        unaLista2 = list(cadena2)

        unaLista1.sort()
        unaLista2.sort()

        pos = 0
        coincide = True

        while pos < len(cadena1) and coincide:
            if unaLista1[pos]==unaLista2[pos]:
                pos = pos + 1
            else:
                coincide = False

        return coincide

    print(anagramaSolucion2('abcde','edcba'))

A primera vista usted podría pensar que este algoritmo es :math:`O(n)`, ya que hay una sola iteración para comparar los *n* caracteres después del proceso de ordenamiento. Sin embargo, las dos llamadas al método ``sort`` de Python no carecen de su propio costo. Como veremos en un capítulo posterior, ordenar es típicamente :math:`O(n^{2})` u :math:`O(n\log n)`, por lo que las operaciones de ordenamiento dominan la iteración. Al fin y al cabo, este algoritmo tendrá el mismo orden de magnitud que aquél del proceso de ordenamiento.

.. At first glance you may be tempted to think that this algorithm is :math:`O(n)`, since there is one simple iteration to compare the *n* characters after the sorting process. However, the two calls to the Python ``sort`` method are not without their own cost. As we will see in a later chapter, sorting is typically either :math:`O(n^{2})` or :math:`O(n\log n)`, so the sorting operations dominate the iteration. In the end, this algorithm will have the same order of magnitude as that of the sorting process.

Solución 3: Fuerza bruta
^^^^^^^^^^^^^^^^^^^^^^^^

Una técnica de **fuerza bruta** para resolver un problema normalmente intenta agotar todas las posibilidades. Para el problema de detección de anagramas, podemos simplemente generar una lista de todas las cadenas posibles usando los caracteres de ``cadena1`` y luego ver si se produce ``cadena2``. Sin embargo, hay una dificultad con este enfoque. Cuando se generan todas las cadenas posibles de ``cadena1``, hay *n* posibles primeros caracteres, :math:`n-1` posibles caracteres para la segunda posición, :math:`n-2` para la tercera, y así sucesivamente. El número total de cadenas candidatas es :math:`n*(n-1)*(n-2)*...*3*2*1`, lo cual es :math:`n!`. Aunque algunas de las cadenas pueden ser versiones duplicadas, el programa no puede saber esto de antemano y por tanto generá de todos modos :math:`n!` cadenas diferentes.

.. A **brute force** technique for solving a problem typically tries to exhaust all possibilities. For the anagram detection problem, we can simply generate a list of all possible strings using the characters from ``cadena1`` and then see if ``cadena2`` occurs. However, there is a difficulty with this approach. When generating all possible strings from ``cadena1``, there are *n* possible first characters, :math:`n-1` possible characters for the second position, :math:`n-2` for the third, and so on. The total number of candidate strings is :math:`n*(n-1)*(n-2)*...*3*2*1`, which is :math:`n!`. Although some of the strings may be duplicates, the program cannot know this ahead of time and so it will still generate :math:`n!` different strings.

Resulta que :math:`n!` crece aún más rápido que :math:`2^{n}` a medida que *n* se hace grande. De hecho, si ``cadena1`` tuviera una longitud de 20 caracteres, habría :math:`20!=2,432,902,008,176,640,000` cadenas candidatas posibles. Si procesáramos una posibilidad cada segundo, aún así nos tomaría 77,146,816,596 años el recorrido de la lista completa. Esto probablemente no va a ser una buena solución.

.. It turns out that :math:`n!` grows even faster than :math:`2^{n}` as *n* gets large. In fact, if ``cadena1`` were 20 characters long, there would be :math:`20!=2,432,902,008,176,640,000` possible candidate strings. If we processed one possibility every second, it would still take us 77,146,816,596 years to go through the entire list. This is probably not going to be a good solution.

Solución 4: Contar y comparar
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Nuestra última solución al problema de los anagramas se aprovecha del hecho de que cualesquiera dos anagramas tendrán el mismo número de letras a, el mismo número de letras b, el mismo número de letras c, y así sucesivamente. Para decidir si dos cadenas son anagramas, primero vamos a contar el número de veces que se produce cada caracter. Puesto que hay 26 caracteres posibles, podemos usar una lista de 26 contadores, uno para cada caracter posible. Cada vez que veamos un caracter en particular, vamos a incrementar el contador en esa posición. Al terminar, si las dos listas de contadores son idénticas, las cadenas deben ser anagramas. El :ref:`ActiveCode 3 <lst_ana4>` muestra esta solución.

.. Our final solution to the anagram problem takes advantage of the fact that any two anagrams will have the same number of a’s, the same number of b’s, the same number of c’s, and so on. In order to decide whether two strings are anagrams, we will first count the number of times each character occurs. Since there are 26 possible characters, we can use a list of 26 counters, one for each possible character. Each time we see a particular character, we will increment the counter at that position. In the end, if the two lists of counters are identical, the strings must be anagrams. :ref:`ActiveCode 3 <lst_ana4>` shows this solution.

.. _lst_ana4:

.. activecode:: active7
    :caption: Contar y comparar

    def anagramaSolucion4(cadena1,cadena2):
        c1 = [0]*26
        c2 = [0]*26

        for i in range(len(cadena1)):
            pos = ord(cadena1[i])-ord('a')
            c1[pos] = c1[pos] + 1

        for i in range(len(cadena2)):
            pos = ord(cadena2[i])-ord('a')
            c2[pos] = c2[pos] + 1

        j = 0
        aunOK = True
        while j<26 and aunOK:
            if c1[j]==c2[j]:
                j = j + 1
            else:
                aunOK = False

        return aunOK

    print(anagramaSolucion4('cero','ocre'))


Nuevamente, la solución tiene varias iteraciones. Sin embargo, a diferencia de la primera solución, ninguna de ellas está anidada. Las dos primeras iteraciones utilizadas para contar los caracteres están ambas basadas en *n*. La tercera iteración, que compara las dos listas de conteos, siempre toma 26 pasos ya que hay 26 caracteres posibles en las cadenas. La suma de todo nos da :math:`T(n)=2n+26` pasos. Es decir :math:`O(n)`. Hemos encontrado un  algoritmo de orden de magnitud lineal para resolver este problema.

.. Again, the solution has a number of iterations. However, unlike the first solution, none of them are nested. The first two iterations used to count the characters are both based on *n*. The third iteration, comparing the two lists of counts, always takes 26 steps since there are 26 possible characters in the strings. Adding it all up gives us :math:`T(n)=2n+26` steps. That is :math:`O(n)`. We have found a linear order of magnitude algorithm for solving this problem.

Antes de dejar este ejemplo, necesitamos decir algo sobre los requisitos de espacio. Aunque la última solución pudo ejecutarse en tiempo lineal, sólo pudo hacerse mediante el uso de almacenamiento adicional para mantener las dos listas de conteo de caracteres. En otras palabras, este algoritmo sacrificó espacio para ganar tiempo.

.. Before leaving this example, we need to say something about space requirements. Although the last solution was able to run in linear time, it could only do so by using additional storage to keep the two lists of character counts. In other words, this algorithm sacrificed space in order to gain time.

Esto ocurre con frecuencia. En muchas ocasiones usted tendrá que tomar decisiones sobre los sacrificios mutuos entre tiempo y espacio. En este caso, la cantidad de espacio adicional no es significativa. Sin embargo, si el alfabeto subyacente tuviera millones de caracteres, habría más preocupación. Como científico de la computación, cuando deba tomar una decisión entre algoritmos, le corresponde a usted determinar el mejor uso de los recursos computacionales dado un problema particular.

.. This is a common occurrence. On many occasions you will need to make decisions between time and space trade-offs. In this case, the amount of extra space is not significant. However, if the underlying alphabet had millions of characters, there would be more concern. As a computer scientist, when given a choice of algorithms, it will be up to you to determine the best use of computing resources given a particular problem.

.. admonition:: Autoevaluación

   .. mchoice:: analysis_1
       :answer_a: O(n)
       :answer_b: O(n^2)
       :answer_c: O(log n)
       :answer_d: O(n^3)
       :correct: b
       :feedback_a: En un ejemplo como éste, usted desea contar los ciclos anidados. Especialmente los ciclos que dependen de la misma variable, en este caso, n.
       :feedback_b: Un ciclo anidado individualmente como éste es O(n^2)
       :feedback_c: log n normalmente se indica cuando el problema se hace iterativamente más pequeño
       :feedback_d: En un ejemplo como éste, usted desea contar los ciclos anidados. Especialmente los ciclos que dependen de la misma variable, en este caso, n.

       Dado el siguiente fragmento de código, ¿cuál es su O-grande de tiempo de ejecución?

       .. code-block:: python

         prueba = 0
         for i in range(n):
            for j in range(n):
               prueba = prueba + i * j

   .. mchoice:: analysis_2
       :answer_a: O(n)
       :answer_b: O(n^2)
       :answer_c: O(log n)
       :answer_d: O(n^3)
       :correct: a
       :feedback_b: Tenga cuidado, al contar los ciclos usted debe asegurarse de que los ciclos están anidados.
       :feedback_d: Tenga cuidado, al contar los ciclos usted debe asegurarse de que los ciclos están anidados.
       :feedback_c: log n normalmente se indica cuando el problema se hace iterativamente más pequeño
       :feedback_a: Aunque hay dos ciclos, ellos no están anidados. Usted podría pensar en esto como O(2n) pero podemos ignorar la constante 2.

       Dado el siguiente fragmento de código, ¿cuál es su O-grande de tiempo de ejecución?

       .. code-block:: python

         prueba = 0
         for i in range(n):
            prueba = prueba + 1

         for j in range(n):
            prueba = prueba - 1

   .. mchoice:: analysis_3
       :answer_a: O(n)
       :answer_b: O(n^2)
       :answer_c: O(log n)
       :answer_d: O(n^3)
       :correct: c
       :feedback_a: Observe cuidadosamente la variable de ciclo i. Note que el valor de i se reduce a la mitad cada vez a través del ciclo. Éste es un gran indicio de que el rendimiento es mejor que O(n)
       :feedback_b: Verifique de nuevo, ¿es éste un ciclo anidado?
       :feedback_d: Verifique de nuevo, ¿es éste un ciclo anidado?       
       :feedback_c: El valor de i es reducido a la mitad cada vez a través del ciclo por lo que sólo habrá log n iteraciones.

       Dado el siguiente fragmento de código, ¿cuál es su O-grande de tiempo de ejecución?

       .. code-block:: python

         i = n
         while i > 0:
            k = 2 + 2
            i = i // 2
