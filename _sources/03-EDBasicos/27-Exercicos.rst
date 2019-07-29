..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.

Programming Exercises 
---------------------

#. Modifique o algoritmo que converte da notação infixa para posfixa de maneira que
   leve em considerações possíveis erros na expressão infixa.

#. Modifique o algoritmo que avalie um expressão posfixa de maneira que
   leve em consideração possíveis erros na expressão  posfixa.

#. Implemente um avaliador de expressões infixas que combine a
   funcionalidade da conversão infixa-para-posfixa e o algoritmo de
   avaliação posfixa.  Seu avaliador deve processar os itens
   (*tokens*) da expressão infixa da esquerda para a direita e usar
   duas pilhas, uma para operadores e outra para operandos, para
   executar a avaliação.

#. Transforme seu avaliador infixa do problema anterior em uma
   calculadora.
   
#. Implemente o TAD ``Queue``, usando uma lista nativa do Python
   (``list``) de tal forma que o fim da fila está no fim da lista

#. Projete e implemente um experimento para fazer comparações de
   *benchmark* de duas implementações de fila. O que você pode
   aprender com tal experimento?

#. É possível implementar uma fila de modo que tanto o ``enqueue()``
   como ``dequeue()`` tenham *consumo de tempo médio*
   :math:`O(1)`. Neste caso, significa que na maioria das vezes
   ``enqueue()`` e o ``dequeue()`` consomem tempo constante exceto em
   uma circunstância particular em que ``dequeue()`` consome tempo
   :math:`O(n)`.

#. Considere uma situação da vida real. Formule uma pergunta e depois
   projete uma simulação que pode ajudar. Situações possíveis incluem:

   - Carros em uma fila de um lava a jato

   - Clientes na fila do caixa de uma mercearia

   - Aviões decolando e pousando em uma pista

   - um caixa de banco

   Certifique-se de declarar quaisquer suposições que você fizer e fornecer
   dados probabilísticos que devem ser considerados como parte do cenário.

#. Modifique a simulação de Batata Quente para permitir uma escolha aleatória do
   valor de contagem de modo que cada passa não seja previsível a partir do anterior.

#. Implemente uma máquina de ordenação *radix*. Uma ordenação radix
   para inteiros na base 10 é uma técnica de ordenação que utiliza uma
   coleção de escaninhos, um escaninho principal e um escaninho para
   cada dígito.  Cada escaninho age como uma fila e mantém seus
   valores na ordem em que eles chegam.  O algoritmo começa colocando
   cada número no escaninho principal.  Em seguida, considera cada
   número dígito por dígito.  O primeiro número é removido e colocado
   no escaninho correspondente ao dígito a ser considerado.  Por
   exemplo, se o dígito sendo considerado é o menos significativo, 534
   é colocado na escaninho do dígito 4 e 667 é colocado na escaninho
   de dígito 7.  Uma vez que todos os valores são colocados em os
   escaninhos de dígitos correspondentes, os valores são coletados do
   escaninho 0 ao 9 e colocados de volta no escaninho principal.  O
   processo continua com o dígito das dezenas, centenas e assim por
   diante.  Depois que o último dígito é processado, a escaninho
   principal contém os valores em ordem.

#. Outro exemplo do problema de parênteses vem de linguagem de
   marcação de hipertexto (HTML). Em HTML, existem marcadores de
   abertura e fechamento que devem ser balanceados para descrever
   adequadamente uma documento web.  Este é um documento HTML muito
   simples:

   ::

       <html>
          <head>
             <title>
                Example
             </title>
          </head>

          <body>
             <h1>Hello, world</h1>
          </body>
       </html>

   destina-se apenas a mostrar a estrutura de correspondência e
   aninhamento de marcadores a linguagem. Escreva um programa que
   possa verificar se um documento HTML tem marcadores apropriados de
   abertura e fechamento.

#. Estenda o programa da Listagem 2.15 para receber palindromos com
   espaços.  For example, ``"ROMA ME TEM AMOR"`` é um palíndromo se
   ignorarmos os espaços.

#. Para implementar o método ``length()``, contamos o número de nós em
   a lista. Uma estratégia alternativa seria armazenar o número de nós
   na lista como uma parte adicional de dados na cabeça da
   lista. Modifique a classe ``UnorderedList`` para incluir esta
   informação e reescreva o método ``length()``.

#. Implemente o método ``remove()`` para que funcione corretamente no
   caso em que o item não está na lista.

#. Modifique as classes ``UnorderedList`` e ``OrderedList`` para
   permitir duplicatas. Quais métodos serão impactados por essa
   mudança?

#. Implemente o método ``__str__()`` da classe ``UnorderedList``.
   Qual seria uma boa representação de string para uma lista?

#. Implemente o método ``__str__()`` para que as listas sejam exibidas
   como em Python (com colchetes).

#. Implemente as operações restantes definidas na classe ``UnorderedList``
   (``append()``, ``index()``, ``pop()``, ``insert()``).

#. Implemente um método de fatia para a classe
   ``UnorderedList``. Deveria receber dois parâmetros, ``start`` e
   ``stop``, e retornar um clone da lista começando na posição
   ``start`` e indo até, mas não incluindo, a posição ``stop``.

#. Implemente as operações restantes definidas na classe
   ``OrderedList``.

#. Considere a relação entre listas não ordenadas e ordenadas. É 
   possível que a herança pudesse ser usada para construir uma
   implementação? Implemente esta hierarquia de herança.

#. Implemente uma pilha usando listas ligadas.

#. Implemente uma fila usando listas ligadas.

#. Implemente um deque usando listas ligadas.

#. Projete e implemente um experimento que irá comparar o desempenho
   de uma lista do Python (``list``) com uma lista implementada como
   uma lista ligada.

#. Projete e implemente um experimento que irá comparar o desempenho
   de pilhas e de filas implementadas com listas do Python e com
   listas ligadas.

#. A implementação da lista ligada fornecida acima é chamada de *lista
   ligada simples* pois cada nó tem uma única referência para o
   próximo nó em seqüência.  Uma implementação alternativa é conhecida
   como *lista duplamente ligada*.  Nesta implementação, cada nó tem
   uma referência para o próximo nó (comumente chamada de ``next``),
   bem como uma referência ao anterior nó (geralmente chamada de
   ``back``). A referência da cabeça também contém duas referências,
   um para o primeiro nó na lista ligada e um para o último. Codifique
   esta implementação em Python.

#. Crie uma implementação de uma fila que teria um desempenho médio de
   :math:`O(1)` para operações ``enqueue()`` e ``dequeue()``.
