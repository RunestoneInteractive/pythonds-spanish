..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Ejercicios de programación
--------------------------

#. Modifique el algoritmo infija-a-sufija para que pueda manejar errores.

#. Modifique el algoritmo de evaluación en notación sufija para que pueda manejar errores.

#. Implemente un evaluador directo de notación infija que combine la funcionalidad de la conversión de notación infija a notación sufija y el algoritmo de evaluación en notación sufija. Su evaluador debe procesar los símbolos en notación infija de izquierda a derecha y utilizar dos pilas, una para los operadores y otra para los operandos, para realizar la evaluación.

#. Convierta su evaluador directo de notación infija del problema anterior en una calculadora.

#. Implemente el TAD ``Cola``, usando una lista tal que el final de la cola esté al final de la lista.

#. Diseñe e implemente un experimento para hacer comparaciones de referencia de las dos implementaciones de Cola. ¿Qué puede usted aprender de tal experimento?

#. Es posible implementar una cola tal que tanto ``agregar`` como ``avanzar`` tengan desempeños :math:`O(1)` *en promedio*. En este caso, significa que la mayoría de las veces ``agregar`` y ``avanzar`` serán :math:`O(1)` excepto en una circunstancia particular en la cual ``avanzar`` será :math:`O(n)`.

#. Considere una situación de la vida real. Formule una pregunta y luego diseñe una simulación que pueda ayudar a responderla. Las posibles situaciones incluyen:

   -  Carros alineados en un servicio "auto-lavado"

   -  Clientes en el punto de pago de una tienda de comestibles

   -  Aviones despegando y aterrizando en una pista

   -  Un cajero de banco

   Asegúrese de indicar cualquier suposición que usted haga y proporcione cualquier dato probabilístico que deba considerarse como parte del escenario.

#. Modifique la simulación de la patata caliente para permitir un valor de conteo elegido al azar de modo que cada pasada no sea predecible a partir de la anterior.

#. Implemente una máquina de ordenamiento radix. Un ordenamiento radix para enteros de base 10 es una técnica de ordenamiento mecánica que utiliza una colección de bins, un bin principal y 10 bins de dígitos. Cada bin actúa como una cola y mantiene sus valores en el orden en que llegan. El algoritmo comienza colocando cada número en el bin principal. Entonces considera cada valor dígito por dígito. El primer valor se elimina y se coloca en un bin de dígitos correspondiente al dígito que se está considerando. Por ejemplo, si se está considerando el dígito de los unos, para 534 se pone 4 en tal bin y para 667 se pone 7. Una vez que todos los valores se colocan en los bins de dígitos correspondientes, los valores se recuperan del bin 0 al bin 9 y se ponen de nuevo en el bin principal. El proceso continúa con el dígito de las decenas, las centenas, y así sucesivamente. Después de procesar el último dígito, el bin principal contiene los valores en orden.

#. Otro ejemplo de un problema de correspondencia entre paréntesis proviene del lenguaje de marcas de hipertexto (HTML). En HTML, las etiquetas existen tanto en la forma de apertura como en la forma de cierre y deben estar balanceadas para describir correctamente un documento web. El siguiente documento sencillo en HTML:

   ::

       <html>
          <head>
             <title>
                Ejemplo
             </title>
          </head>

          <body>
             <h1>Hola mundo</h1>
          </body>
       </html>

   está destinado únicamente a mostrar la estructura de coincidencia y anidamiento de las etiquetas en el lenguaje HTML. Escriba un programa que pueda comprobar que las etiquetas de apertura y cierre en un documento HTML sean adecuadas.

#. Amplíe el Programa 2.15 para manipular palíndromos con espacios. Por ejemplo, ANITA LAVA LA TINA es un palíndromo que se lee igual hacia adelante y hacia atrás si se ignoran los espacios en blanco.

#. Para implementar el método ``tamano`` contamos el número de nodos en la lista. Una estrategia alternativa sería almacenar el número de nodos en la lista como una pieza de datos adicional en la cabeza de la lista. Modifique la clase ``ListaNoOrdenada`` para incluir esta información y reescriba el método ``tamano``.

#. Implementar el método ``remover`` para que funcione correctamente en caso que el ítem no esté en la lista.

#. Modifique las clases de listas para permitir valores duplicados. ¿Qué métodos serán afectados por este cambio?

#. Implemente el método __str__ en la clase ListaNoOrdenada. ¿Cuál sería una buena representación de las cadenas para una lista?

#. Implemente el método __str__ de modo que las listas se muestren a la manera de Python (con corchetes).

#. Implemente las operaciones restantes definidas en el TAD ListaNoOrdenada (anexar, indice, extraer, insertar).

#. Implemente un método extracción de sublistas para la clase ``ListaNoOrdenada``. El método debería tomar dos parámetros, ``desde`` y ``hasta``, y debe devolver una copia de la lista comenzando en la posición ``desde`` y prosiguiendo pero sin incluir la posición ``hasta``.

#. Implemente las operaciones restantes definidas en el TAD ListaOrdenada.

#. Considere la relación entre listas no ordenadas y listas ordenadas. ¿Podría usarse la herencia para construir una implementación más eficiente? Implemente esta jerarquía de herencia.

#. Implemente una pila usando listas enlazadas.

#. Implemente una cola usando listas enlazadas.

#. Implemente una cola doble usando listas enlazadas.

#. Diseñe e implemente un experimento que comparará el desempeño de una lista de Python con una lista implementada como una lista enlazada.

#. Diseñe e implemente un experimento que comparará el desempeño de la pila y de la cola basadas en listas de Python con la implementación de listas enlazadas.

#. La implementación de la lista enlazada dada anteriormente se denomina lista simplemente enlazada porque cada nodo tiene una única referencia al siguiente nodo en la secuencia. Una implementación alternativa se conoce como una lista doblemente enlazada. En esta implementación, cada nodo tiene una referencia al siguiente nodo (comúnmente llamado siguiente) así como una referencia al nodo precedente (comúnmente llamado anterior). La referencia principal también contiene dos referencias, una al primer nodo en la lista enlazada y una al último. Codifique esta implementación en Python.

#. Cree una implementación de una cola que tenga un desempeño promedio de O(1) para las operaciones de agregar y avanzar.
