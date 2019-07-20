..  Copyright (C)  Brad Miller, David Ranum
   This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Dynamic Programming

Programação Dinâmica
--------------------

..  Many programs in computer science are written to optimize some value;
   for example, find the shortest path between two points, find the line
   that best fits a set of points, or find the smallest set of objects that
   satisfies some criteria. There are many strategies that computer
   scientists use to solve these problems. One of the goals of this book is
   to expose you to several different problem solving strategies. **Dynamic
   programming** is one strategy for these types of optimization problems.

Muitos programas em Ciência da Computação são escritos para otimizar algum valor;
por exemplo, 
encontre o caminho mais curto entre dois pontos, 
encontre a linha que melhor se encaixa em um conjunto de pontos, ou 
encontre o menor conjunto de objetos que satisfaz algum critério. 
Existem muitas estratégias que os cientistas da computação
usam para resolver esses problemas. Um dos objetivos deste livro é
expor você a várias estratégias diferentes de solução de problemas. 
A **Programação Dinâmica** é uma estratégia para esses tipos de problemas de otimização.

..  A classic example of an optimization problem involves making change
   using the fewest coins. Suppose you are a programmer for a vending
   machine manufacturer. Your company wants to streamline effort by giving
   out the fewest possible coins in change for each transaction. Suppose a
   customer puts in a dollar bill and purchases an item for 37 cents. What
   is the smallest number of coins you can use to make change? The answer
   is six coins: two quarters, one dime, and three pennies. How did we
   arrive at the answer of six coins? We start with the largest coin in our
   arsenal (a quarter) and use as many of those as possible, then we go to
   the next lowest coin value and use as many of those as possible. This
   first approach is called a **greedy method** because we try to solve as
   big a piece of the problem as possible right away.

Um exemplo clássico de um problema de otimização envolve calcular o troco
usando um número mínimo de moedas. Suponha que você seja um programador de 
um fabricante de máquinas de venda automática. 
Sua empresa quer ajudar seus clientes dando
o menor número possível de moedas como troco para cada transação. Suponha que um
cliente coloca em uma nota de um dólar e compra um item por 37 centavos. 
Qual é o menor número de moedas que você pode dar de troco (usando moedas de
25, 10, 5 e 1 centavos de dólar)? 
A resposta é seis moedas: duas de 25 centavos, uma de 10 centavos e três de 1 centavo. 
Como chegamos à essa resposta? Começamos com a maior moeda a nossa disposição
(de 25 centavos) e usamos tantas quanto possível, então vamos para a próxima moeda
de maior valor (de 10 centavos) e usamos o maior número possível delas. 
Esta primeira abordagem é chamada de **método guloso** porque tenta resolver
os maiores pedaços possíveis do problema primeiro.

..  The greedy method works fine when we are using U.S. coins, but suppose
   that your company decides to deploy its vending machines in Lower
   Elbonia where, in addition to the usual 1, 5, 10, and 25 cent coins they
   also have a 21 cent coin. In this instance our greedy method fails to
   find the optimal solution for 63 cents in change. With the addition of
   the 21 cent coin the greedy method would still find the solution to be
   six coins. However, the optimal answer is three 21 cent pieces.

O método guloso funciona bem quando estamos usando moedas dos EUA, mas suponha
que sua empresa decide implantar suas máquinas de venda automática na 
Elbonia do Sul onde, além das habituais moedas de 1, 5, 10 e 25 centavos dos EUA, 
também tem uma moeda de 21 centavos. 
Neste exemplo, o nosso método guloso não consegue
encontrar a solução ideal para o troco de 63 centavos. Com a adição da
moeda de 21 centavos o método guloso ainda encontra a solução com
seis moedas. No entanto, a resposta ótima seria três moedas de 21 centavos.

..  Let’s look at a method where we could be sure that we would find the
   optimal answer to the problem. Since this section is about recursion,
   you may have guessed that we will use a recursive solution. Let’s start
   with identifying the base case. If we are trying to make change for the
   same amount as the value of one of our coins, the answer is easy, one
   coin.

