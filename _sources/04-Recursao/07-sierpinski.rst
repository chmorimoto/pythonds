..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Sierpinski Triangle

Triângulo de Sierpinski
-----------------------


..  Another fractal that exhibits the property of self-similarity is the
    Sierpinski triangle. An example is shown in :ref:`Figure 3 <fig_sierpinski>`. The
    Sierpinski triangle illustrates a three-way recursive algorithm. The
    procedure for drawing a Sierpinski triangle by hand is simple. Start
    with a single large triangle. Divide this large triangle into four new
    triangles by connecting the midpoint of each side. Ignoring the middle
    triangle that you just created, apply the same procedure to each of the
    three corner triangles. Each time you create a new set of triangles, you
    recursively apply this procedure to the three smaller corner triangles.
    You can continue to apply this procedure indefinitely if you have a
    sharp enough pencil. Before you continue reading, you may want to try
    drawing the Sierpinski triangle yourself, using the method described.

Outro fractal que exibe a propriedade da auto-similaridade é o
Triângulo de Sierpinski. Um exemplo é mostrado na :ref:`Figura 3 <fig_sierpinski>`. 
O triângulo de Sierpinski ilustra um algoritmo recursivo de três vias. O
procedimento para desenhar um triângulo de Sierpinski à mão é simples. Comece
com um único triângulo grande. Divida este triângulo em quatro novos
triângulos ligando o ponto médio de cada lado. Ignorando o triângulo do meio 
que acabou de criar, aplique o mesmo procedimento a cada um dos
três triângulos nos cantos. Cada vez que você criar um novo conjunto de triângulos,
recursivamente aplique este procedimento para os três triângulos menores nos cantos.
Você pode continuar a aplicar este procedimento indefinidamente se tiver um
lápis bastante afiado. Antes de continuar lendo, tente
desenhar um triângulo de Sierpinski usando esse método.

.. _fig_sierpinski:

.. figure:: Figures/sierpinski.png
     :align: center

     Figura 3: O Triângulo de Sierpinski

..  Since we can continue to apply the algorithm indefinitely, what is the
    base case? We will see that the base case is set arbitrarily as the
    number of times we want to divide the triangle into pieces. Sometimes we
    call this number the “degree” of the fractal. Each time we make a
    recursive call, we subtract 1 from the degree until we reach 0. When we
    reach a degree of 0, we stop making recursive calls. The code that
    generated the Sierpinski Triangle in :ref:`Figure 3 <fig_sierpinski>` is shown in
    :ref:`ActiveCode 1 <lst_st>`.

Como podemos continuar aplicando o algoritmo indefinidamente, qual é o
caso base? Vamos ver que o caso base é definido arbitrariamente como o
número de vezes que queremos dividir o triângulo em pedaços. As vezes nós
chamamos esse número de "grau" do fractal. Cada vez que fazemos uma
chamada recursiva, subtraímos 1 do grau até chegarmos a 0. Quando
atingirmos o grau 0, paramos de fazer chamadas recursivas. O código que
gerou o Triângulo de Sierpinski na :ref:`Figura 3 <fig_sierpinski>` é mostrado no
:ref:`ActiveCode 1 <lst_st>`.


.. activecode:: lst_st
    :caption: Desenhando um Triângulo de Sierpinski
    :nocodelens:

    import turtle

    def drawTriangle(points,color,myTurtle):
        myTurtle.fillcolor(color)
        myTurtle.up()
        myTurtle.goto(points[0][0],points[0][1])
        myTurtle.down()
        myTurtle.begin_fill()
        myTurtle.goto(points[1][0],points[1][1])
        myTurtle.goto(points[2][0],points[2][1])
        myTurtle.goto(points[0][0],points[0][1])
        myTurtle.end_fill()

    def getMid(p1,p2):
        return ( (p1[0]+p2[0]) / 2, (p1[1] + p2[1]) / 2)

    def sierpinski(points,degree,myTurtle):
        colormap = ['blue','red','green','white','yellow',
                    'violet','orange']
        drawTriangle(points,colormap[degree],myTurtle)
        if degree > 0:
            sierpinski([points[0],
                            getMid(points[0], points[1]),
                            getMid(points[0], points[2])],
                       degree-1, myTurtle)
            sierpinski([points[1],
                            getMid(points[0], points[1]),
                            getMid(points[1], points[2])],
                       degree-1, myTurtle)
            sierpinski([points[2],
                            getMid(points[2], points[1]),
                            getMid(points[0], points[2])],
                       degree-1, myTurtle)

    def main():
       myTurtle = turtle.Turtle()
       myWin = turtle.Screen()
       myPoints = [[-100,-50],[0,100],[100,-50]]
       sierpinski(myPoints,3,myTurtle)
       myWin.exitonclick()

    main()


