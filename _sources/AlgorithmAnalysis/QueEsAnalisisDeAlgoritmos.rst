..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


¿Qué es análisis de algoritmos?
-------------------------------

Es muy común que los estudiantes principiantes de ciencias de la computación comparen sus programas entre sí. También usted puede haber notado que es común que los programas de computadora se vean muy similares, especialmente los más simples. A menudo surge una pregunta interesante. Cuando dos programas resuelven el mismo problema pero se ven diferentes, ¿es un programa mejor que el otro?

.. It is very common for beginning computer science students to compare their programs with one another. You may also have noticed that it is common for computer programs to look very similar, especially the simple ones. An interesting question often arises. When two programs solve the same problem but look different, is one program better than the other?

Con el fin de responder esta pregunta, tenemos que recordar que hay una diferencia importante entre un programa y el algoritmo subyacente que el programa está representando. Como dijimos en el Capítulo 1, un algoritmo es una lista genérica, paso a paso, de instrucciones para resolver un problema. Es un método para resolver cualquier caso del problema de tal manera que dada una entrada particular, el algoritmo produzca el resultado deseado. Un programa, por otro lado, es un algoritmo que ha sido codificado en algún lenguaje de programación. Pueden existir muchos programas para el mismo algoritmo, dependiendo del programador y del lenguaje de programación que se esté utilizando.

.. In order to answer this question, we need to remember that there is an important difference between a program and the underlying algorithm that the program is representing. As we stated in Chapter 1, an algorithm is a generic, step-by-step list of instructions for solving a problem. It is a method for solving any instance of the problem such that given a particular input, the algorithm produces the desired result. A program, on the other hand, is an algorithm that has been encoded into some programming language. There may be many programs for the same algorithm, depending on the programmer and the programming language being used.

Para explorar aún más esta diferencia, considere la función que se muestra en el :ref:`ActiveCode 1 <lst_sum1>`. Esta función resuelve un problema familiar: calcular la suma de los primeros *n* enteros. El algoritmo utiliza la idea de una variable acumuladora que se inicializa en 0. La solución itera entonces a través de los *n* enteros, agregando cada uno a la variable acumuladora.

.. To explore this difference further, consider the function shown in :ref:`ActiveCode 1 <lst_sum1>`. This function solves a familiar problem, computing the sum of the first *n* integers. The algorithm uses the idea of an accumulator variable that is initialized to 0. The solution then iterates through the *n* integers, adding each to the accumulator.

.. _lst_sum1:

.. activecode:: active1
    :caption: Sumatoria de los primeros n enteros

    def sumaDeN(n):
       laSuma = 0
       for i in range(1,n+1):
           laSuma = laSuma + i

       return laSuma

    print(sumaDeN(10))

Ahora mire la función en el :ref:`ActiveCode 2 <lst_sum2>`. A primera vista puede parecer extraña, pero después de una inspección más profunda se puede ver que esta función está haciendo esencialmente lo mismo que la anterior. La razón por la que esto no es obvio es la deficiente codificación. No usamos buenos nombres de identificación para facilitar la lectura, y usamos una instrucción de asignación extra durante el paso de acumulación que no era realmente necesaria.

.. Now look at the function in :ref:`ActiveCode 2 <lst_sum2>`. At first glance it may look strange, but upon further inspection you can see that this function is essentially doing the same thing as the previous one. The reason this is not obvious is poor coding. We did not use good identifier names to assist with readability, and we used an extra assignment statement during the accumulation step that was not really necessary.

.. _lst_sum2:

.. activecode:: active2
    :caption: Otra sumatoria de los primeros n enteros

    def cosa(fulano):
        mengano = 0
        for zutano in range(1,fulano+1):
           perencejo = zutano
           mengano = mengano + perencejo

        return mengano

    print(cosa(10))

La pregunta que planteamos anteriormente consistía en responder si una función es mejor que la otra. La respuesta depende de sus criterios. La función ``sumaDeN`` es ciertamente mejor que la función ``cosa`` si usted está interesado en la legibilidad. De hecho, probablemente haya visto muchos ejemplos de esto en su curso de programación introductoria, ya que una de los propósitos de dicho curso es ayudar a escribir programas que sean fáciles de leer y de entender. No obstante, en este curso también estamos interesados en caracterizar el propio algoritmo. (Esperamos ciertamente que usted continúe esforzándose por escribir código legible y comprensible.)

.. The question we raised earlier asked whether one function is better than another. The answer depends on your criteria. The function ``sumaDeN`` is certainly better than the function ``cosa`` if you are concerned with readability. In fact, you have probably seen many examples of this in your introductory programming course since one of the goals there is to help you write programs that are easy to read and easy to understand. In this course, however, we are also interested in characterizing the algorithm itself. (We certainly hope that you will continue to strive to write readable, understandable code.)

El análisis de algoritmos se ocupa de compararlos con base en la cantidad de recursos computacionales que utiliza cada algoritmo. Queremos ser capaces de considerar dos algoritmos y decir que uno es mejor que el otro, porque es más eficiente en su uso de esos recursos o simplemente tal vez porque utiliza una menor cantidad. Desde esta perspectiva, las dos funciones anteriores parecen muy similares. Ambos usan en esencia el mismo algoritmo para resolver el problema de la sumatoria.

