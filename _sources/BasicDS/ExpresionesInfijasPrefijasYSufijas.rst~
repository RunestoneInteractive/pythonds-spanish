..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Expresiones en notaciones infija, prefija y sufija
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cuando usted escribe una expresión aritmética como B \* C, la forma de la expresión le proporciona información para que pueda interpretarla correctamente. En este caso sabemos que la variable B está siendo multiplicada por la variable C, ya que el operador de multiplicación \* aparece entre ellos en la expresión. Este tipo de notación se conoce como **infija** ya que el operador está *entre* los dos operandos sobre los que está actuando.

.. When you write an arithmetic expression such as B \* C, the form of the expression provides you with information so that you can interpret it correctly. In this case we know that the variable B is being multiplied by the variable C since the multiplication operator \* appears between them in the expression. This type of notation is referred to as **infix** since the operator is *in between* the two operands that it is working on.

Considere otro ejemplo de notación infija, A + B \* C. Los operadores + y \* siguen apareciendo entre los operandos, pero hay un problema. ¿Sobre qué operandos actúan? ¿Opera el + sobre A y B o el \* opera sobre B y C? La expresión parece ambigua.

.. Consider another infix example, A + B \* C. The operators + and \* still appear between the operands, but there is a problem. Which operands do they work on? Does the + work on A and B or does the \* take B and C? The expression seems ambiguous.

De hecho, usted ha estado leyendo y escribiendo estos tipos de expresiones durante mucho tiempo y no le causan ningún problema. La razón de esto es que usted sabe algo sobre los operadores + y \*. Cada operador tiene un nivel de **precedencia**. Los operadores de mayor precedencia se utilizan antes que los operadores de menor precedencia. Lo único que puede cambiar ese orden es la presencia de paréntesis. El orden de precedencia para los operadores aritméticos ubica la multiplicación y la división por encima de la suma y la resta. Si aparecen dos operadores de igual precedencia, se utiliza un ordenamiento o asociatividad de izquierda a derecha.

.. In fact, you have been reading and writing these types of expressions for a long time and they do not cause you any problem. The reason for this is that you know something about the operators + and \*. Each operator has a **precedence** level. Operators of higher precedence are used before operators of lower precedence. The only thing that can change that order is the presence of parentheses. The precedence order for arithmetic operators places multiplication and division above addition and subtraction. If two operators of equal precedence appear, then a left-to-right ordering or associativity is used.

Interpretemos la expresión problemática A + B \* C usando la precedencia de los operadores. B y C se multiplican primero y A se añade a ese resultado. (A + B) \* C forzaría la suma de A y B antes de la multiplicación. En la expresión A + B + C, por precedencia (vía asociatividad), el + que está más a la izquierda operaría primero.

.. Let’s interpret the troublesome expression A + B \* C using operator precedence. B and C are multiplied first, and A is then added to that result. (A + B) \* C would force the addition of A and B to be done first before the multiplication. In expression A + B + C, by precedence (via associativity), the leftmost + would be done first.

Aunque todo esto puede ser obvio para usted, recuerde que las computadoras necesitan saber exactamente qué operadores deben ejecutarse y en qué orden. Una forma de escribir una expresión que garantice que no habrá confusión con respecto al orden de las operaciones es crear lo que se denomina expresión **completamente agrupada**. Este tipo de expresión utiliza una pareja de paréntesis para cada operador. Los paréntesis dictan el orden de las operaciones; no hay ambigüedad. Tampoco es necesario recordar las reglas de precedencia.

.. Although all this may be obvious to you, remember that computers need to know exactly what operators to perform and in what order. One way to write an expression that guarantees there will be no confusion with respect to the order of operations is to create what is called a **fully parenthesized** expression. This type of expression uses one pair of parentheses for each operator. The parentheses dictate the order of operations; there is no ambiguity. There is also no need to remember any precedence rules.

La expresión A + B \* C + D se puede reescribir como ((A + (B \* C)) + D) para mostrar que la multiplicación ocurre primero, seguida por la adición que está más a la izquierda. A + B + C + D se puede escribir como ((A + B) + C) + D) ya que las operaciones de adición se asocian de izquierda a derecha.

.. The expression A + B \* C + D can be rewritten as ((A + (B \* C)) + D) to show that the multiplication happens first, followed by the leftmost addition. A + B + C + D can be written as (((A + B) + C) + D) since the addition operations associate from left to right.

