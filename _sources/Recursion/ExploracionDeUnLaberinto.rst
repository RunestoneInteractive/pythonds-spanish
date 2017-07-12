..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Exploración de un laberinto
---------------------------

En esta sección examinaremos un problema que tiene relevancia para el mundo en expansión de la robótica: ¿Cómo encontrar la salida de un laberinto? Si usted tiene una aspiradora Roomba para limpiar su habitación (¿no todos los estudiantes universitarios?), deseará que pudiera reprogramarla utilizando lo que ha aprendido en esta sección. El problema que queremos resolver es ayudar a nuestra tortuga a encontrar su salida de un laberinto virtual. El problema del laberinto tiene raíces tan profundas como el mito griego sobre Teseo que fue enviado a un laberinto para matar al minotauro. Teseo usó una madeja de hilo para ayudarse a encontrar su camino de regreso una vez que hubiera eliminado a la bestia. En nuestro problema asumiremos que nuestra tortuga se deja caer en alguna parte en medio del laberinto y debe encontrar su salida. Mire la :ref:`Figura 2 <fig_mazescreen>` para tener una idea de hacia dónde vamos en esta sección.

.. In this section we will look at a problem that has relevance to the expanding world of robotics: How do you find your way out of a maze? If you have a Roomba vacuum cleaner for your dorm room (don’t all college students?) you will wish that you could reprogram it using what you have learned in this section. The problem we want to solve is to help our turtle find its way out of a virtual maze. The maze problem has roots as deep as the Greek myth about Theseus who was sent into a maze to kill the minotaur. Theseus used a ball of thread to help him find his way back out again once he had finished off the beast. In our problem we will assume that our turtle is dropped down somewhere into the middle of the maze and must find its way out. Look at :ref:`Figure 2 <fig_mazescreen>` to get an idea of where we are going in this section.

.. _fig_mazescreen:

.. figure:: Figures/maze.png
   :align: center

   Figura 2: El programa de búsqueda en un laberinto terminado

   Figura 2: El programa de búsqueda en un laberinto terminado

Para que sea más fácil para nosotros, asumiremos que nuestro laberinto está dividido en “cuadrados”. Cada cuadrado del laberinto está abierto u ocupado por una sección de pared. La tortuga sólo puede pasar a través de los cuadrados abiertos del laberinto. Si la tortuga se topa con una pared, debe intentar continuar en una dirección diferente. La tortuga requerirá un procedimiento sistemático para encontrar su salida del laberinto. Aquí está el procedimiento:

.. To make it easier for us we will assume that our maze is divided up into “squares.” Each square of the maze is either open or occupied by a section of wall. The turtle can only pass through the open squares of the maze. If the turtle bumps into a wall it must try a different direction. The turtle will require a systematic procedure to find its way out of the maze. Here is the procedure:

-  Desde nuestra posición de partida, primero intentaremos avanzar un cuadrado hacia el Norte y luego recursivamente probaremos nuestro procedimiento desde allí.

-  Si no tenemos éxito al intentar un camino hacia el Norte como primer paso, daremos un paso hacia el Sur y repetiremos recursivamente nuestro procedimiento.

-  Si ir hacia el Sur no funciona, entonces intentaremos dar un paso hacia el Oeste como nuestro primer paso y aplicaremos nuestro procedimiento recursivamente.

-  Si el Norte, el Sur y el Oeste no han tenido éxito, aplicaremos el procedimiento recursivamente desde una posición un paso hacia nuestro Este.

-  Si ninguna de estas direcciones funciona entonces no hay manera de salir del laberinto y hemos fracasado.