Vamos ver um método onde podemos ter certeza de que encontraríamos a
resposta ótima para o problema. Como esta seção é sobre recursão,
você pode ter adivinhado que usaremos uma solução recursiva. Vamos começar
com a identificação do caso base. Se estamos tentando fazer troco para a
mesma quantia que o valor de uma das nossas moedas, a resposta é simplesmente
uma dessas moedas.

..  If the amount does not match we have several options. What we want is
   the minimum of a penny plus the number of coins needed to make change
   for the original amount minus a penny, or a nickel plus the number of
   coins needed to make change for the original amount minus five cents, or
   a dime plus the number of coins needed to make change for the original
   amount minus ten cents, and so on. So the number of coins needed to make
   change for the original amount can be computed according to the
   following: 

Se o valor não corresponder, temos várias opções. O que nós queremos é
o mínimo de 1 centavo mais o número de moedas necessárias para fazer o troco 
para o valor original menos 1 centavo, ou o mínimo de 5 centavos mais o número de
moedas necessárias para fazer o troco para o valor original menos 5 centavos, ou
10 centavos mais o número de moedas necessárias para fazer o troco para o valor original
menos dez centavos, e assim por diante. Então o número de moedas necessárias para fazer
o troco para o valor original pode ser calculado de acordo com o seguinte:

.. math::

      numCoins =
   min
   \begin{cases}
   1 + numCoins(valor original - 1) \\
   1 + numCoins(valor original - 5) \\
   1 + numCoins(valor original - 10) \\
   1 + numCoins(valor original - 25)
   \end{cases}
   \label{eqn_change}


..  The algorithm for doing what we have just described is shown in
   :ref:`Listing 7 <lst_change1>`. In line 3 we are checking our base case;
   that is, we are trying to make change in the exact amount of one of our
   coins. If we do not have a coin equal to the amount of change, we make
   recursive calls for each different coin value less than the amount of
   change we are trying to make. Line 6 shows how we filter the
   list of coins to those less than the current value of change using a
   list comprehension. The recursive call also reduces the total amount of
   change we need to make by the value of the coin selected. The recursive
   call is made in line 7. Notice that on that same line we add 1
   to our number of coins to account for the fact that we are using a coin.
   Just adding 1 is the same as if we had made a recursive call asking
   where we satisfy the base case condition immediately.

O algoritmo para fazer o que acabamos de descrever é mostrado na
:ref:`Listagem 7 <lst_change1>`. Na linha 3, estamos verificando nosso caso base;
isto é, estamos tentando fazer o troco exato usando apenas uma de nossas
moedas. Se não tivermos uma moeda igual ao troco necessário, fazemos
chamadas recursivas usando cada moeda menor do que a quantidade de
troco que estamos tentando fazer. A linha 6 mostra como filtramos a
lista de moedas para aquelas com valor menor que o troco usando *list comprehension*.
A chamada recursiva também reduz a quantidade total de troco
que precisamos fazer pelo valor da moeda selecionada. A chamada recursiva
é feita na linha 7. Observe que nessa mesma linha nós adicionamos 1
ao número de moedas para contabilizar o seu uso no troco.
Adicionar 1 diretamente economiza uma chamada recursiva pedindo para
fazer o troco no valor da moeda, que cairia imediatamente em um caso base.

.. _lst_change1:


.. highlight:: python
    :linenothreshold: 5

**Listagem 7**

::

    def recMC(coinValueList,change):
       minCoins = change
       if change in coinValueList:
         return 1
       else:
          for i in [c for c in coinValueList if c <= change]:
             numCoins = 1 + recMC(coinValueList,change-i)
             if numCoins < minCoins:
                minCoins = numCoins
       return minCoins

    print(recMC([1,5,10,25],63))


.. highlight:: python
    :linenothreshold: 500

..  The trouble with the algorithm in :ref:`Listing 7 <lst_change1>` is that it is
   extremely inefficient. In fact, it takes 67,716,925 recursive calls to
   find the optimal solution to the 4 coins, 63 cents problem! To
   understand the fatal flaw in our approach look at :ref:`Figure 5 <fig_c1ct>`,
   which illustrates a small fraction of the 377 function calls needed to
   find the optimal set of coins to make change for 26 cents.