.. Algorithm analysis is concerned with comparing algorithms based upon the amount of computing resources that each algorithm uses. We want to be able to consider two algorithms and say that one is better than the other because it is more efficient in its use of those resources or perhaps because it simply uses fewer. From this perspective, the two functions above seem very similar. They both use essentially the same algorithm to solve the summation problem.

En este punto, es importante pensar más en lo que realmente queremos decir con recursos computacionales. Hay dos formas diferentes de ver esto. Una forma es considerar la cantidad de espacio o memoria que un algoritmo requiere para resolver el problema. La cantidad de espacio requerida por una solución suele ser dictada por el caso particular del problema. De vez en cuando, sin embargo, hay algoritmos que tienen requisitos de espacio muy específicos, y en esos casos seremos muy cuidadosos al explicar las variaciones.

.. At this point, it is important to think more about what we really mean by computing resources. There are two different ways to look at this. One way is to consider the amount of space or memory an algorithm requires to solve the problem. The amount of space required by a problem solution is typically dictated by the problem instance itself. Every so often, however, there are algorithms that have very specific space requirements, and in those cases we will be very careful to explain the variations.

Como alternativa a los requerimientos de espacio, podemos analizar y comparar algoritmos basados en la cantidad de tiempo que requieren para ejecutarse. Esta medida se denomina a veces “tiempo de ejecución” o “tiempo de corrida” del algoritmo. Una forma de medir el tiempo de ejecución de la función ``sumaDeN`` es hacer un análisis de pruebas de referencia (*benchmark*). Esto significa que mediremos el tiempo real requerido para que el programa calcule su resultado. En Python, podemos hacer una prueba de referencia de una función observando el tiempo de inicio y el tiempo de finalización con respecto al sistema que estamos utilizando. En el módulo ``time`` hay una función llamada ``time`` que devolverá el tiempo actual del reloj del sistema medido en segundos desde algún punto de inicio arbitrario. Al llamar a esta función dos veces, al inicio y al final, y luego calcular la diferencia, podemos obtener un número exacto de segundos (fracciones en la mayoría de los casos) de la ejecución.

.. As an alternative to space requirements, we can analyze and compare algorithms based on the amount of time they require to execute. This measure is sometimes referred to as the “execution time” or “running time” of the algorithm. One way we can measure the execution time for the function ``sumaDeN`` is to do a benchmark analysis. This means that we will track the actual time required for the program to compute its result. In Python, we can benchmark a function by noting the starting time and ending time with respect to the system we are using. In the ``time`` module there is a function called ``time`` that will return the current system clock time in seconds since some arbitrary starting point. By calling this function twice, at the beginning and at the end, and then computing the difference, we can get an exact number of seconds (fractions in most cases) for execution.

.. _lst_sum11:

**Programa 1**

.. sourcecode:: python

    import time

    def sumaDeN2(n):
       inicio = time.time()

       laSuma = 0
       for i in range(1,n+1):
          laSuma = laSuma + i

       final = time.time()

       return laSuma,final-inicio

El :ref:`Programa 1 <lst_sum11>` muestra la función ``sumaDeN`` con las llamadas de temporización incrustadas antes y después de la suma. La función devuelve una tupla que consiste en el resultado y la cantidad de tiempo (en segundos) requerida para el cálculo. Si realizamos 5 llamados a la función, calculando cada vez la suma de los primeros 10,000 enteros, obtendremos lo siguiente:

.. :ref:`Listing 1 <lst_sum11>` shows the original ``sumaDeN`` function with the timing calls embedded before and after the summation. The function returns a tuple consisting of the result and the amount of time (in seconds) required for the calculation. If we perform 5 invocations of the function, each computing the sum of the first 10,000 integers, we get the following:



::

    >>>for i in range(5):
           print("La suma es %d y requirió %10.7f segundos"%sumaDeN(10000))
    La suma es 50005000 y requirió  0.0018950 segundos
    La suma es 50005000 y requirió  0.0018620 segundos
    La suma es 50005000 y requirió  0.0019171 segundos
    La suma es 50005000 y requirió  0.0019162 segundos
    La suma es 50005000 y requirió  0.0019360 segundos

Descubrimos que el tiempo es bastante consistente y que ejecutar ese código toma en promedio alrededor de 0.0019 segundos. ¿Qué pasará si ejecutamos la función sumando los primeros 100,000 enteros?

.. We discover that the time is fairly consistent and it takes on average about 0.0019 seconds to execute that code. What if we run the function adding the first 100,000 integers?

::

    >>>for i in range(5):
           print("La suma es %d y requirió %10.7f segundos"%sumaDeN(100000))
    La suma es 5000050000 y requirió  0.0199420 segundos
    La suma es 5000050000 y requirió  0.0180972 segundos
    La suma es 5000050000 y requirió  0.0194821 segundos
    La suma es 5000050000 y requirió  0.0178988 segundos
    La suma es 5000050000 y requirió  0.0188949 segundos
    >>>

