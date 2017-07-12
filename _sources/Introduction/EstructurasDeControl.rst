..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Estructuras de control
~~~~~~~~~~~~~~~~~~~~~~

Como hemos observado anteriormente, los algoritmos requieren dos estructuras de control importantes: iteración y selección. Ambas están disponibles en Python en varias formas. El programador puede elegir la instrucción que sea más útil para la circunstancia dada.

.. As we noted earlier, algorithms require two important control structures: iteration and selection. Both of these are supported by Python in various forms. The programmer can choose the statement that is most useful for the given circumstance.

Para la iteración, Python proporciona una instrucción ``while`` estándar y una instrucción ``for`` muy potente. La instrucción ``while`` repite un cuerpo de código mientras una condición sea verdadera. Por ejemplo,

.. For iteration, Python provides a standard ``while`` statement and a very powerful ``for`` statement. The while statement repeats a body of code as long as a condition is true. For example,

::

    >>> contador = 1
    >>> while contador <= 5:
    ...     print("Hola, mundo")
    ...     contador = contador + 1


    Hola, mundo
    Hola, mundo
    Hola, mundo
    Hola, mundo
    Hola, mundo

imprime la frase “Hola, mundo” cinco veces. La condición en la instrucción ``while`` se evalúa al inicio de cada repetición. Si la condición es ``True``, el cuerpo de la instrucción se ejecutará. Es fácil ver la estructura de una instrucción ``while`` de Python debido al patrón de sangrado obligatorio que el lenguaje impone.

.. prints out the phrase “Hola, mundo” five times. The condition on the ``while`` statement is evaluated at the start of each repetition. If the condition is ``True``, the body of the statement will execute. It is easy to see the structure of a Python ``while`` statement due to the mandatory indentation pattern that the language enforces.

La instrucción ``while`` es una estructura iterativa de propósito general que usaremos en una serie de algoritmos diferentes. En muchos casos, una condición compuesta controlará la iteración. Un fragmento como el siguiente

.. The ``while`` statement is a very general purpose iterative structure that we will use in a number of different algorithms. In many cases, a compound condition will control the iteration. A fragment such as

::

    while contador <= 10 and not hecho:
    ...

haría que el cuerpo de la instrucción fuera ejecutado sólo en el caso en que se cumplan ambas partes de la condición. El valor de la variable ``contador`` tendría que ser menor o igual a 10 y el valor de la variable ``hecho`` tendría que ser ``False`` (``not False`` es ``True``) de modo que ``True and True`` da como resultado ``True``.

.. would cause the body of the statement to be executed only in the case where both parts of the condition are satisfied. The value of the variable ``contador`` would need to be less than or equal to 10 and the value of the variable ``done`` would need to be ``False`` (``not False`` is ``True``) so that ``True and True`` results in ``True``.

Aunque este tipo de estructura es muy útil en una amplia variedad de situaciones, otra estructura iterativa, la instrucción ``for``, se puede usar junto con muchas de las colecciones de Python. La instrucción ``for`` puede usarse para iterar sobre los miembros de una colección, siempre y cuando la colección sea una secuencia. Así por ejemplo,

.. Even though this type of construct is very useful in a wide variety of situations, another iterative structure, the ``for`` statement, can be used in conjunction with many of the Python collections. The ``for`` statement can be used to iterate over the members of a collection, so long as the collection is a sequence. So, for example,

::

    >>> for item in [1,3,6,2,5]:
    ...    print(item)
    ...
    1
    3
    6
    2
    5

asigna a la variable ``item`` cada valor sucesivo de la lista [1,3,6,2,5]. Entonces se ejecuta el cuerpo de la iteración. Esto funciona para cualquier colección que sea una secuencia (listas, tuplas y cadenas).

.. assigns the variable ``item`` to be each successive value in the list [1,3,6,2,5]. The body of the iteration is then executed. This works for any collection that is a sequence (lists, tuples, and strings).

Un uso común de la instrucción ``for`` es implementar una iteración definida sobre un rango de valores. La instrucción

.. A common use of the ``for`` statement is to implement definite iteration over a range of values. The statement

::

    >>> for item in range(5):
    ...    print(item**2)
    ...
    0
    1
    4
    9
    16
    >>>

ejecutará la función ``print`` cinco veces. La función ``range`` devolverá un objeto de rango que representa la secuencia 0,1,2,3,4 y cada valor se asignará a la variable ``item``. Este valor es entonces elevado al cuadrado y se imprime en pantalla.

