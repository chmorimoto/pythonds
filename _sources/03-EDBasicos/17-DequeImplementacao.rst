..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementação de uma Deque in Python
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Como fizemos nas seções anteriores, criaremos uma nova classe para o
implementação do tipo de dados abstrato deque. Novamente, a lista do Python
irá fornecer um conjunto muito bom de métodos sobre os quais construir os detalhes
do deque. Nossa implementação (:ref:`Listagem 1 <lst_dequecode>`) assumirá que
o fim da deque está na posição 0 na lista.

.. _lst_dequecode:

.. highlight:: python
   :linenothreshold: 5

**Listagem 1**

::

    class Deque:
        def __init__(self):
            self.items = []

        def isEmpty(self):
            return self.items == []

        def addFront(self, item):
            self.items.append(item)

        def addRear(self, item):
            self.items.insert(0,item)

        def removeFront(self):
            return self.items.pop()

        def removeRear(self):
            return self.items.pop(0)

        def size(self):
            return len(self.items)

.. highlight:: python
   :linenothreshold: 500

Em ``removeFront()`` usamos o método ``pop()`` para remover o último elemento
da lista. No entanto, em ``removeRear()``, o método ``pop(0)`` deve
remover o primeiro elemento da lista. Da mesma forma, precisamos usar o
método ``insert()`` (linha 12) em ``addRear()`` desde o método ``append()``
pressupõe a adição de um novo elemento ao final da lista.

CodeLens 1 mostra a classe ``Deque`` em
ação como nós executamos a seqüência de operações de
:ref:`Tabela 1 <tbl_dequeoperations>`.


.. codelens:: deqtest
   :caption: Exemplo de Operações sobre uma Deque

   class Deque:
       def __init__(self):
           self.items = []

       def isEmpty(self):
           return self.items == []

       def addFront(self, item):
           self.items.append(item)

       def addRear(self, item):
           self.items.insert(0,item)

       def removeFront(self):
           return self.items.pop()

       def removeRear(self):
           return self.items.pop(0)

       def size(self):
           return len(self.items)

   d=Deque()
   print(d.isEmpty())
   d.addRear(4)
   d.addRear('dog')
   d.addFront('cat')
   d.addFront(True)
   print(d.size())
   print(d.isEmpty())
   d.addRear(8.4)
   print(d.removeRear())
   print(d.removeFront())
   

Você pode ver muitas semelhanças com o código Python já descrito para
pilhas (``Stack``)  e filas (``Queue``). É provável que você também observe que nesta
implementação inserir e remover itens do início consomem tempo O(1) enquanto
inserir e remover da parte do fim consome tempo  O(n). Isto é de se esperar dado
que as operações comuns que aparecem para adicionar e remover itens. Novamente,
o importante é ter certeza de que sabemos onde o  início e
parte do fim são atribuídos na implementação.

