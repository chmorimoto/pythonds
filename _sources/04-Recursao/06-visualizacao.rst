..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Introduction: Visualizing Recursion

Introdução: Visualizando Recursão
=================================


..  In the previous section we looked at some problems that were easy to
    solve using recursion; however, it can still be difficult to find a
    mental model or a way of visualizing what is happening in a recursive
    function. This can make recursion difficult for people to grasp. In this
    section we will look at a couple of examples of using recursion to draw
    some interesting pictures. As you watch these pictures take shape you
    will get some new insight into the recursive process that may be helpful
    in cementing your understanding of recursion.

Na seção anterior, analisamos alguns problemas que eram fáceis de
resolver usando recursão; no entanto, ainda pode ser difícil encontrar um
modelo mental ou uma maneira de visualizar o que está acontecendo em uma função
recursiva. Isso pode fazer com que recursão seja difícil para as pessoas entenderem. 
Nessa seção, vamos ver dois exemplos de uso de recursão para desenhar algumas
figuras interessantes. Ao ver essas figuras serem construídas, você vai ganhar
uma visão mais ampla sobre o processo de recursão que pode lhe ser útil 
na concretização do seu entendimento sobre recursão. 

..  The tool we will use for our illustrations is Python’s turtle graphics
    module called ``turtle``. The ``turtle`` module is standard with all
    versions of Python and is very easy to use. The metaphor is quite
    simple. You can create a turtle and the turtle can move forward,
    backward, turn left, turn right, etc. The turtle can have its tail up or
    down. When the turtle’s tail is down and the turtle moves it draws a
    line as it moves. To increase the artistic value of the turtle you can
    change the width of the tail as well as the color of the ink the tail is
    dipped in.

A ferramenta que vamos usar para criar nossas ilustrações é o módulo 
gráfico do Python chamado ``turtle`` (tartaruga). 
O módulo ``turtle`` faz parte de todas as versões do Python e 
é muito fácil de usar. A metáfora é bem
simples. Você pode criar uma tartaruga e a tartaruga pode andar para frente (*forward*),
para trás (*backward*), virar à esquerda (*left*), virar à direita (*right*), etc. A tartaruga pode 
mover sua cauda para cima (*up*) ou para baixo (*down*).
Quando a cauda da tartaruga está para baixo e a tartaruga se move,
ela desenha uma linha ao se mover. Para aumentar a qualidade dos desenhos
a tartaruga você pode mudar a largura da cauda, ​​bem como a cor da tinta 
onde a cauda é mergulhada.

..  Here is a simple example to illustrate some turtle graphics basics. We
    will use the turtle module to draw a spiral recursively.
    :ref:`ActiveCode 1 <lst_turt1>` shows how it is done. After importing the ``turtle``
    module we create a turtle. When the turtle is created it also creates a
    window for itself to draw in. Next we define the drawSpiral function.
    The base case for this simple function is when the length of the line we
    want to draw, as given by the ``len`` parameter, is reduced to zero or
    less. If the length of the line is longer than zero we instruct the
    turtle to go forward by ``len`` units and then turn right 90 degrees.
    The recursive step is when we call drawSpiral again with a reduced
    length. At the end of :ref:`ActiveCode 1 <lst_turt1>` you will notice that we call
    the function ``myWin.exitonclick()``, this is a handy little method of
    the window that puts the turtle into a wait mode until you click inside
    the window, after which the program cleans up and exits.

O exemplo a seguir ilustra alguns conceitos gráficos básicos para usar uma tartaruga.
Usaremos o módulo turtle para desenhar uma espiral recursivamente.
O :ref:`ActiveCode 1 <lst_turt1>` mostra como isso é feito. 
Depois de importar o módulo ``turtle`` criamos uma tartaruga. 
Quando uma tartaruga é criada, cria-se também uma 
janela para se desenhar. Em seguida, definimos a função drawSpiral.
O caso base para esta função simples é quando o comprimento da linha que
desejamos desenhar, dado pelo parâmetro ``lineLen``, se tornar menor ou igual a zero.
Se o comprimento da linha for maior que zero, instruiremos a
tartaruga para avançar ``lineLen`` unidades e depois virar à direita 90 graus.
O passo recursivo é quando chamamos drawSpiral novamente com um
comprimento menor. No final do :ref:`ActiveCode 1 <lst_turt1>` você notará que chamamos
a função ``myWin.exitonclick()``. Esse é um método prático da
janela que coloca a tartaruga em um modo de espera até que você clique dentro
da janela, causando o término do programa.

.. activecode:: lst_turt1
    :caption: Desenhando uma Espiral Recursiva Usando o Módulo turtle
    :nocodelens:


    import turtle

    myTurtle = turtle.Turtle()
    myWin = turtle.Screen()

    def drawSpiral(myTurtle, lineLen):
        if lineLen > 0:
            myTurtle.forward(lineLen)
            myTurtle.right(90)
            drawSpiral(myTurtle,lineLen-5)

    drawSpiral(myTurtle,100)
    myWin.exitonclick()

