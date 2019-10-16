..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Árvores de Busca Binárias Balanceadas
-------------------------------------

Na seção anterior nós vimos como construir uma árvore de busca binária.
Uma coisa que aprendemos é que o desempenho de uma árvore de busca
binária pode degradar para :math:`O(n)` em operações como ``get`` e
``put``, em particular quando a árvore fica desbalanceada. Nesta seção
iremos conhecer um tipo especial de árvore de busca binária que 
automaticamente garante que sempre irá permanecer balanceada. Essa 
árvore é conhecida como **árvore AVL** e tal nome decorre dos seus
inventores: G.M. Adelson-Velskii e E.M. Landis.

Uma árvore AVL implementa o tipo de dado abstrato Map assim como uma 
árvore de busca binária convencional. A única diferença está no
comportamento da árvore. Para implementar nossa árvore AVL, vamos
precisar armazenar um **fator de balanceamento** para cada nó na árvore.
Fazemos isso olhando para as alturas das subárvores esquerda e direita
de cada nó. Mais formalmente, definimos o fator de balanceamento para
um nó como a diferença entre a altura da subárvore esquerda e a altura
da subárvore direita.

.. math::

   balanceFactor = height(leftSubTree) - height(rightSubTree)

Usando a definição de fator de balanceamento acima, dizemos que uma
subárvore está mais pesada à esquerda se o fator de balanceamento for
maior que zero. Se o fator for menor que zero, então a subárvore está
mais pesada à direita. Se o fator for zero, então a árvore está
perfeitamente balanceada. Para fins de implementação -- bem como para
colhermos os benefícios de uma árvore balanceada -- iremos dizer que
uma árvore está balanceada se o fator de balanceamento for -1, 0 ou 1.
Se o fator de balanceamento de um nó estiver fora desses limites, 
precisaremos então de um procedimento para deixar a árvore novamente
balanceada. A :ref:`Figura 1 <fig_unbal>` mostra um exemplo de uma
árvore desbalanceada mais pesada à direita, bem como os fatores de
balanceamento em cada nó.


.. _fig_unbal:

.. figure:: Figures/unbalanced.png
   :align: center

   Figura 1: Uma Árvore Desbalanceada para Direita com Três Fatores de Balanceamento
   

