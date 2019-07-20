..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Programming Exercises


..  #. Write a recursive function to compute the factorial of a number.
   #. Write a recursive function to reverse a list.
   #. Modify the recursive tree program using one or all of the following
      ideas:
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
      If you implement all of the above ideas you will have a very
      realistic looking tree.
   #. Find or invent an algorithm for drawing a fractal mountain. Hint: One
      approach to this uses triangles again.
   #. Write a recursive function to compute the Fibonacci sequence. How
      does the performance of the recursive function compare to that of an
      iterative version?
   #. Implement a solution to the Tower of Hanoi using three stacks to keep
      track of the disks.
   #. Using the turtle graphics module, write a recursive program to
      display a Hilbert curve.
   #. Using the turtle graphics module, write a recursive program to
      display a Koch snowflake.
   #. Write a program to solve the following problem: You have two jugs: a
      4-gallon jug and a 3-gallon jug. Neither of the jugs have markings on
      them. There is a pump that can be used to fill the jugs with water.
      How can you get exactly two gallons of water in the 4-gallon jug?
   #. Generalize the problem above so that the parameters to your solution
      include the sizes of each jug and the final amount of water to be
      left in the larger jug.
   #. Write a program that solves the following problem: Three missionaries
      and three cannibals come to a river and find a boat that holds two
      people. Everyone must get across the river to continue on the
      journey. However, if the cannibals ever outnumber the missionaries on
      either bank, the missionaries will be eaten. Find a series of
      crossings that will get everyone safely to the other side of the
      river.
   #. Modify the Tower of Hanoi program using turtle graphics to animate
      the movement of the disks. Hint: You can make multiple turtles and
      have them shaped like rectangles.
   #. Pascal’s triangle is a number triangle with numbers arranged in
      staggered rows such that 
      .. math::
         a_{nr} = {n! \over{r! (n-r)!}}   
      This equation is the equation for a binomial coefficient. You can
      build Pascal’s triangle by adding the two numbers that are diagonally
      above a number in the triangle. An example of Pascal’s triangle is
      shown below.
      ::
                           1
                        1   1
                        1   2   1
                     1   3   3   1
                  1   4   6   4   1
      Write a program that prints out Pascal’s triangle. Your program
      should accept a parameter that tells how many rows of the triangle to
      print.
   #. Suppose you are a computer scientist/art thief who has broken into a
      major art gallery. All you have with you to haul out your stolen art
      is your knapsack which only holds :math:`W` pounds of art, but for
      every piece of art you know its value and its weight. Write a dynamic
      programming function to help you maximize your profit. Here is a
      sample problem for you to use to get started: Suppose your knapsack
      can hold a total weight of 20. You have 5 items as follows:
      ::    
         item     weight      value
            1        2           3
            2        3           4
            3        4           8
            4        5           8
            5        9          10
   #. This problem is called the string edit distance problem, and is quite
      useful in many areas of research. Suppose that you want to transform
      the word “algorithm” into the word “alligator.” For each letter you
      can either copy the letter from one word to another at a cost of 5,
      you can delete a letter at cost of 20, or insert a letter at a cost
      of 20. The total cost to transform one word into another is used by
      spell check programs to provide suggestions for words that are close
      to one another. Use dynamic programming techniques to develop an
      algorithm that gives you the smallest edit distance between any two
      words.

Exercícios de Programação
-------------------------

#. Escreva uma função recursiva para calcular o fatorial de um número.

#. Escreva uma função recursiva para inverter uma lista.

#. Modifique o programa recursivo para desenhar árvores usando uma ou todas as seguintes idéias:

   - Modifique a espessura dos ramos para que, quando o ``branchLen`` ficar menor, a linha fica mais fina.
   
   - Modifique a cor dos ramos para que, quando o ``branchLen`` ficar muito curto, seja colorido como uma folha.

   - Modifique o ângulo usado na rotação da tartaruga para que em cada bifurcação o ângulo seja selecionado aleatoriamente dentro de algum intervalo. Por exemplo escolha o ângulo entre 15 e 45 graus. Teste alguns valores até descobrir valores que geram boas árvores.

   - Modifique o ``branchLen`` de forma recursiva para que, em vez de subtrair sempre a mesma quantidade, subtraia uma quantidade aleatória dentro de algum intervalo.

   Se você implementar todas as idéias acima, você terá uma árvore bem mais realista.

