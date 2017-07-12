..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Visualización de la recursividad
================================

En la sección anterior examinamos algunos problemas que eran fáciles de resolver mediante la recursividad; sin embargo, todavía puede ser difícil encontrar un modelo mental o una forma de visualizar lo que está sucediendo en una función recursiva. Esto puede dificultar la comprensión de la recursividad. En esta sección examinaremos un par de ejemplos de uso de la recursividad para dibujar algunas imágenes interesantes. A medida que usted observe cómo toman forma estas imágenes, obtendrá una nueva perspectiva del proceso recursivo que puede ser útil para consolidar su comprensión de la recursividad.

.. In the previous section we looked at some problems that were easy to solve using recursion; however, it can still be difficult to find a mental model or a way of visualizing what is happening in a recursive function. This can make recursion difficult for people to grasp. In this section we will look at a couple of examples of using recursion to draw some interesting pictures. As you watch these pictures take shape you will get some new insight into the recursive process that may be helpful in cementing your understanding of recursion.

La herramienta que utilizaremos para nuestras ilustraciones es el módulo gráfico de Python llamado ``turtle`` (*tortuga*). El módulo ``turtle`` es estándar en todas las versiones de Python y es muy fácil de usar. La metáfora es bastante simple. Usted puede crear una tortuga y la tortuga puede moverse hacia delante, hacia atrás, girar a la izquierda, girar a la derecha, etc. La tortuga puede tener su cola hacia arriba o hacia abajo. Cuando la cola de la tortuga está hacia abajo y la tortuga se mueve, dibuja una línea a medida que se desplaza. Para aumentar el valor artístico de la tortuga usted puede cambiar el ancho de la cola, así como el color de la tinta en el que la cola se empapa.

.. The tool we will use for our illustrations is Python’s turtle graphics module called ``turtle``. The ``turtle`` module is standard with all versions of Python and is very easy to use. The metaphor is quite simple. You can create a turtle and the turtle can move forward, backward, turn left, turn right, etc. The turtle can have its tail up or down. When the turtle’s tail is down and the turtle moves it draws a line as it moves. To increase the artistic value of the turtle you can change the width of the tail as well as the color of the ink the tail is dipped in.

Aquí daremos un ejemplo sencillo para ilustrar algunos conceptos básicos de los gráficos con el módulo ``turtle``. Utilizaremos el módulo para dibujar una espiral recursivamente. El :ref:`ActiveCode 1 <lst_turt1>` muestra cómo se hace. Después de importar el módulo ``turtle`` creamos una tortuga. Cuando creamos la tortuga también creamos una ventana para que ella dibuje adentro. A continuación definimos la función dibujarEspiral. El caso base para esta función simple se da cuando la longitud de la línea que queremos dibujar, dada por el parámetro ``len``, se reduce a cero o menos. Si la longitud de la línea es mayor que cero, indicamos a la tortuga que siga adelante por ``len`` unidades  y luego gire a la derecha 90 grados. El paso recursivo ocurre cuando llamamos dibujarEspiral de nuevo con una longitud reducida. Al final del :ref:`ActiveCode 1 <lst_turt1>` notará que llamamos a la función ``miVentana.exitonclick()``, este es un método práctico de la ventana que pone a la tortuga en un modo de espera hasta que usted haga clic dentro de la ventana, después de lo cual el programa la limpia y cierra.

.. Here is a simple example to illustrate some turtle graphics basics. We will use the turtle module to draw a spiral recursively. :ref:`ActiveCode 1 <lst_turt1>` shows how it is done. After importing the ``turtle`` module we create a turtle. When the turtle is created it also creates a window for itself to draw in. Next we define the dibujarEspiral function. The base case for this simple function is when the length of the line we want to draw, as given by the ``len`` parameter, is reduced to zero or less. If the length of the line is longer than zero we instruct the turtle to go forward by ``len`` units and then turn right 90 degrees. The recursive step is when we call dibujarEspiral again with a reduced length. At the end of :ref:`ActiveCode 1 <lst_turt1>` you will notice that we call the function ``miVentana.exitonclick()``, this is a handy little method of the window that puts the turtle into a wait mode until you click inside the window, after which the program cleans up and exits.


.. activecode:: lst_turt1
    :caption: Dibujar una espiral recursiva usando el módulo turtle
    :nocodelens:


    import turtle

    miTortuga = turtle.Turtle()
    miVentana = turtle.Screen()

    def dibujarEspiral(miTortuga, longitudLinea):
        if longitudLinea > 0:
            miTortuga.forward(longitudLinea)
            miTortuga.right(90)
            dibujarEspiral(miTortuga,longitudLinea-5)

    dibujarEspiral(miTortuga,100)
    miVentana.exitonclick()

