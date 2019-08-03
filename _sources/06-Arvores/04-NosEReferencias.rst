..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.

Nós e Referências
~~~~~~~~~~~~~~~~~

Nosso segundo método para representar uma árvore usa nós e referências. Neste
caso, iremos definir uma classe que possui atributos para o valor da raiz,
assim como as subárvores esquerda e direita. Como esta representação está mais
próxima do paradigma de programação orientada a objetos, iremos continuar a usá-la
pelo restante do capítulo.

Usando nós e referências, podemos pensar em uma árvore sendo estruturada como algo
mostrado na figura :ref:`Figura 2 <fig_treerec>`.

.. _fig_treerec:

.. figure:: Figures/treerecs.png
   :align: center
   :alt: image

   Figura 2: Uma Árvore Simples Usando a Abordagem de Nós e Referências

Iremos começar com uma simples definição de classe para a abordagem de nós e
referências, como mostrado no :ref:`Trecho 4 <lst_nar>`. O importante aqui 
nesta representação é lembrar que os atributos ``filhoEsquerdo`` e ``filhoDireito``
irão se tornar referências para outras instâncias da classe ``ArvoreBinaria``.
Por exemplo, quando inserimos um novo filho à esquerda da árvore, criamos
uma nova instância de ``ArvoreBinaria`` e modificamos ``self.filhoEsquerdo``
na raiz para referenciar essa nova árvore.

.. _lst_nar:

**Trecho 4**

::

    class ArvoreBinaria:
        def __init__(self,rootObj):
            self.key = rootObj
            self.filhoEsquerdo = None
            self.filhoDireito = None
        
Note que no :ref:`Trecho 4 <lst_nar>`, o construtor espera algum tipo de objeto
para ser armazenado na raiz. Assim como você pode guardar qualquer tipo de objeto
que você queira em uma lista, o objeto raiz de uma árvore pode ser uma referência
para qualquer tipo de objeto. Para os nossos primeiros exemplos, iremos armazenar
o nome do nó como valor da raiz. Usando nós e referências para representar
árvores como na :ref:`Figura 2 <fig_treerec>`, teríamos que criar seis instâncias
da classe ArvoreBinaria.

Agora vamos olhar para as funções que precisamos para poder criar uma árvore
além do nó raiz. Para adicionar um filho à esquerda, iremos criar um novo objeto
do tipo ArvoreBinaria e definir o ``filhoEsquerdo`` como a raiz que referencia
esse novo objeto. O código para ``insereEsquerda`` é mostrado no trecho
:ref:`Trecho 5 <lst_insl>`.

.. _lst_insl:

**Trecho 5**

.. highlight:: python
    :linenothreshold: 5

::

    def insereEsquerda(self, novoNo):
        if self.filhoEsquerdo == None:
            self.filhoEsquerdo = ArvoreBinaria(novoNo)
        else:  
            t = ArvoreBinaria(novoNo)
            t.filhoEsquerdo = self.filhoEsquerdo
            self.filhoEsquerdo = t
            
.. highlight:: python
    :linenothreshold: 500




#########################






We must consider two cases for insertion. The first case is
characterized by a node with no existing left child. When there is no
left child, simply add a node to the tree. The second case is
characterized by a node with an existing left child. In the second
case, we insert a node and push the existing child down one level in the
tree. The second case is handled by the ``else`` statement on line
4 of :ref:`Listing 5 <lst_insl>`.

The code for ``insertRight`` must consider a symmetric set of cases.
There will either be no right child, or we must insert the node between
the root and an existing right child. The insertion code is shown in
:ref:`Listing 6 <lst_insr>`.

.. _lst_insr:

**Listing 6**

::

    def insertRight(self,newNode):
        if self.rightChild == None:
            self.rightChild = BinaryTree(newNode)
        else:
            t = BinaryTree(newNode)
            t.rightChild = self.rightChild
            self.rightChild = t

To round out the definition for a simple binary tree data structure, we
will write accessor methods (see :ref:`Listing 7 <lst_naracc>`) for the left and right children, as well as
the root values.

.. _lst_naracc:

**Listing 7**

::

    def getRightChild(self):
        return self.rightChild

    def getLeftChild(self):
        return self.leftChild

    def setRootVal(self,obj):
        self.key = obj

    def getRootVal(self):
        return self.key
        

Now that we have all the pieces to create and manipulate a binary tree,
let’s use them to check on the structure a bit more. Let’s make a simple
tree with node a as the root, and add nodes b and c as children. :ref:`ActiveCode 1 <lst_comptest>` creates the tree and looks at the some of the
values stored in ``key``, ``left``, and ``right``. Notice that both the
left and right children of the root are themselves distinct instances of
the ``BinaryTree`` class. As we said in our original recursive
definition for a tree, this allows us to treat any child of a binary
tree as a binary tree itself.

.. _lst_comptest:



.. activecode:: bintree
    :caption: Exercising the Node and Reference Implementation


    class BinaryTree:
        def __init__(self,rootObj):
            self.key = rootObj
            self.leftChild = None
            self.rightChild = None

        def insertLeft(self,newNode):
            if self.leftChild == None:
                self.leftChild = BinaryTree(newNode)
            else:  
                t = BinaryTree(newNode)
                t.leftChild = self.leftChild
                self.leftChild = t

        def insertRight(self,newNode):
            if self.rightChild == None:
                self.rightChild = BinaryTree(newNode)
            else:
                t = BinaryTree(newNode)
                t.rightChild = self.rightChild
                self.rightChild = t


        def getRightChild(self):
            return self.rightChild

        def getLeftChild(self):
            return self.leftChild

        def setRootVal(self,obj):
            self.key = obj

        def getRootVal(self):
            return self.key                


    r = BinaryTree('a')
    print(r.getRootVal())
    print(r.getLeftChild())
    r.insertLeft('b')
    print(r.getLeftChild())
    print(r.getLeftChild().getRootVal())
    r.insertRight('c')
    print(r.getRightChild())
    print(r.getRightChild().getRootVal())
    r.getRightChild().setRootVal('hello')
    print(r.getRightChild().getRootVal())


.. admonition:: Self Check

   Write a function ``buildTree`` that returns a tree using the nodes and references implementation that looks like this:

   .. image:: Figures/tree_ex.png

   .. actex:: mctree_3

      from test import testEqual
      
      def buildTree():
          pass

      ttree = buildTree()

      testEqual(ttree.getRightChild().getRootVal(),'c')
      testEqual(ttree.getLeftChild().getRightChild().getRootVal(),'d')
      testEqual(ttree.getRightChild().getLeftChild().getRootVal(),'e')