#. Encontre ou invente um algoritmo para desenhar uma montanha fractal. Dica: um abordagem para esse problema usa triângulos novamente.

#. Escreva uma função recursiva para calcular a sequência de Fibonacci. Como
   o desempenho da função recursiva se compara com o de uma versão iterativa?

#. Implemente uma solução para a Torre de Hanoi usando três pilhas para manipular os discos.

#. Usando o módulo gráfico turtle, escreva um programa recursivo para
   exibir uma curva de Hilbert.

#. Usando o módulo gráfico turtle, escreva um programa recursivo para
   exibir um floco de neve Koch.

#. Escreva um programa para resolver o seguinte problema: você tem dois jarros:
   um de 4 litros e outro de 3 litros. Nenhum dos jarros tem marcações.
   Existe uma torneira que pode ser usada para encher os jarros com água.
   Como você pode obter exatamente dois litros de água no jarro de 4 litros?

#. Generalize o problema acima para que os parâmetros da sua solução
   incluam os tamanhos de cada jarro e a quantidade final de água a ser
   deixada no jarro maior.

#. Escreva um programa que resolva o seguinte problema: Três missionários
   e três canibais chegam a um rio e encontram um barco que transporta até duas pessoas.
   Todos devem atravessar o rio para continuar a
   viagem. No entanto, se o número de canibais for maior que o número de missionários
   em qualquer lado do rio, os missionários serão comidos. Encontre uma série de
   travessias que vão levar todos com segurança para o outro lado do
   rio.

#. Modifique o programa Torre de Hanoi usando o módulo gráfico turtle para animar
   o movimento dos discos. Dica: você pode criar várias tartarugas na forma de 
   retângulos.

#. O triângulo de Pascal é um triângulo numérico com números dispostos em
   filas escalonadas de tal forma que

   .. math::
      a_{nr} = {n! \over{r! (n-r)!}}   

   Essa equação é a equação de um coeficiente binomial. Você pode
   construir o triângulo de Pascal adicionando os dois números diagonalmente
   acima de um número no triângulo. Um exemplo do triângulo de Pascal é
   mostrado abaixo.

   ::

                           1
                        1     1
                     1     2     1
                  1     3     3     1
               1     4     6     4     1

   Escreva um programa que imprima o triângulo de Pascal. Seu programa
   deve aceitar um parâmetro que define quantas linhas do triângulo devem ser impressas.

#. Suponha que você é um cientista da computação/ladrão de arte que invadiu uma
   grande galeria de arte. Tudo o que você tem para levar sua arte roubada
   é a sua mochila que só consegue carregar :math:`W` kilos, e para
   cada obra de arte você conhece seu valor e seu peso. Escreva uma função 
   usando programação dinâmica para ajudá-lo a maximizar seu lucro. Aqui está um
   exemplo de problema para ajudar você a começar: Suponha que sua mochila
   pode carregar um peso total de 20. Você tem os 5 itens a seguir:

   ::

      item  peso  valor
         1  2  3
         2  3  4
         3  4  8
         4  5  8
         5  9  10

#. Esse problema é chamado de problema de distância de edição de string e é bastante
   útil em muitas áreas de pesquisa. Suponha que você queira transformar
   a palavra "algorithm" na palavra "alligator". Para cada letra que você
   pode copiar a letra de uma palavra para outra a um custo de 5, ou 
   você pode remover a letra ao custo de 20 ou inserir uma letra a um custo
   de 20. O custo total para transformar uma palavra em outra é usado em
   programas de verificação ortográfica para fornecer sugestões de palavras.
   Use técnicas de programação dinâmica para desenvolver um
   algoritmo que lhe dá a menor distância de edição entre quaisquer duas
   palavras.
