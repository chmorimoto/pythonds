..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Exercícios de Programação
-------------------------

#. Estenda a função ``buildParseTree`` para lidar com expressões
   matemáticas que não têm espaços entre cada caractere.

#. Modifique as funções ``buildParseTree`` e ``evaluate`` para lidar
   com declarações booleanas (*e*, *ou* ou *não*). Lembre-se que o
   *não* é um operador unário, então isso pode complicar seu código
   de alguma forma.

#. Usando o método ``findSuccessor``, escreva uma varredura não
   recursiva infixa para uma árvore de busca binária.

#. Modifique o código para uma árvore de busca binária para que seja
   concorrente. Escreva um método de varredura infixa não recursivo
   para a árvore de busca binária concorrente. Uma árvore binária
   com threads mantém uma referência de cada nó para seu sucessor.

#. Modifique nossa implementação da árvore de busca binária para que
   ela lide com chaves duplicadas de forma apropriada. Isto é,
   se uma chave já estiver na árvore, então o novo valor deve
   substituir o antigo em vez de adicionarmos um novo nó com a
   mesma chave.

#. Crie um heap binário com heap de tamanho limitado. Em outras
   palavras, o heap apenas guarda os ``n`` itens mais importantes.
   Se o tamanho do heap ultrapassar ``n``, então o item menos
   importante deve ser eliminado.

#. Limpe a função ``printexp`` para que ela não inclua um par
   extra de parênteses entre cada número.

#. Usando o método ``buildHeap``, escreva uma função de ordenação
   que coloque em ordem uma lista em tempo :math:`O(n\log{n})`.

#. Escreva uma função que recebe uma árvore de expressões para
   uma expressão matemática e calcula a deriva dessa expressão
   com relação a alguma variável.

#. Implemente um heap binário como um max heap.

#. Usando a classe ``BinaryHeap``, implemente uma nova classe
   chamada ``PriorityQueue``. Sua classe ``PriorityQueue`` deve
   ter, além do construtor, os métodos ``enqueue`` e ``dequeue``.