Eso suena bastante fácil, sin embargo hay un par de detalles que discutir primero. Supongamos que tomamos nuestro primer paso recursivo al ir hacia el Norte. Siguiendo nuestro procedimiento, nuestro próximo paso sería también hacia el Norte. Pero si el Norte está bloqueado por una pared debemos mirar el siguiente paso del procedimiento e intentar ir hacia el Sur. Desafortunadamente ese paso hacia el Sur nos lleva de regreso a nuestro lugar de partida original. Si aplicamos el procedimiento recursivo desde allí, simplemente regresaremos un paso hacia el Norte y estaremos en un ciclo infinito. Por lo tanto, debemos contar con una estrategia para recordar dónde hemos estado. En este caso vamos a suponer que tenemos una bolsa de migas de pan que podemos dejar caer a lo largo de nuestro camino. Si damos un paso en una dirección determinada y encontramos que ya hay una miga de pan en ese cuadrado, sabemos que debemos retroceder inmediatamente y probar la siguiente dirección en nuestro procedimiento. Como veremos cuando observemos el código de este algoritmo, retroceder es tan simple como regresar desde una llamada recursiva de una función.

.. Now, that sounds pretty easy, but there are a couple of details to talk about first. Suppose we take our first recursive step by going North. By following our procedure our next step would also be to the North. But if the North is blocked by a wall we must look at the next step of the procedure and try going to the South. Unfortunately that step to the south brings us right back to our original starting place. If we apply the recursive procedure from there we will just go back one step to the North and be in an infinite loop. So, we must have a strategy to remember where we have been. In this case we will assume that we have a bag of bread crumbs we can drop along our way. If we take a step in a certain direction and find that there is a bread crumb already on that square, we know that we should immediately back up and try the next direction in our procedure. As we will see when we look at the code for this algorithm, backing up is as simple as returning from a recursive function call.

Como hacemos con todos los algoritmos recursivos, revisemos los casos base. Puede que usted ya haya adivinado algunos de ellos con base en la descripción del párrafo anterior. En este algoritmo hay cuatro casos base a considerar:

.. As we do for all recursive algorithms let us review the base cases. Some of them you may already have guessed based on the description in the previous paragraph. In this algorithm, there are four base cases to consider:

#. La tortuga se ha topado con una pared. Dado que el cuadrado está ocupado por una pared, no se puede realizar más exploración.

#. La tortuga ha encontrado un cuadrado que ya ha sido explorado. No queremos seguir explorando desde esta posición pues entraríamos en un ciclo.

#. Hemos encontrado un borde exterior que no está ocupado por una pared. En otras palabras, hemos encontrado una salida del laberinto.

#. Hemos explorado un cuadrado sin éxito en las cuatro direcciones.

Para que nuestro programa funcione, necesitaremos contar con una manera de representar el laberinto. Para hacer esto aún más interesante vamos a utilizar el módulo ``turtle`` para dibujar y explorar nuestro laberinto de modo que podamos ver este algoritmo en acción. El objeto ``Laberinto`` proporcionará los siguientes métodos para que los usemos al escribir nuestro algoritmo de búsqueda:

.. For our program to work we will need to have a way to represent the maze. To make this even more interesting we are going to use the turtle module to draw and explore our maze so we can watch this algorithm in action. The maze object will provide the following methods for us to use in writing our search algorithm:

-  ``__init__`` lee en un archivo de datos que representa un laberinto, inicializa la representación interna del laberinto y encuentra la posición inicial para la tortuga.

-  ``dibujarLaberinto`` dibuja el laberinto en una ventana en la pantalla.

-  ``actualizarPosicion`` actualiza la representación interna del laberinto y cambia la posición de la tortuga en la ventana.

-  ``esSalida`` comprueba si la posición actual es una salida del laberinto.

La clase ``Laberinto`` también sobrecarga el operador índice ``[]`` para que nuestro algoritmo pueda acceder fácilmente al estado de cualquier cuadrado particular.

.. The ``Laberinto`` class also overloads the index operator ``[]`` so that our algorithm can easily access the status of any particular square.

Examinemos el código de la función de búsqueda que denominamos ``buscarDesde``. El código se muestra en el :ref:`Programa 3 <lst_mazesearch>`. Observe que esta función toma tres parámetros: un objeto laberinto, la fila de inicio y la columna de inicio. Esto es importante porque, como función recursiva, la búsqueda comienza lógicamente otra vez con cada llamada recursiva.

