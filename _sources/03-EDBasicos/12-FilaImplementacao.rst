..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementando uma Fila em Python
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

É novamente apropriado criar uma nova classe para a implementação do
tipo abstrato de dados fila, a classe ``Queue``. Como antes, vamos usar o poder e
simplicidade das  listas de python (``list``) para construir a representação
interna da fila.

Precisamos decidir qual extremidade da lista usar como parte de fim e qual
usa como  início. A implementação mostrada em :ref:`Listagem 1 <lst_queuecode>`
supõe que o fim está na posição 0 da lista. Isso nos permite
usemos a função ``insert()`` nas listas para adicionar novos elemetos ao final da fila.
A operação ``pop()`` pode ser usada para remover o elemento do início
(o último elemento da lista). Lembre-se de que isso também significa que o consumo de tempo
de ``enqueue()`` será O(n) e o consumo de tempo de ``dequeue()`` será será O(1).

.. _lst_queuecode:

**Listing 1**

::

    class Queue:
        def __init__(self):
            self.items = []

        def isEmpty(self):
            return self.items == []

        def enqueue(self, item):
            self.items.insert(0,item)

        def dequeue(self):
            return self.items.pop()

        def size(self):
            return len(self.items)

CodeLens 1 mostra a classe ``Queue`` em ação
durante uma sequência de operações da :ref:`Tabela 1 <tbl_queueoperations>`.

.. codelens:: ququeuetest
   :caption: Example Queue Operations

   class Queue:
       def __init__(self):
           self.items = []

       def isEmpty(self):
           return self.items == []

       def enqueue(self, item):
           self.items.insert(0,item)

       def dequeue(self):
           return self.items.pop()

       def size(self):
           return len(self.items)

   q=Queue()
   
   q.enqueue(4)
   q.enqueue('dog')
   q.enqueue(True)
   print(q.size())


Outras manipulações de dessa fila produz os seguintes resultados:


::

    >>> q.size()
    3
    >>> q.isEmpty()
    False
    >>> q.enqueue(8.4)
    >>> q.dequeue()
    4
    >>> q.dequeue()
    'dog'
    >>> q.size()
    2

.. admonition:: Teste a sua compreensão

   .. mchoice:: queue_1
      :correct: b
      :answer_a: 'hello', 'dog'
      :answer_b: 'dog', 3
      :answer_c: 'hello', 3
      :answer_d: 'hello', 'dog', 3
      :feedback_a: Lembre-se de que a primeira coisa inserida à fila é a primeira coisa removida. FIFO
      :feedback_b: Sim, primeiro que entra primeiro que sai significa que o 'hello' se foi.
      :feedback_c: Filas e Pilhas são estruturas de dados nas quais você só pode acessar a primeira e a última coisa.
      :feedback_d: Ooops, talvez você tenha perdido a chamada dequeue() no final?

      Suppose que realizamos as seguintes operações.

      ::
      
          q = Queue()
          q.enqueue('hello')
          q.enqueue('dog')
          q.enqueue(3)
          q.dequeue()

      Quais itens são deixados na fila?

