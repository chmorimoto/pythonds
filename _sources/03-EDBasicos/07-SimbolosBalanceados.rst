..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Símbolos Balanceados 
~~~~~~~~~~~~~~~~~~~~

O problema dos parênteses balanceados mostrado anteriormente
é um caso particular de uma
situação mais geral que surge em muitas linguagens de programação.
O problema geral de balancear e aninhar tipos diferentes símbolos
de abertura e fechamento ocorrem com frequência. Por exemplo, em Python
os símbolos colchetes, ``[`` e ``]``, são usados para listas; chaves, ``{`` e ``}``, são usados para dicionários;
e parênteses, ``(`` e ``)``, são usados para tuplas e
expressões aritméticas. É possível misturar símbolos desde que
mantenham sua próprio relação de abertura e fechamento.
Strings de símbolos tais como

::

    { { ( [ ] [ ] ) } ( ) }

    [ [ { { ( ( ) ) } } ] ]

    [ ] [ ] [ ] ( ) { }

são devidamente balanceadas já que não só cada símbolo de abertura corresponde
a um símbolo de fechamento, mas também os tipos de símbolos correspondem.

Compare essas strings com as seguintes strings que não são balanceadas:

::

    ( [ ) ]

    ( ( ( ) ] ) )

    [ { ( ) ]


O verificador de parênteses da seção anterior pode ser facilmente
estendido para lidar com esses novos tipos de símbolos. Lembre-se de que cada
símbolo de abertura é simplesmente inserido (``push()``)
na pilha para aguardar o correspondente símbolo de fechamento
que deve aparecer mais tarde na sequência. Quando um
símbolo de fechamento aparece, a única diferença é que devemos verificar
se o símbolo de abertura que está no topo da tinha é do tipo apropriado.
Se os dois símbolos não casam, a string não está balanceada.
Mais uma vez, se a string inteira é examinada e nenhum símbolo é deixado na
pilha, a string está corretamente balanceada.


O programa em Python que implementa a ideia descrita é mostrado
em:ref:`ActiveCode 1 <lst_parcheck2>`.
A única mudança aparece na linha 16 onde nós chamamos uma função auxiliar,
``matches()``, para ajudar com a correspondência de símbolos.
Cada símbolo que é removido da pilha deve ser examinado para
nos assegurarmos que corresponde ao símbolo de fechamento atual.
Se ocorre uma incompatibilidade, a variável booleana ``balanced``
recebe o valor ``False``.


.. _lst_parcheck2:

.. activecode :: parcheck2
   :caption: Solução do Problema de Símbolos Balanceados
   :nocodelens:

   from pythonds.basic.stack import Stack
   
   def parChecker(symbolString):
       s = Stack()
       balanced = True
       index = 0
       while index < len(symbolString) and balanced:
           symbol = symbolString[index]
           if symbol in "([{":
               s.push(symbol)
           else:
               if s.isEmpty():
                   balanced = False
               else:
                   top = s.pop()
                   if not matches(top,symbol):
                          balanced = False
           index = index + 1
       if balanced and s.isEmpty():
           return True
       else:
           return False

   def matches(open,close):
       opens = "([{"
       closers = ")]}"
       return opens.index(open) == closers.index(close)
       

   print(parChecker('{{([][])}()}'))
   print(parChecker('[{()]'))

Estes dois exemplos mostram que pilhas (*stacks*) são estruturas de dados
muito importantes em ciência da computação para o processamento de expressões
usadas em linguagens de programação. Quase qualquer expressão que você pode
pensar tem algum tipo de símbolos aninhados que devem ser emparelhados de uma
maneira balanceada. Existem vários outros usos de pilhas em
problemas fundamentais em ciência da computação.
Continuaremos a explorá-los nas próximas seções.
