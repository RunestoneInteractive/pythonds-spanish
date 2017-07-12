..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Manejo de excepciones
~~~~~~~~~~~~~~~~~~~~~

Hay dos tipos de errores que normalmente ocurren al escribir programas. El primero, conocido como un error de sintaxis, simplemente significa que el programador ha cometido un error en la estructura de una instrución o de una expresión. Por ejemplo, es incorrecto escribir una instrucción for y olvidar los dos puntos.

.. There are two types of errors that typically occur when writing programs. The first, known as a syntax error, simply means that the programmer has made a mistake in the structure of a statement or expression. For example, it is incorrect to write a for statement and forget the colon.

::

    >>> for i in range(10)
    SyntaxError: invalid syntax (<pyshell#61>, line 1)

En este caso, el intérprete de Python ha encontrado que no puede completar el procesamiento de esta instrucción ya que no se ajusta a las reglas del lenguaje. Los errores de sintaxis suelen ser más frecuentes cuando se está comenzando a aprender un lenguaje.

.. In this case, the Python interpreter has found that it cannot complete the processing of this instruction since it does not conform to the rules of the language. Syntax errors are usually more frequent when you are first learning a language.

El otro tipo de error, conocido como un error lógico, denota una situación en la que el programa se ejecuta pero da el resultado incorrecto. Esto puede deberse a un error en el algoritmo en el que está basado el programa o a un error en la traducción de ese algoritmo. En algunos casos, los errores lógicos conducen a situaciones muy malas, como tratar de dividir por cero o tratar de acceder a un ítem en una lista donde el índice del ítem está fuera de los límites de la lista. En este caso, el error lógico conduce a un error en tiempo de ejecución que hace que el programa se interrumpa. Estos tipos de errores en tiempo de ejecución típicamente se llaman **excepciones**.

.. The other type of error, known as a logic error, denotes a situation where the program executes but gives the wrong result. This can be due to an error in the underlying algorithm or an error in your translation of that algorithm. In some cases, logic errors lead to very bad situations such as trying to divide by zero or trying to access an item in a list where the index of the item is outside the bounds of the list. In this case, the logic error leads to a runtime error that causes the program to terminate. These types of runtime errors are typically called **exceptions**.

La mayoría de las veces, los programadores principiantes simplemente piensan en las excepciones como errores fatales en tiempo de ejecución que causan que la ejecución finalice. Sin embargo, la mayoría de los lenguajes de programación proporcionan una manera de lidiar con estos errores que permitirán al programador tener algún tipo de intervención si así lo desean. Además, los programadores pueden crear sus propias excepciones si detectan una situación en la ejecución del programa que lo justifique.

.. Most of the time, beginning programmers simply think of exceptions as fatal runtime errors that cause the end of execution. However, most programming languages provide a way to deal with these errors that will allow the programmer to have some type of intervention if they so choose. In addition, programmers can create their own exceptions if they detect a situation in the program execution that warrants it.

Cuando se produce una excepción, decimos que se ha “generado”. Usted puede “manejar” la excepción que se ha generado utilizando una instrucción ``try``. Por ejemplo, considere la siguiente sesión que solicita al usuario un número entero y luego llama a la función raíz cuadrada de la biblioteca de matemáticas. Si el usuario introduce un valor mayor o igual a 0, el ``print`` mostrará la raíz cuadrada. Sin embargo, si el usuario ingresa un valor negativo, la función raíz cuadrada reportará una excepción ``ValueError``.

.. When an exception occurs, we say that it has been “raised.” You can “handle” the exception that has been raised by using a ``try`` statement. For example, consider the following session that asks the user for an integer and then calls the square root function from the math library. If the user enters a value that is greater than or equal to 0, the print will show the square root. However, if the user enters a negative value, the square root function will report a ``ValueError`` exception.

::

    >>> unNumero = int(input("Por favor ingrese un entero "))
    Por favor ingrese un entero -23
    >>> print(math.sqrt(unNumero))
    Traceback (most recent call last):
      File "<pyshell#102>", line 1, in <module>
        print(math.sqrt(unNumero))
    ValueError: math domain error
    >>>

Podemos manejar esta excepción llamando a la función ``print`` desde dentro de un bloque ``try``. Un bloque ``except`` correspondiente “captura” la excepción e imprime un mensaje para el usuario en caso de que se produzca una excepción. Por ejemplo:

.. We can handle this exception by calling the print function from within a ``try`` block. A corresponding ``except`` block “catches” the exception and prints a message back to the user in the event that an exception occurs. For example:

::

    >>> try:
           print(math.sqrt(unNumero))
        except:
           print("Valor incorrecto para la raíz cuadrada")
           print("Se usa el valor absoluto en sustitución")
           print(math.sqrt(abs(unNumero)))

    Valor incorrecto para la raíz cuadrada
    Se usa el valor absoluto en sustitución
    4.79583152331
    >>>

capturará el hecho de que una excepción ha sido generada por ``sqrt``, imprimirá los mensajes para el usuario y utilizará el valor absoluto para asegurarse de que estamos tomando la raíz cuadrada de un número no negativo. Esto significa que el programa no se interrumpirá, sino que continuará con las instrucciones siguientes.

.. will catch the fact that an exception is raised by ``sqrt`` and will instead print the messages back to the user and use the absolute value to be sure that we are taking the square root of a non-negative number. This means that the program will not terminate but instead will continue on to the next statements.

También es posible que un programador cause una excepción en tiempo de ejecución utilizando la instrucción ``raise``. Por ejemplo, en lugar de llamar a la función raíz cuadrada con un número negativo, podríamos haber comprobado primero el valor y luego haber generado nuestra propia excepción. El siguiente fragmento de código muestra el resultado de la creación de una nueva excepción ``RuntimeError``. Note que el programa se interrumpiría de todos modos, pero ahora la excepción que causó la interrupción es algo creado explícitamente por el programador.

.. It is also possible for a programmer to cause a runtime exception by using the ``raise`` statement. For example, instead of calling the square root function with a negative number, we could have checked the value first and then raised our own exception. The code fragment below shows the result of creating a new ``RuntimeError`` exception. Note that the program would still terminate but now the exception that caused the termination is something explicitly created by the programmer.

::

    >>> if unNumero < 0:
    ...    raise RuntimeError("Usted no puede usar un número negativo")
    ... else:
    ...    print(math.sqrt(unNumero))
    ...
    Traceback (most recent call last):
      File "<stdin>", line 2, in <module>
    RuntimeError: Usted no puede usar un número negativo
    >>>

Existen muchos tipos de excepciones que pueden generarse además de la excepción ``RuntimeError`` mostrada anteriormente. Consulte el manual de referencia de Python para obtener una lista de todos los tipos de excepciones disponibles y aprender cómo crear las suyas propias.

.. There are many kinds of exceptions that can be raised in addition to the ``RuntimeError`` shown above. See the Python reference manual for a list of all the available exception types and for how to create your own.
