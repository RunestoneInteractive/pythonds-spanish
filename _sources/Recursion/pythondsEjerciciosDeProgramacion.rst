..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Ejercicios de programación
--------------------------

#. Escriba una función recursiva para calcular el factorial de un número.

#. Escriba una función recursiva para invertir una lista.

#. Modifique el programa de árbol recursivo utilizando una o todas las ideas siguientes:

   -  Modifique el grosor de las ramas para que a medida que el valor de ``longitudRama`` se haga más pequeño, la línea se haga más delgada.

   -  Modifique el color de las ramas de modo cuando el valor de ``longitudRama`` se vuelva muy pequeño se coloree como una hoja.

   -  Modifique el ángulo utilizado para girar la tortuga de manera que en cada punto de ramificación el ángulo se seleccione al azar dentro de algún rango. Por ejemplo, elija el ángulo entre 15 y 45 grados. Haga ensayos para ver si se ve bien.

   -  Modifique el valor de ``longitudRama`` recursivamente para que en lugar de siempre restar la misma cantidad, usted reste una cantidad aleatoria dentro de algún rango.

   Si usted implementa todas las ideas anteriores, tendrá un árbol de aspecto muy realista.

#. Encuentre o invente un algoritmo para dibujar una montaña fractal. Sugerencia: Un enfoque para lograr esto también usa triángulos.

#. Escriba una función recursiva para calcular la secuencia de Fibonacci. ¿Cómo se compara el desempeño de la función recursiva con el de una versión iterativa?

#. Implemente una solución al problema de las torres de Hanoi utilizando tres pilas para mantener un seguimiento de los discos.

#. Usando el módulo gráfico ``turtle``, escriba un programa recursivo para mostrar una curva de Hilbert.

#. Usando el módulo gráfico ``turtle``, escriba un programa recursivo para mostrar un copo de nieve de Koch.

#. Escriba un programa para resolver el siguiente problema: Usted tiene dos jarras: una jarra de 4 galones y una jarra de 3 galones. Ninguna de las jarras tiene marcas en ella. Hay una bomba que se puede utilizar para llenar las jarras con agua. ¿Cómo se pueden obtener exactamente dos galones de agua en la jarra de 4 galones?

#. Generalice el problema anterior para que los parámetros de su solución incluyen los tamaños de cada jarra y la cantidad final de agua que queda en la jarra más grande.

#. Escriba un programa que resuelva el siguiente problema: Tres misioneros y tres caníbales llegan a un río y encuentran un bote con capacidad para dos personas. Todos deben cruzar el río para continuar en el viaje. Sin embargo, si los caníbales sobrepasan en número a los misioneros en cada orilla, los misioneros serán comidos. Encuentra una serie de cruces que llevarán a todos a salvo al otro lado del río.

#. Modifique el programa de las torres de Hanoi usando gráficos de tortuga para animar el movimiento de los discos. Sugerencia: Usted puede crear varias tortugas y darles forma de rectángulos.

#. El triángulo de Pascal es un triángulo numérico con números dispuestos en filas escalonadas de manera que

   .. math::
      a_{nr} = {n! \over{r! (n-r)!}}
   
   Esta ecuación es la ecuación para un coeficiente binomial. Usted puede construir el triángulo de Pascal agregando los dos números que están, en diagonal, encima de un número en el triángulo. A continuación se muestra un ejemplo del triángulo de Pascal.

   ::

                         1
                       1   1
                     1   2   1
                   1   3   3   1
                 1   4   6   4   1

   Escriba un programa que imprima el triángulo de Pascal. Su programa debe aceptar un parámetro que indique cuántas filas del triángulo se imprimirán.

#. Suponga que usted es un científico de la computación/ladrón de arte que se ha colado en una galería de arte importante. Todo lo que tiene con usted para sacar las obras de arte robadas es su mochila que sólo puede contener :math:`W` libras de arte; no obstante, para cada pieza de arte usted conoce su valor y su peso. Escriba una función de programación dinámica para ayudarse a maximizar sus ganancias. He aquí un ejemplo del problema que usted puede usar para empezar: Supongamos que su mochila aguanta un peso total de 20. Usted tiene 5 ítems como sigue:

   :: 
   
        ítem      peso       valor
          1        2           3
          2        3           4
          3        4           8
          4        5           8
          5        9          10

#. Este problema se llama el problema de la distancia de edición de cadenas, y es muy útil en muchas áreas de investigación. Suponga que usted desea transformar la cadena “algorithm” en la palabra “alligator”. Para cada letra usted puede copiar la letra de una palabra a otra a un costo de 5, o puede borrar una letra a un costo de 20 o insertar una letra a un costo de 20. El costo total de transformar una palabra en otra es utilizado por los programas de revisión de ortografía para proporcionar sugerencias de palabras que estén cercanas (sean similares) unas con otras. Utilice técnicas de programación dinámica para desarrollar un algoritmo que le dé la menor distancia de edición entre dos palabras.