O problema com o algoritmo na :ref:`Listagem 7 <lst_change1>` é que ele é
extremamente ineficiente. De fato, são necessárias 67.716.925 chamadas recursivas para
encontrar a solução ótima para o problema de fazer o troco de 63 centavos com 4 moedas! 
Para entender a falha fatal em nossa abordagem observe a :ref:`Figura 3 <fig_c1ct>`,
que ilustra uma pequena fração das 377 chamadas de função necessárias para
encontrar o conjunto ótimo de moedas para fazer o troco de 26 centavos.

..  Each node in the graph corresponds to a call to ``recMC``. The label on
   the node indicates the amount of change for which we are computing the
   number of coins. The label on the arrow indicates the coin that we just
   used. By following the graph we can see the combination of coins that
   got us to any point in the graph. The main problem is that we are
   re-doing too many calculations. For example, the graph shows that the
   algorithm would recalculate the optimal number of coins to make change
   for 15 cents at least three times. Each of these computations to find
   the optimal number of coins for 15 cents itself takes 52 function calls.
   Clearly we are wasting a lot of time and effort recalculating old
   results.

Cada nó no grafo corresponde a uma chamada para ``recMC``. O rótulo 
em um nó indica a quantidade de troco para a qual estamos computando o
número de moedas. O rótulo de uma seta indica a moeda que acabamos de
usar. Seguindo o grafo podemos ver a combinação de moedas que
nos levou a qualquer ponto do grafo. O principal problema é que estamos
refazendo cálculos demais. Por exemplo, o grafo mostra que o
algoritmo iria recalcular o número ótimo de moedas para fazer o troco
de 15 centavos pelo menos três vezes. Cada uma dessas computações para encontrar
o número ótimo de moedas para fazer 15 centavos de troco, usa 52 chamadas de função.
Claramente estamos perdendo muito tempo e esforço recalculando resultados.

.. _fig_c1ct:

.. figure:: Figures/callTree.png
   :align: center
   :width: 100%
   :alt: image

   Figura 3: Árvore de Chamadas para a Listagem 7

..  The key to cutting down on the amount of work we do is to remember some
   of the past results so we can avoid recomputing results we already know.
   A simple solution is to store the results for the minimum number of
   coins in a table when we find them. Then before we compute a new
   minimum, we first check the table to see if a result is already known.
   If there is already a result in the table, we use the value from the
   table rather than recomputing. :ref:`ActiveCode 1 <lst_change2>` shows a modified
   algorithm to incorporate our table lookup scheme.

A chave para reduzir a quantidade de trabalho que fazemos é lembrar de alguns
dos resultados anteriores para que possamos evitar recalcular resultados que já conhecemos.
Uma solução simples é armazenar os resultados do número mínimo de
moedas em uma tabela assim que são calculados. Então antes de calcularmos um novo
mínimo, primeiro verificamos a tabela para ver se um resultado já é conhecido.
Se já houver um resultado na tabela, usamos o valor da tabela em vez de recalcular. 
O :ref:`ActiveCode 1 <lst_change2>` mostra uma modificação do
algoritmo para incorporar nossa solução com tabela.

.. activecode:: lst_change2
    :caption: Contagem Recursiva de Moedas Usando Uma Tabela
    :nocodelens:

    def recDC(coinValueList,change,knownResults):
       minCoins = change
       if change in coinValueList:   
          knownResults[change] = 1
          return 1
       elif knownResults[change] > 0:
          return knownResults[change]
       else:
           for i in [c for c in coinValueList if c <= change]:
             numCoins = 1 + recDC(coinValueList, change-i, 
                                  knownResults)
             if numCoins < minCoins:
                minCoins = numCoins
                knownResults[change] = minCoins
       return minCoins

    print(recDC([1,5,10,25],63,[0]*64))

..  Notice that in line 6 we have added a test to see if our table
   contains the minimum number of coins for a certain amount of change. If
   it does not, we compute the minimum recursively and store the computed
   minimum in the table. Using this modified algorithm reduces the number
   of recursive calls we need to make for the four coin, 63 cent problem to
   221 calls!

