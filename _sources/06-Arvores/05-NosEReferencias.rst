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
nesta representação é lembrar que os atributos ``filhoEsquerda`` e ``filhoDireita``
irão se tornar referências para outras instâncias da classe ``ArvoreBinaria``.
Por exemplo, quando inserimos um novo filho à esquerda da árvore, criamos
uma nova instância de ``ArvoreBinaria`` e modificamos ``self.filhoEsquerda``
na raiz para referenciar essa nova árvore.

.. _lst_nar:

**Trecho 4**

::

    class ArvoreBinaria:
        def __init__(self,rootObj):
            self.key = rootObj
            self.filhoEsquerda = None
            self.filhoDireita = None
        
Note que no :ref:`Trecho 4 <lst_nar>`, o construtor espera algum tipo de objeto
para ser armazenado na raiz. Assim como você pode guardar qualquer tipo de objeto
que você queira em uma lista, o objeto raiz de uma árvore pode ser uma referência
para qualquer tipo de objeto. Para os nossos primeiros exemplos, iremos armazenar
o nome do nó como valor da raiz. Usando nós e referências para representar
árvores como na :ref:`Figura 2 <fig_treerec>`, teríamos que criar seis instâncias
da classe ArvoreBinaria.

Agora vamos olhar para as funções que precisamos para poder criar uma árvore
além do nó raiz. Para adicionar um filho à esquerda, iremos criar um novo objeto
do tipo ArvoreBinaria e definir o ``filhoEsquerda`` como a raiz que referencia
esse novo objeto. O código para ``insereEsquerda`` é mostrado no trecho
:ref:`Trecho 5 <lst_insl>`.

.. _lst_insl:

**Trecho 5**

.. highlight:: python
    :linenothreshold: 5

::

    def insereEsquerda(self, novoNo):
        if self.filhoEsquerda == None:
            self.filhoEsquerda = ArvoreBinaria(novoNo)
        else:  
            t = ArvoreBinaria(novoNo)
            t.filhoEsquerda = self.filhoEsquerda
            self.filhoEsquerda = t
            
.. highlight:: python
    :linenothreshold: 500

Devemos considerar dois casos para inserção. O primeiro caso ocorre quando
um nó não tem um filho à esquerda. Nesse caso, nós simplesmente adicionamos
um nó à arvore. O segundo caso ocorre quando um nó possui um filho
à esquerda. Nesse caso, inserimos um nó e empurramos o filho existente
um nível para baixo na árvore. O segundo caso é tratado pelo ``else``
na linha 4 do :ref:`Trecho 5 <lst_insl>`.

O código para ``insereDireita`` considera um conjunto de casos simétricos.
Dependendo do caso, se houver ou não um filho à direita, precisamos inserir
o nó entre a raiz e um filho existente à direita. O código de inserção
é mostrado no :ref:`Trecho 6 < lst_insr>`.

.. _lst_insr:

**Trecho 6**

::

    def insereDireita(self,novoNo):
        if self.filhoDireita == None:
            self.filhoDireita = BinaryTree(novoNo)
        else:
            t = BinaryTree(novoNo)
            t.filhoDireita = self.filhoDireita
            self.filhoDireita = t

Para completar a definição da estrutura de uma árvore binária simples, nós iremos
escrever métodos auxiliares (veja :ref:`Trecho 7 <lst_naracc>`) para os filhos
à esquerda e à direita, bem como para os valores da raiz.

.. _lst_naracc:

**Trecho 7**

::

    def pegueFilhoDireita(self):
        return self.filhoDireita

    def pegueFilhoEsquerda(self):
        return self.filhoEsquerda

    def definaValorRaiz(self,obj):
        self.key = obj

    def pegueValorRaiz(self):
        return self.key
        
Agora que já temos todas as peças para criar e manipular uma árvore binária,
vamos usá-las para estudar melhor sua estrutura. Vamos criar uma árvore
simples com o nó `a` como raiz e adicionar os nós `b` e `c` como filhos.
O :ref:`ActiveCode 1<lst_comptest>` cria a árvore e olha para alguns dos
valores armazenados em ``key``, ``esquerda`` e ``direita``. Note que 
tanto os filhos à esquerda quanto os filhos à direita da raiz são
eles próprios instâncias distintas da classe ``ArvoreBinaria``. Como
dissemos na nossa definição original recursiva de árvore, isso permite que 
a gente trate qualquer filho em uma árvore binária como uma outra
árvore binária.

.. _lst_comptest:



.. activecode:: bintree
    :caption: Exercitando Implementação de Nó e Referência


    class ArvoreBinaria:
        def __init__(self,rootObj):
            self.key = rootObj
            self.filhoEsquerda = None
            self.filhoDireita = None

        def insereEsquerda(self,novoNo):
            if self.filhoEsquerda == None:
                self.filhoEsquerda = ArvoreBinaria(novoNo)
            else:  
                t = ArvoreBinaria(novoNo)
                t.filhoEsquerda = self.filhoEsquerda
                self.filhoEsquerda = t

        def insereDireita(self,novoNo):
            if self.filhoDireita == None:
                self.filhoDireita = BinaryTree(novoNo)
            else:
                t = BinaryTree(novoNo)
                t.filhoDireita = self.filhoDireita
                self.filhoDireita = t

        def pegueFilhoDireita(self):
            return self.filhoDireita

        def pegueFilhoEsquerda(self):
            return self.filhoEsquerda

        def definaValorRaiz(self,obj):
            self.key = obj

        def pegueValorRaiz(self):
            return self.key

    
    r = ArvoreBinaria('a')
    print(r.pegueValorRaiz())
    print(r.pegueFilhoEsquerda())
    r.insereEsquerda('b')
    print(r.pegueFilhoEsquerda())
    print(r.pegueFilhoEsquerda().pegueValorRaiz())
    r.insereDireita('c')
    print(r.pegueFilhoDireita())
    print(r.pegueFilhoDireita().pegueValorRaiz())
    r.pegueFilhoDireita().definaValorRaiz('hello')
    print(r.pegueFilhoDireita().pegueValorRaiz())


.. admonition:: Auto-avaliação

   Escreva uma função ``constroiArvore`` que devolve uma árvore usando a implementação de nós e referências parecida com isso:

   .. image:: Figures/tree_ex.png

   .. actex:: mctree_3

      from test import testEqual
      
      def constroiArvore():
          pass

      arvtest = constroiArvore()

      testEqual(arvtest.pegueFilhoDireita().pegueValorRaiz(),'c')
      testEqual(arvtest.pegueFilhoEsquerda().pegueFilhoDireita().pegueValorRaiz(),'d')
      testEqual(arvtest.pegueFilhoDireita().pegueFilhoEsquerda().pegueValorRaiz(),'e')