.. Let’s examine the code for the search function which we call ``buscarDesde``. The code is shown in :ref:`Listing 3 <lst_mazesearch>`. Notice that this function takes three parameters: a maze object, the starting row, and the starting column. This is important because as a recursive function the search logically starts again with each recursive call.

.. _lst_mazesearch:

.. highlight:: python
    :linenothreshold: 5
    
**Programa 3**

::

    def buscarDesde(laberinto, filaInicio, columnaInicio):
        laberinto.actualizarPosicion(filaInicio, columnaInicio)
       #  Verificar casos base:
       #  1. Hemos tropezado con un obstáculo, devolver False
       if laberinto[filaInicio][columnaInicio] == OBSTACULO :
            return False
        #  2. Hemos encontrado un cuadrado que ya ha sido explorado
        if laberinto[filaInicio][columnaInicio] == INTENTADO:
            return False
        # 3. Éxito, un borde exterior no ocupado por un obstáculo
        if laberinto.esSalida(filaInicio,columnaInicio):
            laberinto.actualizarPosicion(filaInicio, columnaInicio, \
            PARTE_DEL_CAMINO)
            return True
        laberinto.actualizarPosicion(filaInicio, columnaInicio, INTENTADO)

        # De lo contrario, use cortocircuitos lógicos para probar cada
        # dirección a su vez (si fuera necesario)
        encontrado = buscarDesde(laberinto, filaInicio-1, columnaInicio) or \
                buscarDesde(laberinto, filaInicio+1, columnaInicio) or \
                buscarDesde(laberinto, filaInicio, columnaInicio-1) or \
                buscarDesde(laberinto, filaInicio, columnaInicio+1)
        if encontrado:
            laberinto.actualizarPosicion(filaInicio, columnaInicio, \
            PARTE_DEL_CAMINO)
        else:
            laberinto.actualizarPosicion(filaInicio, columnaInicio, \
            CAJELLON_SIN_SALIDA)
        return encontrado

Al examinar el algoritmo usted verá que lo primero que hace el código (línea 2) es llamar a ``actualizarPosicion``. Ésto se hace simplemente para ayudarle a usted a visualizar el algoritmo de modo que pueda ver exactamente cómo explora la tortuga su camino a través del laberinto. A continuación, el algoritmo comprueba los tres primeros de los cuatro casos base: ¿La tortuga ha chocado contra una pared (línea 5)? ¿La tortuga ha regresado a un cuadrado ya explorado (línea 8)? ¿La tortuga ha encontrado una salida (línea 11)? Si ninguna de estas condiciones es verdadera entonces continuamos la búsqueda recursivamente.

.. As you look through the algorithm you will see that the first thing the code does (line 2) is call ``actualizarPosicion``. This is simply to help you visualize the algorithm so that you can watch exactly how the turtle explores its way through the maze. Next the algorithm checks for the first three of the four base cases: Has the turtle run into a wall (line 5)? Has the turtle circled back to a square already explored (line 8)? Has the turtle found an exit (line 11)? If none of these conditions is true then we continue the search recursively.

Usted notará que en el paso recursivo hay cuatro llamadas recursivas a ``buscarDesde``. Es difícil predecir cuántas de estas llamadas recursivas se utilizarán, ya que todas ellas están conectadas por instrucciones ``or``. Si la primera llamada a ``buscarDesde`` devuelve ``True``, entonces ninguna de las tres últimas llamadas sería necesaria. Esto puede interpretarse como queriendo decir que un paso a ``(fila-1, columna)`` (o Norte si se quiere pensar geográficamente) está en el camino hacia la salida del laberinto. Si no hay un buen camino hacia el Norte para salir del laberinto, entonces se intenta la siguiente llamada recursiva, ésta al Sur. Si el Sur falla, se intenta entonces hacia el Oeste y finalmente hacia el Este. Si las cuatro llamadas recursivas devuelven False, entonces hemos encontrado un callejón sin salida. Usted debe descargar o transcribir todo el programa y experimentar con él cambiando el orden de estas llamadas.

