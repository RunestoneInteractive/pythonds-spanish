..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Ejercicios de programación
--------------------------

#. Implemente los métodos sencillos ``obtenerNum`` y ``obtenerDen`` que devolverán el numerador y el denominador de una fracción.

#. Por muchas razones sería mejor si todas las fracciones se mantuvieran en los términos menores desde el principio. Modifique el constructor de la clase ``Fraccion`` para que ``MCD`` se use para simplificar fracciones inmediatamente. Note que esto significa que la función ``__add__`` ya no necesita hacer la simplificación. Haga las modificaciones necesarias.

#. Implemente los operadores aritméticos sencillos restantes (``__sub__``, ``__mul__`` y ``__truediv__``).

#. Implemente los operadores relacionales restantes (``__gt__``, ``__ge__``, ``__lt__``, ``__le__`` y ``__ne__``)

#. Modifique el constructor para la clase ``Fraccion`` de modo que compruebe que el numerador y el denominador sean ambos enteros. Si alguno no es un entero, el constructor debe generar una excepción.

#. En la definición de fracciones asumimos que las fracciones negativas tienen un numerador negativo y un denominador positivo. El uso de un denominador negativo haría que algunos de los operadores relacionales dieran resultados incorrectos. En general, ésta es una restricción innecesaria. Modifique el constructor para permitir que el usuario pase un denominador negativo y que todos los operadores continúen funcionando correctamente.

#. Consulte el método ``__radd__``. ¿En qué se diferencia de ``__add__``? ¿Cuándo se usa? Implemente ``__radd__``.

#. Repita la pregunta anterior, pero esta vez considere el método ``__iadd__``.

#. Consulte el método ``__repr__``. ¿En qué se diferencia de ``__str__``? ¿Cuándo se utiliza? Implemente ``__repr__``.

#. Consulte otros tipos de compuertas que existen (como NAND, NOR, y XOR). Añádalas a la jerarquía de compuertas. ¿Cuánta codificación adicional necesitó?

#. El circuito aritmético más simple se conoce como el semisumador (o sumador incompleto). Consulte el circuito sencillo del semisumador. Implemente este circuito.

#. Ahora extienda dicho circuito e implemente un sumador completo de 8 bits.

#. La simulación del circuito mostrado en este capítulo funciona en sentido inverso. En otras palabras, dado un circuito, la salida se produce retrocediendo hacia los valores de entrada, que a su vez causan que otras salidas sean requeridas. Este retroceso continúa hasta que se encuentran líneas de entrada externas, punto en el cual se piden los valores al usuario. Modifique la implementación para que la acción se dé en la otra dirección (hacia adelante); al recibir las entradas el circuito produce una salida.

#. Diseñe una clase para representar una carta de juego de naipes. Ahora diseñe una clase para representar una baraja de cartas. Usando estas dos clases, implemente su juego de cartas favorito.

#. Encuentre un rompecabezas de Sudoku en el periódico local. Escribe un programa para resolver el rompecabezas.
