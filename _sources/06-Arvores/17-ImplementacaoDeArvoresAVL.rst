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
 
Vamos olhar para uma árvore ligeiramente mais complicada para ilustrar a
rotação à direita. O lado esquerdo da :ref:`Figura 4 <fig_rightrot1>` mostra
uma árvore inclinada à esquerda com um fator de balanceamento de 2 na raiz.
Para fazer uma rotação à direita, basicamente precisamos do seguinte:

-  Promover o filho esquerdo (C) à raiz da subárvore.

-  Mover a raiz antiga (E) para a posição de filho direito da nova raiz.

-  Se a nova raiz (C) já tiver um filho direito (D), então torne-o o
   filho esquerdo do novo filho direito (E). Observação: como a nova
   raiz (C) era o filho esquerdo de E, sabemos a essa altura que E
   não tem mais um filho esquerdo. Isso no permite adicionar um novo
   nó como filho esquerdo sem maiores problemas.

.. _fig_rightrot1:

.. figure:: Figures/rightrotate1.png
  :align: center

  Figura 4: Transformando uma Árvore Desbalanceada Usando Rotação à Direita

Agora que você já viu os tipos de rotação e tem uma ideia básica de como
uma rotação funciona, vamos olhar para o :ref:`Código 2 <lst_bothrotations>`,
que mostra a implementação tanto para rotações à esquerda quanto à direita.
Na linha 2, nós criamos uma variável temporária para guardar a nova raiz
da subárvore. Como dissemos antes, a nova raiz é o filho direito da raiz
anterior. Agora que uma referência para o filho direito foi armazenada
nessa variável temporária, nós podemos substituir o filho direito da
antiga raiz pelo filho esquerdo da nova.

O próximo passo é ajustar os ponteiros para os pais dos dois nós. Se
``newRoot`` tiver um filho esquerdo, então o novo pai do filho esquerdo
se torna a raiz antiga. O pai da nova raiz agora se torna o pai da 
raiz antiga. Se a raiz anterior era a raiz da árvore inteira, então
devemos fazer com que a raiz da árvore aponte para a nova raiz. Mas
se a raiz antiga era um filho esquerdo, então temos que fazer com que
o pai do filho esquerdo aponte para a nova raiz. Se a raiz antiga era
um filho direito, temos que fazer com que o pai do filho direito
aponte para a nova raiz (linhas 10-13). Finalmente, tornamos o pai
da raiz antiga agora pai da nova raiz. Isso pode ser muito para
você acompanhar, então sugerimos que você simule essa função olhando
para a :ref:`Figura 3 <fig_unbalsimple>`. O método ``rotateRight`` é
simétrico a ``rotateLeft``, então deixaremos o estudo de ``rotateRight``
ao seu encargo.

.. _lst_bothrotations:

**Código 2**

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

Finalmente, as linhas 16-17 requerem uma explicação. Nessas duas linhas,
nós atualizamos os fatores de balanceamento tando da antiga quanto da
nova raiz. Como todas as outras transformações envolvem apenas mover
subárvores inteiras, os fatores de balanceamento de todos os outros nós
não são afetados pela rotação. Mas como podemos atualizar os fatores de
balanceamento sem recalcular completamente as alturas das novas
subárvores? A seguinte derivação deve convencê-lo de que essas linhas
estão corretas.

.. _fig_bfderive:

.. figure:: Figures/bfderive.png
   :align: center

   Figura 5: Uma Rotação à Esquerda


A :ref:`Figura 5 <fig_bfderive>` mostra uma rotação à esquerda. B e D
são os nós pivotais e A, C e E são suas subárvores. Seja :mat:`h_x` a
altura de uma subárvore em particular enraizada no nó :math:`x`. Pela
definição, sabemos o seguinte:
   
.. math::

  newBal(B) = h_A - h_C \\
  oldBal(B) = h_A - h_D


Mas sabemos que a altura antiga de D também pode ser dada por
:math:`1 + max(h_C, hE)`, isto é, a altura de D é a altura máxima
entre seus dois filhos mais um. Lembre-se que :math:`h_C` e 
:math:`h_E` não mudaram. Então vamos substituir isso na segunda
equação, o que nos dá:

:math:`oldBal(B) = h_A - (1 + max(h_C, h_E))`

e então subtrair as duas equações. Os passos a seguir realizam a
subtração e usam álgebra para simplificar a equação para
:math:`newBal(B)`.
  
.. math::

   newBal(B) - oldBal(B) = h_A - h_C - (h_A - (1 + max(h_C,h_E))) \\
   newBal(B) - oldBal(B) = h_A - h_C - h_A + (1 + max(h_C,h_E)) \\
   newBal(B) - oldBal(B) = h_A  - h_A + 1 + max(h_C,h_E) - h_C  \\
   newBal(B) - oldBal(B) =  1 + max(h_C,h_E) - h_C 

Em seguida, iremos move :math:`oldBal(B)` para o lado direito da
equação e fazer uso do fato de que :math:`max(a,b)-c = max(a-c,b-c)`.