.. You will notice that in the recursive step there are four recursive calls to ``buscarDesde``. It is hard to predict how many of these recursive calls will be used since they are all connected by ``or`` statements. If the first call to ``buscarDesde`` returns ``True`` then none of the last three calls would be needed. You can interpret this as meaning that a step to ``(row-1,column)`` (or North if you want to think geographically) is on the path leading out of the maze. If there is not a good path leading out of the maze to the North then the next recursive call is tried, this one to the South. If South fails then try West, and finally East. If all four recursive calls return false then we have found a dead end. You should download or type in the whole program and experiment with it by changing the order of these calls.

El código de la clase ``Laberinto`` se muestra en el :ref:`Programa 4 <lst_maze>`, en el :ref:`Programa 5 <lst_maze1>` y en el :ref:`Programa 6 <lst_maze2>`. El método ``__init__`` toma el nombre de un archivo como su único parámetro. Este archivo es un archivo de texto que representa un laberinto usando caracteres “+” para las paredes, espacios en blanco para los cuadrados abiertos y la letra “S” para indicar la posición de inicio. La :ref:`Figura 3 <fig_exmaze>` es un ejemplo de un archivo de datos del laberinto. La representación interna del laberinto es una lista de listas. Cada fila de la variable ``listalaberinto`` también es una lista. Esta lista secundaria contiene un carácter por cada cuadrado utilizando los caracteres descritos anteriormente. Para el archivo de datos en la :ref:`Figura 3 <fig_exmaze>` la representación interna se parece a la siguiente:

.. The code for the ``Laberinto`` class is shown in :ref:`Listing 4 <lst_maze>`, :ref:`Listing 5 <lst_maze1>`, and :ref:`Listing 6 <lst_maze2>`. The ``__init__`` method takes the name of a file as its only parameter. This file is a text file that represents a maze by using “+” characters for walls, spaces for open squares, and the letter “S” to indicate the starting position. :ref:`Figure 3 <fig_exmaze>` is an example of a maze data file. The internal representation of the maze is a list of lists. Each row of the ``listalaberinto`` instance variable is also a list. This secondary list contains one character per square using the characters described above. For the data file in :ref:`Figure 3 <fig_exmaze>` the internal representation looks like the following:

.. highlight:: python
    :linenothreshold: 500

::

    [ ['+','+','+','+',...,'+','+','+','+','+','+','+'],
      ['+',' ',' ',' ',...,' ',' ',' ','+',' ',' ',' '],
      ['+',' ','+',' ',...,'+','+',' ','+',' ','+','+'],
      ['+',' ','+',' ',...,' ',' ',' ','+',' ','+','+'],
      ['+','+','+',' ',...,'+','+',' ','+',' ',' ','+'],
      ['+',' ',' ',' ',...,'+','+',' ',' ',' ',' ','+'],
      ['+','+','+','+',...,'+','+','+','+','+',' ','+'],
      ['+',' ',' ',' ',...,'+','+',' ',' ','+',' ','+'],
      ['+',' ','+','+',...,' ',' ','+',' ',' ',' ','+'],
      ['+',' ',' ',' ',...,' ',' ','+',' ','+','+','+'],
      ['+','+','+','+',...,'+','+','+',' ','+','+','+']]

El método ``dibujarLaberinto`` utiliza esta representación interna para dibujar en la pantalla la vista inicial del laberinto.

.. The ``dibujarLaberinto`` method uses this internal representation to draw the initial view of the maze on the screen.

.. _fig_exmaze:


Figura 3: Un ejemplo del archivo de datos del laberinto

