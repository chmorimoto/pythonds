..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.

Representação de Lista de Listas
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Em uma árvore representada por uma lista de listas, nós iremos começar
com a estrutura de dados 'list' do Python e escrever as funções definidas
anteriormente. Embora programar a interface como um conjunto de operações
em uma lista seja um pouquinho diferente de usar outros tipos de dados
abstratos que implementamos, ainda assim isso é interessante porque
listas nos fornecem uma estrutura de dados simples e recursiva com
a qual podemos trabalhar e examinar mais diretamente. Em uma árvore em
forma de lista de listas, iremos armazenar o valor do nó raiz como o
primeiro elemento da lista. O segundo elemento será uma lista em si,
a qual representa uma subárvore à esquerda. O terceiro elemento da lista
será outra lista que representa uma subárvore à direita. Para ilustrar
essa técnica de armazenamento, vamos olhar um exemplo. A 
:ref:`Figura 1 <fig_smalltree>` mostra uma árvore simples com sua
respectiva implementação em lista.

.. _fig_smalltree:

.. figure:: Figures/smalltree.png
   :align: center
           
   Figura 1: Uma Árvore Pequena

::

        myTree = ['a',   #raiz
              ['b',  #subarvore esquerda
               ['d', [], []],
               ['e', [], []] ],
              ['c',  #subarvore direita
               ['f', [], []],
               [] ]  
             ]           
                  

Note que podemos acessar subárvores da lista usando sua indexação padrão.
A raiz da árvore é ``myTree[0]``, a subárvore à esquerda da raiz é
``myTree[1]``, e a subárvore à direita é ``myTree[2]``.
O :ref:`ActiveCode 1<lst_treelist1>` ilustra a criação de uma
árvore simples usando uma lista. Uma vez que a árvore é construída, 
podemos acessar a raiz e as subárvores esquerda e direita. Uma propriedade
interessante dessa abordagem com lista de listas é que a estrutura de uma
lista que representa uma subárvore é relativa à estrutura que define a
árvore, isto é, a estrutura em si é recursiva! Uma subárvore que tem
uma raiz e duas listas vazias é uma folha. Outra características interessante
da abordagem lista de listas é que ela generaliza o conceito de árvore para
além de árvores binárias. Nesse caso, uma subárvore é apenas só mais uma lista.

.. _lst_treelist1:

.. activecode:: tree_list1
    :caption: Usando Índices para Acessar Subárvores

    myTree = ['a', ['b', ['d',[],[]], ['e',[],[]] ], ['c', ['f',[],[]], []] ]
    print(myTree)
    print('left subtree = ', myTree[1])
    print('root = ', myTree[0])
    print('right subtree = ', myTree[2])


Vamos formalizar essa definição de estrutura de dados em árvore fornecendo
algumas funções que irão tornar mais fácil o uso de listas como árvores.
Observe que nós não iremos definir uma classe para árvore binária. As
funcções que iremos escrever apenas nos ajudarão a manipular uma lista
convencional como se estivéssemos trabalhando com uma árvore.

::


    def ArvoreBinaria(r):
        return [r, [], []]    

A função ``ArvoreBinaria`` simplesmente constrói uma lista com um nó raiz
e duas sublistas vazias para os filhos. Para adicionar uma subárvore
esquerda à raiz da árvore, precisamos inserir uma nova lista na segunda
posição da lista raiz. No entanto, temos que ter cuidado. Se a lista
já tiver algum elemento na segunda posição, precisamos levar isso em
conta e seguir árvore abaixo para inserir esse filho esquerdo.
O :ref:`Código 1 <lst_linsleft>` mostra o código em Python para
inserir um filho esquerdo.


.. _lst_linsleft:

**Código 1**

::

    def insertLeft(root,newBranch):
        t = root.pop(1)
        if len(t) > 1:
            root.insert(1,[newBranch,t,[]])
        else:
            root.insert(1,[newBranch, [], []])
        return root

Observe que para inserir um filho esquerdo, primeiro temos que obter a
a lista (possivelmente vazia) que corresponde ao filho esquerdo. Só então
adicionamos o novo filho esquerdo, deixando o antigo filho esquerdo como
filho esquerdo do novo nó. Isso permite colocar um novo nó na
árvore em qualquer posição. O código para ``insertRight`` é similar
a ``insertLeft`` e pode ser visto em :ref:`Código 2 <lst_linsright>`.
        