Observe que na linha 6 nós adicionamos um teste para ver se a nossa tabela
contém o número mínimo de moedas para uma determinada quantia de troco. E se
ela não contém, calculamos o mínimo recursivamente e o armazenamos
na tabela. Usando este algoritmo modificado, o número
de chamadas recursivas que precisamos fazer para o problema de troco de 63 centavos
usando 4 moedas se reduz para 221 chamadas!

..  Although the algorithm in :ref:`AcitveCode 1 <lst_change2>` is correct, it looks and
   feels like a bit of a hack.  Also, if we look at the ``knownResults`` lists
   we can see that there are some holes in the table. In fact the term for
   what we have done is not dynamic programming but rather we have improved
   the performance of our program by using a technique known as
   “memoization,” or more commonly called “caching.”

Embora o algoritmo no :ref:`AcitveCode 1 <lst_change2>` esteja correto, ele 
dá a impressão de ser um hack.
Além disso, se olharmos para as listas ``knownResults`` (resultados conhecidos)
podemos ver que existem alguns buracos na tabela. Na verdade, o termo para
o que fizemos não é programação dinâmica, mas melhoramos
o desempenho do nosso programa usando uma técnica conhecida como
"memoização" (*memoization*), ou mais comumente chamado de "caching".

..  A truly dynamic programming algorithm will take a more systematic
   approach to the problem. Our dynamic programming solution is going to
   start with making change for one cent and systematically work its way up
   to the amount of change we require. This guarantees us that at each step
   of the algorithm we already know the minimum number of coins needed to
   make change for any smaller amount.

Um algoritmo de programação verdadeiramente dinâmico tratará o problema
de forma mais sistemática. Nossa solução de programação dinâmica vai
começar fazendo troco para 1 centavo e sistematicamente gerar outros valores
de troco até chegar na quantidade necessária. Isso nos garante que a cada passo
do algoritmo já sabemos o número mínimo de moedas necessárias para
fazer o troco para qualquer quantia menor.

..  Let’s look at how we would fill in a table of minimum coins to use in
   making change for 11 cents. :ref:`Figure 4 <fig_dpcoins>` illustrates the
   process. We start with one cent. The only solution possible is one coin
   (a penny). The next row shows the minimum for one cent and two cents.
   Again, the only solution is two pennies. The fifth row is where things
   get interesting. Now we have two options to consider, five pennies or
   one nickel. How do we decide which is best? We consult the table and see
   that the number of coins needed to make change for four cents is four,
   plus one more penny to make five, equals five coins. Or we can look at
   zero cents plus one more nickel to make five cents equals 1 coin. Since
   the minimum of one and five is one we store 1 in the table. Fast forward
   again to the end of the table and consider 11 cents. :ref:`Figure 5 <fig_eleven>`
   shows the three options that we have to consider:

Vejamos como preencher uma tabela com as quantidades mínimas de moedas 
para fazer o troco de 11 centavos. A :ref:`Figura 4 <fig_dpcoins>` ilustra o
processo. Nós começamos com um centavo. A única solução possível é uma moeda
de 1 centavo. A próxima linha mostra o mínimo para 1 e 2 centavos.
Mais uma vez, a única solução para 2 centavos é usando 2 moedas de 1 centavo. 
A quinta fila é onde as coisas começam a ficar interessantes.  
Agora temos duas opções a considerar, 5 moedas de 1 centavo ou 1 moeda de 5 centavos.
Como decidimos qual é a melhor? Começando pela moeda de 1 centavo, consultamos a tabela e vemos
que o número de moedas necessárias para fazer troco para 4 centavos é 4,
mais 1 centavo para totalizar 5, resultando em cinco moedas. Ou podemos usar 
zero moedas de 1 centavo e uma moeda 5 centavos, no total de 1 moeda.
Como o mínimo entre 1 e 5 é 1, armazenamos 1 na tabela. Vamos já avançar 
para o final da tabela e considerar 11 centavos. A :ref:`Figura 5 <fig_eleven>`
mostra as três opções que temos que considerar:

..  #. A penny plus the minimum number of coins to make change for
      :math:`11-1 = 10` cents (1)
   #. A nickel plus the minimum number of coins to make change for
      :math:`11 - 5 = 6` cents (2)
   #. A dime plus the minimum number of coins to make change for
      :math:`11 - 10 = 1` cent (1)

#. Uma moeda de 1 centavo mais o número mínimo de moedas para fazer troco para :math:`11-1 = 10` centavos (1)

#. Uma moeda de 5 centavos mais o número mínimo de moedas para fazer troco para :math:`11 - 5 = 6` centavos (2)

#. Uma moeda de 10 centavos mais o número mínimo de moedas para fazer troco para :math:`11 - 10 = 1` centavo (1)

..  Either option 1 or 3 will give us a total of two coins which is the
   minimum number of coins for 11 cents.

Tanto a opção 1 quanto a 3 nos dá um total de 2 moedas, que é o
número mínimo de moedas para o troco de 11 centavos.

.. _fig_dpcoins:

.. figure:: Figures/changeTable.png
   :align: center
   :alt: image
       
   Figura 4: Mínimo Número de Moedas Necessárias para Fazer o Troco

.. _fig_eleven:

.. figure:: Figures/elevenCents.png
   :align: center
   :alt: image

   Figura 5: Três Opções a Considerar para o Número Mínimo de Moedas para 11 Centavos

..  :ref:`Listing 8 <lst_dpchange>` is a dynamic programming algorithm to solve our
   change-making problem. ``dpMakeChange`` takes three parameters: a list
   of valid coin values, the amount of change we want to make, and a list
   of the minimum number of coins needed to make each value. When the
   function is done ``minCoins`` will contain the solution for all values
   from 0 to the value of ``change``.

A :ref:`Listagem 8 <lst_dpchange>` mostra um algoritmo de programação dinâmica para resolver
nosso problema de troco. A função ``dpMakeChange`` (faz troco) aceita três parâmetros: uma lista
de valores de moedas, a quantidade de troco que queremos fazer e uma lista com as quantidades 
mínimas de moedas necessárias para cada valor. Quando a função termina, ``minCoins`` 
irá conter a solução para todos os valores de 0 até o valor de ``change`` (troco).

.. _lst_dpchange:

.. highlight:: python
    :linenothreshold: 5

**Listagem 8**

::

    def dpMakeChange(coinValueList,change,minCoins):
       for cents in range(change+1):
          coinCount = cents
          for j in [c for c in coinValueList if c <= cents]:
                if minCoins[cents-j] + 1 < coinCount:
                   coinCount = minCoins[cents-j]+1
          minCoins[cents] = coinCount
       return minCoins[change]

..  Note that ``dpMakeChange`` is not a recursive function, even though we
   started with a recursive solution to this problem. It is important to
   realize that just because you can write a recursive solution to a
   problem does not mean it is the best or most efficient solution. The
   bulk of the work in this function is done by the loop that starts on
   line 4. In this loop we consider using all possible coins to
   make change for the amount specified by ``cents``. Like we did for the
   11 cent example above, we remember the minimum value and store it in our
   ``minCoins`` list.

Note que ``dpMakeChange`` não é uma função recursiva, apesar de termos
começado com uma solução recursiva para este problema. É importante
perceber que só porque você pode escrever uma solução recursiva para um
problema não significa que esta é a melhor solução ou a mais eficiente.
Grande parte do trabalho nesta função é feito pelo loop que começa na
linha 4. Neste loop, consideramos o uso de todas as moedas possíveis para
fazer o troco para o valor especificado por ``cents``. Como fizemos para o
exemplo do troco de 11 centavos acima, guardamos o valor mínimo na
lista ``minCoins``.

..  Although our making change algorithm does a good job of figuring out the
   minimum number of coins, it does not help us make change since we do not
   keep track of the coins we use. We can easily extend ``dpMakeChange`` to
   keep track of the coins used by simply remembering the last coin we add
   for each entry in the ``minCoins`` table. If we know the last coin
   added, we can simply subtract the value of the coin to find a previous
   entry in the table that tells us the last coin we added to make that
   amount. We can keep tracing back through the table until we get to the
   beginning. 

