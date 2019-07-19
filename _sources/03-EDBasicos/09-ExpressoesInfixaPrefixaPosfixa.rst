..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Expressões Infixas, Prefixas and Posfixas
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Quando você escreve uma expressão aritmética como B \* C, a forma do
expressão fornece informações para que você possa interpretá-la
corretamente. Neste caso, sabemos que a variável B está sendo multiplicada
pela variável C já que o operador de multiplicação \* aparece entre
elas na expressão. Este tipo de notação é chamada de
**infixa** já que o operador é \* aparece entre os dois operandos sobre os
quais está atuando.

Considere outro exemplo de notação infixa, A + B \* C.
Os operadores + e \* ainda aparecem entre os operandos, mas há um problema.
Sobre quais operando eles estão atuando?
Primeiro aplicamos o + sobre A e B ou o \* sobre B e C?
A expressão parece ambígua.

De fato, você tem lido e escrito esses tipos de expressões
por um longo tempo e elas não lhe causam nenhum problema.
A razão para isto é que você sabe algo sobre os operadores + e \*.
Cada operador tem seu nível de **precedência**.
Operadores de maior precedência são aplicados antes de operadores de menor precedência.
A única coisa que pode mudar essa ordem é a presença de parênteses.
A ordem de precedência para operadores aritméticos coloca multiplicação e divisão antes
adição e subtração. Se dois operadores de precedência igual aparecem um após outro
é utilizada uma ordenação ou associatividade da *esquerda para a direita*.

Vamos interpretar a expressão problemática A + B \* C usando a suas
precedências. B e C são multiplicados primeiro, em seguida,
A é então adicionado ao resultado.
(A + B) \* C forçaria a adição de A e B ser feita
primeiro, antes da multiplicação.
Na expressão A + B + C, pela assiciatividade da precedência,
o + à esquerda + seria feito primeiro; adicionamos A a B e em seguida o resultado a C.

Embora tudo isso possa ser óbvio para você, lembre-se de que os computadores precisam
saber exatamente quais operadores executar e em que ordem.
Uma maneira de escrever uma expressão que garanta que não haverá confusão alguma
com respeito a ordem em que as operações são executadas é criar uma expressão
**totalmente parentizada**.
Este tipo de expressão usa um par de parênteses para cada operador.
Os parênteses ditam a ordem em que as operações são executadas; não há ambiguidade.
Também não há necessidade de lembrar de regras de precedência.

A expressão A + B \* C + D pode ser reescrita como ((A + (B \* C)) + D)
para mostrar que a multiplicação acontece primeiro,
seguida da adição mais à esquerda.
A + B + C + D pode ser escrito como (((A + B) + C) + D) já que
operações de adição são associadas da esquerda para a direita.

Existem dois outros formatos de expressão muito importantes que podem não parecer
óbvios para você no começo.
Considere a expressão infixa A + B.
O que acontecer se movemos o operador para antes dos dois operandos?
O resultado expressão seria + A B.
Da mesma forma, poderíamos mover o operador para o fim.
Nós obteríamos A B +.
Estas expressões parecem um pouco estranhos.

Estas mudanças na posição do operador em relação ao
operandos criam dois novos formatos de expressão, **prefixa** e **posfixa**.
A notação prefixa requer que todos os operadores precedam os dois operandos sobre os quais atuam.
A notação posfixa, por outro lado, requer que seus operadores venham depois dos
operandos correspondentes. Mais alguns exemplos
deve ajudar a tornar isso um pouco mais claro
(veja :ref:`Tabela 2 <tbl_example1>`).

A + B \* C seria escrito como + A \* B C no prefixo.
O operador multiplicação vem imediatamente antes dos operandos B e C,
denotando que \* tem precedência sobre +.
O operador de adição aparece então antes do e o resultado da multiplicação.

A expressão postfixa seria A B C \* +. Mais uma vez, a ordem de
operações são preservadas desde que o \* aparece imediatamente após o B e
o C, denotando que \* tem precedência, com + vindo depois.
Apesar os operadores terem sido movidos para  antes ou depois dos respectivos
operandos, a ordem dos operandos permaneceu exatamente igual.

.. _tbl_example1:

.. table:: **Tabela 2: Examplos de Infixa, Prefixa, and Posfixa**

    ============================ ======================= ========================
            **Expressão Infixa**   **Expressão Prefixa**    **Expressão Posfixa**
    ============================ ======================= ========================
                           A + B                  \+ A B                    A B +
                      A + B \* C             \+ A \* B C               A B C \* +
    ============================ ======================= ========================


