..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Preguntas de discusión
----------------------

#. Indique el desempeño O-grande del siguiente fragmento de código:

   ::

       for i in range(n):
          for j in range(n):
             k = 2 + 2

#. Indique el desempeño O-grande del siguiente fragmento de código:

   ::

       for i in range(n):
            k = 2 + 2

#. Indique el desempeño O-grande del siguiente fragmento de código:

   ::

       i = n
       while i > 0:
          k = 2 + 2
          i = i // 2

#. Indique el desempeño O-grande del siguiente fragmento de código:

   ::

       for i in range(n):
          for j in range(n):
             for k in range(n):
                k = 2 + 2

#. Indique el desempeño O-grande del siguiente fragmento de código:

   ::

       i = n
       while i > 0:
          k = 2 + 2
          i = i // 2

#. Indique el desempeño O-grande del siguiente fragmento de código:

   ::

       for i in range(n):
          k = 2 + 2
       for j in range(n):
          k = 2 + 2
       for k in range(n):
          k = 2 + 2