Hay otros dos formatos de expresión muy importantes que, al principio, pueden no parecer obvios. Considere la expresión infija A + B. ¿Qué pasaría si moviéramos el operador antes de los dos operandos? La expresión resultante sería + A B. Del mismo modo, podríamos mover el operador al final. Obtendríamos A B +. Estas expresiones se ven un poco extrañas.

.. There are two other very important expression formats that may not seem obvious to you at first. Consider the infix expression A + B. What would happen if we moved the operator before the two operands? The resulting expression would be + A B. Likewise, we could move the operator to the end. We would get A B +. These look a bit strange.

Estos cambios en la posición del operador con respecto a los operandos crean dos nuevos formatos de expresión, la **notación prefija** y la **notación sufija (o postfija)**. La notación prefija requiere que todos los operadores precedan a los dos operandos sobre los que actúan. La notación sufija, por otro lado, requiere que sus operadores aparezcan después de los operandos correspondientes. Algunos ejemplos más deberían ayudar a hacer esto un poco más claro (ver la :ref:`Tabla 2 <tbl_example1>`).

.. These changes to the position of the operator with respect to the operands create two new expression formats, **prefix** and **postfix**. Prefix expression notation requires that all operators precede the two operands that they work on. Postfix, on the other hand, requires that its operators come after the corresponding operands. A few more examples should help to make this a bit clearer (see :ref:`Table 2 <tbl_example1>`).

A + B \* C se escribiría como + A \* B C en la notación prefija. El operador de multiplicación aparece inmediatamente antes de los operandos B y C, denotando que el \* tiene precedencia sobre el +. El operador de adición aparece entonces antes de la A y del resultado de la multiplicación.

.. A + B \* C would be written as + A \* B C in prefix. The multiplication operator comes immediately before the operands B and C, denoting that \* has precedence over +. The addition operator then appears before the A and the result of the multiplication.

En notación sufija, la expresión sería A B C \* +. Una vez más, el orden de las operaciones se conserva ya que el \* aparece inmediatamente después de la B y la C, denotando que el \* tiene precedencia, con el + apareciendo después. Aunque los operadores se movieron y ahora aparecen antes o después de sus respectivos operandos, el orden de cada operando se mantuvo exactamente igual en relación con los demás.

.. In postfix, the expression would be A B C \* +. Again, the order of operations is preserved since the \* appears immediately after the B and the C, denoting that \* has precedence, with + coming after. Although the operators moved and now appear either before or after their respective operands, the order of the operands stayed exactly the same relative to one another.

.. _tbl_example1:

.. table:: **Tabla 2: Ejemplos en notación infija, prefija y sufija**

    ============================ ======================= ========================
            **Expresión infija**   **Expresión prefija**     **Expresión sufija**
    ============================ ======================= ========================
                           A + B                  \+ A B                    A B +
                      A + B \* C             \+ A \* B C               A B C \* +
    ============================ ======================= ========================


Ahora considere la expresión infija (A + B) \* C. Recuerde que en este caso, la notación infija requiere los paréntesis para forzar que se lleve a cabo la adición antes de la multiplicación. Sin embargo, cuando A + B fue escrito en notación prefija, el operador de adición fue movido simplemente antes de los operandos, + A B. El resultado de esta operación se convierte en el primer operando para la multiplicación. El operador de multiplicación se mueve delante de toda la expresión, dándonos \* + A B C. Igualmente, en notación sufija A B + obliga a que la adición ocurra primero. La multiplicación se puede hacer sobre ese resultado y el operando restante C. La expresión sufija correcta es entonces A B + C \*.

.. Now consider the infix expression (A + B) \* C. Recall that in this case, infix requires the parentheses to force the performance of the addition before the multiplication. However, when A + B was written in prefix, the addition operator was simply moved before the operands, + A B. The result of this operation becomes the first operand for the multiplication. The multiplication operator is moved in front of the entire expression, giving us \* + A B C. Likewise, in postfix A B + forces the addition to happen first. The multiplication can be done to that result and the remaining operand C. The proper postfix expression is then A B + C \*.