::
    
      ++++++++++++++++++++++
      +   +   ++ ++     +   
      + +   +       +++ + ++
      + + +  ++  ++++   + ++
      +++ ++++++    +++ +  +
      +          ++  ++    +
      +++++ ++++++   +++++ +
      +     +   +++++++  + +
      + +++++++      S +   +
      +                + +++
      ++++++++++++++++++ +++

El método ``actualizarPosicion``, como se muestra en el :ref:`Programa 5 <lst_maze1>`, utiliza la misma representación interna para ver si la tortuga se ha encontrado con una pared. También actualiza la representación interna con un “.” o un “-” para indicar que la tortuga ha visitado un cuadrado particular o si el cuadrado es parte de un callejón sin salida. Además, el método ``actualizarPosicion`` utiliza dos métodos auxiliares, ``moverTortuga`` y ``tirarMigaDePan``, para actualizar la vista en la pantalla.

.. The ``actualizarPosicion`` method, as shown in :ref:`Listing 5 <lst_maze1>` uses the same internal representation to see if the turtle has run into a wall. It also updates the internal representation with a “.” or “-” to indicate that the turtle has visited a particular square or if the square is part of a dead end. In addition, the ``actualizarPosicion`` method uses two helper methods, ``moverTortuga`` and ``tirarMigaDePan``, to update the view on the screen.

Finalmente, el método ``esSalida`` utiliza la posición actual de la tortuga para probar una condición de salida. Una condición de salida se da cuando la tortuga ha navegado hasta el borde del laberinto, ya sea la fila cero o la columna cero, o la columna de la derecha o la fila inferior.

.. Finally, the ``esSalida`` method uses the current position of the turtle to test for an exit condition. An exit condition is whenever the turtle has navigated to the edge of the maze, either row zero or column zero, or the far right column or the bottom row.

.. _lst_maze:

**Programa 4**

.. highlight:: python
    :linenothreshold: 500

::

    class Laberinto:
        def __init__(self,nombreArchivoLaberinto):
            filasEnLaberinto = 0
            columnasEnLaberinto = 0
            self.listaLaberinto = []
            archivoLaberinto = open(nombreArchivoLaberinto,'r')
            filasEnLaberinto = 0
            for linea in archivoLaberinto:
                listaFila = []
                columna = 0
                for caracter in linea[:-1]:
                    listaFila.append(caracter)
                    if caracter == 'S':
                        self.filaInicio = filasEnLaberinto
                        self.columnaInicio = columna
                    columna = columna + 1
                filasEnLaberinto = filasEnLaberinto + 1
                self.listaLaberinto.append(listaFila)
                columnasEnLaberinto = len(listaFila)

            self.filasEnLaberinto = filasEnLaberinto
            self.columnasEnLaberinto = columnasEnLaberinto
            self.xTranslate = -columnasEnLaberinto/2
            self.yTranslate = filasEnLaberinto/2
            self.t = Turtle(shape='turtle')
            setup(width=600,height=600)
            setworldcoordinates(-(columnasEnLaberinto-1)/2-.5,
                                -(filasEnLaberinto-1)/2-.5,
                                (columnasEnLaberinto-1)/2+.5,
                                (filasEnLaberinto-1)/2+.5)

.. _lst_maze1:

**Programa 5**

