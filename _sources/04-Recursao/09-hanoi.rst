..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Tower of Hanoi

Torre de Hanoi
~~~~~~~~~~~~~~

..  The Tower of Hanoi puzzle was invented by the French mathematician
    Edouard Lucas in 1883. He was inspired by a legend that tells of a Hindu
    temple where the puzzle was presented to young priests. At the beginning
    of time, the priests were given three poles and a stack of 64 gold
    disks, each disk a little smaller than the one beneath it. Their
    assignment was to transfer all 64 disks from one of the three poles to
    another, with two important constraints. They could only move one disk
    at a time, and they could never place a larger disk on top of a smaller
    one. The priests worked very efficiently, day and night, moving one disk
    every second. When they finished their work, the legend said, the temple
    would crumble into dust and the world would vanish.

O problema da Torre de Hanoi foi inventado pelo matemático francês
Edouard Lucas em 1883. Ele foi inspirado por uma lenda que fala de um templo Hindu
onde o problema foi apresentado aos jovens sacerdotes. No inicio
dos tempos, os sacerdotes receberam três pinos e uma pilha de 64 discos de ouro, 
sendo cada disco um pouco menor do que aquele abaixo dele. A tarefa
era transferir todos os 64 discos colocados em um dos três pinos para
outro, com duas restrições importantes. Eles só podiam mover um disco
de cada vez, e eles nunca poderiam colocar um disco maior em cima de um disco menor.
Os sacerdotes trabalhavam muito eficientemente, dia e noite, movendo um disco
todo segundo. Quando eles terminassem seu trabalho, diz a lenda, que o templo
se desmoronaria em pó e o mundo desapareceria.

..  Although the legend is interesting, you need not worry about the world
    ending any time soon. The number of moves required to correctly move a
    tower of 64 disks is :math:`2^{64}-1 = 18,446,744,073,709,551,615`. At
    a rate of one move per second, that is :math:`584,942,417,355` years! Clearly
    there is more to this puzzle than meets the eye.

Embora a lenda seja interessante, você não precisa se preocupar com o mundo
terminando em breve. O número de movimentos necessários para mover corretamente uma
torre de 64 discos é :math:`2^{64}-1 = 18,446,744,073,709,551,615`. 
Movimentando um disco por segundo, a tarefa levaria :math:`584.942.417.355` anos para terminar! 
Claramente esse problema é mais complexo do que aparenta.

..  :ref:`Figure 1 <fig_hanoi>` shows an example of a configuration of disks in the
    middle of a move from the first peg to the third. Notice that, as the
    rules specify, the disks on each peg are stacked so that smaller disks
    are always on top of the larger disks. If you have not tried to solve
    this puzzle before, you should try it now. You do not need fancy disks
    and poles–a pile of books or pieces of paper will work.

A :ref:`Figura 1 <fig_hanoi>` mostra um exemplo de configuração de discos no
meio de um movimento do pino origem (*fromPole*) para o pino destino (*toPole*),
usando o segundo pino como intermediário (*withPole*).
Observe que, como as 
regras especificam, os discos em cada pino são empilhados para que discos menores
sempre fiquem em cima de discos maiores. Se você não tentou resolver
esse quebra-cabeça antes, procure resolvê-lo agora. Você não precisa de discos 
e pinos de verdade - basta usar uma pilha de livros ou pedaços de papel.

.. _fig_hanoi:

.. figure:: Figures/hanoi.png
   :align: center
   :alt: image

   
   Figura 1: Um Exemplo de Configuração de Discos da Torre de Hanoi