Agora considere a expressão infixa (A + B) \* C. Lembre-se que neste
caso, a expressão infixa requer os parênteses para forçar a realização da
adição antes da multiplicação. No entanto, quando A + B foi escrito em
prefixo, o operador de adição foi simplesmente movido antes dos operandos,
+ A B. O resultado desta operação torna-se o primeiro operando para o
multiplicação. O operador de multiplicação é movido para frente de
toda a expressão, resultando em \* + A B C. Da mesma forma, no posfixa
A B + obriga a adição a ser realizada primeiro. A multiplicação pode ser aplicada a
esse resultado e o operando C. A expressão posfixa correspondente
é então A B + C \*.

Considere estas três expressões novamente (veja :ref:`Tabela 3 <tbl_parexample>`).
Algo muito importante aconteceu. Para onde os parênteses foram?
Por quê  não precisamos deles na prefixa e na posfixa?
A resposta é que não há mais ambiguidade sobre quais operandos os operadores atuam.
Somente a notação infixa requer os símbolos adicionais.
A ordem das operações em de expressões prefixas e posfixas é completamente
determinado pela posição do operador e nada mais.
De várias maneiras, isso faz infixa a notação menos desejável.

.. _tbl_parexample:

.. table:: **Tabela 3: Uma Expressão com Parênteses**

    ============================ ======================= ========================
            **Expressão Infixa**   **Expressão Prefixa**    **Expressão Posfixa**
    ============================ ======================= ========================
                    (A + B) \* C              \* + A B C               A B + C \*
    ============================ ======================= ========================


:ref:`Table 4 <tbl_example3>`
mostra alguns exemplos adicionais de expressões infixas e
as expressões prefixas e posfixas equivalentes. Certifique-se de que você
entende como elas são equivalentes em termos da ordem das
operações sendo executadas.

.. _tbl_example3:

.. table:: **Tabela 4: Mais Exemplos de Infixa, Prefixa e Posfixa**

    ============================ ======================= ========================
            **Expressão Infixa**   **Expressão Prefixa**    **Expressão Posfixa**
    ============================ ======================= ========================
                  A + B \* C + D        \+ \+ A \* B C D           A B C \* + D +
              (A + B) \* (C + D)          \* + A B + C D           A B + C D + \*
                 A \* B + C \* D        \+ \* A B \* C D          A B \* C D \* +
                   A + B + C + D          \+ + + A B C D            A B + C + D +
    ============================ ======================= ========================


Conversão de Expressões Infixas para Prefixas e Posfixas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Até agora, usamos métodos *ad hoc* para converter expressões infixas
para expressões prefixas e posfixas equivalentes. Como você pode
imaginar, existem maneiras algorítmicas que permitem
convertermos qualquer expressão de qualquer complexidade para uma expressão equivalente.

A primeira técnica que vamos considerar usa a noção de um
expressão entre parênteses que foi discutida anteriormente.
Lembre-se que A + B \* C pode ser escrita como (A + (B \* C)) para mostrar
explicitamente que a multiplicação tem precedência sobre a adição.
Em uma observação mais cuidadosa, no entanto, você pode
ver que cada par de parênteses também determina o
início e o fim de um par de operandos com o operador correspondente
no meio.

Observe o parêntese direito na subexpressão (B \* C) acima.
Se movermos o símbolo de multiplicação para a posição do parêntese a direita e removermos o
parêntese da esquerda, obtendo B C \*, teremos, de fato,
convertido a subexpressão para a notação posfixa.
Se o operador adição também for movido para a posição correspondente ao parêntese à direita
e o parêntese esquerdo correspondente foi removido, teremos a expressão posfixa completa
(veja :ref:`Figura 6 <fig_moveright>`).


.. _fig_moveright:

.. figure:: Figures/moveright.png
   :align: center

   Figure 6: Movendo Operadores para a Direita para a Expressão Posfixa

Se fizermos a mesma coisa, mas em vez de mover o símbolo para a posição
do parêntese direito, nós o movemos para a esquerda, obtemos a notação prefixa
(veja :ref:`Figura 7 <fig_moveleft>`). A posição do par parênteses é
na verdade, uma pista para a posição final do operador entre parênteses.

.. _fig_moveleft:

.. figure:: Figures/moveleft.png
   :align: center

   Figure 7: Movendo Operadores para a Esquerda para a Expressão Prefixa

Então, para converter uma expressão, não importa o quão complexa,
para a
notação de prefixa ou posfixa, considere a expressão totalmente parentizada equivalente.
Em seguida, mova o operador envolto pelos parênteses para a posição do
parêntese esquerdo ou direito, dependendo se você quer notação de prefixa ou posfixa.

Aqui está uma expressão mais complexa: (A + B) \* C - (D - E) \* (F + G).
:ref:`Figure 8 <fig_complexmove>` mostra a conversão para a notação posfixa e prefixa.

.. _fig_complexmove:

.. figure:: Figures/complexmove.png
   :align: center

   Figure 8: Convertendo uma Expressão Complexa para as Notações Prefixa and Posfixa

Conversão Genérica de Infixa para Posfixa
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Precisamos desenvolver um algoritmo para converter qualquer expressão infixa para uma
expressão posfixa equivalente.
Para fazer isso, vamos olhar mais de perto o processo de conversão.

Considere mais uma vez a expressão A + B \* C. Como mostrado acima,
A B C \* + é a posfixa equivalente. Já observamos que o
os operandos A, B e C permanecem em suas posições relativas.
São apenas o operadores que mudam de posição.
Vamos olhar novamente para os operadores na expressão infixada.
O primeiro operador que aparece da esquerda para a direita é +.
No entanto, na expressão posfixa, + está no final ja que o próximo
operador, \*, tem precedência sobre a adição.
A ordem dos operadores na expressão original é invertida na expressão posfixa resultante.

Enquanto processamos a expressão, os operadores precisam ser salvos em algum lugar
já que seus operandos correspondentes ainda não foram vistos.
Também a ordem desses operadores salvos pode precisar ser revertida devido à precedência.
Este é o caso da adição e da multiplicação do exemplo.
Como o operador de adição vem antes do operador de multiplicação e tem menor precedência,
ele precisa aparecer depois que o operador de multiplicação ser aplicado.
Devido a essa reversão de ordem, faz sentido considerar o uso de uma pilha para
manter os operadores até que sejam necessários.

E quanto a (A + B) \* C?
Lembre-se de que A B + C \* é a posfixa equivalente.
Novamente, examinando essa expressão infixada da esquerda para a direita,
nós vemos + primeiro.
Neste caso, quando vemos \*, + já foi colocado na expressão resultante porque tem
precedência sobre \* em virtude dos parênteses.
Agora podemos começar a ver como o algoritmo de conversão vai funcionar.
Quando vemos um parêntese à esquerda, vamos salvá-lo para denotar
que outro operador de alta precedência estará chegando.
Aquele operador terá que esperar até que o parêntese direito correspondente apareça
indicando sua posição (lembre-se da técnica para expressões totalmente parentizadas).
Quando o parêntese direito é aparece, o operador pode ser removido da pilha.

Enquanto examinamos a expressão infixa da esquerda para a direita,
usaremos uma pilha para manter os operadores.
Isso fornecerá a reversão que observamos no primeiro exemplo.
O topo da pilha terá sempre o operador mais recentemente salvo.
Sempre que vemos um novo operador, precisaremos
considerar como a precedência desse operador se compara com a precedência dos operadores
na pilha, caso haja algum.

Suponha que a expressão infixa é uma string de itens (*tokens*) delimitados por espaços.
Os itens operadores são \*, /, + e -. Temos ainda os itens abre e fecha parênteses, ( e ).
Os itens que representam os operandos são os caracteres A, B, C e assim por diante.
Os passos seguintes irão produzir um
string que representa a expressão posfixa equivalente.

#. Crie uma pilha vazia chamada ``opstack`` para manter os operadores.
   Cria uma lista vazia para a saída.

#. Converta a string infixa input para uma lista usando o método ``split()``.

#. Examine os itens da lista da esquerda para a direita.

   -  Se o item é um operador, coloque-o no final da lista da saída.

   -  Se o item é um abre parêntese, insira-o (``push()``) na pilha ``opstack``.

   -  Se o item é um fecha parênteses, remova ( ``pop()``) os itens de ``opstack`` até que
      o abre parêntese correspondente seja removido.
      Coloque cada operador removido no final da lista da saída.

   -  Se i item é um operador, \*, /, +, or -, insira-o na pilha 
      ``opstack``. Entretanto, remova antes os operadores que estão na pilha que têm
      precedência maior ou igual ao operador encontrado e coloque-os na final da lista da saída.

