..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Conversão de Decimal para Binário
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Em seu estudo da ciência da computação, você provavelmente já foi exposto de
uma forma ou de outra à idéia de um número binário.  Binário representação é
importante na ciência da computação, já que todos os valores armazenados em um
computador são essencialmente uma string de dígitos binários, uma string de 0s
e 1s. Sem a habilidade de converter valores da representação comu para a
binária e vice-versa, precisaríamos interagir com computadores de maneiras
muito estranhas.

Valores inteiros são objetos de dados comuns. Eles são usados em
computação o tempo todo. Nas aulas de
matemática do ensino fundamental aprendemos sobre eles e como
representá-los usando o sistema de numeração *decimal*, ou 
*base 10*. O número decimal :math:`233_ {10}` e seu correspondente
binário equivalente :math:`11101001_ {2}` são interpretados
respectivamente como

:math:`2\times10^{2} + 3\times10^{1} + 3\times10^{0}`

e

:math:`1\times2^{7} + 1\times2^{6} + 1\times2^{5} + 0\times2^{4} + 1\times2^{3} + 0\times2^{2} + 0\times2^{1} + 1\times2^{0}`

Mas como podemos facilmente converter valores inteiros da representação decimal para a binária? A
resposta é um algoritmo chamado de "Divisão por 2" ("*Divide by 2*"),
que usa uma pilha para manter os dígitos da representação binária.

O algoritmo *Divisão por 2" supõe que inicialmente temos um inteiro maior
de 0. Em cada iteração do algoritmo dividimos o número decimal
por 2 e mantemos o resto dessa divisão em uma pilha.
O valor do primeiro resto da divisão por 2 nos diz se o o valor é par ou ímpar.
Um valor par tem resto de 0.
Ele terá o dígito 0 na posição da unidade.
Um valor ímpar temresto de 1 e terá o dígito 1 na posição da unidade.
É ideia é construirmos nosso número binário como uma sequência de
dígitos; o primeiro resto que calculamos será realmente o último dígito
na sequência, o *menos significativo*.
Como mostrado em :ref:`Figure 5 <fig_decbin>`.
Nesse mecanismo vemos novamente a
propriedade de reversão que indica que uma pilha é provavelmente a
estrutura de dados apropriada para resolver o problema.

.. _fig_decbin:

.. figure:: Figures/dectobin.png
   :align: center

   Figure 5: Conversão de Decimal para Binário


O código Python em :ref:`ActiveCode 1 <lst_binconverter>`
implementa o algoritmo. A função ``divideBy2()`` recebe como
parâmetros um número decimal e repetidamente divide esse valor por 2.
Na linha 7 o operador nativo de *módulo* ``%`` é usado
para obter o resto da divisão e a linha 8, em seguida, insere-o
na pilha. Após o processo de divisão atingir 0, uma cadeia binária é
construído nas linhas 11-13. A linha 11 cria uma string vazia. Os 
dígitos binários são removidos da pilha um de cada vez e anexados ao
extremidade direita da string. A string binária é então retornada.

.. _lst_binconverter:

.. activecode:: divby2
   :caption: Conversão de Decimal para Binário
   :nocodelens:

   from pythonds.basic.stack import Stack
   
   def divideBy2(decNumber):
       remstack = Stack()

       while decNumber > 0:
           rem = decNumber % 2
           remstack.push(rem)
           decNumber = decNumber // 2

       binString = ""
       while not remstack.isEmpty():
           binString = binString + str(remstack.pop())

       return binString

   print(divideBy2(42))

O algoritmo para conversão binária pode ser facilmente estendido para executar
a conversão entre valores de qualquer base.
Em ciência da computação é comum usarmos representações diferentes.
As mais comuns são os binários (base 2),
octal (base 8) e hexadecimal (base 16).

O número decimal :math:`233` e a sua correspondentes representação :math:`351_ {8}` em octal e :math:`E9_ {16}` em hexadecimais são
interpretadas como

:math:`3\times8^{2} + 5\times8^{1} + 1\times8^{0}`

e

:math:`14\times16^{1} + 9\times16^{0}`

A função ``divideBy2()`` pode ser modificada para receber como parâmetro 
não apenas um valor decimal, mas também a base da conversão pretendida.
A ideia é simplesmente substituir o "dividir por 2" pela mais geral
"Dividir pela base".
Uma nova função chamada ``baseConverter()``, mostrada
em :ref:`ActiveCode 2 <lst_baseconverter>`,
converte um número decimal para sua representação em qualquer base
entre 2 e 16 como parâmetros.
Os restos das divisão são inseridos em uma pilha até o valor sendo
convertido seja 0.
A mesma técnica construção da string da esquerda para a direita
pode ser usada com uma pequena alteração. Nas representações na
base 2 até a base 10 os números usam no máximo 10 dígitos e 
0, 1, 2, 3, 4, 5, 6, 7, 8 e 9 funcionam bem.
O problema surge quando vamos além da base 10.
Nós não podemos mais simplesmente usar os restos das divisões,
como eles são eles próprios representados como números decimais
de dois dígitos. Em vez disso, precisamos
criar um conjunto de dígitos que podem ser usados para representar
esses maiores que 9.

.. _lst_baseconverter:

.. activecode:: baseconvert
    :caption: Conversão de Decimal para uma dada base
    :nocodelens:

    from pythonds.basic.stack import Stack
    
    def baseConverter(decNumber,base):
        digits = "0123456789ABCDEF"

        remstack = Stack()

        while decNumber > 0:
            rem = decNumber % base
            remstack.push(rem)
            decNumber = decNumber // base

        newString = ""
        while not remstack.isEmpty():
            newString = newString + digits[remstack.pop()]

        return newString

    print(baseConverter(25,2))
    print(baseConverter(25,16))

Uma solução para este problema é estender o conjunto de dígitos
para incluir alguns caracteres do alfabeto.
Por exemplo, hexadecimal usa as dez dígitos junto com as
seis primeiros letras do alfabeto para completar os 16 dígitos.
Para implementar isso, uma string de dígitos é criada (linha 4 em
:ref:`Listagem 6 <lst_baseconverter>`) que armazena os dígitos
em suas posições correspondentes: 0 está na posição 0,
1 está na posição 1, A está na posição 10,
B está na posição 11 e assim por diante.
Quando o valor de um resto é removido do pilha,
ele pode ser usado para indexar na seqüência de dígitos e o correspondente
dígito resultante pode ser anexado à resposta.
Por exemplo, se o resto 13 é removido da pilha, o dígito D é anexado a
string resultante.


.. admonition:: Self Check

   .. fillintheblank:: baseconvert1

      .. blank:: bcblank1
         :correct: \\b31\\b
         :feedback1: (".*", "Incorrect")
                     
         Qual é o valor de 25 na base octal

   .. fillintheblank:: baseconvert2

      .. blank:: bcblank2
         :correct: \\b100\\b

         Qual é o valor of 256 na base hexadecimal

   .. fillintheblank:: baseconvert3

      .. blank:: bcblank3
         :correct: \\b10\\b
         :feedback1: ('.*', 'You may need to modify the baseConverter function, or simply find a pattern in the conversion of bases.')

         Qual é o valor de 26 na base 26


.. video:: video_Stack2
    :controls:
    :thumb: ../_static/activecodethumb.png

    http://media.interactivepython.org/pythondsVideos/Stack2.mov
    http://media.interactivepython.org/pythondsVideos/Stack2.webm