Considere nuevamente estas tres expresiones (ver la :ref:`Tabla 3 <tbl_parexample>`). Ha ocurrido algo muy importante. ¿A dónde se fueron los paréntesis? ¿Por qué no los necesitamos en las notaciones prefija y sufija? La respuesta es que los operadores ya no son ambiguos con respecto a los operandos sobre los que actúan. Solamente la notación infija requiere los símbolos adicionales. El orden de las operaciones dentro de las expresiones prefijas y sufijas está completamente determinado por la posición del operador y nada más. De muchas maneras, esto hace que la notación infija sea la notación menos deseable de usar.

.. Consider these three expressions again (see :ref:`Table 3 <tbl_parexample>`). Something very important has happened. Where did the parentheses go? Why don’t we need them in prefix and postfix? The answer is that the operators are no longer ambiguous with respect to the operands that they work on. Only infix notation requires the additional symbols. The order of operations within prefix and postfix expressions is completely determined by the position of the operator and nothing else. In many ways, this makes infix the least desirable notation to use.

.. _tbl_parexample:

.. table:: **Tabla 3: Una expresión con paréntesis**

    ============================ ======================= ========================
            **Expresión infija**   **Expresión prefija**     **Expresión sufija**
    ============================ ======================= ========================
                    (A + B) \* C              \* + A B C               A B + C \*
    ============================ ======================= ========================


La :ref:`Tabla 4 <tbl_example3>` muestra algunos ejemplos adicionales de expresiones infijas y las expresiones equivalentes en notaciones prefija y sufija. Asegúrese de entender cómo son equivalentes en términos del orden de las operaciones que se están realizando.

.. :ref:`Table 4 <tbl_example3>` shows some additional examples of infix expressions and the equivalent prefix and postfix expressions. Be sure that you understand how they are equivalent in terms of the order of the operations being performed.

.. _tbl_example3:

.. table:: **Tabla 4: Ejemplos adicionales en notaciones infija, prefija y sufija**

    ============================ ======================= ========================
            **Expresión infija**   **Expresión prefija**     **Expresión sufija**
    ============================ ======================= ========================
                  A + B \* C + D        \+ \+ A \* B C D           A B C \* + D +
              (A + B) \* (C + D)          \* + A B + C D           A B + C D + \*
                 A \* B + C \* D        \+ \* A B \* C D          A B \* C D \* +
                   A + B + C + D          \+ + + A B C D            A B + C + D +
    ============================ ======================= ========================


Conversión de expresiones infijas a notaciones prefija y sufija
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Hasta el momento, hemos utilizado métodos ad hoc para convertir entre expresiones infijas y las expresiones equivalentes en notaciones prefija y sufija. Como es de esperar, hay formas algorítmicas para realizar la conversión que permiten transformar correctamente cualquier expresión de cualquier complejidad.

.. So far, we have used ad hoc methods to convert between infix expressions and the equivalent prefix and postfix expression notations. As you might expect, there are algorithmic ways to perform the conversion that allow any expression of any complexity to be correctly transformed.

La primera técnica que vamos a considerar utiliza la noción de una expresión completamente agrupada que se discutió anteriormente. Recordemos que A + B \* C se puede escribir como (A + (B \* C)) para mostrar explícitamente que la multiplicación tiene precedencia sobre la adición. Sin embargo, al observar más de cerca, puede verse que cada pareja de paréntesis también indica el comienzo y el final de un par de operandos con el operador correspondiente en la mitad.

.. The first technique that we will consider uses the notion of a fully parenthesized expression that was discussed earlier. Recall that A + B \* C can be written as (A + (B \* C)) to show explicitly that the multiplication has precedence over the addition. On closer observation, however, you can see that each parenthesis pair also denotes the beginning and the end of an operand pair with the corresponding operator in the middle.

Observe el paréntesis derecho en la subexpresión (B \* C) anterior. Si tuviéramos que mover el símbolo de multiplicación a esa posición y quitar el paréntesis izquierdo correspondiente, nos daría B C \*, de hecho habríamos convertido la subexpresión a notación sufija. Si el operador de adición también es movido a la posición de su paréntesis derecho correspondiente y se elimina el paréntesis izquierdo que le corresponde, se produciría la expresión sufija completa (ver la :ref:`Figura 6 <fig_moveright>`).

.. Look at the right parenthesis in the subexpression (B \* C) above. If we were to move the multiplication symbol to that position and remove the matching left parenthesis, giving us B C \*, we would in effect have converted the subexpression to postfix notation. If the addition operator were also moved to its corresponding right parenthesis position and the matching left parenthesis were removed, the complete postfix expression would result (see :ref:`Figure 6 <fig_moveright>`).

