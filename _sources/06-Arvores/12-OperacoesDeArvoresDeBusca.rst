..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Operações de Árvores de Busca
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Antes de entrarmos na implementação, vamos revisar a interface
fornecida pelo mapeamento ADT. Você irá notar que essa interface é
muito semelhante ao dicionário do Python.

-  ``Map()`` Cria um novo mapeamento vazio.

-  ``put(key,val)`` Adiciona um novo par chave-valor ao mapeamento.
   Se a chave já estiver no mapeamento, então substitua o valor
   antigo pelo novo valor.

-  ``get(key)`` Dada uma chave, retorna o valor armazenado no 
     mapeamento ou ``None``, caso contrário.

-  ``del`` Apaga o par chave-valor do mapeamento usando uma declaração
  da forma ``del map[key]``.

-  ``len()`` Retorna o número de pares chave-valor no mapeamento.

-  ``in`` Retorna ``True`` para uma declaração da forma ``key in map``, 
   se a chave em questão estiver no mapeamento.