..  How do we go about solving this problem recursively? How would you go
    about solving this problem at all? What is our base case? Let’s think
    about this problem from the bottom up. Suppose you have a tower of five
    disks, originally on peg one. If you already knew how to move a tower of
    four disks to peg two, you could then easily move the bottom disk to peg
    three, and then move the tower of four from peg two to peg three. But
    what if you do not know how to move a tower of height four? Suppose that
    you knew how to move a tower of height three to peg three; then it would
    be easy to move the fourth disk to peg two and move the three from peg
    three on top of it. But what if you do not know how to move a tower of
    three? How about moving a tower of two disks to peg two and then moving
    the third disk to peg three, and then moving the tower of height two on
    top of it? But what if you still do not know how to do this? Surely you
    would agree that moving a single disk to peg three is easy enough,
    trivial you might even say. This sounds like a base case in the making.

Como podemos resolver este problema recursivamente? Como você resolveria 
esse problema de qualquer outra forma? Qual é o nosso caso base? Vamos pensar
sobre este problema de baixo para cima. Suponha que você tenha uma torre de cinco
discos, originalmente no pino um. Se você souber como mover uma torre de
quatro discos para o pino dois, então você poderia mover facilmente o disco 
inferior para o pino três e, em seguida, mover a torre de quatro discos do pino dois para o três. 
Mas e se você não souber como mover uma torre de altura quatro? Suponha que
você saiba como mover uma torre de três discos para o pino três; então seria
fácil mover o quarto disco para o pino dois e mover os três discos do pino
três em cima dele. Mas e se você não souber como mover uma torre de
três? Que tal mover uma torre de dois discos para o pino dois e depois mover
o terceiro disco para o pino três e, em seguida, mover a torre de altura dois 
em cima dele? Mas e se você ainda não souber como fazer isso? Com certeza você
concordaria que mover um único disco para o pino três é bastante fácil,
trivial você pode até dizer. Isso soa como um caso base se revelando.

..  Here is a high-level outline of how to move a tower from the starting
    pole, to the goal pole, using an intermediate pole:
    #. Move a tower of height-1 to an intermediate pole, using the final
    pole.
    #. Move the remaining disk to the final pole.
    #. Move the tower of height-1 from the intermediate pole to the final
    pole using the original pole.


Segue um rascunho em alto nível de como mover a torre de um 
pino origem para um pino destino, usando um pino intermediário:

#. Mova a torre de :math:`altura - 1` para o pino intermediário, usando o pino destino como intermediário.

#. Mova o disco restante para o pino destino.

#. Mova a torre de :math:`altura - 1` do pino intermediário para o pino destino usando o pino origem como intermediário.

..  As long as we always obey the rule that the larger disks remain on the
    bottom of the stack, we can use the three steps above recursively,
    treating any larger disks as though they were not even there. The only
    thing missing from the outline above is the identification of a base
    case. The simplest Tower of Hanoi problem is a tower of one disk. In
    this case, we need move only a single disk to its final destination. A
    tower of one disk will be our base case. In addition, the steps outlined
    above move us toward the base case by reducing the height of the tower
    in steps 1 and 3. :ref:`Listing 1 <lst_hanoi>` shows the Python code to solve the
    Tower of Hanoi puzzle.

Contanto que sempre obedeçamos a regra de que os discos maiores permanecem na
parte inferior da pilha, podemos usar as três etapas acima recursivamente,
tratando discos maiores como se eles nem estivessem lá. A única
coisa que falta no esquema acima é a identificação de um caso base.
O problema mais simples da Torre de Hanoi é uma torre de um disco.
Neste caso, precisamos mover apenas um único disco para o seu destino final. 
A torre de um disco será o nosso caso base. Além disso, as etapas descritas
acima nos direciona para o caso base, reduzindo a altura da torre
nos passos 1 e 3. A :ref:`Listagem 1 <lst_hanoi>` mostra o código Python para resolver o problema
Torre de Hanoi.


.. _lst_hanoi:

**Listagem 1**

.. highlight:: python
    :linenothreshold: 2

::

    def moveTower(height,fromPole, toPole, withPole):
        if height >= 1:
            moveTower(height-1,fromPole,withPole,toPole)
            moveDisk(fromPole,toPole)
            moveTower(height-1,withPole,toPole,fromPole)
            