De nuevo, el tiempo requerido para cada ejecución, aunque más largo, es muy consistente, promediando alrededor de 10 veces más segundos. Para ``n`` igual a 1,000,000 obtenemos:

.. Again, the time required for each run, although longer, is very consistent, averaging about 10 times more seconds. For ``n`` equal to 1,000,000 we get:

::

    >>>for i in range(5):
           print("La suma es %d y requirió %10.7f segundos"%sumaDeN(1000000))
    La suma es 500000500000 y requirió  0.1948988 segundos
    La suma es 500000500000 y requirió  0.1850290 segundos
    La suma es 500000500000 y requirió  0.1809771 segundos
    La suma es 500000500000 y requirió  0.1729250 segundos
    La suma es 500000500000 y requirió  0.1646299 segundos
    >>>

En este caso, el promedio vuelve a ser aproximadamente 10 veces el anterior.

.. In this case, the average again turns out to be about 10 times the previous.

Ahora considere el :ref:`ActiveCode 3 <lst_sum3>`, el cual muestra una manera diferente de resolver el problema de la sumatoria. Esta función, ``sumaDeN3``, hace uso de una ecuación cerrada :math:`\sum_{i=1}^{n} i = \frac {(n)(n+1)}{2}` para calcular, sin iterar, la suma de los primeros ``n`` números enteros.

.. Now consider :ref:`ActiveCode 3 <lst_sum3>`, which shows a different means of solving the summation problem. This function, ``sumaDeN3``, takes advantage of a closed equation :math:`\sum_{i=1}^{n} i = \frac {(n)(n+1)}{2}` to compute the sum of the first ``n`` integers without iterating.

.. _lst_sum3:

.. activecode:: active3
    :caption: Sumatoria sin iteración

    def sumaDeN3(n):
       return (n*(n+1))/2

    print(sumaDeN3(10))

Si hacemos la misma prueba de referencia para ``sumaDeN3``, usando cinco valores diferentes para ``n`` (10,000, 100,000, 1,000,000, 10,000,000 y 100,000,000), obtendremos los siguientes resultados:

.. If we do the same benchmark measurement for ``sumaDeN3``, using five different values for ``n`` (10,000, 100,000, 1,000,000, 10,000,000, and 100,000,000), we get the following results:

::

    La suma es 50005000 y requirió 0.00000095 segundos
    La suma es 5000050000 y requirió 0.00000191 segundos
    La suma es 500000500000 y requirió 0.00000095 segundos
    La suma es 50000005000000 y requirió 0.00000095 segundos
    La suma es 5000000050000000 y requirió 0.00000119 segundos

Hay dos cosas importantes que observar acerca de este resultado. En primer lugar, los tiempos registrados anteriormente son más cortos que cualquiera de los ejemplos anteriores. En segundo lugar, son muy consistentes sin importar el valor de ``n``. Parece que ``sumaDeN3`` apenas se ve afectada por el número de enteros que se suman.

.. There are two important things to notice about this output. First, the times recorded above are shorter than any of the previous examples. Second, they are very consistent no matter what the value of ``n``. It appears that ``sumaDeN3`` is hardly impacted by the number of integers being added.

Pero, ¿qué nos dice realmente esta prueba de referencia? Intuitivamente, podemos ver que las soluciones iterativas parecen estar haciendo más trabajo ya que algunos pasos del programa se están repitiendo. Ésta es probablemente la razón por la que está tomando más tiempo. Además, el tiempo requerido para la solución iterativa parece aumentar a medida que aumentamos el valor de ``n``. Sin embargo, hay un problema. Si ejecutamos la misma función en una computadora diferente o usamos un lenguaje de programación diferente, es probable que obtengamos resultados diferentes. Podría tomar aún más tiempo ejecutar ``sumaDeN3`` si la computadora fuera una más antigua.

.. But what does this benchmark really tell us? Intuitively, we can see that the iterative solutions seem to be doing more work since some program steps are being repeated. This is likely the reason it is taking longer. Also, the time required for the iterative solution seems to increase as we increase the value of ``n``. However, there is a problem. If we ran the same function on a different computer or used a different programming language, we would likely get different results. It could take even longer to perform ``sumaDeN3`` if the computer were older.

Necesitamos una mejor manera de caracterizar estos algoritmos con respecto al tiempo de ejecución. La técnica de pruebas de referencia calcula el tiempo de ejecución real. Esa técnica en verdad no nos proporciona una medida útil, ya que depende de una máquina, programa, hora del día, compilador y lenguaje de programación  en particular. En su lugar, nos gustaría tener una caracterización que sea independiente del programa o de la computadora que se utilice. Esta medida sería entonces útil para juzgar el algoritmo aisladamente y podría utilizarse para comparar algoritmos en diferentes implementaciones.

.. We need a better way to characterize these algorithms with respect to execution time. The benchmark technique computes the actual time to execute. It does not really provide us with a useful measurement, because it is dependent on a particular machine, program, time of day, compiler, and programming language. Instead, we would like to have a characterization that is independent of the program or computer being used. This measure would then be useful for judging the algorithm alone and could be used to compare algorithms across implementations.