.. math::

   newBal(B) = oldBal(B) + 1 + max(h_C - h_C ,h_E - h_C) \\


Mas :math:`h_E - h_C` é o mesmo que :math:`-oldBal(D)`. Então podemos
usar outra identidade que diz que :math:`max(-a,-b) = -min(a,b)`.
Então podemos terminar nossa derivação de :math:`newBal(B)` com os
seguintes passos:
   
.. math::

   newBal(B) = oldBal(B) + 1 + max(0 , -oldBal(D)) \\
   newBal(B) = oldBal(B) + 1 - min(0 , oldBal(D)) \\

Agora temos todas as partes em termos que já conhecemos. Se lembrarmos que
B é ``rotRoot`` e D é ``newRoot``, então podemos ver que isso corresponde
exatamente à declaração na linha 16:

::

    rotRoot.balanceFactor = rotRoot.balanceFactor + 1 - min(0,newRoot.balanceFactor)

Uma derivação semelhante nos dá a equação para o nó D atualizado, bem como
os fatores de balanceamento depois de uma rotação à direita. Iremos deixar
isso como exercício para você.
    
Você pode estar pensando agora que terminamos. Sabemos como fazer nossas
rotações à esquerda e à direita, sabemos quando devemos realizá-las, mas
preste atenação antes na :ref:`Figura 6 <fig_hardrotate>`. Como o nó A
tem um fator de balanceamento de -2, deveríamos fazer uma rotação à
esquerda. Mas o que acontece se fizermos essa rotação em torno de A?

.. _fig_hardrotate:

.. figure:: Figures/hardunbalanced.png
   :align: center

   Figura 6: Uma Árvore Desbalanceada que é Mais Difícil de Balancear

A :ref:`Figura 7 <fig_badrotate>` mostra que após a rotação à esquerda 
nós ficamos agora desbalanceados de uma outra forma. Se fizermos uma
rotação à direita para corrigir a situação, voltamos à estaca zero.
   
.. _fig_badrotate:

.. figure:: Figures/badrotate.png
   :align: center

   Figura 7: Depois de uma Rotação à Esquerda a Árvore Fica Desbalanceada para o Outro Lado


Para corrigir esse problema, precisamos seguir as seguintes regras:

-  Se uma subárvore precisa de uma rotação à esquerda para ficar balanceada,
   primeiro devemos checar o fator de balanceamento do filho direito. Se o 
   filho direito estiver mais pesado à esquerda, então fazemos uma rotação à
   direita no filho direito, seguida pela rotação à esquerda original.

-  Se uma subárvore precisa de uma rotação à direita para ficar balanceada,
   primeiro devemos checar o fator de balanceamento do filho esquerdo. Se
   o filho esquerdo estiver mais pesado à direita, então fazemos uma rotação
   à esquerda no filho esquerdo, seguida pela rotação à direita original.

A :ref:`Figura 8 <fig_rotatelr>` mostra como essas regras resolvem o
dilema com o qual nos deparamos na :ref:`Figura 6 <fig_hardrotate>` e na
:ref:`Figura 7 <fig_badrotate>`. Começando por uma rotação à direita em 
torno do nó C coloca a árvore em uma posição em que a rotação à esquerda
em torno de A faz com que a subárvore inteira se torne balanceada.

.. _fig_rotatelr:

.. figure:: Figures/rotatelr.png
   :align: center

   Figura 8: Uma Rotação à Direita Seguida por uma Rotação à Esquerda


O código que implementa essas regras pode ser encontrado no método
``rebalance``, conforme mostrado no :ref:`Código 3 <lst_rebalance>`.
A regra 1 acima é implementada pelo ``if`` começando na linha 2.
A regra 2 é implementada pelo ``elif`` começando na linha 8.
   
.. _lst_rebalance:

**Código 3**

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

As :ref:`questões para discussão <tree_discss>` dão a você a oportunidade
de rebalancear uma árvore que requer uma rotação à esquerda seguida por
uma à direita. Além disso, elas também dão oportunidade a você para
rebalancear outras árvores um pouco mais complexas do que aquelas
mostradas na :ref:`Figura 8 <fig_rotatelr>`.

Ao mantermos a árvore balanceada o tempo todo, podemos garantir que o
método ``get`` irá rodar em tempo :mat:`O(log_2(n))`. Mas a questão é:
qual o custo do método ``put``? Vamos quebrar isso em operações feitas
por ``put``. Como um nó novo é inserido como uma folha, atualizando os
fatores de balanceamento de todos os pais irá requerer no máximo
:mat:`log_2(n)` operações, uma para cada nível da árvore. Se uma subárvore
estiver desbalanceada, no máximo duas rotações serão necessárias para 
tornar a árvore balanceada novamente. Mas como cada rotação custa
:mat:`O(1)`, o método ``put`` também terá tempo :math:`O(log_2(n))`.

Nesta altura nós já temos uma árvore AVL funcional, a não ser pela
capacidade de poder remover um nó. Nós iremos deixar a remoação do nó
e a subsequente atualização e rebalanceamento como um exercício para você.