.. _fig_moveright:

.. figure:: Figures/moveright.png
   :align: center

   Figura 6: Traslado de operadores a la derecha para producir la notación sufija

   Figura 6: Traslado de operadores a la derecha para producir la notación sufija

Si hacemos lo mismo pero en lugar de mover el símbolo a la posición del paréntesis derecho, lo movemos a la izquierda, obtenemos la notación prefija (ver la :ref:`Figura 7 <fig_moveleft>`). La posición de la pareja de paréntesis es en realidad una pista sobre la posición final del operador encerrado entre ellos.

.. If we do the same thing but instead of moving the symbol to the position of the right parenthesis, we move it to the left, we get prefix notation (see :ref:`Figure 7 <fig_moveleft>`). The position of the parenthesis pair is actually a clue to the final position of the enclosed operator.

.. _fig_moveleft:

.. figure:: Figures/moveleft.png
   :align: center

   Figura 7: Traslado de operadores a la izquierda para producir la notación prefija

   Figura 7: Traslado de operadores a la izquierda para producir la notación prefija

Así que, para convertir una expresión, independientemente de su complejidad, ya sea a notación prefija o a notación sufija, agrúpela completamente utilizando el orden de las operaciones. A continuación, mueva cada operador a la posición correspondiente de los paréntesis izquierdo o derecho dependiendo de si desea obtener la expresión en notación prefija o en notación sufija.

.. So in order to convert an expression, no matter how complex, to either prefix or postfix notation, fully parenthesize the expression using the order of operations. Then move the enclosed operator to the position of either the left or the right parenthesis depending on whether you want prefix or postfix notation.

La siguiente es una expresión más compleja: (A + B) \* C - (D - E) \* (F + G). La :ref:`Figura 8 <fig_complexmove>` muestra la conversión a las notaciones sufija y prefija.

.. Here is a more complex expression: (A + B) \* C - (D - E) \* (F + G). :ref:`Figure 8 <fig_complexmove>` shows the conversion to postfix and prefix notations.

.. _fig_complexmove:

.. figure:: Figures/complexmove.png
   :align: center

   Figura 8: Conversión de una expresión compleja a notaciones prefija y sufija

   Figura 8: Conversión de una expresión compleja a notaciones prefija y sufija

Conversión general de notación infija a notación sufija
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Necesitamos desarrollar un algoritmo para convertir cualquier expresión infija a una expresión sufija. Para hacer esto vamos a examinar más de cerca el proceso de conversión.

.. We need to develop an algorithm to convert any infix expression to a postfix expression. To do this we will look closer at the conversion process.

Consideremos una vez más la expresión A + B \* C. Como se muestra arriba, A B C \* + es la equivalencia en notación sufija. Ya hemos observado que los operandos A, B y C permanecen en sus posiciones relativas. Sólo los operadores cambian de posición. Veamos de nuevo los operadores en la expresión infija. El primer operador que aparece de izquierda a derecha es el +. Sin embargo, en la expresión sufija, el + está al final dado que el siguiente operador, \*, tiene precedencia sobre la adición. El orden de los operadores en la expresión original se invierte en la expresión sufija resultante.

.. Consider once again the expression A + B \* C. As shown above, A B C \* + is the postfix equivalent. We have already noted that the operands A, B, and C stay in their relative positions. It is only the operators that change position. Let’s look again at the operators in the infix expression. The first operator that appears from left to right is +. However, in the postfix expression, + is at the end since the next operator, \*, has precedence over addition. The order of the operators in the original expression is reversed in the resulting postfix expression.

A medida que procesamos la expresión, los operadores tienen que ser guardados en alguna parte, ya que sus operandos derechos correspondientes no aparecen todavía. También, el orden de estos operadores guardados puede necesitar ser invertido debido a su precedencia. Ése es el caso con la adición y la multiplicación en este ejemplo. Dado que el operador de adición aparece antes del operador de multiplicación y tiene menor precedencia, necesita aparecer después de que se use el operador de multiplicación. Debido a esta inversión del orden, tiene sentido considerar el uso de una pila para almacenar a los operadores hasta que se necesiten.

.. As we process the expression, the operators have to be saved somewhere since their corresponding right operands are not seen yet. Also, the order of these saved operators may need to be reversed due to their precedence. This is the case with the addition and the multiplication in this example. Since the addition operator comes before the multiplication operator and has lower precedence, it needs to appear after the multiplication operator is used. Because of this reversal of order, it makes sense to consider using a stack to keep the operators until they are needed.