Eso es realmente todo lo que usted necesita saber respecto a los gráficos con el módulo ``turtle`` para hacer algunos dibujos bastante impresionantes. Para nuestro próximo programa vamos a dibujar un árbol fractal. Los fractales vienen de una rama de las matemáticas, y tienen mucho en común con la recursividad. La definición de un fractal implica que, que cuando usted lo mira, el fractal tiene la misma forma básica no importa cuánto lo magnifique. Algunos ejemplos de la naturaleza son las costas de los continentes, los copos de nieve, las montañas, e incluso los árboles o arbustos. La naturaleza fractal de muchos de estos fenómenos naturales hace posible que los programadores generen paisajes muy realistas para películas generadas por computadora. En nuestro próximo ejemplo generaremos un árbol fractal.

.. That is really about all the turtle graphics you need to know in order to make some pretty impressive drawings. For our next program we are going to draw a fractal tree. Fractals come from a branch of mathematics, and have much in common with recursion. The definition of a fractal is that when you look at it the fractal has the same basic shape no matter how much you magnify it. Some examples from nature are the coastlines of continents, snowflakes, mountains, and even trees or shrubs. The fractal nature of many of these natural phenomenon makes it possible for programmers to generate very realistic looking scenery for computer generated movies. In our next example we will generate a fractal tree.

Para entender cómo va a funcionar esto es útil pensar en cómo podríamos describir un árbol usando un vocabulario fractal. Recuerde que hemos dicho anteriormente que un fractal es algo que se ve igual en todos los diferentes niveles de ampliación. Si traducimos esto a árboles y arbustos podríamos decir que incluso una pequeña ramita tiene la misma forma y características que un árbol entero. Usando esta idea podríamos decir que un *árbol* es un tronco, con un *árbol* más pequeño que va a la derecha y otro árbol *más pequeño* que va a la izquierda. Si usted piensa en esta definición recursivamente, ella significa que vamos a aplicar la definición recursiva de un árbol a los dos árboles más pequeños de izquierda y derecha.

.. To understand how this is going to work it is helpful to think of how we might describe a tree using a fractal vocabulary. Remember that we said above that a fractal is something that looks the same at all different levels of magnification. If we translate this to trees and shrubs we might say that even a small twig has the same shape and characteristics as a whole tree. Using this idea we could say that a *tree* is a trunk, with a smaller *tree* going off to the right and another smaller *tree* going off to the left. If you think of this definition recursively it means that we will apply the recursive definition of a tree to both of the smaller left and right trees.

Vamos a traducir esta idea a un código en Python. El :ref:`Programa 1 <lst_fractree>` muestra cómo podemos utilizar nuestra tortuga para generar un árbol fractal. Veamos el código un poco más de cerca. Usted verá que en las líneas 5 y 7 estamos haciendo una llamada recursiva. En la línea 5 hacemos la llamada recursiva justo después de que la tortuga gire 20 grados a la derecha; éste es el árbol derecho mencionado anteriormente. Luego en la línea 7 la tortuga hace otra llamada recursiva, pero esta vez después de girar 40 grados a la izquierda. La razón por la que la tortuga debe girar 40 grados a la izquierda es que necesita deshacer el giro original de 20 grados a la derecha y luego hacer un giro adicional de 20 grados a la izquierda para dibujar el árbol izquierdo. Observe también que cada vez que hacemos una llamada recursiva a ``arbol`` restaremos algo del parámetro ``longitudRama``; esto es para asegurarnos de que los árboles recursivos se hagan más y más pequeños. Usted también debe reconocer la instrucción inicial ``if`` en la línea 2 como una verificación para el caso base que consiste en que el valor de ``longitudRama`` se vuelva demasiado pequeño.

.. Let's translate this idea to some Python code. :ref:`Listing 1 <lst_fractree>` shows how we can use our turtle to generate a fractal tree. Let's look at the code a bit more closely. You will see that on lines 5 and 7 we are making a recursive call. On line 5 we make the recursive call right after the turtle turns to the right by 20 degrees; this is the right tree mentioned above. Then in line 7 the turtle makes another recursive call, but this time after turning left by 40 degrees. The reason the turtle must turn left by 40 degrees is that it needs to undo the original 20 degree turn to the right and then do an additional 20 degree turn to the left in order to draw the left tree. Also notice that each time we make a recursive call to ``tree`` we subtract some amount from the ``longitudRama`` parameter; this is to make sure that the recursive trees get smaller and smaller. You should also recognize the initial ``if`` statement on line 2 as a check for the base case of ``longitudRama`` getting too small.

.. _lst_fractree:

**Programa 1**

.. highlight:: python
    :linenothreshold: 5

