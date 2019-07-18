..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.

Vocabulário e Definições
------------------------

Agora que demos uma olhada em alguns exemplos de árvores, nós iremos definir
formalmente o que é uma árvore e seus componentes.

Nó
    Um nó é uma parte fundamental de uma árvore. Ele pode ter um nome, algo
    que denominamos "chave". Um nó também pode conter informação adicional.
    Nós chamamos essa informação adicional de "carga". Embora a informação
    da carga não seja relevante para muitos algoritmos de árvores, ela
    costuma ser muito importante em aplicações que façam uso de árvores.

Aresta
    Uma aresta é outra parte fundamental de uma árvore. Uma aresta conecta
    dois nós para mostrar que há uma relação entre eles. Cada nó (exceto a raiz)
    recebe precisamente uma única aresta de entrada vinda de outro nó, mas
    cada nó pode ter várias arestas de saída.

Raiz
    A raiz de uma árvore é o único nó que não possui arestas de entrada.
    Na Figura :ref:`Figure 2 <fig_filetree>`, / é a raiz da árvore.

Caminho
    Um caminho é uma lista ordenada de nós que estão conectados por
    arestas. Por exemplo, 
    Mamífero :math:`\rightarrow` Carnivora :math:`\rightarrow` Felidae :math:`rightarrow` Felis :math:`\rightarrow` Domestica
    é um caminho.

Filhos
    Os nós de um conjunto :math:`c` que possuem arestas de entrada que vêm de
    um mesmo nó são ditos filhos desse nó. Na Figura :ref:`Figure 2 <fig_filetree>`,
    os nós log/, spool/ e yp/ são filhos do nó var/.

Pai
    Um nó é considerado pai de todos os nós com os quais se conecta por meio de suas
    arestas de saída. Na :ref:`Figure 2 <fig_filetree>`, o nó var/ é o pai dos nós
    log/, spool/ e yp/.






Sibling
    Nodes in the tree that are children of the same parent are said to
    be siblings. The nodes etc/ and usr/ are siblings in the filesystem
    tree.

Subtree
    A subtree is a set of nodes and edges comprised of a parent and all
    the descendants of that parent.

Leaf Node
    A leaf node is a node that has no children. For example, Human and
    Chimpanzee are leaf nodes in :ref:`Figure 1 <fig_biotree>`.

Level
    The level of a node :math:`n` is the number of edges on the path
    from the root node to :math:`n`. For example, the level of the
    Felis node in :ref:`Figure 1 <fig_biotree>` is five. By definition, the level
    of the root node is zero.

Height
    The height of a tree is equal to the maximum level of any node in
    the tree. The height of the tree in :ref:`Figure 2 <fig_filetree>` is two.

With the basic vocabulary now defined, we can move on to a formal
definition of a tree. In fact, we will provide two definitions of a
tree. One definition involves nodes and edges. The second definition,
which will prove to be very useful, is a recursive definition.

*Definition One:* A tree consists of a set of nodes and a set of
edges that connect pairs of nodes. A tree has the following properties:

-  One node of the tree is designated as the root node.

-  Every node :math:`n`, except the root node, is connected by an edge
   from exactly one other node :math:`p`, where :math:`p` is the
   parent of :math:`n`.

-  A unique path traverses from the root to each node.

-  If each node in the tree has a maximum of two children, we say that
   the tree is a **binary tree**.

:ref:`Figure 3 <fig_nodeedgetree>` illustrates a tree that fits definition one.
The arrowheads on the edges indicate the direction of the connection.

.. _fig_nodeedgetree:

.. figure:: Figures/treedef1.png
   :align: center
   :alt: image

   Figure 3: A Tree Consisting of a Set of Nodes and Edges

*Definition Two:* A tree is either empty or consists of a root and zero
or more subtrees, each of which is also a tree. The root of each subtree
is connected to the root of the parent tree by an edge.
:ref:`Figure 4 <fig_recursivetree>` illustrates this recursive definition of a tree.
Using the recursive definition of a tree, we know that the tree in
:ref:`Figure 4 <fig_recursivetree>` has at least four nodes, since each of the
triangles representing a subtree must have a root. It may have many more
nodes than that, but we do not know unless we look deeper into the tree.

.. _fig_recursivetree:

.. figure:: Figures/TreeDefRecursive.png
   :align: center
   :alt: image

   Figure 4: A recursive Definition of a tree
