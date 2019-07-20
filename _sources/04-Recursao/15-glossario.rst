..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Glossary

Glossário
---------

.. glossary::

    atribuição de tupla
        Uma atribuição a todos os elementos em uma tupla usando uma única atribuição. A atribuição de tuplas ocorre em paralelo, em vez de em sequência, tornando-o útil para trocar valores.

    caso base
        Um ramo do comando de seleção em uma função recursiva que terminam a recursão.

    chamada recursiva
        O comando que chama uma função já em execução. Recursão pode ser indireta --- a função `f` pode chamar` g`, que chama `h`, e `h` poderia fazer uma chamada de volta para` f`.

    definição recursiva
        Uma definição que define algo em termos de si mesmo. Para ser útil deve incluir *casos base* que não são recursivos. Desta forma, difere de uma *definição circular*. Definições recursivas frequentemente fornecem uma maneira elegante de expressar estruturas de dados complexas.

    estrutura de dados
        Uma organização de dados com o objetivo de facilitar seu uso.

    exceção
        Um erro que ocorre no tempo de execução.

    levantar uma exceção
        Para causar uma exceção usando a instrução ``raise``.

    recursão
        O processo de chamar a função que já está sendo executada.

    recursão infinita
        Uma função que se chama recursivamente sem nunca atingir o caso base.
        Eventualmente, uma recursão infinita causa um erro de execução.

    tipo de dado imutável
        Um tipo de dado que não pode ser modificado. Atribuições a elementos ou
        fatias de tipos imutáveis ​​causam um erro de execução.

    tipo de dado mutável
        Um tipo de dado que pode ser modificado. Todos os tipos mutáveis ​​são tipos compostos.
        Listas e dicionários (veja o próximo capítulo) são tipos de dado mutáveis;
        strings e tuplas não são.

    tratamento de exceção
        Para impedir que uma exceção encerre um programa envolvendo
        o bloco de código em uma construção ``try`` / ``except``.
    
    tupla
        Um tipo de dados que contém uma sequência de elementos de qualquer tipo, como um
        lista, mas é imutável. Tuplas podem ser usadas sempre que um tipo imutável
        é necessário, como uma chave em um dicionário (veja o próximo capítulo).