::

        def dibujarLaberinto(self):
            for y in range(self.filasEnLaberinto):
                for x in range(self.columnasEnLaberinto):
                    if self.listaLaberinto[y][x] == OBSTACULO:
                        self.dibujarCajaCentrada(x+self.xTranslate,
                                             -y+self.yTranslate,
                                             'tan')
            self.t.color('black','blue')

        def dibujarCajaCentrada(self,x,y,color):
            tracer(0)
            self.t.up()
            self.t.goto(x-.5,y-.5)
            self.t.color('black',color)
            self.t.setheading(90)
            self.t.down()
            self.t.begin_fill()
            for i in range(4):
                self.t.forward(1)
                self.t.right(90)
            self.t.end_fill()
            update()
            tracer(1)

        def moverTortuga(self,x,y):
            self.t.up()
            self.t.setheading(self.t.towards(x+self.xTranslate,
                                             -y+self.yTranslate))
            self.t.goto(x+self.xTranslate,-y+self.yTranslate)

        def tirarMigaDePan(self,color):
            self.t.dot(color)

        def actualizarPosicion(self,fila,columna,val=None):
            if val:
                self.listaLaberinto[fila][columna] = val
            self.moverTortuga(columna,fila)

            if val == PARTE_DEL_CAMINO:
                color = 'green'
            elif val == OBSTACULO:
                color = 'red'
            elif val == INTENTADO:
                color = 'black'
            elif val == CAJELLON_SIN_SALIDA:
                color = 'red'
            else:
                color = None
                
            if color:
                self.tirarMigaDePan(color)

.. _lst_maze2:

**Programa 6**

::

       def esSalida(self,fila,columna):
            return (fila == 0 or
                    fila == self.filasEnLaberinto-1 or
                    columna == 0 or
                    columna == self.columnasEnLaberinto-1 )

       def __getitem__(self,indice):
            return self.listaLaberinto[indice]

El programa completo se muestra en el ActiveCode 1. Este programa utiliza el archivo de datos ``laberinto2.txt`` que se muestra a continuación. Tenga en cuenta que es un archivo de ejemplo mucho más simple en que la salida está muy cerca de la posición inicial de la tortuga.

.. The complete program is shown in ActiveCode 1.  This program uses the data file ``maze2.txt`` shown below. Note that it is a much more simple example file in that the exit is very close to the starting position of the turtle.

.. raw:: html

	<pre id="laberinto2.txt">
  ++++++++++++++++++++++
  +   +   ++ ++        +
        +     ++++++++++
  + +    ++  ++++ +++ ++
  + +   + + ++    +++  +
  +          ++  ++  + +
  +++++ + +      ++  + +
  +++++ +++  + +  ++   +
  +          + + S+ +  +
  +++++ +  + + +     + +
  ++++++++++++++++++++++
    </pre>

