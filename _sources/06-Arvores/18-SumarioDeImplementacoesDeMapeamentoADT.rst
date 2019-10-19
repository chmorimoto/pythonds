..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Sumário de Implementações de Mapeamento ADT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nos últimos dois capítulos nós estudamos várias estruturas de dados
que podem ser usadas para implementar o tipo de dado abstrato *map*.
Uma busca binária em uma lista, uma tabela de espalhamento, uma
árvore de busca binária e uma árvore de busca binária balanceada.
Para concluir esta seção, vamos compilar aqui o desempenho de cada
estrutura de dados para as operações chaves definidas pelo mapeamento
ADT (veja a :ref:`Tabela 1 <tab_compare>`).


.. _tab_compare:

.. table:: **Tabela 1: Comparando o Desempenho de Diferentes Implementações de Mapeamento**

    =========== ======================  ==============   =======================  ====================
    operação    Lista Ordenada          Tabela de Hash   Árvore de Busca Binária  Árvore AVL
    =========== ======================  ==============   =======================  ====================
         put    :math:`O(n)`            :math:`O(1)`     :math:`O(n)`             :math:`O(\log_2{n})`   
         get    :math:`O(\log_2{n})`    :math:`O(1)`     :math:`O(n)`             :math:`O(\log_2{n})`   
         in     :math:`O(\log_2{n})`    :math:`O(1)`     :math:`O(n)`             :math:`O(\log_2{n})`   
         del    :math:`O(n)`            :math:`O(1)`     :math:`O(n)`             :math:`O(\log_2{n})`
    =========== ======================  ==============   =======================  ====================
