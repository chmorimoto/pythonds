..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Parênteses Balanceados
~~~~~~~~~~~~~~~~~~~~~~

Agora voltamos nossa atenção para o uso de pilhas para resolver verdadeiros
problemas de ciência da computação. Você certamente deve já deve ter escrito
expressões aritméticas, como

:math:`(5+6)*(7+8)/(4+3)`

onde parênteses são usados para determinar a ordem em que as operações são executadas. Você também pode ter tido alguma experiência de programação
em uma linguagem como Lisp e escrito construções como

::

    (defun square(n)
         (* n n))

Isto define uma função de nome ``square()`` que retornará o quadrado de
seu argumento ``n``. Lisp é notória por usar muitos e muitos
parênteses.

Em ambos os exemplos, os parênteses devem aparecer de maneira *balanceada*.
**Parênteses balanceados** significa que na expressão para cada abre
parêteses há um correspondente fecha parênteses e os pares de parênteses
estão aninhados. 
Considere as seguintes strings de
parênteses corretamente balanceadas:

::

    (()()()())

    (((())))

    (()((())()))

Compare essas strings com as seguintes, que não são balancedas:

::

    ((((((())

    ()))

    (()()(()

A capacidade de diferenciar entre sequências de parênteses corretamente
balanceadas daquelas que estão desbalanceadas é um componente importante no
reconhecimento estruturas em muitas linguagens de programação.

O desafio então é escrever um algoritmo que leia uma string de
parênteses da esquerda para a direita e decida se os parênteses
estão balanceados. Para resolver este problema, precisamos fazer uma observação
importante. Ao examinar da esquerda para a direita os símbolos na string,
cada fecha parênteses deve ser associado ao abre parênteses que foi examinado mais recentemente e ainda não foi associado a um fecha parênteses
(veja :ref:`Figura 4 <fig_parmatch>`).
Além disso, o primeiro abre parênteses examinado pode ter que
esperar até o último símbolo da string para encontrar o seu fecha parênteses.
Fecha parênteses são associados a abre parênteses na ordem inversa que foram examinados; eles são emparelhados de "dentro para fora".
Este é um indício de que pilhas podem ser usadas para resolver
problema.

.. _fig_parmatch:

.. figure:: Figures/simpleparcheck.png
   :align: center

   Figure 4: Emparelhamento de Parênteses

Uma vez que você concorda que uma pilha é a estrutura de dados apropriada para
mantermos os parênteses, a descrição do algoritmo é clara. Começando com uma
pilha vazia, processe os parênteses na string da esquerda para a direita.
Se um símbolo é um abre parênteses, insira-o (``push()``)
na pilha para indicar queo fecha parênteses correspondente precisa
aparecer mais tarde.
Se, por outro lado, um símbolo é um fecha parênteses, remova (``pop()``)
um abre da pilha. Contanto que seja possível realizarmos um ``pop()`` na
pilha para corresponder a cada fecha parênteses encontrado,
os parênteses estarão balanceados. Se em qualquer
momento não houver um abre parênteses na pilha para corresponder
a um fecha parênteses, a string não está balanceada. No final da
string, quando todos os símbolos tiverem sido processados, a pilha
deve estar vazia.
O código Python que implementa esse algoritmo é mostrado em
:ref:`ActiveCode 1 <lst_parcheck1>`.


.. _lst_parcheck1:

.. activecode:: parcheck1
    :caption: Solving the Balanced Parentheses Problem
    :nocodelens:

    from pythonds.basic.stack import Stack

    def parChecker(symbolString):
        s = Stack()
        balanced = True
        index = 0
        while index < len(symbolString) and balanced:
            symbol = symbolString[index]
            if symbol == "(":
                s.push(symbol)
            else:
                if s.isEmpty():
                    balanced = False
                else:
                    s.pop()

            index = index + 1

        if balanced and s.isEmpty():
            return True
        else:
            return False

    print(parChecker('((()))'))
    print(parChecker('(()'))


Esta função, ``parChecker()``, supõe que uma classe ``Stack`` esta
disponível e retorna um resultado booleano (``bool``)
após decidir se a string está ou não balanceada.
Note que a variável booleana ``balanced`` é
inicializado com ``True`` porque inicialmente
não há razão para supor o contrário.
Se o símbolo atual é ``(``, então ele é inserido na pilha
(linhas 9-10). Note também na linha 15 que ``pop()`` simplesmente remove
um símbolo da pilha. O valor retornado não é usado, pois sabemos que é
um abre parênteses visto anteriormente. No final (linhas 19 a 22),
desde que os fecha parenteses tenha encontrado os correspondentes abre
e a pilha tenha sido completamente limpa,
a string representa uma sequência de parênteses balanceada.

