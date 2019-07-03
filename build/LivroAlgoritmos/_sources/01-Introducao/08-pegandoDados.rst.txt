..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Getting Started with Data

Primeiros passos com dados
~~~~~~~~~~~~~~~~~~~~~~~~~~

..  We stated above that Python supports the object-oriented programming
    paradigm. This means that Python considers data to be the focal point of
    the problem-solving process. In Python, as well as in any other
    object-oriented programming language, we define a **class** to be a
    description of what the data look like (the state) and what the data can
    do (the behavior). Classes are analogous to abstract data types because
    a user of a class only sees the state and behavior of a data item. Data
    items are called **objects** in the object-oriented paradigm. An object
    is an instance of a class.

Nós afirmamos acima que o Python suporta o paradigma de programação orientada 
a objetos. Isso significa que o Python considera os dados como o ponto focal
do processo de resolução de problemas. Em Python, assim como em qualquer outra
linguagem de programação orientada a objetos, definimos uma **classe** para ser uma
descrição de como os dados se parecem (o estado) e o que os dados podem
fazer (o comportamento). As classes são análogas aos tipos de dados abstratos porque
um usuário de uma classe só vê o estado e o comportamento de um item de dados. 
Os itens de dados são chamados de **objetos** no paradigma orientado a objeto. Um objeto
é uma instância de uma classe.

Tipos de dados atômicos nativos
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..  We will begin our review by considering the atomic data types. Python
    has two main built-in numeric classes that implement the integer and
    floating point data types. These Python classes are called ``int`` and
    ``float``. The standard arithmetic operations, +, -, \*, /, and \*\*
    (exponentiation), can be used with parentheses forcing the order of
    operations away from normal operator precedence. Other very useful
    operations are the remainder (modulo) operator, %, and integer division,
    //. Note that when two integers are divided, the result is a floating
    point. The integer division operator returns the integer portion of the
    quotient by truncating any fractional part.

Vamos começar nossa revisão considerando os tipos de dados atômicos. O Python
tem duas classes numéricas nativas principais que implementam os tipos inteiro e
ponto flutuante. Essas classes do Python são chamadas de ``int`` e
``float``. As operações aritméticas padrão, +, -, \*, / e \*\*
(exponenciação), pode ser usado com parênteses forçando a ordem de
operações fora da precedência normal do operador. Outras operações muito 
úteis são o operador resto de divisão (módulo), %, e divisão inteira,
//. Note que quando dois inteiros são divididos, o resultado é um
ponto flutuante. O operador de divisão inteira retorna a porção inteira do
quociente truncando qualquer parte fracionária.