.. will perform the ``print`` function five times. The ``range`` function will return a range object representing the sequence 0,1,2,3,4 and each value will be assigned to the variable ``item``. This value is then squared and printed.

La otra versión muy útil de esta estructura de iteración se utiliza para procesar cada carácter de una cadena. El siguiente fragmento de código itera sobre una lista de cadenas y para cada cadena procesa cada carácter añadiéndolo a una lista. El resultado es una lista de todas las letras en todas las palabras.

.. The other very useful version of this iteration structure is used to process each character of a string. The following code fragment iterates over a list of strings and for each string processes each character by appending it to a list. The result is a list of all the letters in all of the words.

.. activecode:: intro_8
    :caption: Procesamiento de cada carácter en una lista de cadenas

    listaPalabras = ['gato','perro','conejo']
    listaLetras = [ ]
    for unaPalabra in listaPalabras:
        for unaLetra in unaPalabra:
            listaLetras.append(unaLetra)
    print(listaLetras)

Las instrucciones de selección le permiten a los programadores hacer preguntas y luego, con base en el resultado, realizar diferentes acciones. La mayoría de los lenguajes de programación proporcionan dos versiones de esta útil estructura: ``ifelse`` e ``if``. Un ejemplo sencillo de una selección binaria que utiliza la instrucción ``ifelse`` es el siguiente:

.. Selection statements allow programmers to ask questions and then, based on the result, perform different actions. Most programming languages provide two versions of this useful construct: the ``ifelse`` and the ``if``. A simple example of a binary selection uses the ``ifelse`` statement.

::

    if n<0:
       print("Lo siento, el valor es negativo")
    else:
       print(math.sqrt(n))

En este ejemplo, el objeto referenciado por ``n`` se comprueba para ver si es menor que cero. Si así es, se imprime un mensaje indicando que es negativo. Si no es así, la instrucción ejecuta la cláusula ``else`` y calcula la raíz cuadrada.

.. In this example, the object referred to by ``n`` is checked to see if it is less than zero. If it is, a message is printed stating that it is negative. If it is not, the statement performs the ``else`` clause and computes the square root.

Las estructuras de selección, como ocurre con cualquier otra estructura de control, pueden anidarse de modo que el resultado de una pregunta ayude a decidir si se pregunta la siguiente. Por ejemplo, suponga que ``puntaje`` es una variable que contiene una referencia a un puntaje de un examen de ciencias de la computación.

.. Selection constructs, as with any control construct, can be nested so that the result of one question helps decide whether to ask the next. For example, assume that ``score`` is a variable holding a reference to a score for a computer science test.

::

    if puntaje >= 90:
       print('A')
    else:
       if puntaje >= 80:
          print('B')
       else:
          if puntaje >= 70:
             print('C')
          else:
             if puntaje >= 60:
                print('D')
             else:
                print('F')

Este fragmento clasificará un valor llamado ``puntaje`` mediante la impresión de la calificación cualitativa obtenida. Si el puntaje es mayor o igual a 90, la instrucción imprimirá ``A``. Si no lo es (``else``), se hace la pregunta siguiente. Si el puntaje es mayor o igual a 80, entonces debe estar entre 80 y 89, ya que la respuesta a la primera pregunta era falsa. En este caso se imprimirá la letra ``B``. Puede verse que el patrón de sangrado de Python ayuda a dar sentido a la asociación entre ``if`` y ``else`` sin necesidad de elementos sintácticos adicionales.

.. This fragment will classify a value called ``score`` by printing the letter grade earned. If the score is greater than or equal to 90, the statement will print ``A``. If it is not (``else``), the next question is asked. If the score is greater than or equal to 80 then it must be between 80 and 89 since the answer to the first question was false. In this case print ``B`` is printed. You can see that the Python indentation pattern helps to make sense of the association between ``if`` and ``else`` without requiring any additional syntactic elements.

Una sintaxis alternativa para este tipo de selección anidada utiliza la palabra clave ``elif``. El ``else`` y el ``if`` siguiente se combinan para eliminar la necesidad de niveles de anidamiento adicionales. Tenga en cuenta que el último ``else`` sigue siendo necesario para proporcionar el caso por defecto en caso que todas las demás condiciones fallen.

.. An alternative syntax for this type of nested selection uses the ``elif`` keyword. The ``else`` and the next ``if`` are combined so as to eliminate the need for additional nesting levels. Note that the final ``else`` is still necessary to provide the default case if all other conditions fail.

