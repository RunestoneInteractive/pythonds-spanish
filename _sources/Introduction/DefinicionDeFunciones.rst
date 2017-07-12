..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Definición de funciones
~~~~~~~~~~~~~~~~~~~~~~~

En el ejemplo previo de abstracción procedimental se invocó una función del módulo de matemáticas de Python, llamada ``sqrt``, para calcular la raíz cuadrada. En general, podemos ocultar los detalles de cualquier cálculo definiendo una función. La definición de una función requiere un nombre, un grupo de parámetros y un cuerpo. También puede devolver un valor explícitamente. Por ejemplo, la función simple definida a continuación devuelve el cuadrado del valor que se le pasa como parámetro.

.. The earlier example of procedural abstraction called upon a Python function called ``sqrt`` from the math module to compute the square root. In general, we can hide the details of any computation by defining a function. A function definition requires a name, a group of parameters, and a body. It may also explicitly return a value. For example, the simple function defined below returns the square of the value you pass into it.

::

    >>> def cuadrado(n):
    ...    return n**2
    ...
    >>> cuadrado(3)
    9
    >>> cuadrado(cuadrado(3))
    81
    >>>

La sintaxis para esta definición de función incluye el nombre, ``cuadrado``, y una lista entre paréntesis de parámetros formales. Para esta función, ``n`` es el único parámetro formal, lo cual sugiere que ``cuadrado`` sólo necesita una pieza de datos para realizar su trabajo. Los detalles, ocultos “dentro de la caja”, simplemente calculan el resultado de ``n**2`` y lo devuelven. Podemos invocar o llamar a la función ``cuadrado`` pidiendo al entorno de Python que la evalúe, pasándole un valor de parámetro real, en este caso ``3``. Tenga en cuenta que la llamada a ``cuadrado`` devuelve un entero que a su vez puede pasarse a otra invocación.

.. The syntax for this function definition includes the name, ``cuadrado``, and a parenthesized list of formal parameters. For this function, ``n`` is the only formal parameter, which suggests that ``cuadrado`` needs only one piece of data to do its work. The details, hidden “inside the box,” simply compute the result of ``n**2`` and return it. We can invoke or call the ``cuadrado`` function by asking the Python environment to evaluate it, passing an actual parameter value, in this case, ``3``. Note that the call to ``cuadrado`` returns an integer that can in turn be passed to another invocation.

Podríamos implementar nuestra propia función de raíz cuadrada usando una técnica bien conocida llamada “Método de Newton”. El Método de Newton para aproximar raíces cuadradas realiza un cálculo iterativo que converge al valor correcto. La ecuación :math:`estimacionNueva = \frac {1}{2} * (estimacionVieja + \frac {n}{estimacionVieja})` toma un valor :math:`n` y repetidamente estima la raíz cuadrada haciendo que :math:`estimacionNueva` sea :math:`estimacionVieja` en la iteración subsiguiente. La estimación inicial utilizada aquí es :math:`\frac {n}{2}`. El :ref:`Programa 1 <lst_root>` muestra una definición de función que acepta un valor :math:`n` y devuelve la raíz cuadrada de :math:`n` después de hacer 20 estimaciones. Una vez más, los detalles del Método de Newton están ocultos dentro de la definición de la función y el usuario no tiene que saber nada sobre la implementación para usar la función para su finalidad prevista. El :ref:`Programa 1 <lst_root>` también muestra el uso del caracter # como marcador de comentario. Los caracteres que siguen al # en una renglón se ignoran.

.. We could implement our own square root function by using a well-known technique called “Newton’s Method.” Newton’s Method for approximating square roots performs an iterative computation that converges on the correct value. The equation :math:`newguess = \frac {1}{2} * (oldguess + \frac {n}{oldguess})` takes a value :math:`n` and repeatedly guesses the square root by making each :math:`newguess` the :math:`oldguess` in the subsequent iteration. The initial guess used here is :math:`\frac {n}{2}`. :ref:`Listing 1 <lst_root>` shows a function definition that accepts a value :math:`n` and returns the square root of :math:`n` after making 20 guesses. Again, the details of Newton’s Method are hidden inside the function definition and the user does not have to know anything about the implementation to use the function for its intended purpose. :ref:`Listing 1 <lst_root>` also shows the use of the # character as a comment marker. Any characters that follow the # on a line are ignored.

.. _lst_root:

**Programa 1**

.. sourcecode:: python

    def raizCuadrada(n):
        raiz = n/2    #La estimación inicial será 1/2 de n
        for k in range(20):
            raiz = (1/2)*(raiz + (n / raiz))

        return raiz


::

    >>>raizCuadrada(9)
    3.0
    >>>raizCuadrada(4563)
    67.549981495186216
    >>>

.. admonition:: Autoevaluación

   He aquí una autoevaluación que realmente cubre todo lo visto hasta ahora. Puede que usted haya oído hablar del teorema del mono infinito. El teorema dice que un mono golpeando las teclas, al azar y por por una cantidad infinita de tiempo, en un teclado de máquina de escribir casi con completa seguridad escribirá cualquier texto dado como por ejemplo las obras completas de William Shakespeare. Bueno, supongamos que vamos a reemplazar al mono con una función de Python. ¿Cuánto tiempo cree usted que le tomaría a una función de Python generar tan sólo una frase de Shakespeare? La frase que aspiramos generar es: "yo creo que parece una comadreja".

   Usted no querrá ejecutar esto en el navegador, así que abra su entorno de desarrollo de Python favorito. La forma en que vamos a simular esto es escribiendo una función que genere una cadena de 27 caracteres de longitud, mediante la elección aleatoria de cada caracter de entre las 26 letras del alfabeto más el espacio en blanco. Escribiremos otra función que calificará cada cadena generada aleatoriamente mediante su comparación con la cadena objetivo.

   Una tercera función llamará repetidamente a las funciones generar y calificar, entonces habremos terminado si el 100% de las letras son correctas. Si las letras no son correctas, generaremos entonces una nueva cadena completa. Para hacer más fácil seguir el progreso de su programa, esta tercera función debe imprimir la mejor secuencia generada hasta el momento y su calificación correspondiente cada 1000 intentos.


.. admonition:: Reto de autoevaluación

    Vea si puede mejorar el programa de la autoevaluación manteniendo las letras que sean correctas y modificando sólo un carácter en la mejor secuencia hasta el momento. Éste es un tipo de algoritmo en la clase de algoritmos de 'ascenso de colinas (*hill climbing* en la literatura en inglés)', es decir, sólo mantenemos el resultado si es mejor que el anterior.
