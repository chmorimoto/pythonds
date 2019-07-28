..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


O Tipo Abstrato de Dados Deque
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

O tipo de dado abstrato de deque (*fila dupla*) é definido pela seguinte estrutura e
operações. Um deque é estruturado, como descrito anteriormente, como um
coleção de itens em que os itens são inseridos e removidos de qualquer extremidade
início ou fim. As operações deque são dadas abaixo.

- ``Deque ()`` cria um novo deque que está vazia. Não precisa de parâmetros
   e retorna um deque vazia.

- ``addFront(item)`` insere um novo item no início da deque. Isto precisa do item como parâmetro e não retorna nada.

- ``addRear(item)`` insere um novo item no fim da deque. Precisa do item e não retorna nada.

- ``removeFront()`` remove o item do início da deque. Não precisa de parâmetros e retorna o item. A deque é modificada.

- ``removeRear()`` remove o item do fim da deque. Não precisa de parâmetros e retorna o item. A deque é modificada.

- ``isEmpty()`` testa se a deque está vazia. Não precisa de parâmetros e retorna um valor booleano (``bool``); ``True`` se a fila está vazia e ``False`` em caso contrário.

- ``size()`` retorna o número de itens na deque. Não precisa de parâmetros e retorna um inteiro (``int``).

Por exemplo, se supormos que ``d`` é uma deque que foi criada
e está atualmente vazia, então Table {dequeoperations} mostra os resultados
de uma seqüência de operações sobre a deque.
Note que o conteúdo do início é listado à direita.
É muito importante acompanhar o início e o fim a medida que itens são inseridos e removidos da deque já que as coisas podem
ficar um pouco confusas.

.. _tbl_dequeoperations:

.. table:: **Tabela 1: Examplos de Operações sobre Deques**

    ============================ ============================ ================== 
                    **Operação**        **Conteúdo da Deque** **Valor Retornado** 
    ============================ ============================ ================== 
                 ``d.isEmpty()``                       ``[]``           ``True`` 
                ``d.addRear(4)``                      ``[4]``                    
            ``d.addRear('dog')``               ``['dog',4,]``                    
           ``d.addFront('cat')``          ``['dog',4,'cat']``                    
            ``d.addFront(True)``     ``['dog',4,'cat',True]``                    
                    ``d.size()``     ``['dog',4,'cat',True]``              ``4`` 
                 ``d.isEmpty()``     ``['dog',4,'cat',True]``          ``False`` 
              ``d.addRear(8.4)`` ``[8.4,'dog',4,'cat',True]``                    
              ``d.removeRear()``     ``['dog',4,'cat',True]``            ``8.4`` 
             ``d.removeFront()``          ``['dog',4,'cat']``           ``True`` 
    ============================ ============================ ================== 


