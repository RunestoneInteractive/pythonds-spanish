..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Problemas de la ruta más corta
------------------------------

Cuando usted navega por la web, envía un correo electrónico o ingresa a una computadora del laboratorio desde otra ubicación en el campus, tras bambalinas se lleva a cabo mucho trabajo para transferir la información de su computadora a otra computadora. El estudio en profundidad de cómo fluye la información de una computadora a otra a través de Internet es el tema principal de una asignatura de redes de computadoras. Sin embargo, hablaremos lo suficiente sobre cómo funciona Internet como para entender otro algoritmo de grafos muy importante.

.. When you surf the web, send an email, or log in to a laboratory computer from another location on campus a lot of work is going on behind the scenes to get the information on your computer transferred to another computer. The in-depth study of how information flows from one computer to another over the Internet is the primary topic for a class in computer networking. However, we will talk about how the Internet works just enough to understand another very important graph algorithm.

.. _fig_inet:

.. figure:: Figures/Internet.png
   :align: center

   Figura 1: Descripción general de la conectividad en Internet

   Figura 1: Descripción general de la conectividad en Internet


La :ref:`Figura 1 <fig_inet>` muestra una visión general de alto nivel de cómo funciona la comunicación en Internet. Cuando usted usa su navegador para solicitar la consulta de una página web de un servidor, la solicitud debe viajar a través de su red de área local y salir a Internet a través de un enrutador. La solicitud viaja a través de Internet y finalmente llega a un enrutador para la red de área local donde se encuentra el servidor. La página web que usted solicitó viaja a través de los mismos enrutadores para llegar a su navegador. Dentro de la nube etiquetada como “Internet” en la :ref:`Figura 1 <fig_inet>` hay enrutadores adicionales. La tarea de todos estos enrutadores es trabajar juntos para lograr que su información viaje de un lugar a otro. Usted podría verificar que hay muchos enrutadores para su computadora si ésta admite el comando ``traceroute``. El texto mostrado a continuación presenta la salida del comando ``traceroute`` que ilustra que hay 13 enrutadores entre el servidor web en el Luther College y el servidor de correo en la Universidad de Minnesota.

.. :ref:`Figure 1 <fig_inet>` shows you a high-level overview of how communication on the Internet works. When you use your browser to request a web page from a server, the request must travel over your local area network and out onto the Internet through a router. The request travels over the Internet and eventually arrives at a router for the local area network where the server is located. The web page you requested then travels back through the same routers to get to your browser. Inside the cloud labelled “Internet” in :ref:`Figure 1 <fig_inet>` are additional routers. The job of all of these routers is to work together to get your information from place to place. You can see there are many routers for yourself if your computer supports the ``traceroute`` command. The text below shows the output of the ``traceroute`` command which illustrates that there are 13 routers between the web server at Luther College and the mail server at the University of Minnesota.

::

         1  192.203.196.1  
         2  hilda.luther.edu (216.159.75.1)  
         3  ICN-Luther-Ether.icn.state.ia.us (207.165.237.137)
         4  ICN-ISP-1.icn.state.ia.us (209.56.255.1)  
         5  p3-0.hsa1.chi1.bbnplanet.net (4.24.202.13)
         6  ae-1-54.bbr2.Chicago1.Level3.net (4.68.101.97)
         7  so-3-0-0.mpls2.Minneapolis1.Level3.net (64.159.4.214)
         8  ge-3-0.hsa2.Minneapolis1.Level3.net (4.68.112.18) 
         9  p1-0.minnesota.bbnplanet.net (4.24.226.74)
         10  TelecomB-BR-01-V4002.ggnet.umn.edu (192.42.152.37)
         11  TelecomB-BN-01-Vlan-3000.ggnet.umn.edu (128.101.58.1)
         12  TelecomB-CN-01-Vlan-710.ggnet.umn.edu (128.101.80.158)
         13  baldrick.cs.umn.edu (128.101.80.129)(N!)  88.631 ms (N!)
            

         Enrutadores desde un servidor hasta el siguiente en Internet      

Cada enrutador en Internet está conectado a uno o más enrutadores. Así que si usted ejecuta el comando ``traceroute`` en diferentes momentos del día, es probable que vea que su información fluye a través de diferentes enrutadores en momentos diferentes. Esto se debe a que hay un costo asociado con cada conexión entre una pareja de enrutadores que depende del volumen de tráfico, la hora del día y muchos otros factores. En este momento no le sorprenderá saber que podemos representar la red de enrutadores como un grafo con aristas ponderadas.

.. Each router on the Internet is connected to one or more other routers. So if you run the ``traceroute`` command at different times of the day, you are likely to see that your information flows through different routers at different times. This is because there is a cost associated with each connection between a pair of routers that depends on the volume of traffic, the time of day, and many other factors. By this time it will not surprise you to learn that we can represent the network of routers as a graph with weighted edges.

.. _fig_network:


.. figure:: Figures/routeGraph.png
   :align: center

   Figura 2: Conexiones y ponderaciones entre enrutadores en Internet

   Figura 2: Conexiones y ponderaciones entre enrutadores en Internet
          

La :ref:`Figura 2 <fig_network>` muestra un pequeño ejemplo de un grafo ponderado que representa la interconexión de enrutadores en Internet. El problema que queremos resolver es encontrar la ruta con la menor ponderación total a través de la cual enrutar cualquier mensaje dado. Este problema debería sonar familiar pues es similar al problema que resolvimos usando una búsqueda en anchura, excepto que aquí nos interesa la ponderación total de la ruta en lugar del número de saltos en ella. Cabe señalar que si todas las ponderaciones son iguales, el problema es el mismo.

.. :ref:`Figure 2 <fig_network>` shows a small example of a weighted graph that represents the interconnection of routers in the Internet. The problem that we want to solve is to find the path with the smallest total weight along which to route any given message. This problem should sound familiar because it is similar to the problem we solved using a breadth first search, except that here we are concerned with the total weight of the path rather than the number of hops in the path. It should be noted that if all the weights are equal, the problem is the same.