Y ¿qué ocurrirá con (A + B) \* C? Recuerde que A B + C \* es la equivalencia en notación sufija. De nuevo, procesando esta expresión infija de izquierda a derecha, vemos primero el +. En este caso, cuando vemos el \*, el + ya se ha transcrito en la expresión de resultado porque tiene precedencia sobre el \* en virtud de los paréntesis. Ahora podemos empezar a ver cómo funcionará el algoritmo de conversión. Cuando veamos un paréntesis izquierdo, lo guardaremos para indicar que habrá otro operador de alta precedencia. Ese operador tendrá que esperar hasta que aparezca el paréntesis derecho correspondiente para indicar su posición (recuerde la técnica de agrupar completamente). Cuando aparezca ese paréntesis derecho, el operador puede ser extraído de la pila.

.. What about (A + B) \* C? Recall that A B + C \* is the postfix equivalent. Again, processing this infix expression from left to right, we see + first. In this case, when we see \*, + has already been placed in the result expression because it has precedence over \* by virtue of the parentheses. We can now start to see how the conversion algorithm will work. When we see a left parenthesis, we will save it to denote that another operator of high precedence will be coming. That operator will need to wait until the corresponding right parenthesis appears to denote its position (recall the fully parenthesized technique). When that right parenthesis does appear, the operator can be popped from the stack.

Al recorrer la expresión infija de izquierda a derecha, usaremos una pila para almacenar los operadores. Esto proporcionará la inversión que hemos observado en el primer ejemplo. El tope de la pila siempre será el operador guardado más recientemente. Siempre que leamos a un operador nuevo, tendremos que comparar la precedencia de ese operador con la de los operadores que ya estén en la pila, si los hay.

.. As we scan the infix expression from left to right, we will use a stack to keep the operators. This will provide the reversal that we noted in the first example. The top of the stack will always be the most recently saved operator. Whenever we read a new operator, we will need to consider how that operator compares in precedence with the operators, if any, already on the stack.

Suponga que la expresión infija es una cadena de símbolos delimitados por espacios. Los símbolos de operaciones son \*, /, + y -, junto con los paréntesis izquierdo y derecho, ( y ). Los símbolos de operandos son los identificadores de un solo carácter A, B, C, y así sucesivamente. Los siguientes pasos producirán una cadena de símbolos en el orden sufijo.

.. Assume the infix expression is a string of tokens delimited by spaces. The operator tokens are \*, /, +, and -, along with the left and right parentheses, ( and ). The operand tokens are the single-character identifiers A, B, C, and so on. The following steps will produce a string of tokens in postfix order.

#. Crear una pila vacía llamada ``pilaOperadores`` para almacenar los operadores.
   Crear una lista vacía para almacenar la salida.

#. Corvertir la cadena de entrada de notación infija a una lista, usando el método ``split``.

#. Recorrer la lista de símbolos de izquierda a derecha:

   -  Si el símbolo es un operando, agregarlo al final de la lista de salida.

   -  Si el símbolo es un paréntesis izquierdo, enviarlo a ``pilaOperadores``.

   -  Si el símbolo es un paréntesis derecho, extraer de ``pilaOperadores`` hasta que el correspondiente paréntesis izquierdo se haya extraído. Agregar cada operador al final de la lista de salida.

   -  Si el símbolo es un operador \*, /, +, ó -, incluirlo en ``pilaOperadores``. No obstante, extraer previamente de la pila los operadores que tengan mayor o igual precedencia y agregarlos a la lista de salida.

#. Cuando la expresión de entrada ha sido procesada completamente, verificar ``pilaOperadores``. Todos los operadores que aún estén almacenados en ella se deben enviar a la lista de salida.

La :ref:`Figura 9 <fig_intopost>` muestra el algoritmo de conversión trabajando sobre la expresión A \* B + C \* D. Observe que el primer operador \* se elimina al verse el operador +. Además, el + permanece en la pila cuando aparece el segundo \*, ya que la multiplicación tiene precedencia sobre la adición. Al final de la expresión infija, se extrae dos veces de la pila, eliminando ambos operadores y colocando el + como el último operador en la expresión sufija.