.. highlight:: python
    :linenothreshold: 500

..  Notice that the code in :ref:`Listing 1 <lst_hanoi>` is almost identical to the
    English description. The key to the simplicity of the algorithm is that
    we make two different recursive calls, one on line 3 and a
    second on line 5. On line 3 we move all but the bottom
    disk on the initial tower to an intermediate pole. The next line simply
    moves the bottom disk to its final resting place. Then on line
    5 we move the tower from the intermediate pole to the top of
    the largest disk. The base case is detected when the tower height is 0;
    in this case there is nothing to do, so the ``moveTower`` function
    simply returns. The important thing to remember about handling the base
    case this way is that simply returning from ``moveTower`` is what
    finally allows the ``moveDisk`` function to be called.

Observe que o código na :ref:`Listagem 1 <lst_hanoi>` é quase idêntico ao
rascunho mas em inglês. A chave para a simplicidade do algoritmo é que
fazemos duas chamadas recursivas diferentes, uma na linha 3 e uma
segunda na linha 5. Na linha 3 nos movemos todos os discos do pino origem para o pino intermediário,
a menos do disco mais baixo. A linha seguinte simplesmente move esse último disco para a sua posição final no pino destino. Então, na linha 5, movemos a torre no pino intermediário para o topo do
maior disco. O caso base é detectado quando a altura da torre é 0;
neste caso não há nada para fazer, então a função ``moveTower`` (mova torre)
simplesmente retorna. O importante a lembrar sobre usar o caso base
desta forma é que o fim de ``moveTower`` é o que
permite que a função ``moveDisk`` (mova disco) seja chamada.

..  The function ``moveDisk``, shown in :ref:`Listing 2 <lst_movedisk>`, is very
    simple. All it does is print out that it is moving a disk from one pole
    to another. If you type in and run the ``moveTower`` program you can see
    that it gives you a very efficient solution to the puzzle.

A função ``moveDisk``, mostrada na :ref:`Listagem 2 <lst_movedisk>`, é muito
simples. Tudo o que faz é imprimir que está movendo um disco de um pino
para outro. Se você digitar e executar o programa ``moveTower`` você pode verificar 
que ela fornece uma solução muito eficiente para o quebra-cabeça.

.. _lst_movedisk:

**Listagem 2**

::

    def moveDisk(fp,tp):
        print("moving disk from",fp,"to",tp)
        
..  The program in ActiveCode 1 provides the entire solution for three disks.

O programa no ActiveCode 1 descreve a solução completa para três discos.        
        
.. activecode:: hanoi
    :caption: Solução Recursiva do Problema Torre de Hanoi

    def moveTower(height,fromPole, toPole, withPole):
        if height >= 1:
            moveTower(height-1,fromPole,withPole,toPole)
            moveDisk(fromPole,toPole)
            moveTower(height-1,withPole,toPole,fromPole)

    def moveDisk(fp,tp):
        print("Movendo o disco de", fp, "para", tp)
    
    moveTower(3,"A","B","C")

..  Now that you have seen the code for both ``moveTower`` and ``moveDisk``,
    you may be wondering why we do not have a data structure that explicitly
    keeps track of what disks are on what poles. Here is a hint: if you were
    going to explicitly keep track of the disks, you would probably use
    three ``Stack`` objects, one for each pole. The answer is that Python
    provides the stacks that we need implicitly through the call stack.

Agora que você viu o código para ``moveTower`` e ``moveDisk``,
você pode estar se perguntando por que não temos uma estrutura de dados que explicitamente
mantém o controle de quais discos estão em quais pinos. Aqui vai uma dica: se você fosse
explicitamente controlar os discos, você provavelmente usaria
três objetos ``Pilha``, um para cada pino. A resposta é que o Python
fornece as pilhas que precisamos implicitamente através da pilha de chamadas.