.. _lst_linsright:

**Código 2**

::

    def insertRight(root,newBranch):
        t = root.pop(2)
        if len(t) > 1:
            root.insert(2,[newBranch,[],t])
        else:
            root.insert(2,[newBranch,[],[]])
        return root

Para fechar esse conjunto de funções para construção de árvores 
(veja :ref:`Código 3 <lst_treeacc>`), vamos escrever algumas 
funções de acesso para pegar e definir o valor da raiz, bem como 
para acessar as árvores direita e esquerda.
        
.. _lst_treeacc:

**Código 3**

::


    def getRootVal(root):
        return root[0]
    
    def setRootVal(root,newVal):
        root[0] = newVal
    
    def getLeftChild(root):
        return root[1]
    
    def getRightChild(root):
        return root[2]


O :ref:`ActiveCode 2 <lst_bintreetry>` contém exercícios
para as funções de árvores que mencionamos anteriormente.
Tente resolvê-los. Um dos exercícios pede para você
desenhar a estrutura de árvore resultante desse conjunto
de chamadas.

.. _lst_bintreetry:


.. activecode:: bin_tree
    :caption: Uma Sessão Python para Ilustrar Funções Básicas para Árvores

    def ArvoreBinaria(r):
        return [r, [], []]    

    def insertLeft(root,newBranch):
        t = root.pop(1)
        if len(t) > 1:
            root.insert(1,[newBranch,t,[]])
        else:
            root.insert(1,[newBranch, [], []])
        return root

    def insertRight(root,newBranch):
        t = root.pop(2)
        if len(t) > 1:
            root.insert(2,[newBranch,[],t])
        else:
            root.insert(2,[newBranch,[],[]])
        return root

    def getRootVal(root):
        return root[0]
    
    def setRootVal(root,newVal):
        root[0] = newVal
    
    def getLeftChild(root):
        return root[1]
    
    def getRightChild(root):
        return root[2]

    r = BinaryTree(3)
    insertLeft(r,4)
    insertLeft(r,5)
    insertRight(r,6)
    insertRight(r,7)
    l = getLeftChild(r)
    print(l)
    
    setRootVal(l,9)
    print(r)
    insertLeft(l,11)
    print(r)
    print(getRightChild(getRightChild(r)))
    

.. admonition:: Auto-Avaliação

   .. mchoice:: mctree_1
      :correct: c
      :answer_a: ['a', ['b', [], []], ['c', [], ['d', [], []]]]
      :answer_b: ['a', ['c', [], ['d', ['e', [], []], []]], ['b', [], []]]
      :answer_c: ['a', ['b', [], []], ['c', [], ['d', ['e', [], []], []]]]
      :answer_d: ['a', ['b', [], ['d', ['e', [], []], []]], ['c', [], []]]
      :feedback_a: Não exatamente, está faltando o nó 'e' na árvore.
      :feedback_b: Quase, mas se olhar com cuidado, você vai ver que os filhos esquerdo e direito da raiz estão trocados.
      :feedback_c: Muito bem.
      :feedback_d: Próximo, mas os nomes dos filhos esquerdo e direito foram trocados, junto com as estruturas subjacentes.

      Dado o seguinte código:

      .. sourcecode:: python
      
          x = ArvoreBinaria('a')
          insertLeft(x,'b')
          insertRight(x,'c')
          insertRight(getRightChild(x),'d')
          insertLeft(getRightChild(getRightChild(x)),'e')    

      Qual das respostas contém a representação correta da árvore?

   Escreva uma função ``buildTree`` que retorna uma árvore usando funções de lista de listas que se parece com esta:

   .. image:: Figures/tree_ex.png

   .. actex:: mctree_2

      from test import testEqual
      
      def buildTree():
          pass
          
      ttree = buildTree()
      testEqual(getRootVal(getRightChild(ttree)),'c')
      testEqual(getRootVal(getRightChild(getLeftChild(ttree))),'d')      
      testEqual(getRootVal(getRightChild(getRightChild(ttree))),'f')            
      