::

    if puntaje >= 90:
       print('A')
    elif puntaje >= 80:
       print('B')
    elif puntaje >= 70:
       print('C')
    elif puntaje >= 60:
       print('D')
    else:
       print('F')

Python también tiene una estructura de selección de una sola vía, la instrucción ``if``. Con esta instrucción, si la condición es verdadera, se realiza una acción. En caso que la condición sea falsa, el procesamiento simplemente continúa con la instrucción que siga después del ``if``. Por ejemplo, el siguiente fragmento comprobará primero si el valor de una variable ``n`` es negativo. Si lo es, entonces es modificado mediante la función de valor absoluto. Sea cual sea el caso, la siguiente acción es calcular la raíz cuadrada.

.. Python also has a single way selection construct, the ``if`` statement. With this statement, if the condition is true, an action is performed. In the case where the condition is false, processing simply continues on to the next statement after the ``if``. For example, the following fragment will first check to see if the value of a variable ``n`` is negative. If it is, then it is modified by the absolute value function. Regardless, the next action is to compute the square root.

::

    if n<0:
       n = abs(n)
    print(math.sqrt(n))


.. admonition:: Autoevaluación

    Pruebe su comprensión de lo que hemos cubierto hasta ahora al intentar solucionar el siguiente ejercicio.
    Modifique el código de Activecode 8 de modo que la lista final sólo contenga una sola copia de cada letra.

    .. activecode:: auto_eval_1

       # la respuesta es: ['c', 'a', 't', 'd', 'o', 'g', 'r', 'b', 'i']

Regresando a las listas, existe un método alternativo para crear una lista que usa estructuras de iteración y de selección y es conocido como **comprensión de listas**. Una comprensión de lista permite crear fácilmente una lista basada en algunos criterios de procesamiento o de selección. Por ejemplo, si quisiéramos crear una lista de los primeros 10 cuadrados perfectos, podríamos usar una instrucción ``for``:

.. Returning to lists, there is an alternative method for creating a list that uses iteration and selection constructs known as a **list comprehension**. A list comprehension allows you to easily create a list based on some processing or selection criteria. For example, if we would like to create a list of the first 10 perfect squares, we could use a ``for`` statement:

::

    >>> listaCuadrados=[]
    >>> for x in range(1,11):
             listaCuadrados.append(x*x)

    >>> listaCuadrados
    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
    >>>

Usando comprensión de listas, podemos hacer lo mismo en un único paso como

.. Using a list comprehension, we can do this in one step as

::

    >>> listaCuadrados=[x*x for x in range(1,11)]
    >>> listaCuadrados
    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
    >>>

La variable ``x`` toma los valores de 1 a 10 especificados por la estructura ``for``. El valor de ``x*x`` se calcula y se agrega a la lista que se está construyendo. La sintaxis general para una comprensión de listas también permite agregar un criterio de selección para que únicamente se agreguen ciertos ítems. Por ejemplo,

.. The variable ``x`` takes on the values 1 through 10 as specified by the ``for`` construct. The value of ``x*x`` is then computed and added to the list that is being constructed. The general syntax for a list comprehension also allows a selection criteria to be added so that only certain items get added. For example,

::

    >>> listaCuadrados=[x*x for x in range(1,11) if x%2 != 0]
    >>> listaCuadrados
    [1, 9, 25, 49, 81]
    >>>

Esta comprensión de listas construyó una lista que contenía solamente los cuadrados de los números impares en el rango de 1 a 10. Cualquier secuencia que soporte la iteración se puede utilizar dentro de una comprensión de listas para construir una nueva lista.

.. This list comprehension constructed a list that only contained the squares of the odd numbers in the range from 1 to 10. Any sequence that supports iteration can be used within a list comprehension to construct a new list.

::

    >>>[letra.upper() for letra in 'estructuras' if letra not in 'aeiou']
    ['S', 'T', 'R', 'C', 'T', 'R', 'S']
    >>>

.. admonition:: Autoevaluación

    Compruebe si entendió las comprensiones de listas utilizando dicha estrategia para rehacer el programa intro_8.
    Como un desafío adicional, intente averiguar cómo eliminar las duplicaciones.

    .. activecode:: auto_eval_2

       # la respuesta es: ['g', 'a', 't', 'o', 'p', 'e', 'r', 'r', 'o', 'c', 'o', 'n', 'e', 'j', 'o']