..  The program in :ref:`ActiveCode 1 <lst_st>` follows the ideas outlined above. The
    first thing ``sierpinski`` does is draw the outer triangle. Next, there
    are three recursive calls, one for each of the new corner triangles we
    get when we connect the midpoints. Once again we make use of the
    standard turtle module that comes with Python. You can learn all the
    details of the methods available in the turtle module by using
    ``help('turtle')`` from the Python prompt.

O programa no :ref:`ActiveCode 1 <lst_st>` segue as idéias descritas acima. 
A primeira coisa que a função ``sierpinski`` faz é desenhar o triângulo externo. Em seguida, 
são feitas três chamadas recursivas, uma para cada um dos novos triângulos que obtemos 
nos cantos quando conectamos os pontos médios. Mais uma vez fazemos uso do
módulo turtle, nativo do Python. Você pode aprender todos os
detalhes dos métodos disponíveis no módulo de turtle usando
``help('turtle')`` do prompt do Python.

..  Look at the code and think about the order in which the triangles will
    be drawn. While the exact order of the corners depends upon how the
    initial set is specified, let’s assume that the corners are ordered
    lower left, top, lower right. Because of the way the ``sierpinski``
    function calls itself, ``sierpinski`` works its way to the smallest
    allowed triangle in the lower-left corner, and then begins to fill out
    the rest of the triangles working back. Then it fills in the triangles
    in the top corner by working toward the smallest, topmost triangle.
    Finally, it fills in the lower-right corner, working its way toward the
    smallest triangle in the lower right.

Olhe para o código e pense na ordem em que os triângulos serão desenhados. 
Enquanto a ordem exata dos cantos depende de como o
conjunto inicial for especificado, vamos supor que os cantos estejam ordenados
como inferior esquerdo, superior e inferior direito. 
Por causa da maneira como a função ``sierpinski`` chama a si mesma,
``sierpinski`` desenha até o menor
triângulo permitido no canto inferior esquerdo e, em seguida, começa a preencher
o resto dos triângulos no caminho de volta. Então preenche os triângulos
no canto superior, desenhando até o menor e mais alto triângulo.
Finalmente, ele preenche o canto inferior direito, desenhando até o 
menor triângulo no canto inferior direito.

..  Sometimes it is helpful to think of a recursive algorithm in terms of a
    diagram of function calls. :ref:`Figure 4 <fig_stcalltree>` shows that the recursive
    calls are always made going to the left. The active functions are
    outlined in black, and the inactive function calls are in gray. The
    farther you go toward the bottom of :ref:`Figure 4 <fig_stcalltree>`, the smaller the
    triangles. The function finishes drawing one level at a time; once it is
    finished with the bottom left it moves to the bottom middle, and so on.

Às vezes é útil pensar em um algoritmo recursivo em termos de um
diagrama de chamadas de função. A :ref:`Figura 4 <fig_stcalltree>` mostra que 
as chamadas recursivas são sempre feitas para a esquerda. As funções ativas são
delineadas em preto, e as chamadas de função inativas estão em cinza. Quanto
mais longe você for em direção ao final da :ref:`Figura 4 <fig_stcalltree>`,
tanto menor serão os triângulos. 
A função termina desenhando um nível de cada vez; uma vez que ela
termina com a parte inferior esquerda, ela se move para a parte inferior do meio, 
e assim por diante.

.. _fig_stcalltree:

.. figure:: Figures/stCallTree.png
    :align: center   
   
    Figura 4: Construindo um Triângulo de Sierpinski

..  The ``sierpinski`` function relies heavily on the ``getMid`` function.
    ``getMid`` takes as arguments two endpoints and returns the point
    halfway between them. In addition, :ref:`ActiveCode 1 <lst_st>` has a function that
    draws a filled triangle using the ``begin_fill`` and ``end_fill`` turtle
    methods.

A função ``sierpinski`` depende muito da função ``getMid``, que
recebe como argumentos dois pontos extremos e retorna o ponto posicionado no
meio entre eles. Além disso, o :ref:`ActiveCode 1 <lst_st>` tem uma função que
desenha um triângulo preenchido usando os métodos ``begin_fill`` e ``end_fill``
do módulo turtle.
