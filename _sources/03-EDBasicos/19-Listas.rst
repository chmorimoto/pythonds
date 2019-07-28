..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Listas
------

Ao longo da discussão das estruturas básicas de dados, usamos as listas do Python
para implementar os tipos abstratos de dados apresentados. A lista (``list``) é uma
mecanismo de coleção de itens poderoso, porém simples, que fornece ao programador
com uma ampla variedade de operações. No entanto, nem toda linguagem de programação
incluem uma coleção de listas nativa. Nestes casos, a noção de
lista deve ser implementada pelo programador.

Uma **lista** é uma coleção de itens em que cada item tem uma 
posição relativa em relação aos outros.
Mais especificamente, nos referiremos este tipo de lista como uma lista não ordenada.
Podemos considerar que a lista possui um primeiro item,
um segundo item,
um terceiro item e assim por diante.
Nós também podemos no referirmos ao início da lista (o primeiro item) ou ao final da
lista (o último item). Por simplicidade, vamos supor que as listas não podem
conter itens duplicados.

Por exemplo, a coleção dos inteiros 54, 26, 93, 17, 77 e 31 pode
representar uma lista simples e não ordenada de pontuações de um exame.
Note que nós os escrevemos como valores delimitados por vírgula,
uma maneira comum de mostrar uma estrutura lista. Claro, o Python mostraria essa lista como
:math:'[54, 26, 93, 17, 77, 31]`.

