..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Ejercicios de programación
--------------------------

#. Diseñe un experimento aleatorio para probar la diferencia entre una búsqueda secuencial y una búsqueda binaria en una lista de enteros.

#. Utilice las funciones de búsqueda binaria que aparecen en el texto (la recursiva y la iterativa). Genere una lista ordenada aleatoria de números enteros y realice una prueba de referencia (benchmark) para cada función. ¿Cuáles son sus resultados? ¿Puede explicarlos?

#. Implemente la búsqueda binaria usando recursión sin el operador de partición. Recuerde que tendrá que pasar la lista junto con los valores de los índices inicial y final para la sublista. Genere una lista ordenada y aleatoria de números enteros y realice una prueba de referencia.

#. Implemente el método ``len`` (\_\_len\_\_) para la implementación del TAD Vector Asociativo de las tablas hash.

#. Implemente el método ``in`` (\_\_contains\_\_) para la implementación del TAD Vector Asociativo de las tablas hash.

#. ¿Cómo puede usted eliminar ítems de una tabla hash que utiliza encadenamiento para la solución de colisiones? ¿Qué tal si se usa direccionamiento abierto? ¿Cuáles son las circunstancias especiales que deben manejarse? Implemente el método ``eliminar`` para la clase ``TablaHash``.

#. En la implementación de Vector Asociativo de las tablas hash, se eligió que el tamaño de la tabla hash fuera 11. Si la tabla se llena, ésta debe agrandarse. Vuelva a implementar el método ``agregar`` para que la tabla se redimensione automáticamente cuando el factor de carga alcance un valor predeterminado (usted puede decidir el valor con base en su apreciación de la carga en función del desempeño).

#. Implemente la prueba cuadrática como una técnica de rehash.

#. Utilizando un generador de números aleatorios, cree una lista de 500 enteros. Realice una prueba de referencia usando algunos de los algoritmos de ordenamiento de este capítulo. ¿Cuál es la diferencia en la velocidad de ejecución?

#. Implemente el ordenamiento burbuja usando asignación simultánea.

#. Un ordenamiento burbuja puede modificarse para que “burbujee” en ambas direcciones. La primera pasada mueve la lista hacia “arriba”, y la segunda pasada la mueve hacia “abajo”. Este patrón alternante continúa hasta que no son necesarias más pasadas. Implemente esta variación y describa en qué circunstancias podría ser apropiada.

#. Implemente el ordenamiento por selección usando asignación simultánea.

#. Realice una prueba de referencia para un ordenamiento de Shell, utilizando diferentes conjuntos de incrementos en la misma lista.

#. Implemente la función ``ordenamientoPorMezcla`` sin usar el operador de partición.

#. Una forma de mejorar el ordenamiento rápido es usar un ordenamiento por inserción en listas que tengan una longitud pequeña (llamémosla “límite de partición”). ¿Por qué esto tiene sentido? Re-implemente el ordenamiento rápido y utilícelo para ordenar una lista aleatoria de enteros. Realice un análisis utilizando diferentes tamaños de lista para el límite de partición.

#. Implemente el método de mediana de tres para seleccionar un valor pivote como una modificación de ``ordenamientoRapido``. Lleve a cabo un experimento para comparar las dos técnicas.