#. Quando a expressão tiver sido completamente examinada, verifique 
   ``opstack``. Qualquer operador que ainda está na pilha deve ser removido e
   colocado na lista da saída.

:ref:`Figure 9 <fig_intopost>`
mostra o algoritmo de conversão trabalhando sobre a expressão A \* B + C \* D.
Note que o primeiro \* é removido assim que o operador + é encontrado.
Também, + permanece na pilha quando o segundo \* ocorre, já que multiplicação tem precedência sobre adição. Ao final da expressão infixa removemos da pilha ambos operadores + colocando-os como
últimos opredaores da expressão posfixa.

.. _fig_intopost:

.. figure:: Figures/intopost.png
   :align: center

   Figure 9: Convertendo A \* B + C \* D para Notação Postfixa

Para implementar o algoritmo em Python, usaremos um dicionário
chamado ``prec`` para manter os valores de precedência dos operadores.
Este dicionário associará a cada operador um número inteiro que pode ser comparado
com a precedência de outros operadores (arbitrariamente usamos os inteiros 3, 2 e 1).
O parêntese esquerdo receberá o menor valor possível.
Desta forma, qualquer operador que é comparado com ele
terá maior precedência e será colocado em sobre ele na pilha.
A linha 15 define os operandos como qualquer letra maiúsculo ou dígito .
A função de conversão completa é mostrado em :ref:`ActiveCode 1 <lst_intopost>`.

.. _lst_intopost:

.. activecode:: intopost
   :caption: Converting Infix Expressions to Postfix Expressions
   :nocodelens:

   from pythonds.basic.stack import Stack

   def infixToPostfix(infixexpr):
       prec = {}
       prec["*"] = 3
       prec["/"] = 3
       prec["+"] = 2
       prec["-"] = 2
       prec["("] = 1
       opStack = Stack()
       postfixList = []
       tokenList = infixexpr.split()

       for token in tokenList:
           if token in "ABCDEFGHIJKLMNOPQRSTUVWXYZ" or token in "0123456789":
               postfixList.append(token)
           elif token == '(':
               opStack.push(token)
           elif token == ')':
               topToken = opStack.pop()
               while topToken != '(':
                   postfixList.append(topToken)
                   topToken = opStack.pop()
           else:
               while (not opStack.isEmpty()) and \
                  (prec[opStack.peek()] >= prec[token]):
                     postfixList.append(opStack.pop())
               opStack.push(token)

       while not opStack.isEmpty():
           postfixList.append(opStack.pop())
       return " ".join(postfixList)

   print(infixToPostfix("A * B + C * D"))
   print(infixToPostfix("( A + B ) * C - ( D - E ) * ( F + G )"))

--------------

Mais alguns exemplos de conversão no Python shell estão logo abaixo.

::

    >>> infixtopostfix("( A + B ) * ( C + D )")
    'A B + C D + *'
    >>> infixtopostfix("( A + B ) * C")
    'A B + C *'
    >>> infixtopostfix("A + B * C")
    'A B C * +'
    >>>

Postfix Evaluation
^^^^^^^^^^^^^^^^^^

As a final stack example, we will consider the evaluation of an
expression that is already in postfix notation. In this case, a stack is
again the data structure of choice. However, as you scan the postfix
expression, it is the operands that must wait, not the operators as in
the conversion algorithm above. Another way to think about the solution
is that whenever an operator is seen on the input, the two most recent
operands will be used in the evaluation.

To see this in more detail, consider the postfix expression
``4 5 6 * +``. As you scan the expression from left to right, you first
encounter the operands 4 and 5. At this point, you are still unsure what
to do with them until you see the next symbol. Placing each on the stack
ensures that they are available if an operator comes next.

In this case, the next symbol is another operand. So, as before, push it
and check the next symbol. Now we see an operator, \*. This means that
the two most recent operands need to be used in a multiplication
operation. By popping the stack twice, we can get the proper operands
and then perform the multiplication (in this case getting the result
30).

We can now handle this result by placing it back on the stack so that it
can be used as an operand for the later operators in the expression.
When the final operator is processed, there will be only one value left
on the stack. Pop and return it as the result of the expression.
:ref:`Figure 10 <fig_evalpost1>` shows the stack contents as this entire example
expression is being processed.

