..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  The Three Laws of Recursion

As Três Leis da Recursão
~~~~~~~~~~~~~~~~~~~~~~~~

..  Like the robots of Asimov, all recursive algorithms must obey three important laws:

Como os robôs de Asimov, todos os algoritmos recursivos devem obedecer três leis importantes: 

#. Um algoritmo recursivo deve possuir um **caso base** (*base case*).

#. Um algoritmo recursivo deve modificar o seu estado e se aproximar do caso base.

#. Um algoritmo recursivo deve chamar a si mesmo, recursivamente.

..  #. A recursive algorithm must have a **base case**.
    #. A recursive algorithm must change its state and move toward the base case.
    #. A recursive algorithm must call itself, recursively.

..  Let’s look at each one of these laws in more detail and see how it was
    used in the ``listsum`` algorithm. First, a base case is the condition
    that allows the algorithm to stop recursing. A base case is typically a
    problem that is small enough to solve directly. In the ``listsum``
    algorithm the base case is a list of length 1.

Vamos olhar para cada uma dessas leis em detalhes e ver como foi
usado no algoritmo ``somalista``. Primeiro, um caso base é a condição
que permite que o algoritmo termine a recursão. Um caso base é tipicamente um
problema que é pequeno o suficiente para ser resolvido diretamente. 
No algoritmo ``somalista`` o caso base é uma lista de comprimento 1.

..  To obey the second law, we must arrange for a change of state that moves
    the algorithm toward the base case. A change of state means that some
    data that the algorithm is using is modified. Usually the data that
    represents our problem gets smaller in some way. In the ``listsum``
    algorithm our primary data structure is a list, so we must focus our
    state-changing efforts on the list. Since the base case is a list of
    length 1, a natural progression toward the base case is to shorten the
    list. This is exactly what happens on line 5 of :ref:`ActiveCode 2 <lst_recsum>` when we call ``listsum`` with a shorter list.

Para obedecer a segunda lei, devemos providenciar uma mudança de estado que mova
o algoritmo em direção ao caso base. Uma mudança de estado significa que parte 
dos dados que o algoritmo está usando são modificados. Geralmente os dados que
representam nosso problema ficam menores de alguma forma. No algoritmo ``somalista``
nossa estrutura de dados primária é uma lista, por isso devemos focar nossos
esforços de mudança de estado na lista. Como o caso base é uma lista de
comprimento 1, uma progressão natural em direção ao caso base é encurtar a
lista. Isto é exatamente o que acontece na linha 5 do :ref:`ActiveCode 2 <lst_recsum>` 
quando chamamos ``somalista`` com uma lista menor.

..  The final law is that the algorithm must call itself. This is the very
    definition of recursion. Recursion is a confusing concept to many
    beginning programmers. As a novice programmer, you have learned that
    functions are good because you can take a large problem and break it up
    into smaller problems. The smaller problems can be solved by writing a
    function to solve each problem. When we talk about recursion it may seem
    that we are talking ourselves in circles. We have a problem to solve
    with a function, but that function solves the problem by calling itself!
    But the logic is not circular at all; the logic of recursion is an
    elegant expression of solving a problem by breaking it down into a
    smaller and easier problems.

A última lei é que o algoritmo deve chamar a si mesmo. Esta é a própria
definição de recursão. A recursão é um conceito confuso para muitos
programadores iniciantes. Como um programador novato, você aprendeu que
funções são boas porque permitem você pode pegar um problema grande e quebrá-lo
em problemas menores. Os problemas menores podem ser resolvidos escrevendo
uma função para resolver cada problema. Quando falamos de recursão, parece
que estamos falando em círculos. Nós temos um problema para resolver
com uma função, mas essa função resolve o problema chamando a si mesma!
Mas a lógica não é circular de forma alguma; a lógica da recursão é uma
expressão elegante de resolver um problema, dividindo-o em
problemas menores e mais fáceis.

..  In the remainder of this chapter we will look at more examples of
    recursion. In each case we will focus on designing a solution to a
    problem by using the three laws of recursion.

No restante deste capítulo, veremos mais exemplos de recursão. Em cada caso, 
vamos nos concentrar em projetar uma solução para um problema usando as três 
leis da recursão.

.. admonition:: Auto Avaliação

   .. mchoice:: question_recsimp_1
      :correct: c
      :answer_a: 6
      :answer_b: 5
      :answer_c: 4
      :answer_d: 3
      :feedback_a: Existem apenas cinco números na lista, o número de chamadas recursivas não será maior que o tamanho da lista.
      :feedback_b: A chamada inicial para somalista não é uma chamada recursiva.
      :feedback_c: A primeira chamada recursiva passa a lista [4,6,8,10], a segunda [6,8,10] e assim por diante até [10].
      :feedback_d: Isso não seria suficiente para cobrir todos os números da lista

      Quantas chamadas recursivas são feitas ao calcular a soma da lista [2,4,6,8,10]?


   .. mchoice:: question_recsimp_2
      :correct: d
      :answer_a: n == 0
      :answer_b: n == 1
      :answer_c: n &gt;= 0
      :answer_d: n &lt;= 1
      :feedback_a: Embora isso funcione, há escolhas melhores e ligeiramente mais eficientes, já que fat(1) e fat(0) são os mesmos.
      :feedback_b: Uma boa escolha, mas o que acontece se você chamar fat(0)?
      :feedback_c: Este caso base seria verdadeiro para todos os números maiores que zero, então o fat de qualquer número positivo seria 1.
      :feedback_d: Bom, esse caso é o mais eficiente e até mesmo evita que o seu programa falhe se você tentar calcular o fatorial de um número negativo.

      Suponha que você vai escrever uma função recursiva para calcular o fatorial de um número. fat(n) retorna n * n-1 * n-2 * .... onde o fatorial de zero é definido como 1. Qual seria o caso base mais apropriado?