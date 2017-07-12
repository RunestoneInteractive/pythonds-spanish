..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Símbolos balanceados (Un caso general)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

El problema de paréntesis balanceados mostrado anteriormente es un caso específico de una situación más general que surge en muchos lenguajes de programación. El problema general de balancear y anidar diferentes tipos de símbolos de apertura y cierre ocurre con frecuencia. Por ejemplo, en Python, los corchetes, ``[`` y ``]``, se utilizan para las listas; las llaves, ``{`` y ``}``, se utilizan para los diccionarios; y los paréntesis, ``(`` y ``)``, se utilizan para las tuplas y las expresiones aritméticas. Es posible mezclar símbolos siempre y cuando cada uno mantenga su propia relación de apertura y cierre. Cadenas de símbolos como

.. The balanced parentheses problem shown above is a specific case of a more general situation that arises in many programming languages. The general problem of balancing and nesting different kinds of opening and closing symbols occurs frequently. For example, in Python square brackets, ``[`` and ``]``, are used for lists; curly braces, ``{`` and ``}``, are used for dictionaries; and parentheses, ``(`` and ``)``, are used for tuples and arithmetic expressions. It is possible to mix symbols as long as each maintains its own open and close relationship. Strings of symbols such as

::

    { { ( [ ] [ ] ) } ( ) }

    [ [ { { ( ( ) ) } } ] ]

    [ ] [ ] [ ] ( ) { }

están adecuadamente balanceados puesto que no sólo cada símbolo de apertura tiene un símbolo de cierre correspondiente, sino que los tipos de símbolos también coinciden.

.. are properly balanced in that not only does each opening symbol have a corresponding closing symbol, but the types of symbols match as well.

Compare aquellos con las siguientes cadenas que no están balanceadas:

.. Compare those with the following strings that are not balanced:

::

    ( [ ) ]

    ( ( ( ) ] ) )

    [ { ( ) ]

El verificador de paréntesis simples de la sección anterior se puede ampliar fácilmente para manejar estos nuevos tipos de símbolos. Recuerde que cada símbolo de apertura simplemente se incluye en la pila para esperar que el símbolo de cierre coincidente aparezca más adelante en la secuencia. Cuando aparece un símbolo de cierre, la única diferencia es que debemos comprobar que coincide correctamente con el tipo del símbolo de apertura en el tope de la pila. Si los dos símbolos no coinciden, la cadena no está balanceada. Una vez más, si toda la cadena es procesada y no queda nada en la pila, la cadena está correctamente balanceada.

.. The simple parentheses checker from the previous section can easily be extended to handle these new types of symbols. Recall that each opening symbol is simply pushed on the stack to wait for the matching closing symbol to appear later in the sequence. When a closing symbol does appear, the only difference is that we must check to be sure that it correctly matches the type of the opening symbol on top of the stack. If the two symbols do not match, the string is not balanced. Once again, if the entire string is processed and nothing is left on the stack, the string is correctly balanced.

El programa en Python para implementar esto se muestra en el :ref:`ActiveCode 1 <lst_parcheck2>`. El único cambio aparece en la línea 16 donde llamamos una función auxiliar, ``parejas``, para ayudar con la verificación de los símbolos. Cada símbolo que se extrae de la pila se debe comprobar para ver si coincide con el símbolo de cierre actual. Si no hay coincidencia, la variable booleana ``balancedos`` se pone en ``False``.

.. The Python program to implement this is shown in :ref:`ActiveCode 1 <lst_parcheck2>`. The only change appears in line 16 where we call a helper function, ``matches``, to assist with symbol-matching. Each symbol that is removed from the stack must be checked to see that it matches the current closing symbol. If a mismatch occurs, the boolean variable ``balanced`` is set to ``False``.

.. _lst_parcheck2:

.. activecode :: parcheck2
   :caption: Solución del problema general de símbolos balanceados
   :nocodelens:

   from pythoned.basicas.pila import Pila
   
   def verificarSimbolos(cadenaSimbolos):
       p = Pila()
       balanceados = True
       indice = 0
       while indice < len(cadenaSimbolos) and balanceados:
           simbolo = cadenaSimbolos[indice]
           if simbolo in "([{":
               p.incluir(simbolo)
           else:
               if p.estaVacia():
                   balanceados = False
               else:
                   tope = p.extraer()
                   if not parejas(tope,simbolo):
                          balanceados = False
           indice = indice + 1
       if balanceados and p.estaVacia():
           return True
       else:
           return False

   def parejas(simboloApertura, simboloCierre):
       aperturas = "([{"
       cierres = ")]}"
       return aperturas.index(simboloApertura) == cierres.index(simboloCierre)
       

   print(verificarSimbolos('{{([][])}()}'))
   print(verificarSimbolos('[{()]'))

Estos dos ejemplos muestran que las pilas son estructuras de datos muy importantes para el procesamiento de instrucciones de lenguajes en ciencias de la computación. Casi cualquier notación que usted se pueda imaginar tiene algún tipo de símbolo anidado que debe coincidir en un orden balanceado. Hay una serie de otros usos importantes para las pilas en ciencias de la computación. Seguiremos explorándolos en las próximas secciones.

.. These two examples show that stacks are very important data structures for the processing of language constructs in computer science. Almost any notation you can think of has some type of nested symbol that must be matched in a balanced order. There are a number of other important uses for stacks in computer science. We will continue to explore them in the next sections.
