..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Resumen de implementaciones del TAD Vector Asociativo
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

En los últimos dos capítulos hemos examinado varias estructuras de datos que se pueden utilizar para implementar el tipo abstracto de datos Vector Asociativo. Una búsqueda binaria en una lista, una tabla hash, un árbol  binario de búsqueda y un árbol binario de búsqueda equilibrado. Para concluir esta sección, vamos a resumir el desempeño de cada estructura de datos para las operaciones clave definidas por el TAD Vector Asociativo (ver la :ref:`Tabla 1 <tab_compare>`).

.. Over the past two chapters we have looked at several data structures that can be used to implement the map abstract data type. A binary Search on a list, a hash table, a binary search tree, and a balanced binary search tree. To conclude this section, let’s summarize the performance of each data structure for the key operations defined by the map ADT (see :ref:`Table 1 <tab_compare>`).


.. _tab_compare:

.. table:: **Tabla 1: Comparación del desempeño de diferentes implementaciones del TAD Vector Asociativo**

    =========== ======================  ============   =========================  ====================
    Operación   Lista ordenada          Tabla hash     Árbol binario de búsqueda  Árbol AVL
    =========== ======================  ============   =========================  ====================
     agregar    :math:`O(n)`            :math:`O(1)`                :math:`O(n)`  :math:`O(\log_2{n})`   
     obtener    :math:`O(\log_2{n})`    :math:`O(1)`                :math:`O(n)`  :math:`O(\log_2{n})`   
         in     :math:`O(\log_2{n})`    :math:`O(1)`                :math:`O(n)`  :math:`O(\log_2{n})`   
    eliminar    :math:`O(n)`            :math:`O(1)`                :math:`O(n)`  :math:`O(\log_2{n})`
    =========== ======================  ============   =========================  ====================
