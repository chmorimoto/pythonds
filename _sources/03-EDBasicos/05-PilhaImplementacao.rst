..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementando uma Pilha em Python
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Agora que definimos claramente a pilha como um tipo de dados abstrato,
vamos voltar nossa atenção para o uso do Python para implementar uma pilha.
Lembre-se que quando damos uma implementação particular a um tipo de dados abstrato
nós chamamos esta implementação de uma *estrutura de dados*.

Como descrevemos no capítulo 1, em Python, como em qualquer
linguagem de programação orientada a objetos, a implementação de um
tipo abstrato de dados como uma pilha é feita através da criação de uma nova classe.
As operações sobre uma pilha são implementadas como métodos.
Além disso, para implementar uma pilha, 
que é uma coleção de elementos, faz sentido utilizar o poder
e simplicidade das coleções primitivas fornecidas pelo Python.
Nós usaremos uma lista (``list``).

Lembre-se de que a classe de lista no Python fornece mecanismo para mantermos
coleção ordenada de itens e um conjunto de métodos para manipularmos essa coleção.
Por exemplo, se tivermos a lista ``[2, 5, 3, 6, 7, 4]``,
precisamos apenas decidir qual extremidade da lista será
considerado o *topo* da pilha e qual será a *base*.
Uma vez que essa decisão é tomada, as operações podem ser implementadas
usando uma lista e métodos como ``append()`` e ``pop()``.

A seguinte implementação de pilha (:ref:`ActiveCode 1 <lst_stackcode1>`) supõe
que o final da lista mantém o elemento do topo.
Como a pilha cresce (como ocorrem as operações ``push()``),
novos itens serão inseridos no final da lista.
As operações ``pop()`` atuarão na mesma extremidade.

.. note:: A implementação mantém os termos em inglês. Assim a classe implementada receberá o nome ``Stack`` em vez de ``Pilha``.

.. _lst_stackcode1:


.. activecode:: stack_1ac
   :caption: Implementação de uma classe Stack usando listas de Python
   :nocodelens:

   class Stack:
        def __init__(self):
            self.items = []

        def isEmpty(self):
            return self.items == []

        def push(self, item):
            self.items.append(item)

        def pop(self):
            return self.items.pop()

        def peek(self):
            return self.items[len(self.items)-1]

        def size(self):
            return len(self.items)

Lembre-se que quando clicamos no botão ``run`` nada acontece além da
definição da classe. Nós devemos criar um objeto ``Stack`` e então usá-lo.
:ref:`ActiveCode 2 <lst_stackcode1>` mostra a classe ``Stack`` em ação
ao executarmos a seqüência de operações na
:ref:`Tabela 1 <tbl_stackops>`. Observe que a definição da classe ``Stack`` é
importada do módulo ``pythond``.

.. note::
    O módulo ``pythonds`` contém implementações de todas as estruturas de dados discutidas
    neste livro. Está estruturado de acordo com as seções: básico, árvores e grafos.
    O módulo pode ser baixado de `pythonworks.org <http://www.pythonworks.org/pythonds>`_.

.. activecode:: stack_ex_1
   :nocodelens:

   from pythonds.basic.stack import Stack

   s=Stack()
   
   print(s.isEmpty())
   s.push(4)
   s.push('dog')
   print(s.peek())
   s.push(True)
   print(s.size())
   print(s.isEmpty())
   s.push(8.4)
   print(s.pop())
   print(s.pop())
   print(s.size())



É importante notar que poderíamos ter escolhido implementar a pilha
usando uma lista em que o topo estaria no início e não no final. 
Neste caso, os métodos ``pop()`` e ``append()`` não seriam apropriados
pois deveríamos indexar a posição 0 (o primeiro item da lista)
explicitamente usando ``pop(0)`` e ``insert(0, item)``.
A implementação é mostrada em :ref:`CodeLens 1 <lst_stackcode2>`.
       

.. _lst_stackcode2:

.. codelens:: stack_cl_1
   :caption: Implementação alternativa da classe Stack

   class Stack:
        def __init__(self):
            self.items = []

        def isEmpty(self):
            return self.items == []

        def push(self, item):
            self.items.insert(0,item)

        def pop(self):
            return self.items.pop(0)

        def peek(self):
            return self.items[0]

        def size(self):
            return len(self.items)

   s = Stack()
   s.push('hello')
   s.push('true')
   print(s.pop())

Essa capacidade de alterar a implementação de um tipo abstrato de dados
mantendo as características lógicas é um exemplo de abstração.
No entanto, mesmo que a pilha funcione da mesma forma,
se considerarmos o desempenho das duas implementações, há definitivamente uma diferença.
Lembre-se que o ``append()`` e ``pop()`` são operações que consomem tempo constante, 
ou seja  O(1). Isso significa que na primeira implementação
cada executação de ``push()`` e ``pop()`` consome tempo constante,
independentemente do número de itens na pilha.
Na segunda implementação, o consumo de tempo de ``push()`` e ``pop()`` é
proporcional ao número n de itens na pilha já que 
as operações ``insert(0)`` e ``pop(0)`` requererem tempo O(n).
Claramente, mesmo que as implementações sejam logicamente
equivalentes, tenham o mesmo comportamento, elas apresentarão desempenhos
diferentes ao serem executadas.

.. admonition:: Teste a sua compreensão

   .. mchoice:: stack_1
      :answer_a: 'x'
      :answer_b: 'y'
      :answer_c: 'z'
      :answer_d: A pilha está vazia
      :correct: c
      :feedback_a: Lembre que uma pilha é montada da base para o topo.
      :feedback_b: Lembre que uma pilha é montada da base para o topo.
      :feedback_c: Bom trabalho.
      :feedback_d: Lembre que uma pilha é montada da base para o topo.

      Ao final da seguinte sequência de operações em uma pilha qual é o item no topo da pilha?
       
      .. code-block:: python
       
       m = Stack()
       m.push('x')
       m.push('y')
       m.pop()
       m.push('z')
       m.peek()

   .. mchoice:: stack_2
      :answer_a: 'x'
      :answer_b: a pilha está vazia
      :answer_c: ocorre um erro
      :answer_d: 'z'
      :correct: c
      :feedback_a: Você talvez queira verificar a documentação de ``isEmpty()``.
      :feedback_b: Há um número ímpar de itens na pilha, mas cada iteração do laço 2 itens são removidos.
      :feedback_c: Bom trabalho.
      :feedback_d: Você talvez queira verificar a documentação de ``isEmpty()``.

      Ao final da seguinte sequência de operações em uma pilha qual é o item no topo da pilha?

      .. code-block:: python
  
        m = Stack()
        m.push('x')
        m.push('y')
        m.push('z')
        while not m.isEmpty():
           m.pop()
           m.pop()

   Escreva uma função `revstring(mystr)` que usa uma pilha para inverter uma string.
 
   .. actex:: stack_stringrev
      :nocodelens:

      from test import testEqual
      from pythonds.basic.stack import Stack

      def revstring(mystr):
          # your code here

      testEqual(revstring('apple'),'elppa')
      testEqual(revstring('x'),'x')
      testEqual(revstring('1234567890'),'0987654321')


.. video:: stack1_video
    :controls:
    :thumb: ../_static/activecodethumb.png

    http://media.interactivepython.org/pythondsVideos/Stack1.mov
    http://media.interactivepython.org/pythondsVideos/Stack1.webm

