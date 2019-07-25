..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


O que é uma Fila?
~~~~~~~~~~~~~~~~~

Uma **fila** (*queue*)  é uma coleção ordenada de itens em que a inserção de novos
itens acontece em uma extremidade, chamado de "fim" (*rear*), e a remoção de itens existente
ocorre no outro extremo, comumente chamado de "início" (*front*).
Um elemento é inserido no fim da fila  e faz o seu caminho em direção
ao início, esperando até aquele momento em que é o próximo elemento a ser
removido.

O item inserido mais recentemente na fila deve aguardar no final do
coleção. O item que está na coleção há mais tempo está mais próximo do início.
Este princípio de ordenação é às vezes chamado de **FIFO**,
**primeiro a entrar, primeiro a sair** (*first-in first-out*).
Também é conhecido como “primeiro a chegar, primeiro a ser servido” (*first-come first-serverd*).

O exemplo mais simples de uma fila é a fila típica que todos nós
participarmos de tempos em tempos. Nós esperamos em uma fila do cinema00000000000000000,
esperamos na fila do supermercado, e esperamos na fila da lanchonete
(para pegarmos uma bandeja da pilha de bandejas). Filas bem comportadas 
são muito restritivas em que elas têm apenas uma maneira de entrarmos e apenas uma maneira
de sairmos. Não é permitido furar a fila e sair antes de você ter
esperado o tempo necessário para chegar ao início.
:ref:`Figura 1 <fig_qubasicqueue>` mostra uma fila simples de objetos de dados Python.

.. _fig_qubasicqueue:

.. figure:: Figures/basicqueue.png
   :align: center

   Figure 1: Um fila de objetos de Python


iência da computação também tem exemplos comuns de filas.
Nosso laboratório tem 30 computadores em rede com uma única impressora.
Quando os alunos querem imprimir, suas tarefas de impressão "entram na fila" com todas as
outras tarefas de impressão que estão aguardando. A primeira tarefa é a próxima a
ser completada. Se a sua tarefa de impressão é a última na fila,
você deve esperar que todas as outras tarefas que chegaram antes sejam
impressas antes que a sua possa ser impressa.
Vamos explorar este exemplo interessante em mais detalhes depois.

Além de filas de impressão, os sistemas operacionais usam várias
filas diferentes para controlar processos dentro de um computador.
O escalonamento (*scheduling*) da tarefa que será feita em seguida é tipicamente baseado
em um algoritmo de enfileiramento que
tenta executar programas o mais rápido possível e atender a tantos usuários
quanto possível. Além disso, à medida que digitamos, às vezes, as
os caracteres das teclas pressionadas ficam à frente de
caracteres que aparecem na tela. Isto é devido ao computador estar fazendo
outro trabalho naquele momento. Os caracteres a serem exibidos estão sendo colocadas
em um *buffer* de fila, para que possam ser exibidos na tela na ordem correta.
