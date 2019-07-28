..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Tipo Abstrato de Dados Lista não Ordenada
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A estrutura de uma lista não ordenada, como descrita acima, é uma coleção
de itens em que cada item detém uma posição relativa em relação aos demais
Algumas operações possíveis sobre lista não ordenadas são dadas abaixo.

- ``List()`` cria uma nova lista que está vazia. Não precisa de parâmetros
   e retorna uma lista vazia.

- `` add(item)`` insere um item novo à lista. Precisa do item e
   não retorna nada. Supõe que o item ainda não está na lista.

- ``remove(item)`` remove um item da lista. Precisa do item e modifica a lista. Supõe que o item está presente na lista.

- ``search(item)`` procura o item na lista. Precisa do item e retorna um valor booleano (``bool``):  ``True`` se o item está na lista e ``False`` em caso contrário.

- ``isEmpty()`` verifica se a lista está vazia. Não precisa de parâmetros e retorna um valor booleano (``bool``):  ``True`` se a lista está vazia e ``False`` em caso contrário.

- ``size()`` retorna o número de itens na lista. Não precisa de parâmetros e retorna um inteiro (``int``).

- ``append(item)`` adiciona um novo item ao final da lista, tornando-o último item da coleção. Precisa do item e não retorna nada.
   Supõe que o item ainda não está na lista.

- ``index(item)`` retorna a posição do item na lista. Precisa o item e retorna o índice. Supõe que o item está na lista.

- ``insert(pos, item)`` adiciona um novo item à lista na posição pos. Precisa do item e não retorna nada. Supõe que o item ainda não está na lista e existem itens existentes suficientes para ter posição pos.

- ``pop()`` remove e retorna o último item da lista. Não precisa coisa alguma e retorna um item. Supõe que a lista tenha pelo menos um item.

- ``pop(pos)`` remove e retorna o item na posição pos. Precisa a posição e retorna o item. Supõe que o item está na lista.

