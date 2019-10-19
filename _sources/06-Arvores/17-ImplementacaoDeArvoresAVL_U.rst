..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Implementação de Árvores AVL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Agora que já demonstramos que manter uma árvore AVL balanceada significará
uma grande melhora de desempenho, vamos ver agora como incrementar o
procedimento de inserir uma nova chave na árvore. Como todas as chaves
novas são inseridas na árvore como folhas, e como sabemos que o fator de
balanceamento para uma nova folha é zero, não há novos requisitos para
esse nó que acabou de ser inserido. Mas uma vez que a nova folha é
adicionada, precisamos atualizar o fator de balanceamento do nó pai.
A maneira como esse nó folha afeta o fator de balanceamento do nó pai
depende da folha ser um filho esquerdo ou direito. Se o novo nó é um 
filho direito, o fator de balanceamento do pai será diminuído em um. Se
o novo nó for um filho esquerdo, então o fator de balanceamento do pai
será incrementado em um. Essa relação pode ser aplicada recursivamente
para o avô do novo nó, e possivelmente para cada ancestral até chegarmos
à raiz. Como esse é um procedimento recursivo, vamos examinar os dois
casos bases para atualizar os fatores de balanceamento:

- A chamada recursiva chegou à raiz da árvore.

- O fator de balanceamento do pai foi ajustado para zero. Você deve se
  convencer de que uma vez que uma subárvore tem fator de balanceamento
  igual a zero, então o balanceamento dos seus ancestrais não é alterado.

Iremos implementar a árvore AVL como uma subclasse de ``BinarySearchTree``.
Para começar, iremos sobrescrever o método ``_put`` e escrever um novo
método auxiliar ``updateBalance``. Esses métodos são mostrados no
:ref:`Código 1 <lst_updbal>`. Você irá notar que a definição de ``_put``
é exatamente a mesma de árvores de busca binária simples, exceto pelas
chamadas adicionais a ``updateBalance`` nas linhas 7 e 13.


**Código 1**

.. _lst_updbal:

.. code-block:: python
    
    def _put(self,key,val,currentNode):
    	if key < currentNode.key:
    	    if currentNode.hasLeftChild():
    		    self._put(key,val,currentNode.leftChild)
    	    else:
    		    currentNode.leftChild = TreeNode(key,val,parent=currentNode)
    		    self.updateBalance(currentNode.leftChild)
    	else:
    	    if currentNode.hasRightChild():
    		    self._put(key,val,currentNode.rightChild)
    	    else:
    		    currentNode.rightChild = TreeNode(key,val,parent=currentNode)
    		    self.updateBalance(currentNode.rightChild)		

    def updateBalance(self,node):
    	if node.balanceFactor > 1 or node.balanceFactor < -1:
    	    self.rebalance(node)    
    	    return
    	if node.parent != None:
    	    if node.isLeftChild():
    		    node.parent.balanceFactor += 1
    	    elif node.isRightChild():
    		    node.parent.balanceFactor -= 1

    	    if node.parent.balanceFactor != 0:
    		    self.updateBalance(node.parent)
    		    
    		    

O novo método ``updateBalance`` é onde a maior parte do trabalho é feita.
Ele implementa o procedimento recursivo que descrevemos anteriormente. O
método ``updateBalance`` primeiro checa para ver se o nó atual está 
desbalanceado o bastante para requerer um rebalanceamento (linha 16). Se
esse for o caso, então o rebalanceamento é feito e não é preciso 
atualizar o fator dos pais. Se o nó atual não requer rebalanceamento, 
então o fator de balanceamento do nó pai precisa ser ajustado. Se o 
fator de balanceamento do pai for diferente de zero, então o algoritmo
continua seu trabalho, subindo a árvore recursivamente em direção à
raiz por meio da chamada ``updateBalance`` feita no pai.

Quando o rebalanceamento da árvore é necessário, como isso é feito?
Um rebalanceamento eficiente é a chave para fazer com que árvores AVL
funcionem bem sem sacrifício de desempenho. Para fazer com que árvores
AVL voltem a ficar balanceadas, iremos realizar uma ou mais
**rotações** na árvore.
                    
Para entender o que é uma rotação, vamos ver um exemplo bem simples.
Considere a árvore na metade esquerda de :ref:`Figura 3 <fig_unbalsimple>`.
Essa árvore está desbalanceada, com um fator de balanceamento de -2.
Para balancear novamente essa árvore, precisamos realizar uma rotação
à esquerda na subárvore com raiz no nó A.

.. _fig_unbalsimple:

.. figure:: Figures/simpleunbalanced.png
   :align: center

   Figura 3: Transformando uma Árvore Desbalanceada Usando uma Rotação À Esquerda
   

Para fazer uma rotação à esquerda, basicamente precisamos do seguinte:

-  Promover o filho direito (B) à raiz da subárvore.

-  Mover a raiz antiga (A) para a posição de filho esquerdo da nova raiz.

