..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Varredura em Árvores
~~~~~~~~~~~~~~~~~~~~

Agora que já examinamos a funcionalidade básica da nossa estrutura
em árvore, chegou a hora de conhecermos mais alguns padrões de
uso para árvores. Esses padrões podem ser divididos em três formas 
com as quais podemos acessar os nós de uma árvore. Isso porque
existem três padrões comumente usados para visitar todos os nós
de uma árvore. A diferença entre esses padrões está na ordem em
que cada nó é visitado. Chamamos essa visita aos nós de "varredura".
As três formas de varredura que iremos estudar são chamadas de
**prefixa**, **infixa** e **posfixa**. Vamos começar definindo
mais cuidadosamente o que são esses padrões e, a partir daí,
estudar alguns exemplos em que esses padrões podem ser úteis.

prefixa
    Em uma varredura prefixa, nós visitamos primeiro o nó
    raiz e então, recursivamente, fazemos uma varredura
    prefixa na subárvore esquerda, seguida por uma
    varredura prefixa recursiva na subárvore direita.

infixa
    Em uma varredura infixa, começamos a fazer recursivamente
    uma varredura infixa na subárvore esquerda, depois
    visitamos o nó raiz e finalmente fazemos uma 
    varredura infixa recursiva na subárvore direita.

posfixa
    Em uma varredura posfixa, começamos a fazer recursivamente
    uma varredura posfixa nas subárvores esquerda e direita,
    e só depois visitamos o nó raiz.

Vamos ver alguns exemplos que ilustram o funcionamento de cada um
desses três tipos de varredura. Primeiro, vamos olhar para a 
varredura prefixa. Como exemplo de árvore para percorrer,
vamos pegar este próprio livro. Podemos tomar o livro em si
como a raiz da árvore e cada capítulo como filho dessa raiz.
Cada seção dentro de um capítulo é um filho desse capítulo,
cada subseção é um filho de uma seção, e assim por diante.
A :ref:`Figura 5 <fig_booktree>` mostra uma versão limitada
de um livro com apenas dois capítulos. Observe que o algoritmo
de varredura funciona para árvores com qualquer número de filhos,
mas vamos considerar apenas árvores binárias por enquanto.
    

.. _fig_booktree:

.. figure:: Figures/booktree.png
   :align: center
   :alt: image

   Figura 5: Representando um Livro como uma Árvore

Suponha que você queira ler este livro do começo ao fim. A varredura
prefixa segue exatamente essa ordem. Começando pela raiz da árvore
(o nó Livro), iremos realizar as instruções para a varredura prefixa.
Nós chamamos recursivamente ``preorder`` (prefixa) no filho esquerdo,
o Capítulo 1, nesse caso. Em seguida, chamamos novamente de modo
recursivo ``preorder`` no filho esquerdo para acessar a Seção 1.1.
Como a Seção 1.1 não possui filhos, não fazemos mais nenhuma chamada
recursiva. Quando terminamos com a Seção 1.1, subimos de volta na
árvore para o Capítulo 1. Nessa altura ainda resta visitar a subárvore
direita do Capítulo 1, que é a Seção 1.2. Como feito anteriormente,
nós visitamos então a subárvore esquerda, o que nos leva à Seção 1.2.1,
e depois visitamos o nó representando a Seção 1.2.2. Com a Seção 1.2
finalizada, retornamos para o Capítulo 1. Finalmente, retornamos para
o nó Livro e realizamos o mesmo procedimento para o Capítulo 2.

O código que descreve varredura em árvores é surpreendentemente
elegante, possivelmente porque as varreduras são escritas de forma
recursiva. O :ref:`Código 2 <lst_preorder1>` mostra o código em 
Python para uma varredura prefixa de uma árvore binária.

Você pode se perguntar qual seria a melhor maneira de escrever um
algoritmo como o da varredura prefixa. Ele deve ser uma função que
simplesmente usa uma árvore como estrutura de dados, ou um método
em si da estrutura de dados em árvore? O :ref:`Código 2 <lst_preorder1>`
mostra uma versão da varredura prefixa escrita como uma função
externa que recebe uma árvore binária como parâmetro.
A função externa é particularmente elegante porque nosso caso
base é simplesmente checar se a árvore existe. Se o parâmetro da
árvore for ``None``, então a função retorna sem realizar nenhuma ação.


.. _lst_preorder1:

**Código 2**

::

    def preorder(tree):
        if tree:
            print(tree.getRootVal())
            preorder(tree.getLeftChild())
            preorder(tree.getRightChild())  


