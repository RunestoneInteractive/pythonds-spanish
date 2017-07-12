..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Entrada y salida
~~~~~~~~~~~~~~~~

A menudo tenemos la necesidad de interactuar con los usuarios, ya sea para obtener datos o para proporcionar algún tipo de resultado. La mayoría de los programas de hoy en día utilizan un cuadro de diálogo como una forma de pedir al usuario que proporcione algún tipo de entrada. Aunque Python tiene una forma de crear cuadros de diálogo, hay una función mucho más sencilla que podemos usar. Python nos brinda una función que nos permite pedirle a un usuario que introduzca algunos datos y devuelve una referencia a ellos en forma de cadena. La función se llama ``input``.

.. We often have a need to interact with users, either to get data or to provide some sort of result. Most programs today use a dialog box as a way of asking the user to provide some type of input. While Python does have a way to create dialog boxes, there is a much simpler function that we can use. Python provides us with a function that allows us to ask a user to enter some data and returns a reference to the data in the form of a string. The function is called ``input``.

La función de entrada de Python toma un solo parámetro que es una cadena. Esta cadena a menudo se denomina **prompt** porque contiene algún texto útil que le pide al usuario que introduzca algo. Por ejemplo, usted puede invocar a ``input`` de la siguiente manera:

.. Python’s input function takes a single parameter that is a string. This string is often called the **prompt** because it contains some helpful text prompting the user to enter something. For example, you might call input as follows:

::

    unNombre = input('Por favor ingrese su nombre: ')

Ahora todo lo que el usuario digite después del prompt se almacenará en la variable ``unNombre``. Usando la función ``input``, podemos escribir fácilmente instrucciones que le pedirán al usuario que ingrese datos y luego incorporarán esos datos a otro procesamiento. Por ejemplo, en las siguientes dos declaraciones, la primera pregunta al usuario por su nombre y la segunda imprime el resultado de algún procesamiento simple basado en la cadena que se proporciona.

.. Now whatever the user types after the prompt will be stored in the ``aName`` variable. Using the input function, we can easily write instructions that will prompt the user to enter data and then incorporate that data into further processing. For example, in the following two statements, the first asks the user for their name and the second prints the result of some simple processing based on the string that is provided.

.. activecode::  strstuff
    :caption: La función input devuelve una cadena

    unNombre = input("Por favor ingrese se nombre ")
    print("Su nombre en mayúsculas es ",unNombre.upper(),
          "y tiene longitud ", len(unNombre))

Es importante tener en cuenta que el valor devuelto por la función ``input`` será una cadena que representa los caracteres exactos que se ingresaron después de la solicitud. Si usted desea que esta cadena sea interpretada como otro tipo, debe indicar la conversión de tipo de forma explícita. En las instrucciones siguientes, la cadena que es introducida por el usuario se convierte a flotante para que pueda utilizarse en otro procesamiento aritmético.

.. It is important to note that the value returned from the ``input`` function will be a string representing the exact characters that were entered after the prompt. If you want this string interpreted as another type, you must provide the type conversion explicitly. In the statements below, the string that is entered by the user is converted to a float so that it can be used in further arithmetic processing.

::

    cadenaRadio = input("Por favor introduzca el radio del círculo ")
    radio = float(cadenaRadio)
    diametro = 2 * radio

Formato de cadenas
^^^^^^^^^^^^^^^^^^

Ya hemos visto que la función ``print`` proporciona una forma muy sencilla de imprimir en pantalla los valores de un programa de Python. ``print`` toma cero o más parámetros y los muestra usando un espacio en blanco como el separador predeterminado. Es posible cambiar el carácter de separación mediante el ajuste del argumento ``sep``. Además, cada impresión finaliza, por defecto, con un carácter de nueva línea. Este comportamiento se puede cambiar ajustando el argumento ``end``. Estas variaciones se muestran en la siguiente sesión:

.. We have already seen that the ``print`` function provides a very simple way to output values from a Python program. ``print`` takes zero or more parameters and displays them using a single blank as the default separator. It is possible to change the separator character by setting the ``sep`` argument. In addition, each print ends with a newline character by default. This behavior can be changed by setting the ``end`` argument. These variations are shown in the following session:

