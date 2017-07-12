..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Listas
------

A lo largo de la discusión de las estructuras de datos básicas, hemos utilizado listas de Python para implementar los tipos abstractos de datos presentados. La lista es un mecanismo de colección potente, pero simple, que proporciona al programador una amplia variedad de operaciones. Sin embargo, no todos los lenguajes de programación incluyen una colección de listas. En estos casos, la noción de una lista debe ser implementada por el programador.

.. Throughout the discussion of basic data structures, we have used Python lists to implement the abstract data types presented. The list is a powerful, yet simple, collection mechanism that provides the programmer with a wide variety of operations. However, not all programming languages include a list collection. In these cases, the notion of a list must be implemented by the programmer.

Una **lista** es una colección de ítems donde cada ítem mantiene una posición relativa con respecto a los otros. Más específicamente, nos referiremos a este tipo de lista como una lista no ordenada. Podemos considerar que la lista tiene un primer ítem, un segundo ítem, un tercer ítem, y así sucesivamente. También podemos referirnos al inicio de la lista (el primer ítem) o al final de la lista (el último). Por simplicidad, asumiremos que las listas no pueden contener ítems duplicados.

.. A **list** is a collection of items where each item holds a relative position with respect to the others. More specifically, we will refer to this type of list as an unordered list. We can consider the list as having a first item, a second item, a third item, and so on. We can also refer to the beginning of the list (the first item) or the end of the list (the last item). For simplicity we will assume that lists cannot contain duplicate items.

Por ejemplo, la colección de números enteros 54, 26, 93, 17, 77 y 31 puede representar una lista desordenada simple de calificaciones de exámenes. Tenga en cuenta que los hemos escrito como valores delimitados por comas, una forma común de mostrar la estructura de la lista. Por supuesto, Python mostraría esta lista como :math:`[54,26,93,17,77,31]`.

.. For example, the collection of integers 54, 26, 93, 17, 77, and 31 might represent a simple unordered list of exam scores. Note that we have written them as comma-delimited values, a common way of showing the list structure. Of course, Python would show this list as :math:`[54,26,93,17,77,31]`.