.. :ref:`Figure 9 <fig_intopost>` shows the conversion algorithm working on the expression A \* B + C \* D. Note that the first \* operator is removed upon seeing the + operator. Also, + stays on the stack when the second \* occurs, since multiplication has precedence over addition. At the end of the infix expression the stack is popped twice, removing both operators and placing + as the last operator in the postfix expression.

.. _fig_intopost:

.. figure:: Figures/intopost.png
   :align: center

   Figura 9: Conversión de A \* B + C \* D a notación sufija

   Figura 9: Conversión de A \* B + C \* D a notación sufija

Para codificar el algoritmo en Python, usaremos un diccionario llamado ``precedencia`` para almacenar los valores de precedencia para los operadores. Este diccionario mapeará cada operador a un entero que se pueda comparar con los niveles de precedencia de otros operadores (hemos utilizado arbitrariamente los números enteros 3, 2 y 1). El paréntesis izquierdo recibirá el valor más bajo posible. De esta manera cualquier operador que se compara con él tendrá mayor precedencia y se colocará encima de él. La línea 15 define los operandos como cualquier carácter en mayúsculas o dígito. La función de conversión completa se muestra en el :ref:`ActiveCode 1 <lst_intopost>`.

.. In order to code the algorithm in Python, we will use a dictionary called ``prec`` to hold the precedence values for the operators. This dictionary will map each operator to an integer that can be compared against the precedence levels of other operators (we have arbitrarily used the integers 3, 2, and 1). The left parenthesis will receive the lowest value possible. This way any operator that is compared against it will have higher precedence and will be placed on top of it. Line 15 defines the operands to be any upper-case character or digit. The complete conversion function is shown in :ref:`ActiveCode 1 <lst_intopost>`.

.. _lst_intopost:

.. activecode:: intopost
   :caption: Conversión de expresiones infijas a expresiones sufijas
   :nocodelens:

   from pythoned.basicas.pila import Pila

   def infija_a_sufija(expresionInfija):
       precedencia = {}
       precedencia["*"] = 3
       precedencia["/"] = 3
       precedencia["+"] = 2
       precedencia["-"] = 2
       precedencia["("] = 1
       pilaOperadores = Pila()
       listaSufija = []
       listaSimbolos = expresionInfija.split()

       for simbolo in listaSimbolos:
           if simbolo in "ABCDEFGHIJKLMNOPQRSTUVWXYZ" or simbolo in "0123456789":
               listaSufija.append(simbolo)
           elif simbolo == '(':
               pilaOperadores.incluir(simbolo)
           elif simbolo == ')':
               simboloTope = pilaOperadores.extraer()
               while simboloTope != '(':
                   listaSufija.append(simboloTope)
                   simboloTope = pilaOperadores.extraer()
           else:
               while (not pilaOperadores.estaVacia()) and \
                  (precedencia[pilaOperadores.inspeccionar()] >= \
                   precedencia[simbolo]):
                     listaSufija.append(pilaOperadores.extraer())
               pilaOperadores.incluir(simbolo)

       while not pilaOperadores.estaVacia():
           listaSufija.append(pilaOperadores.extraer())
       return " ".join(listaSufija)

   print(infija_a_sufija("A * B + C * D"))
   print(infija_a_sufija("( A + B ) * C - ( D - E ) * ( F + G )"))

--------------

A continuación se muestran algunos ejemplos de ejecución en la consola de Python.

.. A few more examples of execution in the Python shell are shown below.

::

    >>> infija_a_sufija("( A + B ) * ( C + D )")
    'A B + C D + *'
    >>> infija_a_sufija("( A + B ) * C")
    'A B + C *'
    >>> infija_a_sufija("A + B * C")
    'A B C * +'
    >>>

Evaluación de expresiones en notación sufija
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Como ejemplo final sobre las pilas, consideraremos la evaluación de una expresión que ya está en notación sufija. En este caso, una pila será de nuevo la estructura de datos elegida. Sin embargo, al recorrer la expresión sufija, son los operandos los que deben esperar, no los operadores como en el algoritmo de conversión anterior. Otra forma de pensar en la solución es que siempre que se vea un operador en la entrada, se usarán en la evaluación los dos operandos más recientes.

.. As a final stack example, we will consider the evaluation of an expression that is already in postfix notation. In this case, a stack is again the data structure of choice. However, as you scan the postfix expression, it is the operands that must wait, not the operators as in the conversion algorithm above. Another way to think about the solution is that whenever an operator is seen on the input, the two most recent operands will be used in the evaluation.