..  That is really about all the turtle graphics you need to know in order
    to make some pretty impressive drawings. For our next program we are
    going to draw a fractal tree. Fractals come from a branch of
    mathematics, and have much in common with recursion. The definition of a
    fractal is that when you look at it the fractal has the same basic shape
    no matter how much you magnify it. Some examples from nature are the
    coastlines of continents, snowflakes, mountains, and even trees or
    shrubs. The fractal nature of many of these natural phenomenon makes it
    possible for programmers to generate very realistic looking scenery for
    computer generated movies. In our next example we will generate a
    fractal tree.

Isso é realmente tudo que você precisa saber sobre o módulo gráfico turtle
para fazer alguns desenhos bem impressionantes. Em nosso próximo programa, 
vamos desenhar uma árvore fractal. Fractais é um ramo da
matemática que têm muito em comum com recursão. A definição de um
fractal é que quando você olha para ele, o fractal mantem sua mesma forma básica
não importa o quanto você a amplie. Alguns exemplos que ocorrem na natureza são as
costas de continentes, flocos de neve, montanhas e até árvores ou
arbustos. A natureza fractal de muitos desses fenômenos naturais 
permite que os programadores criem cenários muito realistas para
filmes gerados por computador. No nosso próximo exemplo, vamos gerar uma
árvore fractal.

..  To understand how this is going to work it is helpful to think of how we
    might describe a tree using a fractal vocabulary. Remember that we said
    above that a fractal is something that looks the same at all different
    levels of magnification. If we translate this to trees and shrubs we
    might say that even a small twig has the same shape and characteristics
    as a whole tree. Using this idea we could say that a *tree* is a trunk,
    with a smaller *tree* going off to the right and another smaller *tree*
    going off to the left. If you think of this definition recursively it
    means that we will apply the recursive definition of a tree to both of
    the smaller left and right trees.

Para entender como isso vai funcionar, é útil pensar em como
podemos descrever uma árvore usando um vocabulário fractal. Lembre-se que dissemos
acima que um fractal é algo que tem a mesma aparência em todos os diferentes
níveis de ampliação. Se traduzirmos isso para árvores e arbustos,
podemos dizer que mesmo um pequeno galho tem a mesma forma e características
de uma árvore inteira. Usando esta ideia, poderíamos dizer que uma *árvore* é um tronco,
com uma *árvore* menor indo para a direita e outra *árvore* menor
indo para a esquerda. Se você pensar nesta definição recursivamente,
significa que vamos aplicar a definição recursiva de uma árvore para ambas
as árvores menores, à esquerda e à direita.

..  Let's translate this idea to some Python code. :ref:`Listing 1 <lst_fractree>`
    shows how we can use our turtle to generate a fractal tree. Let's look at
    the code a bit more closely. You will see that on lines 5 and 7 we are
    making a recursive call. On line 5 we make the recursive call right
    after the turtle turns to the right by 20 degrees; this is the right
    tree mentioned above. Then in line 7 the turtle makes another recursive
    call, but this time after turning left by 40 degrees. The reason the
    turtle must turn left by 40 degrees is that it needs to undo the
    original 20 degree turn to the right and then do an additional 20 degree
    turn to the left in order to draw the left tree. Also notice that each
    time we make a recursive call to ``tree`` we subtract some amount from
    the ``branchLen`` parameter; this is to make sure that the recursive
    trees get smaller and smaller. You should also recognize the initial
    ``if`` statement on line 2 as a check for the base case of ``branchLen``
    getting too small.

Vamos traduzir essa ideia para algum código em Python. A :ref:`Listagem 1 <lst_fractree>`
mostra como podemos usar nossa tartaruga para gerar uma árvore fractal. Vamos olhar para
o código um pouco mais de perto. Você vai ver que nas linhas 5 e 7 estamos
fazendo uma chamada recursiva. Na linha 5, fazemos a chamada recursiva
depois que a tartaruga vira 20 graus para a direita; esta é a árvore à direita
mencionada acima. Então, na linha 7, a tartaruga faz outra chamada recursiva,
mas desta vez depois de virar 40 graus à esquerda. A razão pela qual a
tartaruga deve virar à esquerda em 40 graus é que ela precisa desfazer o
giro inicial de 20 graus à direita e, em seguida, fazer um giro adicional de 20 graus
à esquerda para desenhar a árvore da esquerda. Observe também que cada
vez que fazemos uma chamada recursiva para ``tree`` subtraímos alguma quantidade
do parâmetro ``branchLen``; isso é para nos certificar de que as árvores
recursivas ficam cada vez menores. Você também deve reconhecer o comando inicial
``if`` na linha 2, que verifica o caso base de ``branchLen`` ser muito pequeno.

.. _lst_fractree:

**Listagem 1**

.. highlight:: python
    :linenothreshold: 5

::

    def tree(branchLen,t):
        if branchLen > 5:
            t.forward(branchLen)
            t.right(20)
            tree(branchLen-15,t)
            t.left(40)
            tree(branchLen-10,t)
            t.right(20)
            t.backward(branchLen)
            
            
