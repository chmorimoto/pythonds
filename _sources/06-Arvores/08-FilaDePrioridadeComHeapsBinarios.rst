..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Fila de Prioridade com Heaps Binários
-------------------------------------
 
Em seções anteriores você aprendeu uma estrutura de dados conhecida como
fila em que o primeiro elemento a entrar é o primeiro a sair. Uma variação
importante de uma fila é uma **fila de prioridade**. Uma fila de prioridade
funciona como uma fila convencional, no sentido de que você remove o
elemento que está na frente. Contudo, numa fila de prioridade, a ordem lógica
de elementos dentro dela é determinada por sua prioridade. Os itens com
maior prioridade ficam armazenados na frente da fila os itens com menor
prioridade ficam atrás. Assim, quando você coloca um elemento em uma
fila de prioridade, esse novo item pode ser reposicionado até a frente.
Veremos que uma fila de prioridade é uma estrutura de dados útil para
alguns dos algoritmos em grafo que iremos estudar no próximo capítulo.

Você pode pensar em uma ou outra forma fácil de implementar uma fila de
prioridade usando algoritmos de ordenação e listas. No entanto, inserir
um elemento em uma lista é :mat:`O(n)` e ordenar uma lista custa
:math:`O(n \log[ n})`. Podemos fazer melhor. O jeito clássico de implementar
uma fila de prioridade é usando uma estrutura de dados conhecida como
**heap binário**. Um heap binário nos permitirá tanto colocar quanto
retirar elementos na fila em tempo :math:`O(\log[ n})`.

O heap binário é um tópico interessante de estudo porque quando fazemos
um diagrama de um heap notamos que ele se parece com uma árvore, mas
quando o implementamos, utilizamos apenas uma única lista como
representação interna. O heap binário geralmente tem duas variantes:
o **min heap**, no qual a chave de menor valor fica no topo, e o 
**max heap**, em que a chave de maior valor tem maior prioridade.
Nesta seção iremos implementar o min heap. Deixaremos a implementação
do max heap como exercício.