Também podemos implementar ``preorder`` como um método da classe
``ArvoreBinaria``. O código para a implementação de ``preorder``
como um método interno é mostrado em :ref:`Código 3 <lst_preorder2>`.
Observe o que acontece quando nós mudamos o código de externo
para interno. Em geral, nós apenas substituímos ``tree``
por ``self``. Contudo, também precisamos modificar o caso base.
O método interno precisa checar se existem filhos esquerdo e direito
*antes* de fazer uma chamada recursiva com ``preorder``.


.. _lst_preorder2:

**Código 3**

::

    def preorder(self):
        print(self.key)
        if self.leftChild:
            self.leftChild.preorder()
        if self.rightChild:
            self.rightChild.preorder()


----------------------
Which of these two ways to implement ``preorder`` is best? The answer is
that implementing ``preorder`` as an external function is probably
better in this case. The reason is that you very rarely want to just
traverse the tree. In most cases you are going to want to accomplish
something else while using one of the basic traversal patterns. In fact,
we will see in the next example that the ``postorder`` traversal pattern
follows very closely with the code we wrote earlier to evaluate a parse
tree. Therefore we will write the rest of the traversals as external
functions.

The algorithm for the ``postorder`` traversal, shown in
:ref:`Listing 4 <lst_postorder1>`, is nearly identical to ``preorder`` except that
we move the call to print to the end of the function.

.. _lst_postorder1:

**Listing 4**

::

    def postorder(tree):
        if tree != None:
            postorder(tree.getLeftChild())
            postorder(tree.getRightChild())
            print(tree.getRootVal())



We have already seen a common use for the postorder traversal, namely
evaluating a parse tree. Look back at :ref:`Listing 1 <lst_eval>` again. What
we are doing is evaluating the left subtree, evaluating the right
subtree, and combining them in the root through the function call to an
operator. Assume that our binary tree is going to store only expression
tree data. Let’s rewrite the evaluation function, but model it even more
closely on the ``postorder`` code in :ref:`Listing 4 <lst_postorder1>` (see :ref:`Listing 5 <lst_postordereval>`).

.. _lst_postordereval:

**Listing 5**

::

    def postordereval(tree):
        opers = {'+':operator.add, '-':operator.sub, '*':operator.mul, '/':operator.truediv}
        res1 = None
        res2 = None
        if tree:
            res1 = postordereval(tree.getLeftChild())
            res2 = postordereval(tree.getRightChild())
            if res1 and res2:
                return opers[tree.getRootVal()](res1,res2)
            else:
                return tree.getRootVal()
                

.. highlight:: python
    :linenothreshold: 500

Notice that the form in :ref:`Listing 4 <lst_postorder1>` is the same as the form
in :ref:`Listing 5 <lst_postordereval>`, except that instead of printing the key at
the end of the function, we return it. This allows us to save the values
returned from the recursive calls in lines 6 and 7. We
then use these saved values along with the operator on line 9.

The final traversal we will look at in this section is the inorder
traversal. In the inorder traversal we visit the left subtree, followed
by the root, and finally the right subtree. :ref:`Listing 6 <lst_inorder1>` shows
our code for the inorder traversal. Notice that in all three of the
traversal functions we are simply changing the position of the ``print``
statement with respect to the two recursive function calls.

.. _lst_inorder1:

**Listing 6**

::


    def inorder(tree):
      if tree != None:
          inorder(tree.getLeftChild())
          print(tree.getRootVal())
          inorder(tree.getRightChild())


If we perform a simple inorder traversal of a parse tree we get our
original expression back, without any parentheses. Let’s modify the
basic inorder algorithm to allow us to recover the fully parenthesized
version of the expression. The only modifications we will make to the
basic template are as follows: print a left parenthesis *before* the
recursive call to the left subtree, and print a right parenthesis
*after* the recursive call to the right subtree. The modified code is
shown in :ref:`Listing 7 <lst_printexp>`.

.. _lst_printexp:

**Listing 7**

::

    def printexp(tree):
      sVal = ""
      if tree:
          sVal = '(' + printexp(tree.getLeftChild())
          sVal = sVal + str(tree.getRootVal())
          sVal = sVal + printexp(tree.getRightChild())+')'
      return sVal



Notice that the ``printexp`` function as we have implemented it puts
parentheses around each number. While not incorrect, the parentheses are
clearly not needed. In the exercises at the end of this chapter you are
asked to modify the ``printexp`` function to remove this set of parentheses.
