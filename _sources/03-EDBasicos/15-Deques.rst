..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


O que é uma Deque?
~~~~~~~~~~~~~~~~~~

Uma **deque**, também é conhecida como fila de duas extremidades, é uma coleção ordenada
de itens semelhantes à fila. Tem duas extremidades, uma é o início (*front*) e uma é 
o  fim (*rear*), e os itens permanecem posicionados na coleção. O que faz um
deque diferente é a natureza não-restritiva de adicionar e remover
itens. Novos itens podem ser adicionados no início ou no fim. Da mesma forma,
itens existentes podem ser removidos de qualquer uma das extremidades.
De certa forma, esta estrutura híbrida fornece todas as capacidades de pilhas e filas
em uma única estrutura de dados :ref:`Figura 1 <fig_basicdeque>` mostra um deque de objetos de dados do Python.

É importante notar que, embora a deque possa assumir muitas
das características de pilhas e filas, não requer a oredanação LIFO
nem a FIFO que são impostas para essas estruturas de dados. É sua responsabilidade
fazer uso consistente das operações de inserção e remoção.

.. _fig_basicdeque:

.. figure:: Figures/basicdeque.png
   :align: center

   Figura 1: Uma Deque de Objetos do Python