::

    >>> print("Hola")
    Hola
    >>> print("Hola","Mundo")
    Hola Mundo
    >>> print("Hola","Mundo", sep="***")
    Hola***Mundo
    >>> print("Hola","Mundo", end="***")
    Hola Mundo***>>>

A menudo es útil tener más control sobre la apariencia de su salida. Afortunadamente, Python nos proporciona una alternativa llamada **cadenas formateadas**. Una cadena formateada es una plantilla en la que las palabras o espacios que permanecen constantes se combinan con marcadores de posición para las variables que se insertarán en la cadena. Por ejemplo, la declaración

.. It is often useful to have more control over the look of your output. Fortunately, Python provides us with an alternative called **formatted strings**. A formatted string is a template in which words or spaces that will remain constant are combined with placeholders for variables that will be inserted into the string. For example, the statement

::

    print(unNombre, "tiene", edad, "años de edad.")

Contiene las palabras ``tiene`` y ``años de edad``, pero el nombre y la edad cambiarán dependiendo de los valores de las variables en el momento de la ejecución. Usando una cadena formateada, escribimos la declaración anterior como

.. contains the words ``tiene`` and ``años de edad``, but the name and the age will change depending on the variable values at the time of execution. Using a formatted string, we write the previous statement as

::

    print("%s tiene %d años de edad." % (unNombre, edad))

Este ejemplo sencillo ilustra una nueva expresión de cadenas. El operador ``%`` es un operador de cadena llamado **operador de formato**. El lado izquierdo de la expresión contiene la plantilla o cadena de formato y el lado derecho contiene una colección de valores que se sustituirá en la cadena de formato. Note que el número de valores en la colección del lado derecho corresponde con el número de caracteres ``%`` en la cadena de formato. Los valores se toman en orden, de izquierda a derecha de la colección y se insertan en la cadena de formato.

.. This simple example illustrates a new string expression. The ``%`` operator is a string operator called the **format operator**. The left side of the expression holds the template or format string, and the right side holds a collection of values that will be substituted into the format string. Note that the number of values in the collection on the right side corresponds with the number of ``%`` characters in the format string. Values are taken—in order, left to right—from the collection and inserted into the format string.

Demos un vistazo a ambos lados de esta expresión de formato con más detalle. La cadena de formato puede contener una o más especificaciones de conversión. Un carácter de conversión le dice al operador de formato qué tipo de valor va a ser insertado en esa posición en la cadena. En el ejemplo anterior, el ``%s`` especifica una cadena, mientras que el ``%d`` especifica un entero. Otras posibles especificaciones de tipo son ``i``, ``u``, ``f``, ``e``, ``g``, ``c``, o ``%``. La :ref:`Tabla 9 <tab_fmta>` resume todas las especificaciones de los distintos tipos.

.. Let’s look at both sides of this formatting expression in more detail. The format string may contain one or more conversion specifications. A conversion character tells the format operator what type of value is going to be inserted into that position in the string. In the example above, the ``%s`` specifies a string, while the ``%d`` specifies an integer. Other possible type specifications include ``i``, ``u``, ``f``, ``e``, ``g``, ``c``, or ``%``. :ref:`Table 9 <tab_fmta>` summarizes all of the various type specifications.

.. _tab_fmta:

.. table:: **Tabla 9: Caracteres de conversión de formato de cadenas**

    ========================== ==========================================================================================================
                  **Carácter**                                                                                      **Formato de salida**
    ========================== ==========================================================================================================
                  ``d``, ``i``                                                                                                     Entero
                         ``u``                                                                                           Entero sin signo
                         ``f``                                                                                Punto flotante como m.ddddd
                         ``e``                                                                          Punto flotante como m.ddddde+/-xx
                         ``E``                                                                          Punto flotante como m.dddddE+/-xx
                         ``g``     Usa ``%e`` para exponentes menores que :math:`-4` o mayores que :math:`+5`, de lo contrario usa ``%f``
                         ``c``                                                                                             Carácter único
                         ``s`` Cadena o cualquier objeto de datos de Python que pueda convertirse a una cadena usando la función ``str``.
                         ``%``                                                                              Inserta un carácter % literal
    ========================== ==========================================================================================================