-  Se a nova raiz (B) já tiver um filho esquerdo, então faça com que 
   ele se torne o filho direito do novo filho esquerdo (A). Observação:
   como a nova raiz (B) era o filho direito de A, sabemos a esta altura
   que A não tem mais um filho direito. Isso nos permite adicionar um
   novo nó como filho direito sem maiores problemas. 
   
Embora esse procedimento seja relativamente tranquilo na teoria, o código
necessita de cuidado redobrado, uma vez que precisamos mover os nós na
ordem certa para garantir que todas as propriedades de uma Árvore de 
Busca Binária sejam preservadas. Além disso, precisamos ter certeza
de que todos os ponteiros dos pais serão atualizados apropriadamente.
 
-----------------------------
Let's look at a slightly more complicated tree to illustrate the right
rotation. The left side of :ref:`Figure 4 <fig_rightrot1>` shows a tree that is
left-heavy and with a balance factor of 2 at the root. To perform a
right rotation we essentially do the following:

-  Promote the left child (C) to be the root of the subtree.

-  Move the old root (E) to be the right child of the new root.

-  If the new root(C) already had a right child (D) then make it the
   left child of the new right child (E). Note: Since the new root (C)
   was the left child of E, the left child of E is guaranteed to be
   empty at this point. This allows us to add a new node as the left
   child without any further consideration.

.. _fig_rightrot1:

.. figure:: Figures/rightrotate1.png
  :align: center

  Figure 4: Transforming an Unbalanced Tree Using a Right Rotation

Now that you have seen the rotations and have the basic idea of how a
rotation works let us look at the code. :ref:`Listing 2 <lst_bothrotations>` shows the
code for both the right and the left rotations. In line 2
we create a temporary variable to keep track of the new root of the
subtree. As we said before the new root is the right child of the
previous root. Now that a reference to the right child has been stored
in this temporary variable we replace the right child of the old root
with the left child of the new.

The next step is to adjust the parent pointers of the two nodes. If
``newRoot`` has a left child then the new parent of the left child
becomes the old root. The parent of the new root is set to the parent of
the old root. If the old root was the root of the entire tree then we
must set the root of the tree to point to this new root. Otherwise, if
the old root is a left child then we change the parent of the left child
to point to the new root; otherwise we change the parent of the right
child to point to the new root. (lines 10-13).
Finally we set the parent of the old root to be the new root. This is a
lot of complicated bookkeeping, so we encourage you to trace through
this function while looking at :ref:`Figure 3 <fig_unbalsimple>`. The
``rotateRight`` method is symmetrical to ``rotateLeft`` so we will leave
it to you to study the code for ``rotateRight``.

.. _lst_bothrotations:

**Listing 2**

.. code-block:: python

    def rotateLeft(self,rotRoot):
    	newRoot = rotRoot.rightChild
    	rotRoot.rightChild = newRoot.leftChild
    	if newRoot.leftChild != None:
    	    newRoot.leftChild.parent = rotRoot
    	newRoot.parent = rotRoot.parent
    	if rotRoot.isRoot():
    	    self.root = newRoot
    	else:
    	    if rotRoot.isLeftChild():
    		    rotRoot.parent.leftChild = newRoot
    	    else:
    	    	rotRoot.parent.rightChild = newRoot
    	newRoot.leftChild = rotRoot
    	rotRoot.parent = newRoot
    	rotRoot.balanceFactor = rotRoot.balanceFactor + 1 - min(newRoot.balanceFactor, 0)
    	newRoot.balanceFactor = newRoot.balanceFactor + 1 + max(rotRoot.balanceFactor, 0)
			      
			      
.. highlight:: python
  :linenothreshold: 500

Finally, lines 16-17 require some explanation. In
these two lines we update the balance factors of the old and the new
root. Since all the other moves are moving entire subtrees around the
balance factors of all other nodes are unaffected by the rotation. But
how can we update the balance factors without completely recalculating
the heights of the new subtrees? The following derivation should
convince you that these lines are correct.

.. _fig_bfderive:

.. figure:: Figures/bfderive.png
   :align: center

   Figure 5: A Left Rotation


:ref:`Figure 5 <fig_bfderive>` shows a left rotation. B and D are the pivotal
nodes and A, C, E are their subtrees. Let :math:`h_x` denote the
height of a particular subtree rooted at node :math:`x`. By definition
we know the following:

.. math::

  newBal(B) = h_A - h_C \\
  oldBal(B) = h_A - h_D


But we know that the old height of D can also be given by :math:`1 +
max(h_C,h_E)`, that is, the height of D is one more than the maximum
height of its two children. Remember that :math:`h_c` and
:math:`h_E` hav not changed. So, let us substitute that in to the
second equation, which gives us 

:math:`oldBal(B) = h_A - (1 + max(h_C,h_E))` 

and then subtract the two equations. The following steps
do the subtraction and use some algebra to simplify the equation for
:math:`newBal(B)`.