.. activecode:: completemaze
    :caption: Solucionador completo del laberinto
    :nocodelens:
    :timelimit: off

    import turtle

    PARTE_DEL_CAMINO = 'O'
    INTENTADO = '.'
    OBSTACULO = '+'
    CAJELLON_SIN_SALIDA = '-'

    class Laberinto:
        def __init__(self,nombreArchivoLaberinto):
            filasEnLaberinto = 0
            columnasEnLaberinto = 0
            self.listaLaberinto = []
            archivoLaberinto = open(nombreArchivoLaberinto,'r')
            filasEnLaberinto = 0
            for linea in archivoLaberinto:
                listaFila = []
                columna = 0
                for caracter in linea[:-1]:
                    listaFila.append(caracter)
                    if caracter == 'S':
                        self.filaInicio = filasEnLaberinto
                        self.columnaInicio = columna
                    columna = columna + 1
                filasEnLaberinto = filasEnLaberinto + 1
                self.listaLaberinto.append(listaFila)
                columnasEnLaberinto = len(listaFila)

            self.filasEnLaberinto = filasEnLaberinto
            self.columnasEnLaberinto = columnasEnLaberinto
            self.xTranslate = -columnasEnLaberinto/2
            self.yTranslate = filasEnLaberinto/2
            self.t = turtle.Turtle()
            self.t.shape('turtle')
            self.wn = turtle.Screen()
            self.wn.setworldcoordinates(-(columnasEnLaberinto-1)/2-.5,-(filasEnLaberinto-1)/2-.5,(columnasEnLaberinto-1)/2+.5,(filasEnLaberinto-1)/2+.5)

        def dibujarLaberinto(self):
            self.t.speed(10)
            self.wn.tracer(0)        
            for y in range(self.filasEnLaberinto):
                for x in range(self.columnasEnLaberinto):
                    if self.listaLaberinto[y][x] == OBSTACULO:
                        self.dibujarCajaCentrada(x+self.xTranslate,-y+self.yTranslate,'orange')
            self.t.color('black')
            self.t.fillcolor('blue')
            self.wn.update()
            self.wn.tracer(1)

        def dibujarCajaCentrada(self,x,y,color):
            self.t.up()
            self.t.goto(x-.5,y-.5)
            self.t.color(color)
            self.t.fillcolor(color)
            self.t.setheading(90)
            self.t.down()
            self.t.begin_fill()
            for i in range(4):
                self.t.forward(1)
                self.t.right(90)
            self.t.end_fill()

        def moverTortuga(self,x,y):
            self.t.up()
            self.t.setheading(self.t.towards(x+self.xTranslate,-y+self.yTranslate))
            self.t.goto(x+self.xTranslate,-y+self.yTranslate)

        def tirarMigaDePan(self,color):
            self.t.dot(10,color)

        def actualizarPosicion(self,fila,columna,val=None):
            if val:
                self.listaLaberinto[fila][columna] = val
            self.moverTortuga(columna,fila)

            if val == PARTE_DEL_CAMINO:
                color = 'green'
            elif val == OBSTACULO:
                color = 'red'
            elif val == INTENTADO:
                color = 'black'
            elif val == CAJELLON_SIN_SALIDA:
                color = 'red'
            else:
                color = None

            if color:
                self.tirarMigaDePan(color)

        def esSalida(self,fila,columna):
            return (fila == 0 or
                    fila == self.filasEnLaberinto-1 or
                    columna == 0 or
                    columna == self.columnasEnLaberinto-1 )
        
        def __getitem__(self,indice):
            return self.listaLaberinto[indice]


    def buscarDesde(laberinto, filaInicio, columnaInicio):
        laberinto.actualizarPosicion(filaInicio, columnaInicio)
       #  Verificar casos base:
       #  1. Hemos tropezado con un obstáculo, devolver False
        if laberinto[filaInicio][columnaInicio] == OBSTACULO :
            return False
        #  2. Hemos encontrado un cuadrado que ya ha sido explorado
        if laberinto[filaInicio][columnaInicio] == INTENTADO:
            return False
        # 3. Éxito, un borde exterior no ocupado por un obstáculo
        if laberinto.esSalida(filaInicio,columnaInicio):
            laberinto.actualizarPosicion(filaInicio, columnaInicio, PARTE_DEL_CAMINO)
            return True
        laberinto.actualizarPosicion(filaInicio, columnaInicio, INTENTADO)

        # De lo contrario, use cortocircuitos lógicos para probar cada
        # dirección a su vez (si fuera necesario)
        encontrado = buscarDesde(laberinto, filaInicio-1, columnaInicio) or \
                buscarDesde(laberinto, filaInicio+1, columnaInicio) or \
                buscarDesde(laberinto, filaInicio, columnaInicio-1) or \
                buscarDesde(laberinto, filaInicio, columnaInicio+1)
        if encontrado:
            laberinto.actualizarPosicion(filaInicio, columnaInicio, PARTE_DEL_CAMINO)
        else:
            laberinto.actualizarPosicion(filaInicio, columnaInicio, CAJELLON_SIN_SALIDA)
        return encontrado

    miLaberinto = Laberinto('laberinto2.txt')
    miLaberinto.dibujarLaberinto()
    miLaberinto.actualizarPosicion(miLaberinto.filaInicio,miLaberinto.columnaInicio)

    buscarDesde(miLaberinto, miLaberinto.filaInicio, miLaberinto.columnaInicio)

.. admonition:: Autoevaluación

   Modifique el programa de búsqueda en un laberinto para que las llamadas a buscarDesde se encuentren en un orden diferente. Vea la ejecución del programa. ¿Puede usted explicar por qué el comportamiento es diferente? ¿Puede usted predecir qué camino seguirá la tortuga para un cambio dado del orden?
