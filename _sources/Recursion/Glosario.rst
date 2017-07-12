..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Glosario
--------

.. glossary::

    caso base
        Una rama de la instrucción condicional en una función recursiva que no da lugar a nuevas llamadas recursivas.

    estructura de datos
        Una organización de datos con el fin de facilitar su uso.

    excepción
        Un error que ocurre en tiempo de ejecución.

    manejar una excepción
        Envolver el bloque de código en una instrucción ``try`` / ``except`` para evitar que una excepción termine un programa.

    tipo de datos inmutable
        Un tipo de datos que no se puede modificar. Las asignaciones a elementos o porciones de los tipos inmutables causan un error de tiempo de ejecución.

    recursividad infinita
        Una función que se llama a sí misma recursivamente sin llegar nunca al caso base. Eventualmente, una recursividad infinita provoca un error de tiempo de ejecución.

    tipo de datos mutable
        Un tipo de datos que se puede modificar. Todos los tipos mutables son tipos compuestos. Las listas y los diccionarios (ver capítulo siguiente) son tipos de datos mutables; las cadenas y tuplas no lo son.

    causar
        Causar una excepción mediante el uso de la instrucción ``raise``.

    recursividad
        El proceso de llamar a la función que ya se está ejecutando.

    llamada recursiva
        La instrucción que llama a una función que ya se está ejecutando. La recursividad puede incluso ser indirecta --- la función `f` puede llamar a la función `g` que llama a la función `h`, y la función `h` podría hacer una llamada a la función `f`.

    definición recursiva
        Una definición que define algo en términos de sí misma. Para ser útil debe incluir *casos base* que no sean recursivos. De esta manera difiere de una *definición circular*. Las definiciones recursivas a menudo proporcionan una manera elegante de expresar estructuras de datos complejas.

    tupla
        Tipo de datos que contiene una secuencia de elementos de cualquier tipo, como una lista, pero es inmutable. Las tuplas se pueden usar en cualquier lugar que se requiera un tipo inmutable, por ejemplo como una clave en un diccionario (ver el capítulo siguiente).

    asignacion de tupla
        Una asignación a todos los elementos de una tupla utilizando una sola instrucción de asignación. La asignación de tupla se produce en paralelo en lugar de en secuencia, por lo que es útil para intercambiar valores.
