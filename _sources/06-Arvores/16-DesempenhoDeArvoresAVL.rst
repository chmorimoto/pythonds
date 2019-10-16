..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Desempenho de Árvores AVL
~~~~~~~~~~~~~~~~~~~~~~~~~

Antes de seguirmos adiante, vamos olhar para as consequências de garantirmos
esse novo requisito de fator de balanceamento. Nossa afirmação é de que ao
garantirmos que uma árvore tenha somente fator de balanceamento de -1, 0 ou 1
nós podemos desempenho assintótico melhor com operações chaves. Vamos começar
imaginando como essa condição de balanceamento altera a árvore em seu pior
caso. Há duas possibilidades a serem consideradas: uma árvore pesada à
esquerda ou pesada à direita. Se considerarmos árvores com alturas 0, 1, 2 e 3,
a :ref:`Figura 2 <fig_worstAVL>` ilustra a árvore pesada à esquerda mais
desbalanceada sob essas novas regras.

.. _fig_worstAVL:

.. figure:: Figures/worstAVL.png
   :align: center

   Figura 2: Pior Caso de uma Árvore AVL Pesada à Esquerda
   

Olhando para o número total de nós na árvore, nós vemos que para uma
árvore de altura 0 temos 1 nó, para uma árvore de altura 1, existem
:math:`1+1 = 2` nós, para uma árvore de altura 2, são :math:`1+1+2 = 4`
e para uma árvore de altura 3, são :math:`1 + 2 + 4 = 7`. De modo geral,
o padrão que vemos para o número de nós em uma árvore de altura h
(:math:`N_h`) é:

.. math::

   N_h = 1 + N_{h-1} + N_{h-2}  


Essa recorrência pode parecer familiar para você porque ela é de fato muito
parecida com a sequência de Fibonacci. Podemos usar esse fato para derivar
uma fórmula para a altura da árvore AVL dado o número de nós na árvore. 
Lembre-se que para a sequência de Fibonacci o :math:`i_{ésimo}` número de
Fibonacci é dado por:
   
.. math::

   F_0 = 0 \\
   F_1 = 1 \\
   F_i = F_{i-1} + F_{i-2}  \text{ for all } i \ge 2


Um resultado matemático importante disso é que conforme os números da
sequência de Fibonacci se tornam maiores, a razão :math:`F_i / F_{i-1}`
se aproxima cada vez mais da razão de ouro :math:`\Phi`, definida como
:math:`Phi = \frac{1 + \sqrt{5}}{2}`. Você pode consultar um livro de
matemática para saber como a equação anterior é derivada. O que nós 
faremos aqui é simplesmente utilizar essa equação para aproximar
:math:`F_i` a :math:`F_i = \Phi^i/\sqrt{5}`. Se fizermos uso dessa
aproximação, podemos reescrever a equação para :math:`N_h` como:

.. math::

   N_h = F_{h+2} - 1, h \ge 1


Substituindo a referência de Fibonacci por sua aproximação da razão
de ouro, temos:

.. math::

   N_h = \frac{\Phi^{h+2}}{\sqrt{5}} - 1


Rerranjando os termos e tomando o log na base 2 em ambos os lados, 
conseguimos a seguinte derivação ao buscar a solução para :math:`h`:

.. math::

   \log{N_h+1} = (H+2)\log{\Phi} - \frac{1}{2} \log{5} \\
   h = \frac{\log{N_h+1} - 2 \log{\Phi} + \frac{1}{2} \log{5}}{\log{\Phi}} \\
   h = 1.44 \log{N_h}


Essa derivação nos mostra que a todo mmomento a altura da nossa árvore AVL
é igual a uma constante (1,44) vezes o log do número de nós na árvore. Isso
é uma ótima notícia para buscas em nossa árvore AVL porque limita essas
operações a :mat:`O(\log{N})`.