.. _fig_evalpost1:

.. figure:: Figures/evalpostfix1.png
   :align: center

   Figure 10: Stack Contents During Evaluation


:ref:`Figure 11 <fig_evalpost2>` shows a slightly more complex example, 7 8 + 3 2
+ /. There are two things to note in this example. First, the stack size
grows, shrinks, and then grows again as the subexpressions are
evaluated. Second, the division operation needs to be handled carefully.
Recall that the operands in the postfix expression are in their original
order since postfix changes only the placement of operators. When the
operands for the division are popped from the stack, they are reversed.
Since division is *not* a commutative operator, in other words
:math:`15/5` is not the same as :math:`5/15`, we must be sure that
the order of the operands is not switched.

.. _fig_evalpost2:

.. figure:: Figures/evalpostfix2.png
   :align: center

   Figure 11: A More Complex Example of Evaluation


Assume the postfix expression is a string of tokens delimited by spaces.
The operators are \*, /, +, and - and the operands are assumed to be
single-digit integer values. The output will be an integer result.

#. Create an empty stack called ``operandStack``.

#. Convert the string to a list by using the string method ``split``.

#. Scan the token list from left to right.

   -  If the token is an operand, convert it from a string to an integer
      and push the value onto the ``operandStack``.

   -  If the token is an operator, \*, /, +, or -, it will need two
      operands. Pop the ``operandStack`` twice. The first pop is the
      second operand and the second pop is the first operand. Perform
      the arithmetic operation. Push the result back on the
      ``operandStack``.

#. When the input expression has been completely processed, the result
   is on the stack. Pop the ``operandStack`` and return the value.

The complete function for the evaluation of postfix expressions is shown
in :ref:`ActiveCode 2 <lst_postfixeval>`. To assist with the arithmetic, a helper
function ``doMath`` is defined that will take two operands and an
operator and then perform the proper arithmetic operation.

.. _lst_postfixeval:

.. activecode:: postfixeval
   :caption: Postfix Evaluation
   :nocodelens:

   from pythonds.basic.stack import Stack

   def postfixEval(postfixExpr):
       operandStack = Stack()
       tokenList = postfixExpr.split()

       for token in tokenList:
           if token in "0123456789":
               operandStack.push(int(token))
           else:
               operand2 = operandStack.pop()
               operand1 = operandStack.pop()
               result = doMath(token,operand1,operand2)
               operandStack.push(result)
       return operandStack.pop()

   def doMath(op, op1, op2):
       if op == "*":
           return op1 * op2
       elif op == "/":
           return op1 / op2
       elif op == "+":
           return op1 + op2
       else:
           return op1 - op2

   print(postfixEval('7 8 + 3 2 + /'))

It is important to note that in both the postfix conversion and the
postfix evaluation programs we assumed that there were no errors in the
input expression. Using these programs as a starting point, you can
easily see how error detection and reporting can be included. We leave
this as an exercise at the end of the chapter.

.. admonition:: Self Check

   .. fillintheblank:: postfix1

      .. blank:: pfblank1
         :correct: \\b10\\s+3\\s+5\\s*\\*\\s*16\\s+4\\s*-\\s*/\\s*\\+
         :feedback1:  ('10.*3.*5.*16.*4', 'The numbers appear to be in the correct order check your operators')
         :feedback2: ('.*', 'Remember the numbers will be in the same order as the original equation')

         Without using the activecode infixToPostfix function, convert the following expression to postfix  ``10 + 3 * 5 / (16 - 4)``

   .. fillintheblank:: postfix2

      .. blank:: pfblank2
         :correct: \\b9\\b
         :feedback1: ('.*', "Remember to push each intermediate result back on the stack" )

         What is the result of evaluating the following: ``17 10 + 3 * 9 / ==``

   .. fillintheblank:: postfix3

      .. blank:: pfblank3
         :correct: 5\\s+3\\s+4\\s+2\\s*-\\s*\\^\\s*\\*
         :feedback1: ('.*', 'Hint: You only need to add one line to the function!!')

         Modify the infixToPostfix function so that it can convert the following expression:  ``5 * 3 ^ (4 - 2)``   Paste the answer here:


.. video:: video_Stack3
    :controls:
    :thumb: ../_static/activecodethumb.png

    http://media.interactivepython.org/pythondsVideos/Stack3.mov
    http://media.interactivepython.org/pythondsVideos/Stack3.webm