Además del carácter de formato, usted también puede incluir un modificador de formato entre el ``%`` y el carácter de formato. Los modificadores de formato se pueden utilizar para justificar el valor a la izquierda o a la derecha con un ancho de campo especificado. Los modificadores también se pueden utilizar para especificar el ancho del campo junto con un número de dígitos después del punto decimal. La :ref:`Tabla 10 <tab_fmtaddsa>` explica estos modificadores de formato.

.. In addition to the format character, you can also include a format modifier between the ``%`` and the format character. Format modifiers may be used to left-justify or right-justifiy the value with a specified field width. Modifiers can also be used to specify the field width along with a number of digits after the decimal point. :ref:`Table 10 <tab_fmtaddsa>` explains these format modifiers

.. _tab_fmtaddsa:

.. table:: **Tabla 10: Opciones de formato adicionales**

    ========================= =============== ===================================================================================================
              **Modificador**     **Ejemplo**                                                                                    **Descripción**
    ========================= =============== ===================================================================================================
                       número        ``%20d``                                                         Pone el valor en una anchura de campo de 20
                        ``-``       ``%-20d``                     Pone el valor en un campo de 20 caracteres de ancho, justificado a la izquierda
                        ``+``       ``%+20d``                       Pone el valor en un campo de 20 caracteres de ancho, justificado a la derecha
                        ``0``       ``%020d``            Pone el valor en un campo de 20 caracteres de ancho, rellenando con ceros a la izquierda
                        ``.``      ``%20.2f`` Pone el valor en un campo de 20 caracteres de ancho con 2 caracteres a la derecha del punto decimal
                 ``(nombre)``  ``%(nombre)d``                          Obtiene el valor del diccionario suministrado usando ``nombre`` como clave
    ========================= =============== ===================================================================================================

El lado derecho del operador de formato es una colección de valores que se insertarán en la cadena de formato. La colección será una tupla o un diccionario. Si la colección es una tupla, los valores se insertan en el orden de la posición. Es decir, el primer elemento de la tupla corresponde al primer carácter de formato en la cadena de formato. Si la colección es un diccionario, los valores se insertan de acuerdo con sus claves. En este caso, todos los caracteres de formato deben utilizar el modificador ``(nombre)`` para especificar el nombre de la clave.

.. The right side of the format operator is a collection of values that will be inserted into the format string. The collection will be either a tuple or a dictionary. If the collection is a tuple, the values are inserted in order of position. That is, the first element in the tuple corresponds to the first format character in the format string. If the collection is a dictionary, the values are inserted according to their keys. In this case all format characters must use the ``(name)`` modifier to specify the name of the key.

::

    >>> precio = 24
    >>> item = "banano"
    >>> print("El %s cuesta %d centavos"%(item,precio))
    El banano cuesta 24 centavos
    >>> print("El %+10s cuesta %5.2f centavos"%(item,precio))
    El     banano cuesta 24.00 centavos
    >>> print("El %+10s cuesta %10.2f centavos"%(item,precio))
    El     banano cuesta      24.00 centavos
    >>> diccitem = {"item":"banano","costo":24}
    >>> print("El %(item)s cuesta %(costo)7.1f centavos"%diccitem)
    El banano cuesta    24.0 centavos
    >>>

Además de las cadenas de formato que utilizan caracteres de formato y modificadores de formato, las cadenas de Python también incluyen un método ``format`` que se puede usar junto con una nueva clase ``Formatter`` para implementar formateos complejos de cadenas. En el manual de referencia de la biblioteca de Python se puede encontrar más información sobre estas características.

.. In addition to format strings that use format characters and format modifiers, Python strings also include a ``format`` method that can be used in conjunction with a new ``Formatter`` class to implement complex string formatting. More about these features can be found in the Python library reference manual.