Para ver esto con más detalle, considere la expresión sufija ``4 5 6 * +``. Al recorrer la expresión de izquierda a derecha, usted encuentra primero los operandos 4 y 5. En este punto, usted todavía no está seguro respecto a qué hacer con ellos hasta que vea el siguiente símbolo. Ubicando cada uno en la pila asegura que estén disponibles si un operador viene a continuación.

.. To see this in more detail, consider the postfix expression ``4 5 6 * +``. As you scan the expression from left to right, you first encounter the operands 4 and 5. At this point, you are still unsure what to do with them until you see the next symbol. Placing each on the stack ensures that they are available if an operator comes next.

En este caso, el símbolo siguiente es otro operando. Así pues, como antes, inclúyalo en la pila y examine el símbolo siguiente. Ahora vemos un operador, \*. Esto significa que los dos operandos más recientes necesitan ser utilizados en una operación de multiplicación. Al extraer dos veces de la pila, podemos obtener los operandos adecuados y luego realizar la multiplicación (en este caso obtenemos 30 como resultado).

.. In this case, the next symbol is another operand. So, as before, push it and check the next symbol. Now we see an operator, \*. This means that the two most recent operands need to be used in a multiplication operation. By popping the stack twice, we can get the proper operands and then perform the multiplication (in this case getting the result 30).

Ahora podemos manejar este resultado colocándolo de nuevo en la pila para que pueda ser utilizado como un operando para los operadores posteriores en la expresión. Cuando se procesa el operador final, sólo quedará un valor en la pila. Se extrae y se devuelve como el resultado de la expresión. La :ref:`Figura 10 <fig_evalpost1>` muestra el contenido de la pila a medida que se procesa toda la expresión de ejemplo.

.. We can now handle this result by placing it back on the stack so that it can be used as an operand for the later operators in the expression. When the final operator is processed, there will be only one value left on the stack. Pop and return it as the result of the expression. :ref:`Figure 10 <fig_evalpost1>` shows the stack contents as this entire example expression is being processed.

.. _fig_evalpost1:

.. figure:: Figures/evalpostfix1.png
   :align: center

   Figura 10: Contenido de la pila durante la evaluación

   Figura 10: Contenido de la pila durante la evaluación

La :ref:`Figura 11 <fig_evalpost2>` muestra un ejemplo un poco más complejo, 7 8 + 3 2 + /. Hay dos cosas a tener en cuenta en este ejemplo. En primer lugar, el tamaño de la pila crece, disminuye y, a continuación, crece de nuevo a medida que las subexpresiones se evalúan. En segundo lugar, la operación de división necesita ser manejada cuidadosamente. Recuerde que los operandos en la expresión sufija están en su orden original ya que la notación sufija cambia sólo la ubicación de los operadores. Cuando los operandos para la división se extraen de la pila, estos se invierten. Dado que la división *no* es un operador conmutativo, en otras palabras :math:`15/5` no es lo mismo que :math:`5/15`, debemos estar seguros de que el orden de los operandos no esté intercambiado.

.. :ref:`Figure 11 <fig_evalpost2>` shows a slightly more complex example, 7 8 + 3 2 + /. There are two things to note in this example. First, the stack size grows, shrinks, and then grows again as the subexpressions are evaluated. Second, the division operation needs to be handled carefully. Recall that the operands in the postfix expression are in their original order since postfix changes only the placement of operators. When the operands for the division are popped from the stack, they are reversed. Since division is *not* a commutative operator, in other words :math:`15/5` is not the same as :math:`5/15`, we must be sure that the order of the operands is not switched.

.. _fig_evalpost2:

.. figure:: Figures/evalpostfix2.png
   :align: center

   Figura 11: Un ejemplo más complejo de evaluación

   Figura 11: Un ejemplo más complejo de evaluación

Supongamos que la expresión sufija es una cadena de símbolos delimitados por espacios. Los operadores son \*, /, + y -; además, se supone que los operandos son valores enteros de un solo dígito. La salida será un resultado entero.

.. Assume the postfix expression is a string of tokens delimited by spaces. The operators are \*, /, +, and - and the operands are assumed to be single-digit integer values. The output will be an integer result.

#. Crear una pila vacía llamada ``pilaOperandos``.

#. Convertir la cadena a una lista mediante la aplicación del método ``split``.