.. highlight:: python
    :linenothreshold: 500

..  The complete program for this tree example is shown in :ref:`ActiveCode 2 <lst_complete_tree>`.  Before you run
    the code think about how you expect to see the tree take shape. Look at
    the recursive calls and think about how this tree will unfold. Will it
    be drawn symmetrically with the right and left halves of the tree taking
    shape simultaneously? Will it be drawn right side first then left side?

O programa completo para este exemplo de árvore é mostrado 
no :ref:`ActiveCode 2 <lst_complete_tree>`. Antes de executar
o código, pense em como você espera ver a árvore no final. Olhe para a
as chamadas recursivas e pense em como essa árvore se desdobrará. Será que vai
ser desenhada simetricamente com as metades direita e esquerda da árvore se formando
simultaneamente? Ou será que o lado direito será desenhado primeiro e depois o lado esquerdo?

.. activecode:: lst_complete_tree
    :caption: Recursively Drawing a Tree
    :nocodelens:

    import turtle
    
    def tree(branchLen,t):
        if branchLen > 5:
            t.forward(branchLen)
            t.right(20)
            tree(branchLen-15,t)
            t.left(40)
            tree(branchLen-15,t)
            t.right(20)
            t.backward(branchLen)

    def main():
        t = turtle.Turtle()
        myWin = turtle.Screen()
        t.left(90)
        t.up()
        t.backward(100)
        t.down()
        t.color("green")
        tree(75,t)
        myWin.exitonclick()
        
    main()


..  Notice how each branch point on the tree corresponds to a recursive
    call, and notice how the tree is drawn to the right all the way down to
    its shortest twig. You can see this in :ref:`Figure 1 <fig_tree1>`. Now, notice
    how the program works its way back up the trunk until the entire right
    side of the tree is drawn. You can see the right half of the tree in
    :ref:`Figure 2 <fig_tree2>`. Then the left side of the tree is drawn, but not by
    going as far out to the left as possible. Rather, once again the entire
    right side of the left tree is drawn until we finally make our way out
    to the smallest twig on the left.

Observe como cada ponto de ramificação na árvore corresponde a uma chamada recursiva e
observe como a árvore é desenhada toda à direita, seguindo o caminho até
seu galho mais curto. Você pode ver isto an :ref:`Figura 1 <fig_tree1>`. Agora observe
como o programa percorre o caminho de volta no tronco até que todo o 
lado da árvore é desenhado. Você pode ver a metade direita da árvore na
:ref:`Figura 2 <fig_tree2>`. Então o lado esquerdo da árvore é desenhado, mas não 
indo o mais longe possível para a esquerda. Em vez disso, mais uma vez todo o
lado direito da árvore da esquerda é desenhado até que finalmente terminamos com
o menor galho à esquerda.

.. _fig_tree1:

.. figure:: Figures/tree1.png
   :align: center

   Figura 1: O Início de uma Árvore Fractal
   
.. _fig_tree2:

.. figure:: Figures/tree2.png
   :align: center

   Figura 2: A Primeira Metade de uma Árvore


..  This simple tree program is just a starting point for you, and you will
    notice that the tree does not look particularly realistic because nature
    is just not as symmetric as a computer program. The exercises at the end
    of the chapter will give you some ideas for how to explore some
    interesting options to make your tree look more realistic.

Este programa simples para desenhar árvores é apenas um ponto de partida.
Você vai ver que a árvore não parece muito realista porque a natureza
não é tão simétrica quanto um programa de computador. Os exercícios no final
do capítulo fornecem algumas idéias de como explorar alguns
opções interessantes para fazer sua árvore parecer mais realista.

..  Modify the recursive tree program using one or all of the following ideas:
    -  Modify the thickness of the branches so that as the ``branchLen``
        gets smaller, the line gets thinner.
    -  Modify the color of the branches so that as the ``branchLen`` gets
        very short it is colored like a leaf.
    -  Modify the angle used in turning the turtle so that at each branch
        point the angle is selected at random in some range. For example
        choose the angle between 15 and 45 degrees. Play around to see
        what looks good.
    -  Modify the ``branchLen`` recursively so that instead of always
        subtracting the same amount you subtract a random amount in some
        range.


.. admonition:: Auto Avaliação

    Modifique o programa de árvore recursiva usando uma ou todas as seguintes idéias:

    - Modifique a espessura dos ramos para que, quando ``branchLen`` fica menor, a linha fica mais fina.

    - Modifique a cor dos ramos para, quando ``branchLen`` ficar  muito curto, ser colorido como uma folha.

    - Modifique o ângulo usado na rotação da tartaruga para que em cada ponto de ramificação o ângulo seja  selecionado aleatoriamente dentro de algum intervalo. Por exemplo, escolha um ângulo entre 15 e 45 graus. Experimente vários valores para ver o que parece bom.

    - Modifique o ``branchLen`` para que, em vez de sempre subtrair a mesma quantidade, subtraia uma quantidade aleatória dentro de algum intervalo.


   .. actex:: recursion_sc_3
      :nocodelens:


