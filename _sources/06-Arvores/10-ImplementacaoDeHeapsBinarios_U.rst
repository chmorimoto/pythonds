..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementação de Heaps Binários
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 
A Propriedade da Estrutura
^^^^^^^^^^^^^^^^^^^^^^^^^^

Para fazer com que o nosso heap trabalhe de forma eficiente, vamos tirar
vantagem da natureza logarítmica da árvore binária para representar
nosso heap. Para garantir o desempenho logarítmico, temos que manter
nossa árvore balanceada. Uma árvore binária balanceada tem aproximadamente
o mesmo número de nós nas subárvores esquerda e direita da raiz. Na nossa
implementação de heap, mantemos a árvore balanceada ao criar uma
**árvore binária completa**. Esse tipo de árvore é aquela em que cada
nĩvel apresenta todos os nós. A exceção é o nível mais baixo da árvore,
no qual os nós vão sendo preenchidos da esquerda para direita.
A :ref:`Figura 1 <fig_comptree>` mostra um exemplo de uma árvore binária
completa.

.. _fig_comptree:

.. figure:: Figures/compTree.png
   :align: center
   :alt: image

   Figura 1: Uma Árvore Binária Completa

Uma outra propriedade interessante de uma árvore completa é que podemos
representá-la usando apenas uma lista. Não precisamos recorrer a nós
e referências, ou mesmo listas de listas. Como a árvore é completa, o
filho esquerdo de um nó pai (na posição :math:`p`) é o nó que se encontra
na posição :math:`2p` da lista. Da mesma forma, o filho direito desse
nó pai está na posição :math:`2p + 1` da lista. Para encontrar o pai 
de qualquer nó na árvore, simplesmente fazemos a divisão por inteiro
do Python. Dado que um nó está na posição :math:`n` da lista, o pai 
se encontra na posição :math:`n/2`. A :ref:`Figura 2 <fig_heapOrder>`
mostra uma árvore binária completa e também exibe a lista representando
essa árvore. Observe como :math:`2p` e :math:`2p+1` definem uma relação
entre pais e filhos. A representação em lista da árvore, junto com
a propriedade da estrutura completa, permite-nos varrer eficientemente
uma árvore binária completa utilizando apenas algumas simples
operações matemáticas. Veremos que isso também leva a uma implementação
eficiente do nosso heap binário.
   

A Propriedade Heap
^^^^^^^^^^^^^^^^^^

O método que iremos usar para armazenar itens em um heap depende de
mantermos o que chamamos de **propriedade heap**. Essa propriedade
subentende uma ordenação e pode ser expressa da seguinte forma:
Em um heap, para cada nó :math:`x` com pai :math:`p`, a chave em :math:`p`
é menor ou igual à chave em :math:`x`. A :ref:`Figura 2 <fig_heapOrder>`
também ilustra uma árvore binária completa que mantém a propriedade heap.

.. _fig_heapOrder:

.. figure:: Figures/heapOrder.png
   :align: center
   :alt: image

   Figura 2: Uma Árvore Binária Completa, Junto com sua Representação em Lista


Operações Heap
^^^^^^^^^^^^^^

Iremos começar nossa implementação de um heap binário com o construtor.
Como o heap inteiro pode ser representado por uma única lista, tudo o que
o construtor irá fazer é inicializar a lista e um atributo ``currentSize``
para armazenar o tamanho atual do heap. O :ref:`Código 1 <lst_heap1a>`
mostra o código em Python para o construtor. Você irá notar que um
heap binário vazio tem um único zero como o primeiro elemento da
``heapList`` e que esse zero não é utilizado, mas está lá para que
a divisão por inteiros seja possível em outros métodos.

.. _lst_heap1a:


**Código 1**

::
    
    class BinHeap:
        def __init__(self):
            self.heapList = [0]
            self.currentSize = 0

O próximo método que iremos implementar é o ``insert``. O jeito mais fácil e
eficiente de adicionar um item à lista é simplesmente juntar o item ao final
da lista. A notícia boa sobre juntar itens é que essa prática garante que
iremos manter a propriedade da árvore completa. A notícia ruim é que muito
provavelmente iremos violar a propriedade heap. Contudo, é possível escrever
um método que nos permitirá manter a propriedade heap ao comparar o novo
item com o seu pai. Se o novo elemento adicionado for menor que o seu pai,
então podemos trocá-lo com a posição do pai. A :ref:`Figura 2 <fig_percUp>`
mostra uma série de trocas necessárias para percolar o novo item até sua
posição correta na árvore.

.. _fig_percUp:

.. figure:: Figures/percUp.png
   :align: center
   :alt: image

   Figura 2: Percolação do Novo Nó até sua Posição Correta


   -----------------------
Notice that when we percolate an item up, we are restoring the heap
property between the newly added item and the parent. We are also
preserving the heap property for any siblings. Of course, if the newly
added item is very small, we may still need to swap it up another level.
In fact, we may need to keep swapping until we get to the top of the
tree. :ref:`Listing 2 <lst_heap2>` shows the ``percUp`` method, which
percolates a new item as far up in the tree as it needs to go to
maintain the heap property. Here is where our wasted element in
``heapList`` is important. Notice that we can compute the parent of any
node by using simple integer division. The parent of the current node
can be computed by dividing the index of the current node by 2.

We are now ready to write the ``insert`` method (see :ref:`Listing 3 <lst_heap3>`). Most of the work in the
``insert`` method is really done by ``percUp``. Once a new item is
appended to the tree, ``percUp`` takes over and positions the new item
properly.

.. _lst_heap2:

**Listing 2**

::

    def percUp(self,i):
        while i // 2 > 0:
          if self.heapList[i] < self.heapList[i // 2]:
             tmp = self.heapList[i // 2]
             self.heapList[i // 2] = self.heapList[i]
             self.heapList[i] = tmp
          i = i // 2


.. _lst_heap3:

**Listing 3**

::

    def insert(self,k):
        self.heapList.append(k)
        self.currentSize = self.currentSize + 1
        self.percUp(self.currentSize)
        
        

With the ``insert`` method properly defined, we can now look at the
``delMin`` method. Since the heap property requires that the root of the
tree be the smallest item in the tree, finding the minimum item is easy.
The hard part of ``delMin`` is restoring full compliance with the heap
structure and heap order properties after the root has been removed. We
can restore our heap in two steps. First, we will restore the root item
by taking the last item in the list and moving it to the root position.
Moving the last item maintains our heap structure property. However, we
have probably destroyed the heap order property of our binary heap.
Second, we will restore the heap order property by pushing the new root
node down the tree to its proper position. :ref:`Figure 3 <fig_percDown>` shows
the series of swaps needed to move the new root node to its proper
position in the heap.

.. _fig_percdown:

.. figure:: Figures/percDown.png
   :align: center
   :alt: image

   Figure 3: Percolating the Root Node down the Tree

In order to maintain the heap order property, all we need to do is swap
the root with its smallest child less than the root. After the initial
swap, we may repeat the swapping process with a node and its children
until the node is swapped into a position on the tree where it is
already less than both children. The code for percolating a node down
the tree is found in the ``percDown`` and ``minChild`` methods in
:ref:`Listing 4 <lst_heap4>`.

.. _lst_heap4:

**Listing 4**


::

    def percDown(self,i):
        while (i * 2) <= self.currentSize:
            mc = self.minChild(i)
            if self.heapList[i] > self.heapList[mc]:
                tmp = self.heapList[i]
                self.heapList[i] = self.heapList[mc]
                self.heapList[mc] = tmp
            i = mc

    def minChild(self,i):
        if i * 2 + 1 > self.currentSize:
            return i * 2
        else:
            if self.heapList[i*2] < self.heapList[i*2+1]:
                return i * 2
            else:
                return i * 2 + 1

The code for the ``delmin`` operation is in :ref:`Listing 5 <lst_heap5>`. Note
that once again the hard work is handled by a helper function, in this
case ``percDown``.

.. _lst_heap5:

**Listing 5**

::

    def delMin(self):
        retval = self.heapList[1]
        self.heapList[1] = self.heapList[self.currentSize]
        self.currentSize = self.currentSize - 1
        self.heapList.pop()
        self.percDown(1)
        return retval

To finish our discussion of binary heaps, we will look at a method to
build an entire heap from a list of keys. The first method you might
think of may be like the following. Given a list of keys, you could
easily build a heap by inserting each key one at a time. Since you are
starting with a list of one item, the list is sorted and you could use
binary search to find the right position to insert the next key at a
cost of approximately :math:`O(\log{n})` operations. However, remember
that inserting an item in the middle of the list may require
:math:`O(n)` operations to shift the rest of the list over to make
room for the new key. Therefore, to insert :math:`n` keys into the
heap would require a total of :math:`O(n \log{n})` operations.
However, if we start with an entire list then we can build the whole
heap in :math:`O(n)` operations. :ref:`Listing 6 <lst_heap6>` shows the code
to build the entire heap.

.. _lst_heap6:

**Listing 6**

::

    def buildHeap(self,alist):
        i = len(alist) // 2
        self.currentSize = len(alist)
        self.heapList = [0] + alist[:]
        while (i > 0):
            self.percDown(i)
            i = i - 1


.. _fig_buildheap:

.. figure:: Figures/buildheap.png
   :align: center
   :alt: image

   Figure 4: Building a Heap from the List [9, 6, 5, 2, 3]

:ref:`Figure 4 <fig_buildheap>` shows the swaps that the ``buildHeap`` method
makes as it moves the nodes in an initial tree of [9, 6, 5, 2, 3] into
their proper positions. Although we start out in the middle of the tree
and work our way back toward the root, the ``percDown`` method ensures
that the largest child is always moved down the tree. Because the heap is a
complete binary tree, any nodes past the halfway point will be leaves
and therefore have no children. Notice that when ``i=1``, we are
percolating down from the root of the tree, so this may require multiple
swaps. As you can see in the rightmost two trees of
:ref:`Figure 4 <fig_buildheap>`, first the 9 is moved out of the root position,
but after 9 is moved down one level in the tree, ``percDown`` ensures
that we check the next set of children farther down in the tree to
ensure that it is pushed as low as it can go. In this case it results in
a second swap with 3. Now that 9 has been moved to the lowest level of
the tree, no further swapping can be done. It is useful to compare the
list representation of this series of swaps as shown in
:ref:`Figure 4 <fig_buildheap>` with the tree representation.

::

          i = 2  [0, 9, 5, 6, 2, 3]
          i = 1  [0, 9, 2, 6, 5, 3]
          i = 0  [0, 2, 3, 6, 5, 9]
          

The complete binary heap implementation can be seen in ActiveCode 1.



.. activecode:: completeheap
   :caption: The Complete Binary Heap Example
   :hidecode:
   
   class BinHeap:
       def __init__(self):
           self.heapList = [0]
           self.currentSize = 0


       def percUp(self,i):
           while i // 2 > 0:
             if self.heapList[i] < self.heapList[i // 2]:
                tmp = self.heapList[i // 2]
                self.heapList[i // 2] = self.heapList[i]
                self.heapList[i] = tmp
             i = i // 2

       def insert(self,k):
         self.heapList.append(k)
         self.currentSize = self.currentSize + 1
         self.percUp(self.currentSize)

       def percDown(self,i):
         while (i * 2) <= self.currentSize:
             mc = self.minChild(i)
             if self.heapList[i] > self.heapList[mc]:
                 tmp = self.heapList[i]
                 self.heapList[i] = self.heapList[mc]
                 self.heapList[mc] = tmp
             i = mc

       def minChild(self,i):
         if i * 2 + 1 > self.currentSize:
             return i * 2
         else:
             if self.heapList[i*2] < self.heapList[i*2+1]:
                 return i * 2
             else:
                 return i * 2 + 1

       def delMin(self):
         retval = self.heapList[1]
         self.heapList[1] = self.heapList[self.currentSize]
         self.currentSize = self.currentSize - 1
         self.heapList.pop()
         self.percDown(1)
         return retval

       def buildHeap(self,alist):
         i = len(alist) // 2
         self.currentSize = len(alist)
         self.heapList = [0] + alist[:]
         while (i > 0):
             self.percDown(i)
             i = i - 1

   bh = BinHeap()
   bh.buildHeap([9,5,6,2,3])

   print(bh.delMin())
   print(bh.delMin())
   print(bh.delMin())
   print(bh.delMin())
   print(bh.delMin())
   
   
   

The assertion that we can build the heap in :math:`O(n)` may seem a
bit mysterious at first, and a proof is beyond the scope of this book.
However, the key to understanding that you can build the heap in
:math:`O(n)` is to remember that the :math:`\log{n}` factor is
derived from the height of the tree. For most of the work in
``buildHeap``, the tree is shorter than :math:`\log{n}`.

Using the fact that you can build a heap from a list in :math:`O(n)`
time, you will construct a sorting algorithm that uses a heap and sorts
a list in :math:`O(n\log{n}))` as an exercise at the end of this
chapter.