#. Recorrer la lista de símbolos de izquierda a derecha.

   -  Si el símbolo es un operando, convertirlo de tipo cadena a tipo entero e incluir el valor en ``pilaOperandos``.

   -  Si el símbolo es un operador, *, /, +, ó -, éste necesitará dos operandos. Extraer dos veces de ``pilaOperandos``. La primera extracción corresponde al segundo operando y la segunda al primer operando. Realizar la operación aritmética. Incluir el resultado en ``pilaOperandos``.

#. Cuando la expresión de entrada se ha procesado completamente, el resultado queda en la pila. Extraerlo de ``pilaOperandos`` y devolver dicho valor.

La función completa para la evaluación de expresiones sufijas se muestra en el :ref:`ActiveCode 2 <lst_postfixeval>`. Para ayudar con la aritmética, se define una función auxiliar ``hacerAritmetica`` que tomará dos operandos y un operador y luego realizará la operación aritmética apropiada.

.. The complete function for the evaluation of postfix expressions is shown in :ref:`ActiveCode 2 <lst_postfixeval>`. To assist with the arithmetic, a helper function ``doMath`` is defined that will take two operands and an operator and then perform the proper arithmetic operation.

.. _lst_postfixeval:

.. activecode:: postfixeval
   :caption: Evaluación de expresiones sufijas
   :nocodelens:

   from pythoned.basicas.pila import Pila

   def evaluacionNotacionSufija(expresionSufija):
       pilaOperandos = Pila()
       listaSimbolos = expresionSufija.split()

       for simbolo in listaSimbolos:
           if simbolo in "0123456789":
               pilaOperandos.incluir(int(simbolo))
           else:
               operando2 = pilaOperandos.extraer()
               operando1 = pilaOperandos.extraer()
               resultado = hacerAritmetica(simbolo,operando1,operando2)
               pilaOperandos.incluir(resultado)
       return pilaOperandos.extraer()

   def hacerAritmetica(operador, operandoIzquierda, operandoDerecha):
       if operador == "*":
           return operandoIzquierda * operandoDerecha
       elif operador == "/":
           return operandoIzquierda / operandoDerecha
       elif operador == "+":
           return operandoIzquierda + operandoDerecha
       else:
           return operandoIzquierda - operandoDerecha

   print(evaluacionNotacionSufija('7 8 + 3 2 + /'))

Es importante tener en cuenta que tanto en el programa de conversión de expresiones sufijas como en el programa de evaluación de expresiones sufijas asumimos que no había errores en la expresión de entrada. Utilizando estos programas como punto de partida, usted puede fácilmente pensar cómo podría incluirse una detección de errores y la generación de informes. Dejamos esto como un ejercicio para el final del capítulo.

.. It is important to note that in both the postfix conversion and the postfix evaluation programs we assumed that there were no errors in the input expression. Using these programs as a starting point, you can easily see how error detection and reporting can be included. We leave this as an exercise at the end of the chapter.

.. admonition:: Autoevaluación

   .. fillintheblank:: postfix1

      .. blank:: pfblank1
         :correct: \\b10\\s+3\\s+5\\s*\\*\\s*16\\s+4\\s*-\\s*/\\s*\\+
         :feedback1:  ('10.*3.*5.*16.*4', 'Los n&uacute;meros parecen estar en el orden correcto, compruebe sus operadores')
         :feedback2: ('.*', 'Recuerde que los n&uacute;meros estar&aacute;n en el mismo orden que en la ecuaci&oacute;n original')

         Sin usar la función infija_a_sufija del activecode, convierta la siguiente expresión a notación sufija ``10 + 3 * 5 / (16 - 4)``

   .. fillintheblank:: postfix2

      .. blank:: pfblank2
         :correct: \\b9\\b
         :feedback1: ('.*', "Recuerde incluir cada resultado intermedio en la pila" )

         ¿Cuál es el resultado de evaluar lo siguiente?: ``17 10 + 3 * 9 / ==``

   .. fillintheblank:: postfix3

      .. blank:: pfblank3
         :correct: 5\\s+3\\s+4\\s+2\\s*-\\s*\\^\\s*\\*
         :feedback1: ('.*', 'Hint: You only need to add one line to the function!!')

         Modifique la función infija_a_sufija de modo que pueda convertir la siguiente expresión:  ``5 * 3 ** (4 - 2)``   Pegue aquí la respuesta:


