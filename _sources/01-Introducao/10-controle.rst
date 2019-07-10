..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Control Structures

Estruturas de Controle
~~~~~~~~~~~~~~~~~~~~~~

..  As we noted earlier, algorithms require two important control
   structures: iteration and selection. Both of these are supported by
   Python in various forms. The programmer can choose the statement that is
   most useful for the given circumstance.

Como observamos anteriormente, algoritmos exigem duas importantes 
estruturas de controle: iteração e seleção. Ambas são suportadas pelo
Python em várias formas. O programador pode escolher o comando que 
lhe for mais útil dada uma circunstância.

..  For iteration, Python provides a standard ``while`` statement and a very
   powerful ``for`` statement. The while statement repeats a body of code
   as long as a condition is true. For example,

Para a iteração, o Python fornece um comando padrão ``while`` e um comando muito
poderoso ``for``. O comando while repete um corpo de código enquanto
uma condição for verdadeira. Por exemplo,

::

    >>> contador = 1
    >>> while contador <= 5:
    ...     print("Olá, mundo")
    ...     contador = contador + 1

    Olá, mundo
    Olá, mundo
    Olá, mundo
    Olá, mundo
    Olá, mundo

..  prints out the phrase “Hello, world” five times. The condition on the
   ``while`` statement is evaluated at the start of each repetition. If the
   condition is ``True``, the body of the statement will execute. It is
   easy to see the structure of a Python ``while`` statement due to the
   mandatory indentation pattern that the language enforces.

imprime a frase "Olá, mundo" cinco vezes. A condição no comando
``while`` é avaliada no início de cada repetição. Se o
condição é ``True`` (verdadeira), o corpo do comando será executado. 
É fácil ver a estrutura de um comando ``while`` do Python devido ao
padrão de tabulação obrigatório imposto pela linguagem.

..  The ``while`` statement is a very general purpose iterative structure
   that we will use in a number of different algorithms. In many cases, a
   compound condition will control the iteration. A fragment such as

O comando ``while`` é uma estrutura iterativa de propósito geral
que usaremos em vários algoritmos diferentes. Em muitos casos, uma
condição composta controlará a iteração. Um fragmento como

::

    while contador <= 10 and not acabou:
    ...

..  would cause the body of the statement to be executed only in the case
   where both parts of the condition are satisfied. The value of the
   variable ``contador`` would need to be less than or equal to 10 and the
   value of the variable ``acabou`` would need to be ``False`` (``not False``
   is ``True``) so that ``True and True`` results in ``True``.

faria com que o corpo da declaração fosse executado apenas no caso
onde ambas as partes da condição são satisfeitas. O valor da
variável ``contador`` precisaria ser menor ou igual a 10 e a variável
``acabou`` precisaria ser ``False`` (pois ``not False``
é ``True``) para que ``True and True`` resulte em ``True``.

..  Even though this type of construct is very useful in a wide variety of
   situations, another iterative structure, the ``for`` statement, can be
   used in conjunction with many of the Python collections. The ``for``
   statement can be used to iterate over the members of a collection, so
   long as the collection is a sequence. So, for example,

Mesmo que este tipo de construção seja muito útil em uma ampla variedade de
situações, outra estrutura iterativa, o comando ``for``, pode ser
usado em conjunto com muitas das coleções do Python. O  comando ``for``
pode ser usado para iterar sobre os membros de uma coleção,
desde que a coleção seja uma sequência. Então, por exemplo,

::

    >>> for item in [1,3,6,2,5]:
    ...    print(item)
    ...
    1
    3
    6
    2
    5

..  assigns the variable ``item`` to be each successive value in the list
   [1,3,6,2,5]. The body of the iteration is then executed. This works for
   any collection that is a sequence (lists, tuples, and strings).

atribui à variável ``item`` a cada valor sucessivo na lista
[1,3,6,2,5]. O corpo da iteração é então executado. Isso funciona para
qualquer coleção que seja uma sequência (listas, tuplas e strings).

..  A common use of the ``for`` statement is to implement definite iteration
   over a range of values. The statement

Um uso comum do comando ``for`` é implementar uma iteração definida
em um intervalo de valores. O comando

::

    >>> for item in range(5):
    ...    print(item**2)
    ...
    0
    1
    4
    9
    16
    >>>

..  will perform the ``print`` function five times. The ``range`` function
   will return a range object representing the sequence 0,1,2,3,4 and each
   value will be assigned to the variable ``item``. This value is then
   squared and printed.

executará a função ``print`` cinco vezes. A função ``range``
retornará um objeto de intervalo representando a sequência 0,1,2,3,4 e cada
valor será atribuído à variável ``item``. Este valor é então elevado ao
quadrado e impresso.

..  The other very useful version of this iteration structure is used to
   process each character of a string. The following code fragment iterates
   over a list of strings and for each string processes each character by
   appending it to a list. The result is a list of all the letters in all
   of the words.

A outra versão muito útil desta estrutura de iteração é usada para
processar cada caractere de uma string. O seguinte fragmento de código itera
sobre uma lista de strings e para cada string processa cada caractere, 
anexando-o no final de uma lista. O resultado é uma lista de todas as letras em todas
as palavras.

.. activecode:: intro_8
    :caption: Processando Cada Caractere em uma Lista de Strings

    lista_palavras = ['gato','rato','coelho']
    lista_letras = [ ]
    for palavra in lista_palavras:
        for letra in palavra:
            lista_letras.append(letra)
    print(lista_letras)


..  Selection statements allow programmers to ask questions and then, based
   on the result, perform different actions. Most programming languages
   provide two versions of this useful construct: the ``ifelse`` and the
   ``if``. A simple example of a binary selection uses the ``ifelse``
   statement.

Os comandos de seleção permitem que os programadores façam perguntas e, em seguida,
dependendo do resultado, execute ações diferentes. A maioria das linguagens de programação
fornecem duas versões desta construção útil: o ``ifelse`` (se-senão) e o
``if`` (se). Segue um exemplo simples de uma seleção binária usando o comando  ``ifelse``.

::

    if n<0:
       print("Desculpe, o valor é negativo")
    else:
       print(math.sqrt(n))

..  In this example, the object referred to by ``n`` is checked to see if it
   is less than zero. If it is, a message is printed stating that it is
   negative. If it is not, the statement performs the ``else`` clause and
   computes the square root.

Neste exemplo, o objeto referido por ``n`` é verificado para ver se
é menor que zero. Se for, uma mensagem é impressa informando que é
negativo. Se não for, a declaração executa a cláusula ``else`` e
calcula a raiz quadrada.

..  Selection constructs, as with any control construct, can be nested so
   that the result of one question helps decide whether to ask the next.
   For example, assume that ``score`` is a variable holding a reference to
   a score for a computer science test.

Construções de seleção, assim como em qualquer construção de controle, podem ser aninhadas
de forma que o resultado de uma pergunta ajuda a decidir o que perguntar em seguida.
Por exemplo, suponha que ``nota`` seja uma variável contendo uma referência a
uma pontuação para um teste de ciência da computação.

::

    if nota >= 90:
       print('A')
    else:
       if nota >=80:
          print('B')
       else:
          if nota >= 70:
             print('C')
          else:
             if nota >= 60:
                print('D')
             else:
                print('F')

..  This fragment will classify a value called ``score`` by printing the
   letter grade earned. If the score is greater than or equal to 90, the
   statement will print ``A``. If it is not (``else``), the next question
   is asked. If the score is greater than or equal to 80 then it must be
   between 80 and 89 since the answer to the first question was false. In
   this case print ``B`` is printed. You can see that the Python
   indentation pattern helps to make sense of the association between
   ``if`` and ``else`` without requiring any additional syntactic elements.

Este fragmento irá classificar um valor chamado ``nota`` imprimindo 
uma categoria correspondente de ``A`` a ``F``. 
Se a pontuação for maior ou igual a 90, o código 
irá imprimir ``A``. Senão (``else``), a próxima pergunta
é feita. Se a pontuação for maior ou igual a 80, então a nota deve estar
entre 80 e 89, uma vez que a resposta à primeira questão foi falsa.
Neste caso, a categoria ``B`` é impressa. Você pode ver que o padrão de
tabulação do Python ajuda a dar sentido à associação entre 
``if`` e ``else`` sem precisar de elementos sintáticos adicionais.

..  An alternative syntax for this type of nested selection uses the
   ``elif`` keyword. The ``else`` and the next ``if`` are combined so as to
   eliminate the need for additional nesting levels. Note that the final
   ``else`` is still necessary to provide the default case if all other
   conditions fail.

Uma sintaxe alternativa para esse tipo de seleção aninhada usa o
palavra-chave ``elif``. O ``else`` e o próximo ``if`` são combinados de modo
a eliminar a necessidade de níveis adicionais de aninhamento. Note que o
``else`` final ainda é necessário para fornecer o caso default se todas as outras
condições falharem.

::

    if nota >= 90:
       print('A')
    elif nota >=80:
       print('B')
    elif nota >= 70:
       print('C')
    elif nota >= 60:
       print('D')
    else:
       print('F')

..  Python also has a single way selection construct, the ``if`` statement.
   With this statement, if the condition is true, an action is performed.
   In the case where the condition is false, processing simply continues on
   to the next statement after the ``if``. For example, the following
   fragment will first check to see if the value of a variable ``n`` is
   negative. If it is, then it is modified by the absolute value function.
   Regardless, the next action is to compute the square root.

O Python também possui uma construção de seleção unária, o comando  ``if``.
Com esse comando, se a condição for verdadeira, uma ação será executada.
No caso da condição ser falsa, o processamento simplesmente continua
para a próxima instrução após o ``if``. Por exemplo, o seguinte
fragmento irá primeiro verificar se o valor de uma variável ``n`` é
negativo. Se for, então é modificado pela função de valor absoluto.
Independentemente disso, a próxima ação é calcular a raiz quadrada.

::

    if n<0:
        n = abs(n)
    print(math.sqrt(n))



.. admonition:: Auto avaliação

    Teste sua compreensão do que cobrimos até agora resolvendo o seguinte exercício. Modifique o código do Activecode 8 para que a lista final contenha apenas uma única cópia de cada letra.

    .. activecode:: self_check_1

       # a resposta é: ['g', 'a', 't', 'o', 'r', 'c', 'e', 'l', 'h']



.. video:: list_unique
   :controls:
   :thumb: ../_static/videothumb.png

   http://media.interactivepython.org/pythondsVideos/list_unique.mov
   http://media.interactivepython.org/pythondsVideos/list_unique.webm

..  Returning to lists, there is an alternative method for creating a list
   that uses iteration and selection constructs known as a **list
   comprehension**. A list comprehension allows you to easily create a list
   based on some processing or selection criteria. For example, if we would
   like to create a list of the first 10 perfect squares, we could use a
   ``for`` statement:

Voltando às listas, existe um método alternativo para criar uma lista
que usa construções de iteração e seleção conhecidas 
como **preenchimento de lista** (do inglês *list comprehension*). 
Uma construção para preenchimento de lista permite que você crie facilmente uma lista
com base em alguns critérios de processamento ou seleção. Por exemplo, se quiséssemos
criar uma lista dos primeiros 10 quadrados perfeitos, poderíamos usar um
comando ``for``:

::

    >>> quadrados=[]
    >>> for x in range(1,11):
             quadrados.append(x*x)

    >>> quadrados
    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
    >>>

..  Using a list comprehension, we can do this in one step as

Usando preenchimento de lista, podemos fazer isso em um passo apenas 

::

    >>> quadrados=[x*x for x in range(1,11)]
    >>> quadrados
    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
    >>>

..  The variable ``x`` takes on the values 1 through 10 as specified by the
   ``for`` construct. The value of ``x*x`` is then computed and added to
   the list that is being constructed. The general syntax for a list
   comprehension also allows a selection criteria to be added so that only
   certain items get added. For example,

A variável ``x`` assume os valores de 1 a 10, conforme especificado pelo comando
``for``. O valor de ``x * x`` é então computado e adicionado à
lista que está sendo construída. A sintaxe geral de um preenchimento de lista
também permite que um critério de seleção seja adicionado de forma que
somente certos itens sejam adicionados. Por exemplo,

::

    >>> quadrados=[x*x for x in range(1,11) if x%2 != 0]
    >>> quadrados
    [1, 9, 25, 49, 81]
    >>>

..  This list comprehension constructed a list that only contained the
   squares of the odd numbers in the range from 1 to 10. Any sequence that
   supports iteration can be used within a list comprehension to construct
   a new list.

Esse preenchimento de lista construiu uma lista que contém apenas
quadrados dos números ímpares no intervalo de 1 a 10. Qualquer sequência que
suporta iteração pode ser usada dentro de um preenchimento de lista para construir
uma nova lista.

::

    >>>[c.upper() for c in 'preenchimento' if c not in 'aeiou']
    ['P', 'R', 'N', 'C', 'H', 'M', 'N', 'T']
    >>>



.. admonition:: Auto Avaliação

    Teste sua compreensão sobre preenchimento de lista refazendo o Activecode 8 usando preenchimentos de lista. Para um desafio extra, veja se você consegue descobrir como remover as duplicatas.

    .. activecode:: self_check_2

       # the answer is: ['g', 'a', 't', 'o', 'r', 'a', 't', 'o', 'c', 'o', 'e', 'l', 'h', 'o']



.. video:: listcomp
   :controls:
   :thumb: ../_static/videothumb.png

   http://media.interactivepython.org/pythondsVideos/listcomp.mov
   http://media.interactivepython.org/pythondsVideos/listcomp.webm


