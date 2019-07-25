..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


O Tipo Abstrato de Dados Fila
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

O tipo de dados abstrato (*abstract data type*) da fila é definido pela seguinte
estrutura e operações. Uma fila é estruturada, conforme descrito anteriormente,
como uma coleção ordenada de itens que são inseridos em uma extremidade, chamada de “fim”,
e removidos da outra extremidade, chamada de "início".
As filas mantêm uma ordenação FIFO.
As operações da fila são dadas abaixo.

- ``Queue()`` cria uma nova fila que está vazia. Não precisa de parâmetros e retorna uma fila vazia.

- ``enqueue(item)`` insere um novo item no final da fila. Precisa o item e não retorna nada.

- ``dequeue()`` remove o item do início da fila. Não precisa de parâmetros e retorna o item. A fila é modificada.

- ``isEmpty()`` testa para ver se a fila está vazia. Não precisa de parâmetros e retorna um valor booleano (``bool``); ``True`` se a fila está vazia e ``False`` em caso contrário.

- ``size()`` retorna o número de itens na fila. Não precisa de parâmetros e retorna um inteiro (``int``).

Como exemplo, se supormos que ``q`` é uma fila que foi criada
e está atualmente vazia, então :ref:`Tabela 1 <tbl_queueoperations>` mostra o
resultados de uma seqüência de operações sobre filas.
O conteúdo da fila é mostrado de tal forma que o início está à direita.
4 foi o primeiro item enfileirado (``enqueue()``) por isso
é o primeiro item removido e retornado ``dequeue()``.

.. _tbl_queueoperations:

.. table:: **Tabela 1: Examplos de operações sobre filas**

    ============================ ======================== =================== 
                    **Operação**     **Conteúdo da fila** **Valor retornado** 
    ============================ ======================== =================== 
                 ``q.isEmpty()``                   ``[]``            ``True`` 
                ``q.enqueue(4)``                  ``[4]``                    
            ``q.enqueue('dog')``            ``['dog',4]``                    
             ``q.enqueue(True)``       ``[True,'dog',4]``                    
                    ``q.size()``       ``[True,'dog',4]``               ``3`` 
                 ``q.isEmpty()``       ``[True,'dog',4]``           ``False`` 
              ``q.enqueue(8.4)``   ``[8.4,True,'dog',4]``                    
                 ``q.dequeue()``     ``[8.4,True,'dog']``               ``4`` 
                 ``q.dequeue()``           ``[8.4,True]``           ``'dog'`` 
                    ``q.size()``           ``[8.4,True]``               ``2`` 
    ============================ ======================== =================== 


