..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


O Tipo Abstrado de Dados Lista Ordenada
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Vamos agora considerar um tipo de lista conhecida como uma lista ordenada. Por
exemplo, se a lista de números inteiros mostrada acima fosse uma lista ordenada
(ordem crescente), então poderia ser escrita como 17, 26, 31, 54, 77 e 93.
Como 17 é o menor item, ocupa a primeira posição no
Lista. Da mesma forma, como 93 é o maior, ocupa a última posição.

A estrutura de uma lista ordenada é uma coleção de itens onde cada
item detém uma posição relativa que é baseada em algumas características
subjacentes aos itens. A ordenação é tipicamente ascendente
ou descendente e supondo que os itens da lista têm uma operação de comparação 
já  definida. Muitas das operações de lista ordenadas
são as mesmas da lista desordenada.

- ``OrderedList()`` cria uma nova lista ordenada que está vazia. Não precisa de parâmetros e retorna uma lista vazia.

- ``add(item)`` insere um novo item à lista, certificando-se de que a ordem é preservada. Precisa do item e não retorna nada. Supõe que o item ainda não está na lista.

- ``remove(item)`` remove o item da lista. Precisa do item e modifica a lista. Supõe que o item está na lista.

- ``search(item)`` procura o item na lista. Precisa do item e retorna um valor booleano (``bool``); ``True`` se o item está na lista e ``False`` em caso contrário..

- ``isEmpty()`` testa se a lista está vazia. Não precisa de parâmetros e retorna um valor booleano (``bool``); ``True`` se a lista está vazia e ``False`` em caso contrário.

- ``size()`` retorna o número de itens na lista. Não precisa de parâmetros e retorna um inteiro.

- ``index(item)`` retorna a posição do item na lista. Precisa do item e retorna um índice. Supõe que o item está na lista.

- ``pop()`` remove e retorna o último item da lista. Não precisa de parâmetros e retorna um item. Supõe que a lista tenha pelo menos um item.

- ``pop(pos)`` remove e retorna o item na posição pos. Precisa da posição e retorna o item. Supõe que a lista tem um item na posição dada.