.. activecode:: intro_1
    :caption: Operadores aritméticos básicos

    print(2+3*4)
    print((2+3)*4)
    print(2**10)
    print(6/3)
    print(7/3)
    print(7//3)
    print(7%3)
    print(3/6)
    print(3//6)
    print(3%6)
    print(2**100)


..  The boolean data type, implemented as the Python ``bool`` class, will be
    quite useful for representing truth values. The possible state values
    for a boolean object are ``True`` and ``False`` with the standard
    boolean operators, ``and``, ``or``, and ``not``.

O tipo de dado booleano, implementado como a classe ``bool`` do Python, será
bastante útil para representar valores booleanos. Os possíveis valores de estado 
para um objeto booleano são ``True`` e ``False`` com os operadores booleanos, 
``and``, ``or`` e ``not``.

::

    >>> True
    True
    >>> False
    False
    >>> False or True
    True
    >>> not (False or True)
    False
    >>> True and True
    True

..  Boolean data objects are also used as results for comparison operators
    such as equality (==) and greater than (:math:`>`). In addition,
    relational operators and logical operators can be combined together to
    form complex logical questions. :ref:`Table 1 <tab_relational>` shows the relational
    and logical operators with examples shown in the session that follows.

Objetos de dados booleanos também são usados como resultado para operadores de comparação
como igualdade (==) e maior que (:math:`>`). Além disso, 
operadores relacionais e operadores lógicos podem ser combinados para
formar questões lógicas complexas. A :ref:`Tabela 1 <tab_relational>` mostra 
os operadores relacionais e lógicos com exemplos mostrados na seção a seguir.


.. _tab_relational:

.. table:: **Tabela 1: Operadores Relacionais e Lógicos**

    =========================== ============== ==========================================================
           **Nome do Operador**   **Operador**                                              **Descrição**
    =========================== ============== ==========================================================
                      menor que   :math:`<`                                            operador menor que
                      maior que   :math:`>`                                            operador maior que
             menor que ou igual   :math:`<=`                                operador menor que ou igual a
             maior que ou igual   :math:`>=`                                operador maior que or igual a
                          igual   :math:`==`                                           operador igualdade
                      não igual   :math:`!=`                                        operador desigualdade
                       e lógico   :math:`and`             Resulta em True quando ambos operandos são True
                      ou lógico   :math:`or`      Resulta em True quando ao menos um dos operandos é True
                     não lógico   :math:`not`      Nega o valor, False se torna True, True se torna False
    =========================== ============== ==========================================================



.. activecode:: intro_2
    :caption: Operadores Relacionais e Lógicos Básicos

    print(5==10)
    print(10 > 5)
    print((5 >= 1) and (5 <= 10))

..  Identifiers are used in programming languages as names. In Python,
    identifiers start with a letter or an underscore (_), are case
    sensitive, and can be of any length. Remember that it is always a good
    idea to use names that convey meaning so that your program code is
    easier to read and understand.

Identificadores são usados em linguagens de programação como nomes. Em Python,
identificadores começam com uma letra ou um sublinhado (_), são
sensíveis a letras minúsculas e maiúsculas, e podem ser de qualquer comprimento. 
Lembre-se que é sempre uma boa idéia usar nomes que transmitem significado para que o código 
de seu programa seja mais fácil de ler e entender.

..  A Python variable is created when a name is used for the first time on
    the left-hand side of an assignment statement. Assignment statements
    provide a way to associate a name with a value. The variable will hold a
    reference to a piece of data and not the data itself. Consider the
    following session:

Uma variável em Python é criada quando um nome é usado pela primeira vez
do lado esquerdo de um comando de atribuição. Comandos de atribuição
fornecem uma maneira de associar um nome a um valor. A variável manterá uma
referência a um pedaço dos dados e não os dados em si. Considere a
seguinte seção:

::

    >>> soma = 0
    >>> soma
    0
    >>> soma = soma + 1
    >>> soma
    1
    >>> soma = True
    >>> soma
    True

..  The assignment statement ``theSum = 0`` creates a variable called
    ``theSum`` and lets it hold the reference to the data object ``0`` (see
    :ref:`Figure 3 <fig_assignment1>`). In general, the right-hand side of the assignment
    statement is evaluated and a reference to the resulting data object is
    “assigned” to the name on the left-hand side. At this point in our
    example, the type of the variable is integer as that is the type of the
    data currently being referred to by ``theSum``. If the type of the data
    changes (see :ref:`Figure 4 <fig_assignment2>`), as shown above with the boolean
    value ``True``, so does the type of the variable (``theSum`` is now of
    the type boolean). The assignment statement changes the reference being
    held by the variable. This is a dynamic characteristic of Python. The
    same variable can refer to many different types of data.

O comando de atribuição ``soma = 0`` cria uma variável chamada
``soma`` e permite manter a referência ao objeto de dados ``0`` (veja
:ref:`Figura 3 <fig_assignment1>`). Em geral, o lado direito do comando
de atribuição é avaliado e uma referência ao objeto de dados resultante é
“atribuída” ao nome no lado esquerdo. Neste ponto em nosso
exemplo, o tipo da variável é inteiro por ser esse o tipo de
dado atualmente sendo referido por ``soma``. Se o tipo de dado for
modificado (veja :ref:`Figura 4 <fig_assignment2>`), como mostrado acima com o 
valor booleano ``True``, o mesmo acontece com o tipo da variável (``soma`` é agora 
do tipo booleano). O comando de atribuição altera a referência sendo
mantida pela variável. Essa é uma característica dinâmica do Python.
A mesma variável pode se referir a muitos tipos diferentes de dados.

.. _fig_assignment1:

.. figure:: Figures/assignment1.png
   :align: center

   Figure 3: Variáveis mantém referências a objetos de dados

.. _fig_assignment2:

.. figure:: Figures/assignment2.png
   :align: center

   Figure 4: Atribuição modifica a referência


..  Built-in Collection Data Types

Tipos Nativos de Dados Coletivos
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..  In addition to the numeric and boolean classes, Python has a number of
    very powerful built-in collection classes. Lists, strings, and tuples
    are ordered collections that are very similar in general structure but
    have specific differences that must be understood for them to be used
    properly. Sets and dictionaries are unordered collections.

Além das classes numéricas e booleanas, o Python possui várias
classes nativas muito poderosas para coleções. Listas (tipo `list`), 
strings (tipo `str`) e tuplas (tipo `tuple`) 
são coleções ordenadas que são muito semelhantes na estrutura geral, mas
tem diferenças específicas que devem ser entendidas para serem usadas
devidamente. Conjuntos (tipo `set`) e dicionários (tipo `dict`) 
são coleções não ordenadas.

..  A **list** is an ordered collection of zero or more references to Python
    data objects. Lists are written as comma-delimited values enclosed in
    square brackets. The empty list is simply ``[ ]``. Lists are
    heterogeneous, meaning that the data objects need not all be from the
    same class and the collection can be assigned to a variable as below.
    The following fragment shows a variety of Python data objects in a list.

Uma **lista** é uma coleção ordenada de zero ou mais referências a
objetos de dados em Python. As listas são escritas como valores separados por vírgulas e
delimitadas por colchetes. A lista vazia é simplesmente ``[]``. Listas são
heterogêneas, o que significa que os objetos de dados não precisam ser todos da
mesma classe e a coleção pode ser atribuída a uma variável como abaixo.
O fragmento a seguir mostra vários objetos de dados do Python em uma lista.

::

    >>> [1,3,True,6.5]
    [1, 3, True, 6.5]
    >>> minhaLista = [1,3,True,6.5]
    >>> minhaLista
    [1, 3, True, 6.5]

..  Note that when Python evaluates a list, the list itself is returned.
    However, in order to remember the list for later processing, its
    reference needs to be assigned to a variable.

Observe que, quando o Python avalia uma lista, a própria lista é retornada.
No entanto, para lembrar da lista para processamento posterior,
sua referência precisa ser atribuída a uma variável.

..  Since lists are considered to be sequentially ordered, they support a
    number of operations that can be applied to any Python sequence.
    :ref:`Table 2 <tab_sequence>` reviews these operations and the following session
    gives examples of their use.

Como as listas são consideradas sequencialmente ordenadas, elas suportam
um número de operações que podem ser aplicadas a qualquer sequência do Python.
:ref:`Tabela 2 <tab_sequence>` revisa essas operações e a seguinte seção
fornece exemplos de seu uso.

.. _tab_sequence:

.. table:: **Tabela 2: Operações sobre Qualquer Sequência em Python** 

    =========================== ============== ===========================================
           **Nome da Operação**   **Operador**                               **Descrição**
    =========================== ============== ===========================================
                      indexação            [ ]             Acessa um elemento da sequência
                   concatenação             \+                     Combina duas sequências
                      repetição             \*          Concatena um certo número de vezes
                    pertinência             in    responde se um item pertence à sequência
                    comprimento            len      fornece o número de itens da sequência
                     fatiamento          [ : ]               Extrai parte de uma sequência
    =========================== ============== ===========================================


..  Note that the indices for lists (sequences) start counting with 0. The
    slice operation, minhaLista[1:3], returns a list of items starting with the
    item indexed by 1 up to but not including the item indexed by 3.

Note que os índices das listas (sequências) começam a contar do 0. A 
operação de fatiamento, minhaLista[1:3], retorna uma lista de itens 
que começam com o
item indexado por 1 até, mas não incluindo o item indexado por 3.

..  Sometimes, you will want to initialize a list. This can quickly be
    accomplished by using repetition. For example,

Às vezes, você desejará inicializar uma lista. Isso pode ser
realizado rapidamente usando repetição. Por exemplo,

::

    >>> minhaLista = [0] * 6
    >>> minhaLista
    [0, 0, 0, 0, 0, 0]

..  One very important aside relating to the repetition operator is that the
    result is a repetition of references to the data objects in the
    sequence. This can best be seen by considering the following session:

Um lado muito importante relacionado ao operador de repetição é que o
resultado é uma repetição de referências aos objetos de dados na
sequência. Isso pode ser melhor visto considerando a seguinte seção:


.. activecode:: intro_3
    :caption: Repetição de Referências

    minhaLista = [1,2,3,4]
    A = [minhaLista]*3
    print(A)
    minhaLista[2]=45
    print(A)


..  The variable ``A`` holds a collection of three references to the
    original list called ``minhaLista``. Note that a change to one element of
    ``minhaLista`` shows up in all three occurrences in ``A``.

A variável ``A`` contém uma coleção de três referências à
lista original chamada ``minhaLista``. Observe que uma alteração em um elemento de
``minhaLista`` aparece em todas as três ocorrências em ``A``.

..  Lists support a number of methods that will be used to build data
    structures. :ref:`Table 3 <tab_listmethods>` provides a summary. Examples of their
    use follow.

As listas suportam vários métodos que serão usados para criar estruturas de 
dados. :ref:`Tabela 3 <tab_listmethods>` fornece um resumo. Exemplos de seus
use seguir.


.. _tab_listmethods:

.. table:: **Tabela 3: Métodos Proporcionados por Listas em Python**

    ======================== ========================== =======================================================
          **Nome do Método**         **Exemplo de Uso**                                           **Descrição**
    ======================== ========================== =======================================================
                  ``append``     ``alist.append(item)``             Adiciona um novo item ao final de uma lista
                  ``insert``   ``alist.insert(i,item)``          Insere um item na i-ésima posição de uma lista
                     ``pop``            ``alist.pop()``             Remove e retorna o último item de uma lista
                     ``pop``           ``alist.pop(i)``            Remove e retorna o i-ésimo item de uma lista
                    ``sort``           ``alist.sort()``                  Modifica uma lista para ficar ordenada
                 ``reverse``        ``alist.reverse()``        Modifica uma lista, invertendo a ordem dos itens
                ``del``           ``del alist[i]``                                   Exclui o item na posição i
                   ``index``      ``alist.index(item)``     Retorna o índice da primeira ocorrência de ``item``
                   ``count``      ``alist.count(item)``             Retorna o número de ocorrências de ``item``
                  ``remove``     ``alist.remove(item)``                Remove a primeira ocorrência de ``item``
    ======================== ========================== =======================================================


.. activecode:: intro_5
    :caption: Exemplos de Métodos de Lista

    minhaLista = [1024, 3, True, 6.5]
    minhaLista.append(False)
    print(minhaLista)
    minhaLista.insert(2,4.5)
    print(minhaLista)
    print(minhaLista.pop())
    print(minhaLista)
    print(minhaLista.pop(1))
    print(minhaLista)
    minhaLista.pop(2)
    print(minhaLista)
    minhaLista.sort()
    print(minhaLista)
    minhaLista.reverse()
    print(minhaLista)
    print(minhaLista.count(6.5))
    print(minhaLista.index(4.5))
    minhaLista.remove(6.5)
    print(minhaLista)
    del minhaLista[0]
    print(minhaLista)

..  You can see that some of the methods, such as ``pop``, return a value
    and also modify the list. Others, such as ``reverse``, simply modify the
    list with no return value. ``pop`` will default to the end of the list
    but can also remove and return a specific item. The index range starting
    from 0 is again used for these methods. You should also notice the
    familiar “dot” notation for asking an object to invoke a method.
    ``minhaLista.append(False)`` can be read as “ask the object ``minhaLista`` to
    perform its ``append`` method and send it the value ``False``.” Even
    simple data objects such as integers can invoke methods in this way.

Você pode ver que alguns dos métodos, como ``pop``, retornam um valor
e também modificam a lista. Outros, como ``reverse``, simplesmente modificam a
lista sem valor de retorno. ``pop`` por default remove e devolve o último item da lista
mas também pode remover e devolver um item específico. O intervalo de índices começando
de 0 é novamente usado por esses métodos. Você também deve notar a
notação familiar usando “ponto” para pedir a um objeto para invocar um método.
``minhaLista.append(False)`` pode ser lido como “pergunte ao objeto ``minhaLista`` para
executar seu método ``append`` passando-lhe o valor ``False``".
Mesmo objetos de dados simples, como inteiros, podem invocar métodos dessa maneira.

::

    >>> (54).__add__(21)
    75
    >>>

..  In this fragment we are asking the integer object ``54`` to execute its
    ``add`` method (called ``__add__`` in Python) and passing it ``21`` as
    the value to add. The result is the sum, ``75``. Of course, we usually
    write this as ``54+21``. We will say much more about these methods later
    in this section.

Neste fragmento estamos pedindo ao objeto inteiro ``54`` para executar seu
método ``add`` (chamado ``__add__`` em Python) e passando-lhe ``21`` como
valor a adicionar. O resultado é a soma, ``75``. Claro, nós geralmente
escrevemos isto como ``54 + 21``. Falaremos muito mais sobre esses métodos mais tarde
nesta seção.

..  One common Python function that is often discussed in conjunction with
    lists is the ``range`` function. ``range`` produces a range object that
    represents a sequence of values. By using the ``list`` function, it is
    possible to see the value of the range object as a list. This is
    illustrated below.

Uma função comum do Python que é frequentemente discutida em conjunto com
listas é a função ``range``. ``range`` produz um objeto de intervalo que
representa uma sequência de valores. Usando a função ``list``, é
possível ver o valor do objeto de intervalo como uma lista. Isto é
ilustrado abaixo.


::

    >>> range(10)
    range(0, 10)
    >>> list(range(10))
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    >>> range(5,10)
    range(5, 10)
    >>> list(range(5,10))
    [5, 6, 7, 8, 9]
    >>> list(range(5,10,2))
    [5, 7, 9]
    >>> list(range(10,1,-1))
    [10, 9, 8, 7, 6, 5, 4, 3, 2]
    >>>

..  The range object represents a sequence of integers. By default, it will
    start with 0. If you provide more parameters, it will start and end at
    particular points and can even skip items. In our first example,
    ``range(10)``, the sequence starts with 0 and goes up to but does not
    include 10. In our second example, ``range(5,10)`` starts at 5 and goes
    up to but not including 10. ``range(5,10,2)`` performs similarly but
    skips by twos (again, 10 is not included).

O objeto de intervalo representa uma sequência de inteiros. Por padrão, ela
começa com 0. Se você fornecer mais parâmetros, ela começará e terminará em
pontos específicos e pode até mesmo pular itens. Em nosso primeiro exemplo,
``range(10)``, a sequência começa com 0 e vai até, mas não
inclui, o 10. Em nosso segundo exemplo, ``range(5,10)`` começa em 5 e vai
até, mas não inclui, o 10. ``range(5,10,2)`` tem efeito similar, mas
pula de dois em dois (mais uma vez, 10 não está incluído).


..  **Strings** are sequential collections of zero or more letters, numbers
    and other symbols. We call these letters, numbers and other symbols
    *characters*. Literal string values are differentiated from identifiers
    by using quotation marks (either single or double).

**Strings** são coleções sequenciais de zero ou mais letras, números
e outros símbolos. Nós chamamos essas letras, números e outros símbolos de
*caracteres*. Valores literais de string são diferenciados dos identificadores
usando aspas (simples ou duplas).

::

    >>> "David"
    'daniel'
    >>> meuNome = "David"
    >>> meuNome[3]
    'i'
    >>> meuNome*2
    'DavidDavid'
    >>> len(meuNome)
    5
    >>>

..  Since strings are sequences, all of the sequence operations described
    above work as you would expect. In addition, strings have a number of
    methods, some of which are shown in :ref:`Table 4<tab_stringmethods>`. For example,

Como strings são sequências, todas as operações de sequência descritas
acima funcionam como seria de se esperar. Além disso, as strings têm vários
métodos, alguns dos quais são mostrados em :ref:`Tabela 4 <tab_stringmethods>`. Por exemplo,


::

    >>> meuNome
    'Daniel'
    >>> meuNome.upper()
    'DANIEL'
    >>> meuNome.center(10)
    '  Daniel  '
    >>> meuNome.find('n')
    2
    >>> meuNome.split('n')
    ['Da', 'iel']

..  Of these, ``split`` will be very useful for processing data. ``split``
    will take a string and return a list of strings using the split
    character as a division point. In the example, ``v`` is the division
    point. If no division is specified, the split method looks for
    whitespace characters such as tab, newline and space.

Destes, ``split`` será muito útil para processar dados. ``split``
pegará uma string e retornará uma lista de strings usando a string de
entrada como um ponto de divisão. No exemplo, ``v`` é o ponto de divisão.
Se nenhuma divisão for especificada, o método de divisão procurará
caracteres de espaço em branco, como tabulação, nova linha e espaço.


.. _tab_stringmethods:

.. table:: **Tabela 4: Métodos Nativos do Python para Strings**

    ======================== ========================= =======================================================================
          **Nome do método**        **Exemplo de Uso**                                                           **Descrição**
    ======================== ========================= =======================================================================
                  ``center``     ``astring.center(w)``                Retorna uma string centrada em um campo de tamanho ``w``
                   ``count``   ``astring.count(item)``                   Retorna o número de ocorrências de ``item`` na string
                   ``ljust``      ``astring.ljust(w)``  Retorna uma string justificada à esquerda em um campo de tamanho ``w``
                   ``lower``       ``astring.lower()``                                        Retorna uma string em minúsculas
                   ``rjust``      ``astring.rjust(w)``    etorna uma string justificada à direita em um campo de tamanho ``w``
                    ``find``    ``astring.find(item)``                     Retorna o índice da primeira ocorrência de ``item``
                   ``split``  ``astring.split(schar)``                            Divide uma string em substrings em ``schar``
    ======================== ========================= =======================================================================


..  A major difference between lists and strings is that lists can be
    modified while strings cannot. This is referred to as **mutability**.
    Lists are mutable; strings are immutable. For example, you can change an
    item in a list by using indexing and assignment. With a string that
    change is not allowed.

Uma diferença importante entre listas e strings é que as listas podem ser
modificado enquanto strings não podem. Isso é chamado de **mutabilidade**.
As listas são mutáveis; strings são imutáveis. Por exemplo, você pode alterar um
item em uma lista usando indexação e atribuição. Com uma string essa
mudança não é permitida.


::

    >>> minhaLista
    [1, 3, True, 6.5]
    >>> minhaLista[0]=2**10
    >>> minhaLista
    [1024, 3, True, 6.5]
    >>>
    >>> meuNome
    'daniel'
    >>> meuNome[0]='X'

    Traceback (most recent call last):
      File "<pyshell#84>", line 1, in -toplevel-
        meuNome[0]='X'
    TypeError: object doesn't support item assignment
    >>>

..  Tuples are very similar to lists in that they are heterogeneous
    sequences of data. The difference is that a tuple is immutable, like a
    string. A tuple cannot be changed. Tuples are written as comma-delimited
    values enclosed in parentheses. As sequences, they can use any operation
    described above. For example,

As tuplas são muito semelhantes às listas por serem sequências de dados heterogêneas. 
A diferença é que uma tupla é imutável, como uma string.
Uma tupla não pode ser alterada. As tuplas são escritas como valores delimitados por vírgula
fechados entre parênteses. Como sequências, eles podem usar qualquer operação
descrita acima. Por exemplo,

::

    >>> minhaTupla = (2,True,4.96)
    >>> minhaTupla
    (2, True, 4.96)
    >>> len(minhaTupla)
    3
    >>> minhaTupla[0]
    2
    >>> minhaTupla * 3
    (2, True, 4.96, 2, True, 4.96, 2, True, 4.96)
    >>> minhaTupla[0:2]
    (2, True)
    >>>

..  However, if you try to change an item in a tuple, you will get an error.
    Note that the error message provides location and reason for the
    problem.

Porém, se você tentar modificar um item em uma tupla, você vai obter um erro.
Note que a mensagem de erro fornece o local e a razão do problema.

::

    >>> minhaTupla[1]=False

    Traceback (most recent call last):
      File "<pyshell#137>", line 1, in -toplevel-
        minhaTupla[1]=False
    TypeError: object doesn't support item assignment
    >>>

..  A set is an unordered collection of zero or more immutable Python data
    objects. Sets do not allow duplicates and are written as comma-delimited
    values enclosed in curly braces. The empty set is represented by
    ``set()``. Sets are heterogeneous, and the collection can be assigned to
    a variable as below.

Um conjunto é uma coleção não ordenada de zero ou mais objetos de dados imutáveis do Python.
Conjuntos não permitem duplicatas e são gravados como valores delimitados por vírgula
fechados entre chaves. O conjunto vazio é representado por
``set()``. Conjuntos são heterogêneos e a coleção pode ser atribuída a
uma variável como abaixo.

::

    >>> {3,6,"cat",4.5,False}
    {False, 4.5, 3, 6, 'gato'}
    >>> umConjunto = {3,6,"cat",4.5,False}
    >>> umConjunto
    {False, 4.5, 3, 6, 'gato'}
    >>>

..  Even though sets are not considered to be sequential, they do support a
    few of the familiar operations presented earlier. :ref:`Table 5 <tab_setops>` reviews
    these operations and the following session gives examples of their use.

Mesmo que os conjuntos não sejam considerados sequenciais, eles suportam algumas 
das operações familiares apresentadas anteriormente. A :ref:`Tabela 5 <tab_setops>`
descreve estas operações e a seção seguinte dá exemplos de seu uso.

.. _tab_setops:

.. table:: **Tabela 5: Operações sobre Conjuntos em Python**

    =========================== ===================== ==================================================================================
           **Nome do Operador**          **Operador**                                                                      **Descrição**
    =========================== ===================== ==================================================================================
                    pertinência                    in                                                            se pertence ao conjunto
                         length                   len                                                Retorna a cardinalidade do conjunto
                          ``|``   ``aset | otherset``              Retorna um novo conjunto com todos os elementos de ambos os conjuntos
                          ``&``   ``aset & otherset``                    Retorna um novo conjunto com apenas os elementos comuns a ambos
                          ``-``   ``aset - otherset``   Retorna um novo conjunto com todos os itens do primeiro conjunto, não no segundo
                         ``<=``  ``aset <= otherset``               Pergunta se todos os elementos do primeiro conjunto estão no segundo
    =========================== ===================== ==================================================================================


::

    >>> umConjunto
    {False, 4.5, 3, 6, 'gato'}
    >>> len(umConjunto)
    5
    >>> False in umConjunto
    True
    >>> "dog" in umConjunto
    False
    >>>

..  Sets support a number of methods that should be familiar to those who
    have worked with them in a mathematics setting. :ref:`Table 6 <tab_setmethods>`
    provides a summary. Examples of their use follow. Note that ``union``,
    ``intersection``, ``issubset``, and ``difference`` all have operators
    that can be used as well.

Os conjuntos suportam vários métodos que devem ser familiares àqueles que já
trabalharam com eles em um contexto matemático. A :ref:`Tabela 6 <tab_setmethods>`
fornece um resumo e exemplos de seu uso. Note que ``union``,
``intersection``, ``issubset`` e ``difference`` possuem operadores
que pode ser usados também.


.. _tab_setmethods:

.. table:: **Tabela 6: Métodos Fornecidos para Conjuntos em Python**

    ======================== ================================= ==================================================================================
          **Nome do Método**                **Exemplo de Uso**                                                                      **Descrição**
    ======================== ================================= ==================================================================================
                   ``union``          ``aset.union(otherset)``              Retorna um novo conjunto com todos os elementos de ambos os conjuntos
            ``intersection``   ``aset.intersection(otherset)``       Retorna um novo conjunto com apenas os elementos comuns a ambos os conjuntos
              ``difference``     ``aset.difference(otherset)``   Retorna um novo conjunto com todos os itens do primeiro conjunto, não no segundo
                ``issubset``       ``aset.issubset(otherset)``                       Pergunta se todos os elementos de um conjunto estão no outro
                     ``add``                ``aset.add(item)``                                                          Adiciona item ao conjunto     
                  ``remove``             ``aset.remove(item)``                                                            Remove item do conjunto
                     ``pop``                    ``aset.pop()``                                          Remove um elemento arbitrário do conjunto
                   ``clear``                  ``aset.clear()``                                              Remove todos os elementos do conjunto   
    ======================== ================================= ==================================================================================


::

    >>> umConjunto
    {False, 4.5, 3, 6, 'gato'}
    >>> outroConjunto = {99,3,100}
    >>> umConjunto.union(outroConjunto)
    {False, 4.5, 3, 100, 6, 'gato', 99}
    >>> umConjunto | outroConjunto
    {False, 4.5, 3, 100, 6, 'gato', 99}
    >>> umConjunto.intersection(outroConjunto)
    {3}
    >>> umConjunto & outroConjunto
    {3}
    >>> umConjunto.difference(outroConjunto)
    {False, 4.5, 6, 'gato'}
    >>> umConjunto - outroConjunto
    {False, 4.5, 6, 'gato'}
    >>> {3,100}.issubset(outroConjunto)
    True
    >>> {3,100}<=outroConjunto
    True
    >>> umConjunto.add("house")
    >>> umConjunto
    {False, 4.5, 3, 6, 'casa', 'gato'}
    >>> umConjunto.remove(4.5)
    >>> umConjunto
    {False, 3, 6, 'casa', 'gato'}
    >>> umConjunto.pop()
    False
    >>> umConjunto
    {3, 6, 'casa', 'gato'}
    >>> umConjunto.clear()
    >>> umConjunto
    set()
    >>>

..  Our final Python collection is an unordered structure called a
    **dictionary**. Dictionaries are collections of associated pairs of
    items where each pair consists of a key and a value. This key-value pair
    is typically written as key:value. Dictionaries are written as
    comma-delimited key:value pairs enclosed in curly braces. For example,

Nossa última coleção do Python é uma estrutura desordenada chamada
**dicionário**. Dicionários são coleções de pares associados de
itens onde cada par consiste de uma chave e um valor. Este par chave-valor
é tipicamente escrito como chave:valor. Dicionários são escritos como pares
chave:valor separados por vírgula e delimitados por chaves. Por exemplo,

::

    >>> capitais = {'Amazonas':'Manaus','Paraná':'Curitiba'}
    >>> capitais
    {'Amazonas': 'Manaus', 'Paraná': 'Curitiba'}
    >>>

..  We can manipulate a dictionary by accessing a value via its key or by
    adding another key-value pair. The syntax for access looks much like a
    sequence access except that instead of using the index of the item we
    use the key value. To add a new value is similar.

Podemos manipular um dicionário acessando um valor por meio de sua chave ou
adicionando outro par chave-valor. A sintaxe de acesso se parece muito com um
acesso de sequência, exceto que em vez de usar o índice do item nós
usamos o valor da chave. Para adicionar um novo valor é semelhante.

.. activecode:: intro_7
    :caption: Usando um Dicionário

    capitais = {'Amazonas':'Manaus','Paraná':'Curitiba'}
    print(capitais['Amazonas'])
    capitais['Minas Gerais']='Belo Horizonte'
    print(capitais)
    capitais['Bahia']='Salvador'
    print(len(capitais))
    for k in capitais:
       print(capitais[k]," é a capital de[a/o] ", k)

..  capitals = {'Iowa':'DesMoines','Wisconsin':'Madison'}
    print(capitals['Iowa'])
    capitals['Utah']='SaltLakeCity'
    print(capitals)
    capitals['California']='Sacramento'
    print(len(capitals))
    for k in capitals:
    print(capitals[k]," is the capital of ", k)

..  It is important to note that the dictionary is maintained in no
    particular order with respect to the keys. The first pair added
    (``'Utah':`` ``'SaltLakeCity'``) was placed first in the dictionary and
    the second pair added (``'California':`` ``'Sacramento'``) was placed
    last. The placement of a key is dependent on the idea of “hashing,”
    which will be explained in more detail in Chapter 4. We also show the
    length function performing the same role as with previous collections.

É importante notar que o dicionário é mantido sem nenhuma
ordem em particular com relação às chaves. O primeiro par adicionado
(``'Amazonas':`` ``'Manaus'``) foi colocado primeiro no dicionário e
o segundo par adicionado (``'Bahia':`` ``'Salvador'``) foi colocado por
último. A colocação de uma chave depende da ideia de "hashing"
que será explicada em mais detalhes no Capítulo 4. Também mostramos
a função length executando o mesmo papel que nas coleções anteriores.

..  Dictionaries have both methods and operators. :ref:`Table 7 <tab_dictopers>` and
    :ref:`Table 8 <tab_dictmethods>` describe them, and the session shows them in action. The
    ``keys``, ``values``, and ``items`` methods all return objects that
    contain the values of interest. You can use the ``list`` function to
    convert them to lists. You will also see that there are two variations
    on the ``get`` method. If the key is not present in the dictionary,
    ``get`` will return ``None``. However, a second, optional parameter can
    specify a return value instead.


Os dicionários têm métodos e operadores, descritos na :ref:`Tabela 7 <tab_dictopers>` e
na :ref:`Tabela 8 <tab_dictmethods>`. A sessão de Python os mostra em ação.
Os métodos ``keys``, ``values`` e ``items`` retornam objetos que
contém os valores de interesse. Você pode usar a função ``list`` para
convertê-los em listas. Observe também que existem duas variações
no método ``get``. Se a chave não estiver presente no dicionário,
``get`` retornará ``None``. No entanto, um segundo parâmetro opcional pode
especificar um outro valor de retorno.


.. _tab_dictopers:

.. table:: **Tabela 7: Operadores Fornecidos por Dicionários em Python**

    ===================== ================== =============================================================================
             **Operador**        **Exemplo**                                                                 **Descrição**
    ===================== ================== =============================================================================
                   ``[]``      ``myDict[k]``                   Retorna o valor associado a ``k``, caso contrário é um erro
                   ``in``   ``key in adict``   Retorna ``True`` se key estiver no dicionário, ``False`` caso contrário
                  ``del`` del ``adict[key]``                                   Remove o item do dicionário associado a key       
    ===================== ================== =============================================================================



::

    >>> ramal={'daniel':1410,'adriana':1137}
    >>> ramal
    {'adriana': 1137, 'daniel': 1410}
    >>> ramal.keys()
    dict_keys(['adriana', 'daniel'])
    >>> list(ramal.keys())
    ['adriana', 'daniel']
    >>> ramal.values()
    dict_values([1137, 1410])
    >>> list(ramal.values())
    [1137, 1410]
    >>> ramal.items()
    dict_items([('adriana', 1137), ('daniel', 1410)])
    >>> list(ramal.items())
    [('adriana', 1137), ('daniel', 1410)]
    >>> ramal.get("pedro")
    >>> ramal.get("pedro","SEM RAMAL")
    'SEM RAMAL'
    >>>

.. _tab_dictmethods:

.. table:: **Table 8: Methods Provided by Dictionaries in Python**

    ======================== ==================== ===============================================================
          **Nome do Método**   **Exemplo de Uso**                                                   **Descrição**
    ======================== ==================== ===============================================================
                    ``keys``     ``adict.keys()``          Retorna as chaves do dicionário em um objeto dict_keys
                  ``values``   ``adict.values()``       Retorna os valores do dicionário em um objeto dict_values
                   ``items``    ``adict.items()``         Retorna os pares de chave-valor em um objeto dict_items
                     ``get``     ``adict.get(k)``      Retorna o valor associado a ``k``, ``None`` caso contrário
                     ``get`` ``adict.get(k,alt)``       Retorna o valor associado a ``k``, ``alt`` caso contrário
    ======================== ==================== ===============================================================


.. note::

    Essa área de trabalho é fornecida para sua conveniência. Você pode usar essa janela de activecode para testar qualquer coisa que desejar. 

    .. activecode:: scratch_01_01


