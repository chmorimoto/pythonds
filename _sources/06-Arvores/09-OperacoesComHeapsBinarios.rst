..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Operações com Heaps Binários
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As operações básicas que iremos implementar para nosso heap binário
são as seguintes:

-  ``BinaryHeap()`` cria um novo heap binário vazio.

-  ``insert(k)`` adiciona um novo elemento ao heap.

-  ``findMin()`` retorna o item com a chave de menor valor, deixando o elemento no heap.

-  ``delMin()`` retorna o item com a chave de menor valor, removendo o elemnto do heap.

-  ``isEmpty()`` retorna `True` se o heap estiver vazio ou `False`, caso contrário.

-  ``size()`` returna o número de itens no heap.

-  ``buildHeap(list)`` constrói um novo heap a partir de uma lista de chaves.

O :ref:`ActiveCode 1 <lst_heap1>` mostra o uso de alguns dos métodos para heaps
binários. Observe que não importa a ordem com que adicionamos os itens ao heap, 
sempre o item de menor valor que é removido toda vez. Iremos voltar nossa
atenção agora para a criação e implementação dessa ideia.

.. _lst_heap1:


.. activecode:: heap1
    :caption: Usando um Heap Binário
    :nocodelens:
    
    from pythonds.trees.binheap import BinHeap
    
    bh = BinHeap()
    bh.insert(5)
    bh.insert(7)
    bh.insert(3)
    bh.insert(11)
    
    print(bh.delMin())

    print(bh.delMin())

    print(bh.delMin())

    print(bh.delMin())


