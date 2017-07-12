..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementación
--------------

Teniendo en mente las definiciones de la sección previa, podemos usar las siguientes funciones para crear y manipular un árbol binario:

-  ``ArbolBinario()`` crea una nueva instancia de un árbol binario.

-  ``obtenerHijoIzquierdo()`` devuelve el árbol binario correspondiente al hijo izquierdo del nodo actual.

-  ``obtenerHijoDerecho()`` devuelve el árbol binario correspondiente al hijo derecho del nodo actual.

-  ``asignarValorRaiz(valor)`` almacena el objeto del parámetro ``valor`` en el nodo actual.

-  ``obtenerValorRaiz()`` devuelve el objeto almacenado en el nodo actual.

-  ``insertarIzquierdo(valor)`` crea un nuevo árbol binario y lo instala como el hijo izquierdo del nodo actual.

-  ``insertarDerecho(valor)`` crea un nuevo árbol binario y lo instala como el hijo derecho del nodo actual.

La decisión clave en la implementación de un árbol es escoger una buena técnica de almacenamiento interno. Python nos permite dos posibilidades muy interesantes, así que examinaremos ambas antes de escoger una de ellas. La primera técnica se denomina “lista de listas”, a la segunda técnica la llamaremos de “nodos y referencias”.