.. math::

   newBal(B) - oldBal(B) = h_A - h_C - (h_A - (1 + max(h_C,h_E))) \\
   newBal(B) - oldBal(B) = h_A - h_C - h_A + (1 + max(h_C,h_E)) \\
   newBal(B) - oldBal(B) = h_A  - h_A + 1 + max(h_C,h_E) - h_C  \\
   newBal(B) - oldBal(B) =  1 + max(h_C,h_E) - h_C 


Next we will move :math:`oldBal(B)` to the right hand side of the
equation and make use of the fact that
:math:`max(a,b)-c = max(a-c, b-c)`.

.. math::

   newBal(B) = oldBal(B) + 1 + max(h_C - h_C ,h_E - h_C) \\


But, :math:`h_E - h_C` is the same as :math:`-oldBal(D)`. So we can
use another identity that says :math:`max(-a,-b) = -min(a,b)`. So we
can finish our derivation of :math:`newBal(B)` with the following
steps:

.. math::

   newBal(B) = oldBal(B) + 1 + max(0 , -oldBal(D)) \\
   newBal(B) = oldBal(B) + 1 - min(0 , oldBal(D)) \\


Now we have all of the parts in terms that we readily know. If we
remember that B is ``rotRoot`` and D is ``newRoot`` then we can see this
corresponds exactly to the statement on line 16, or:

::

    rotRoot.balanceFactor = rotRoot.balanceFactor + 1 - min(0,newRoot.balanceFactor)

A similar derivation gives us the equation for the updated node D, as
well as the balance factors after a right rotation. We leave these as
exercises for you.

Now you might think that we are done. We know how to do our left and
right rotations, and we know when we should do a left or right rotation,
but take a look at :ref:`Figure 6 <fig_hardrotate>`. Since node A has a balance
factor of -2 we should do a left rotation. But, what happens when we do
the left rotation around A?

.. _fig_hardrotate:

.. figure:: Figures/hardunbalanced.png
   :align: center

   Figure 6: An Unbalanced Tree that is More Difficult to Balance


:ref:`Figure 7 <fig_badrotate>` shows us that after the left rotation we are now
out of balance the other way. If we do a right rotation to correct the
situation we are right back where we started.

.. _fig_badrotate:

.. figure:: Figures/badrotate.png
   :align: center

   Figure 7: After a Left Rotation the Tree is Out of Balance in the Other Direction


To correct this problem we must use the following set of rules:

-  If a subtree needs a left rotation to bring it into balance, first
   check the balance factor of the right child. If the right child is
   left heavy then do a right rotation on right child, followed by the
   original left rotation.

-  If a subtree needs a right rotation to bring it into balance, first
   check the balance factor of the left child. If the left child is
   right heavy then do a left rotation on the left child, followed by
   the original right rotation.

:ref:`Figure 8 <fig_rotatelr>` shows how these rules solve the dilemma we
encountered in :ref:`Figure 6 <fig_hardrotate>` and :ref:`Figure 7 <fig_badrotate>`. Starting
with a right rotation around node C puts the tree in a position where
the left rotation around A brings the entire subtree back into balance.

.. _fig_rotatelr:

.. figure:: Figures/rotatelr.png
   :align: center

   Figure 8: A Right Rotation Followed by a Left Rotation


The code that implements these rules can be found in our ``rebalance``
method, which is shown in :ref:`Listing 3 <lst_rebalance>`. Rule number 1 from
above is implemented by the ``if`` statement starting on line 2.
Rule number 2 is implemented by the ``elif`` statement starting on
line 8.

.. _lst_rebalance:

**Listing 3**

.. highlight:: python
  :linenothreshold: 5

::

    def rebalance(self,node):
      if node.balanceFactor < 0:
	     if node.rightChild.balanceFactor > 0:
	        self.rotateRight(node.rightChild)
	        self.rotateLeft(node)
	     else:
	        self.rotateLeft(node)
      elif node.balanceFactor > 0:
	     if node.leftChild.balanceFactor < 0:
	        self.rotateLeft(node.leftChild)
	        self.rotateRight(node)
	     else:
	        self.rotateRight(node)


.. highlight:: python
   :linenothreshold: 500

The :ref:`discussion questions <tree_discuss>` provide you the opportunity to rebalance a tree
that requires a left rotation followed by a right. In addition the
discussion questions provide you with the opportunity to rebalance some
trees that are a little more complex than the tree in
:ref:`Figure 8 <fig_rotatelr>`.

By keeping the tree in balance at all times, we can ensure that the
``get`` method will run in order :math:`O(log_2(n))` time. But the
question is at what cost to our ``put`` method? Let us break this down
into the operations performed by ``put``. Since a new node is inserted
as a leaf, updating the balance factors of all the parents will require
a maximum of :math:`log_2(n)` operations, one for each level of the
tree. If a subtree is found to be out of balance a maximum of two
rotations are required to bring the tree back into balance. But, each of
the rotations works in :math:`O(1)` time, so even our ``put``
operation remains :math:`O(log_2(n))`.

At this point we have implemented a functional AVL-Tree, unless you need
the ability to delete a node. We leave the deletion of the node and
subsequent updating and rebalancing as an exercise for you.