Embora nosso algoritmo de troco consiga descobrir a quantidade 
mínima de moedas, isso não nos ajuda a fazer o troco uma vez que não
sabemos que moedas foram usadas. Podemos facilmente estender a função 
``dpMakeChange`` para manter as moedas usadas simplesmente 
guardando a última moeda que adicionamos para cada entrada na tabela 
``minCoins``. Se sabemos qual foi a última moeda
adicionada, podemos subtrair o valor da moeda para encontrar uma
entrada anterior na tabela que nos diz a última moeda adicionada
que resulta no valor restante.
Podemos continuar percorrendo a tabela até chegarmos ao início.

..  :ref:`ActiveCode 2 <lst_dpremember>` shows the ``dpMakeChange`` algorithm
   modified to keep track of the coins used, along with a function
   ``printCoins`` that walks backward through the table to print out the
   value of each coin used.
   This shows the algorithm in
   action solving the problem for our friends in Lower Elbonia. The first
   two lines of ``main`` set the amount to be converted and create the list of coins used. The next two
   lines create the lists we need to store the results. ``coinsUsed`` is a
   list of the coins used to make change, and ``coinCount`` is the minimum
   number of coins used to make change for the amount corresponding to the
   position in the list.

O :ref:`ActiveCode 2 <lst_dpremember>` mostra o algoritmo ``dpMakeChange``
modificado para guardar as moedas usadas, juntamente com uma função
``printCoins`` que percorre a tabela para imprimir o valor de cada moeda utilizada.
Isso mostra o algoritmo em ação resolvendo o problema para nossos amigos na Elbonia do Sul. As duas
primeira linhas da função ``main`` definem o valor a ser convertido e criam a lista de moedas usadas. 
As duas próximas linhas criam as listas para armazenar os resultados. A lista ``coinsUsed`` (moedas usadas)
armazena as moedas usadas para fazer o troco, e ``coinCount`` (conta moeda) guarda o número mínimo
de moedas utilizadas para fazer o troco para o valor correspondente à
posição na lista.

..  Notice that the coins we print out come directly from the ``coinsUsed``
   array. For the first call we start at array position 63 and print 21.
   Then we take :math:`63 - 21 = 42` and look at the 42nd element of the
   list. Once again we find a 21 stored there. Finally, element 21 of the
   array also contains 21, giving us the three 21 cent pieces.

Observe que as moedas que são impressas vêm diretamente da lista "coinsUsed".
Para a primeira chamada, começamos na posição 63 e na impressão 21.
Então pegamos :math:`63 - 21 = 42` e olhamos o 42º elemento da lista.
Mais uma vez encontramos um 21 armazenado lá. Finalmente, o elemento 21 da lista
também contém 21, resultando em três moedas de 21 centavos.


.. activecode:: lst_dpremember
    :caption: Solução Completa para o Problema de Troco
    :nocodelens:

    def dpMakeChange(coinValueList,change,minCoins,coinsUsed):
       for cents in range(change+1):
          coinCount = cents
          newCoin = 1
          for j in [c for c in coinValueList if c <= cents]:  
                if minCoins[cents-j] + 1 < coinCount:
                   coinCount = minCoins[cents-j]+1
                   newCoin = j
          minCoins[cents] = coinCount
          coinsUsed[cents] = newCoin
       return minCoins[change]

    def printCoins(coinsUsed,change):
       coin = change
       while coin > 0:
          thisCoin = coinsUsed[coin]
          print(thisCoin)
          coin = coin - thisCoin

    def main():
        amnt = 63
        clist = [1,5,10,21,25]
        coinsUsed = [0]*(amnt+1)
        coinCount = [0]*(amnt+1)
        
        print("Fazendo troco para",amnt,"requer")
        print(dpMakeChange(clist,amnt,coinCount,coinsUsed),"moedas")
        print("Elas são:")
        printCoins(coinsUsed,amnt)
        print("Lista de moedas usadas:")
        print(coinsUsed)
        
    main()
        



