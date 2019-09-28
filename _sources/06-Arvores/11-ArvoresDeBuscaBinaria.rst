..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Árvores de Busca Binária
------------------------

Nós já vimos duas formas diferentes de acessar pares chave-valor em uma
coleção. Lembre-se de que essas coleções implementam o tipo de dado
abstrato chamado **mapeamento** (map). As duas implementações de um
mapeamento ADT que discutimos foram busca binária em uma lista e tabelas
de espalhamento ou hash. Nesta seção iremos estudar **árvores de busca binária**
como uma nova maneira de fazer o mapeamento de uma chave para um valor.
Neste caso, não estamos interessados na posição exata dos itens na árvore,
mas sim em utilizar a estrutura de dados da árvore binária para realizar
uma busca eficiente.