::

    def arbol(longitudRama,t):
        if longitudRama > 5:
            t.forward(longitudRama)
            t.right(20)
            arbol(longitudRama-15,t)
            t.left(40)
            arbol(longitudRama-10,t)
            t.right(20)
            t.backward(longitudRama)
            
            
.. highlight:: python
    :linenothreshold: 500

El programa completo para este ejemplo de árbol se muestra en el :ref:`ActiveCode 2 <lst_complete_tree>`. Antes de ejecutar el código, piense en cómo espera usted ver que el árbol irá tomando forma. Mire las llamadas recursivas y piense en cómo se desarrollará este árbol. ¿Se dibujará simétricamente con las mitades derecha e izquierda del árbol tomando forma simultáneamente? ¿Será dibujado el lado derecho primero y depués el lado izquierdo?

.. The complete program for this tree example is shown in :ref:`ActiveCode 2 <lst_complete_tree>`. Before you run the code think about how you expect to see the tree take shape. Look at the recursive calls and think about how this tree will unfold. Will it be drawn symmetrically with the right and left halves of the tree taking shape simultaneously? Will it be drawn right side first then left side?


.. activecode:: lst_complete_tree
    :caption: Dibujar un árbol recursivamente
    :nocodelens:

    import turtle
    
    def arbol(longitudRama,t):
        if longitudRama > 5:
            t.forward(longitudRama)
            t.right(20)
            arbol(longitudRama-15,t)
            t.left(40)
            arbol(longitudRama-15,t)
            t.right(20)
            t.backward(longitudRama)

    def main():
        t = turtle.Turtle()
        miVentana = turtle.Screen()
        t.left(90)
        t.up()
        t.backward(100)
        t.down()
        t.color("green")
        arbol(75,t)
        miVentana.exitonclick()
        
    main()

Observe cómo cada punto de ramificación en el árbol corresponde a una llamada recursiva, y note cómo el árbol se dibuja por la derecha hasta llegar a su rama más corta. Puede ver esto en la :ref:`Figura 1 <fig_tree1>`. Ahora, observe cómo el programa regresa al tronco sólo después que se ha dibujado todo el lado derecho del árbol. La mitad derecha del árbol puede verse en la :ref:`Figura 2 <fig_tree2>`. Luego se dibuja el lado izquierdo del árbol, pero no yendo tan lejos hacia la izquierda como es posible. Más bien, una vez más, todo el lado derecho del árbol izquierdo se dibuja hasta que finalmente llegamos a la ramita más pequeña de la izquierda.


.. Notice how each branch point on the tree corresponds to a recursive call, and notice how the tree is drawn to the right all the way down to its shortest twig. You can see this in :ref:`Figure 1 <fig_tree1>`. Now, notice how the program works its way back up the trunk until the entire right side of the tree is drawn. You can see the right half of the tree in :ref:`Figure 2 <fig_tree2>`. Then the left side of the tree is drawn, but not by going as far out to the left as possible. Rather, once again the entire right side of the left tree is drawn until we finally make our way out to the smallest twig on the left.


.. _fig_tree1:

.. figure:: Figures/tree1.png
   :align: center

   Figura 1: El comienzo de un árbol fractal

   Figura 1: El comienzo de un árbol fractal
   
.. _fig_tree2:

.. figure:: Figures/tree2.png
   :align: center

   Figura 2: La primera mitad del árbol

   Figura 2: La primera mitad del árbol

Este sencillo programa para dibujar un árbol es sólo un punto de partida para usted; notará además que el árbol no parece particularmente realista porque la naturaleza no es tan simétrica como un programa de computadora. Los ejercicios al final del capítulo le darán algunas ideas sobre cómo explorar algunas opciones interesantes para hacer que su árbol parezca más realista.

.. This simple tree program is just a starting point for you, and you will notice that the tree does not look particularly realistic because nature is just not as symmetric as a computer program. The exercises at the end of the chapter will give you some ideas for how to explore some interesting options to make your tree look more realistic.

.. admonition:: Autoevaluación

   Modifique el programa de árbol recursivo utilizando una o todas las ideas siguientes:

   -  Modifique el grosor de las ramas para que a medida que el valor de ``longitudRama`` se haga más pequeño, la línea se haga más delgada.

   -  Modifique el color de las ramas de modo que cuando el valor de ``longitudRama`` se vuelva muy pequeño se coloree como una hoja.

   -  Modifique el ángulo utilizado para girar la tortuga de manera que en cada punto de ramificación el ángulo se seleccione aleatoriamente dentro de algún rango. Por ejemplo, elija el ángulo entre 15 y 45 grados. Haga ensayos para ver si luce bien.

   -  Modifique el valor de ``longitudRama`` recursivamente para que en vez de restar siempre la misma cantidad, usted reste una cantidad aleatoria dentro de algún rango.

   .. actex:: recursion_sc_3
      :nocodelens:


