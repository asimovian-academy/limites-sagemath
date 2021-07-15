PRECÁLCULO
==========

FUNCIONES Y SUS LÍMITES
-----------------------

Juliho Castillo Colmenares 
~~~~~~~~~~~~~~~~~~~~~~~~~~

*IMPORTANTE: Para correr el siguiente código,
necesitarás*\ `Sagemath. <https://youtu.be/8KT9GMruOrU>`__

El cálculo es muy diferente de las matemáticas que has estudiado hasta
hoy, porque tiene que ver con cambios. En esta sección estudiaremos el
comportamiento en cambio de funciones y sus límites.

.. _funciones-y-su-representación:

Funciones y su representación. 
------------------------------

Las funciones surgen cuando una cantidad depende de otra. Consideremos
algunos ejemplos.

Ejemplo A
~~~~~~~~~

| El área de un círculo depende del radio del mismo:
| :math:` A = \pi r^2 `

.. code:: python

   def area_circulo(radio):
       return 3.14159*radio^2

   print(area_circulo(2.5267490372))

.. code:: 

   20.0573578810604

Ejemplo B
~~~~~~~~~

La población humana (en todo el mundo) :math:`P` depende del tiempo
:math:`t`. En la siguiente tabla, se muestra el año y la población en
milliones correspondiente:

.. code:: python

   poblacion = [
       [1900, 1650],
       [1910, 1750],
       [1920, 1860],
       [1930, 2070],
       [1940, 2300],
       [1950, 2560],
       [1960, 3040],
       [1970, 3710],
       [1980, 4450],
       [1990, 5280],
       [2000, 6080],
       [2010, 6870]
               ]

A partir de esta tabla, podemos crear una función punto a punto:

.. code:: python

   def P(t):
       for dato in poblacion:
           if t==dato[0]:
               return dato[1]
           
   print(P(1950))

.. code:: 

   2560

Ejemplo C
~~~~~~~~~

El costo :math:`C` de enviar un paquete depende del peso :math:`w`. Por
ejemplo, supongamos que los precio están dados por las siguiente reglas:

-  Menor o igual a 10 kgs: Costo fijo de $150 más $10 por kilogramo

-  Mayor a 10 kgs: $25 por kilogramo

-  La capacidad máxima del envíoi es 20 kgs

.. code:: python

   """
   Definimos la función de costo C en función del peso w
   """
   def C(w):
       if w<0:
           return "¿Seguro que estás enviando algo?"
       elif w<=10:
           return 150 + 10*w
       elif w<=20:
           return 25*w
       else:
           return "¡Excediste la capacidad!"    

.. code:: python

   """
   Graficamos en el intervalo (0,20)
   """
   import numpy as np
   import matplotlib.pyplot as plt

   x = np.arange(0,20,0.01)
   C = np.vectorize(C)
   y = C(x)

   plt.plot(x,y)
   plt.show()

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_10_0.png
   :alt: 

Ejemplo D
~~~~~~~~~

| La aceleracion vertical :math:`a` del suelo en un terremoto
| |image1|

.. code:: python

   """
   Simularemos la acelaración a respecto al tiempo t
   """
   def a(t):
       return np.sin(t)*np.random.normal()

.. code:: python

   """
   Graficamos en el intervalo (0, pi)
   """
   x = np.arange(0,np.pi,0.01)
   a = np.vectorize(a)
   y = a(x)

   plt.plot(x,y)

.. code:: 

   [<matplotlib.lines.Line2D object at 0x6ffe91c1f1d0>]

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_13_1.png
   :alt: 

Una **función** :math:`f` es una regla que asigna a cada elemento
:math:`x` de un conjunto :math:`D` un elemento :math:`f(x)` de un
conjunto :math:`E`.

Al conjunto :math:`D` se le llama **dominio**, mientras que a :math:`E`
se le llama **contradominio**.

.. code:: python

   x = var("x")
   f(x) = exp(-x^2)*sin(x)
   grafica = plot(f)
   show(grafica)

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_15_0.png
   :alt: 

.. code:: python

   grafica = plot(f, (x,-5,5))
   show(grafica)

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_16_0.png
   :alt: 

Representación de funciones
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _ejercicio-1:

Ejercicio
^^^^^^^^^

Encuentre el dominio de cada función:

-  :math:`f(x)=\sqrt{x+2}`

-  :math:`g(x)=\dfrac{1}{x^2-x}`

Prueba de la linea vertical 
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Una curva en el plano :math:`xy` es la gráfica de una función
:math:`y=f(x)` si y solo si no existe línea vertical alguna que
intersecte la curva más de dos veces.

.. _ejemplo-1:

Ejemplo
^^^^^^^

Determina si la ecuación :math:`x^2-y^2=1` define una función
:math:`y=f(x)`.

.. code:: python

   x,y = var("x,y")
   ecuacion = x^2-y^2==1
   grafica = implicit_plot(ecuacion, (x,-2,2), (y,-2,2))
   show(grafica)

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_21_0.png
   :alt: 

.. _ejemplo-2:

Ejemplo
^^^^^^^

Determina si la ecuación :math:`(x-1)^2=4(y-2)` define una función
:math:`y=f(x)`.

.. code:: python

   x,y = var("x,y")
   ecuacion = (x-1)^2==4*(y-2)
   grafica = implicit_plot(ecuacion, (x,0,2), (y,1,3))
   show(grafica)

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_23_0.png
   :alt: 

.. _ejemplo-3:

Ejemplo 
^^^^^^^

| Determina si la gráfica de las ecuaciones paramétricas:
| :math:` x = 10t, y = 50+5t-\dfrac{1}{2}(9.8)t^2`
| define una función :math:`y=f(x)`.

.. code:: python

   t = var("t")
   x(t) = 10*t
   y(t) = 50+5*t-(1/2)*(9.8)*t^2
   grafica = parametric_plot((x(t),y(t)), (t,0,1))

   show(grafica)

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_25_0.png
   :alt: 

.. _ejercicio-de-exploración-1:

Ejercicio de exploración
^^^^^^^^^^^^^^^^^^^^^^^^

Las funciones anteriores representan la posición de un proyectil en
función del tiempo. Determina gráficamente:

-  la distancia a la que choca contra el suelo

-  cuanto tiempo tarde en ocurrir esto

-  la altura máxima y el tiempo en que se alcanza

¿Puedes determinar cuál es la función :math:`y=f(x)`?

.. _ejercicio-de-exploración-2:

Ejercicio de exploración
^^^^^^^^^^^^^^^^^^^^^^^^

Muchas relaciones fundamentales en matemáticas y física no se pueden
expresar como funciones. Aún así se puede definir el dominio de una
relación. Averigua en internet como es que se hace esto y determinalo
gráficamente para la relación

:math:` \dfrac{(x-2)^2}{9} + \dfrac{(y-3)^2}{4} = 1. `

*¿Cuál es el intervalo minimal en el eje :math:`y` que necesitas para
graficar completamente la relación?*

Funciones representadas a trozos
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _ejemplo-4:

Ejemplo
^^^^^^^

| Una función :math:`f` esta definida por
| :math:`f(x)=
  \begin{cases}
  1-x & x \leq 1\\
  x^2 & x>1
  \end{cases}
  `

Evaluar :math:`f(0), f(1), f(2)` y graficar la función.

.. code:: python

   def f(x):
       if x<=1:
           return 1-x
       else:
           return x**2

.. code:: python

   import numpy as np
   f = np.vectorize(f)
   x = [0,1,2]
   y = f(x)
   print(y)

.. code:: 

   [1 0 4]

.. code:: python

   import matplotlib.pyplot as plt

   x = np.arange(0,2,0.001)
   y = f(x)

   plt.plot(x,y)
   plt.show()

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_32_0.png
   :alt: 

Ejercicio (Valor absoluto)
^^^^^^^^^^^^^^^^^^^^^^^^^^

-  Investiga como se define la función *valor absoluto*

-  Implementala en ``Python``

-  Evaluala en el arreglo :math:`x=-1,0,1`

-  Traza la gráfica

Simetría
~~~~~~~~

Si una función :math:`f(x)` satisface la relación :math:`f(x)=f(-x)` en
su dominio, diremos que la función es **par**. Su gráfica es simétrica
respecto al eje :math:`y`.

.. _ejemplo-5:

Ejemplo
^^^^^^^

:math:` f(x) = x^2 `

.. code:: python

   x = var("x")
   f(x) = x^2
   show(f(-x))

\\newcommand{\Bold}[1]{\mathbf{#1}}x^{2}

.. code:: python

   plot(f)

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_37_0.png
   :alt: 

.. _ejemplo-6:

Ejemplo
^^^^^^^

:math:` g(x) = cos(x) `

.. code:: python

   x = var("x")
   g(x) = cos(x)
   show(g(-x).simplify())

\\newcommand{\Bold}[1]{\mathbf{#1}}\cos\left(x\right)

.. code:: python

   plot(g, (x,-2*pi, 2*pi))

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_40_0.png
   :alt: 

Si una función :math:`f(x)` satisface la relación :math:`f(-x)=-f(x)` en
su dominio, diremos que la función es **impar**. Su gráfica es simétrica
respecto al origen.

Ejemplo 4
^^^^^^^^^

:math:`f(x) = x^3`

.. code:: python

   x = var("x")
   f(x) = x^3
   show(f(-x).simplify())

\\newcommand{\Bold}[1]{\mathbf{#1}}-x^{3}

.. code:: python

   plot(f)

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_44_0.png
   :alt: 

.. _ejemplo-7:

Ejemplo 
^^^^^^^

:math:`g(x) = \sin(x)`

.. code:: python

   x = var("x")
   g(x) = sin(x)
   show(g(-x).simplify())

\\newcommand{\Bold}[1]{\mathbf{#1}}-\sin\left(x\right)

.. code:: python

   plot(g, (x,-pi,pi))

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_47_0.png
   :alt: 

.. _ejercicio-2:

Ejercicio
^^^^^^^^^

Determina si las siguiente funciones son pares, impares o ninguna:

-  :math:`f(x)=x^5+x`

-  :math:`g(x)=1-x^4`

-  :math:`h(x)=2x-x^2`

Funciones crecientes y decrecientes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

| Una función :math:`f` es **creciente** en un intervalo :math:`I` si
| :math:`f(x_0) < f(x_1)` siempre que :math:`x_1 < x_2`.

| Una función :math:`f` es **decreciente** en un intervalo :math:`I` si
| :math:`f(x_0) < f(x_1)` siempre que :math:`x_1 < x_2`.

**Observación** El intervalo es muy importante para determinar si la
función es creciente o no. Consideremos la función :math:`f(x)=x^2` en
los intervalos

-  :math:`I=(-1,0)`

-  :math:`I=(0,1)`

-  :math:`I=(-1,-1)`

.. code:: python

   x = var("x")
   f(x) = x^2

.. code:: python

   plot(f, (x,-1,0))

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_52_0.png
   :alt: 

.. code:: python

   plot(f, (x,0,1))

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_53_0.png
   :alt: 

.. code:: python

   plot(f, (x,-1,1))

.. figure:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\output_54_0.png
   :alt: 

.. |image1| image:: C:\Users\julih\Dropbox%20(Centro%20Turing)\Repositorios\precalculo-sagemath\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACI%C3%93N\%5B1%5D%20FUNCIONES%20Y%20SU%20REPRESENTACION\IM10101.png
