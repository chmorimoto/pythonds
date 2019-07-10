..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Input and Output

Entrada e Saída
~~~~~~~~~~~~~~~

..  We often have a need to interact with users,
    either to get data or to provide some sort of result. Most programs
    today use a dialog box as a way of asking the user to provide some type
    of input. While Python does have a way to create dialog boxes, there is
    a much simpler function that we can use. Python provides us with a
    function that allows us to ask a user to enter some data and returns a
    reference to the data in the form of a string. The function is called
    ``input``.

Geralmente, precisamos interagir com os usuários
para obter dados ou fornecer algum tipo de resultado. A maioria dos programas
hoje usa uma caixa de diálogo como forma de pedir ao usuário para fornecer algum tipo
de entrada. Embora o Python tenha uma maneira de criar caixas de diálogo,
há uma função muito mais simples que podemos usar. O Python nos fornece uma
função que permite pedir a um usuário para inserir alguns dados e retorna um
referência aos dados na forma de uma string. A função é chamada
``input``.

..  Python’s input function takes a single parameter that is a string. This
    string is often called the **prompt** because it contains some helpful
    text prompting the user to enter something. For example, you might call
    input as follows:

A função ``input`` do Python recebe um único parâmetro que é uma string. 
Essa string é frequentemente chamada de **prompt** porque contém um 
texto informativo que informa o usuário para digitar alguma coisa. 
Por exemplo, você pode chamar a função ``input`` da seguinte forma:



::

    umNome = input('Por favor digite o seu nome: ')

..  Now whatever the user types after the prompt will be stored in the
    ``aName`` variable. Using the input function, we can easily write
    instructions that will prompt the user to enter data and then
    incorporate that data into further processing. For example, in the
    following two statements, the first asks the user for their name and the
    second prints the result of some simple processing based on the string
    that is provided.

Agora, o que o usuário digitar após o prompt será armazenado na
variável ``umNome``. Usando a função ``input``, podemos facilmente escrever
instruções que solicitarão ao usuário que insira dados e, em seguida,
incorporar esses dados no processamento. Por exemplo, nas duas 
seguintes instruções, a primeira pergunta ao usuário pelo nome e a
segunda imprime o resultado de algum processamento simples baseado na string
que fornecida.

.. activecode::  strstuff
    :caption: A Função ``input`` Retorna Uma String

    umNome = input('Por favor digite o seu nome: ')
    print("Seu nome todo em maiúsculas é", umNome.upper(), 
          "e tem comprimento", len(umNome))

..  It is important to note that the value returned from the ``input``
    function will be a string representing the exact characters that were
    entered after the prompt. If you want this string interpreted as another
    type, you must provide the type conversion explicitly. In the statements
    below, the string that is entered by the user is converted to a float so
    that it can be used in further arithmetic processing.

É importante notar que o valor retornado pela função ``input``
será uma string representando os caracteres exatos que foram
inserido após o prompt. Se você quiser que essa string seja interpretada como 
outro tipo, você deve fornecer a conversão de tipo explicitamente. Nas declarações
abaixo, a string inserida pelo usuário é convertida em um float
que pode ser usado em seguida para processamento aritmético.

::

    raio_str = input("Por favor digite o raio do círculo: ")
    raio = float(raio_str)
    diametro = 2 * raio

..  String Formatting

Formatação de Strings
^^^^^^^^^^^^^^^^^^^^^

..  We have already seen that the ``print``
    function provides a very simple way to output values from a Python
    program. ``print`` takes zero or more parameters and displays them using
    a single blank as the default separator. It is possible to change the
    separator character by setting the ``sep`` argument. In addition, each
    print ends with a newline character by default. This behavior can be
    changed by setting the ``end`` argument. These variations are shown in
    the following session:

Nós já vimos que a função ``print``
fornece uma maneira muito simples para exibir valores de saída de um programa em Python.
O ``print`` aceita zero ou mais parâmetros e os exibe usando
um único espaço em branco como o separador padrão. É possível alterar o
caracter separador, definindo o parâmetro opcional ``sep``. Além disso, cada ``print``
termina com um caractere de nova linha por default. Esse comportamento pode ser
alterado, definindo o parâmetro opcional ``end``. Estas variações são mostradas 
a seguir:

::

    >>> print("Olá")
    Olá
    >>> print("Olá","Mundo")
    Olá Mundo
    >>> print("Olá","Mundo", sep="***")
    Olá***Mundo
    >>> print("Olá","Mundo", end="***")
    Olá Mundo***
    >>>

..  It is often useful to have more control over the look of your output.
    Fortunately, Python provides us with an alternative called **formatted
    strings**. A formatted string is a template in which words or spaces
    that will remain constant are combined with placeholders for variables
    that will be inserted into the string. For example, the statement

Geralmente, é útil ter mais controle sobre a aparência da sua saída.
Felizmente, o Python nos fornece uma alternativa chamada **string de formatação**.
Uma string de formatação é um modelo (*template*) no qual palavras ou espaços
que permanecerão constantes são combinados com espaços reservados para variáveis
que serão inseridas na string. Por exemplo, o comando

::

    print(umNome, "tem", anos, "anos de idade.")

..  contains the words ``is`` and ``years old``, but the name and the age
    will change depending on the variable values at the time of execution.
    Using a formatted string, we write the previous statement as

contém as palavras ``tem `` e ``anos de idade`` que são constantes, 
mas o nome e a idade dependem do valor das variáveis no momento da execução.
Usando uma string de formatação, nós escrevemos o comando anterior como

::

    print("%s tem %d anos de idade." % (umNome, anos))


..  This simple example illustrates a new string expression. The ``%``
    operator is a string operator called the **format operator**. The left
    side of the expression holds the template or format string, and the
    right side holds a collection of values that will be substituted into
    the format string. Note that the number of values in the collection on
    the right side corresponds with the number of ``%`` characters in the
    format string. Values are taken—in order, left to right—from the
    collection and inserted into the format string.

Este exemplo simples ilustra uma nova expressão com strings. 
O operador ``%`` é chamado **operador de formatação**. O lado esquerdo
da expressão contém o modelo ou string de formatação, e o
lado direito contém uma coleção de valores que serão substituídos na
string de formatação. Observe que o número de valores na coleção 
do lado direito corresponde ao número de caracteres ``%`` na
string de formatação. Os valores são usados na sequência,
da esquerda para a direita da coleção e inseridos na string de formatação.

..  Let’s look at both sides of this formatting expression in more detail.
    The format string may contain one or more conversion specifications. A
    conversion character tells the format operator what type of value is
    going to be inserted into that position in the string. In the example
    above, the ``%s`` specifies a string, while the ``%d`` specifies an
    integer. Other possible type specifications include ``i``, ``u``, ``f``,
    ``e``, ``g``, ``c``, or ``%``. :ref:`Table 9 <tab_fmta>` summarizes all of the
    various type specifications.

Vamos ver os dois lados dessa expressão de formatação em mais detalhes.
A string de formatação pode conter uma ou mais especificações de conversão. Um
caractere de conversão informa ao operador de formatação que tipo de dado
vai ser inserido nessa posição na string. No exemplo
acima, o ``%s`` especifica uma string, enquanto o ``%d`` especifica um
inteiro. Outras especificações possíveis incluem ``i``, ``u``, ``f``,
``e``, ``g``, ``c`` ou ``%``. A :ref:`Tabela 9 <tab_fmta>` resume todos os
diversos tipos de caracteres de conversão.

.. _tab_fmta:

.. table:: **Tabela 9: Conversão de Caracteres para Formatação de Strings**

    ========================== ====================================================================================================
    **Caractere de conversão**                                                                                       **Usado para**
    ========================== ====================================================================================================
                  ``d``, ``i``                                                                                        Inteiro (int)
                         ``u``                                                                                    Inteiro sem sinal
                         ``f``                                                                 Ponto flutuante (float) como m.ddddd
                         ``e``                                                           Ponto flutuante (float) como m.ddddde+/-xx
                         ``E``                                                           Ponto flutuante (float) como m.dddddE+/-xx
                         ``g`` Usa ``%e`` com expoentes menores que :math:`-4` ou maiores que :math:`+5`, caso contrário usa ``%f``
                         ``c``                                                                           Inserir um único caractere
                         ``s``      String, ou qualquer tipo do Python que possa ser convertido para string usando a função ``str``
                         ``%``                                                                            Inserir um caractere ``%``
    ========================== ====================================================================================================


..  In addition to the format character, you can also include a format
    modifier between the ``%`` and the format character. Format modifiers may
    be used to left-justify or right-justifiy the value with a specified
    field width. Modifiers can also be used to specify the field width along
    with a number of digits after the decimal point. :ref:`Table 10 <tab_fmtaddsa>`
    explains these format modifiers

Além do caractere de conversão, você também pode incluir um modificador de formato
entre o caractere ``%`` e o caractere de conversão. Modificadores de formato podem
ser usados para justificar o valor à esquerda ou à direita, dentro de um campo 
com determinada largura. Modificadores também podem ser usados para especificar a largura do campo
bem como um número de dígitos após o ponto decimal. A :ref:`Tabela 10 <tab_fmtaddsa>`
explica esses modificadores de formato


.. _tab_fmtaddsa:

.. table:: **Tabela 10: Opções adicionais de formatação**

    ========================= ============= ==================================================================================================
              **Modificador**   **Exemplo**                                                                                     **Descrição**
    ========================= ============= ==================================================================================================
                       número      ``%20d``                                                        Coloca o valor em um campo de 20 caracteres
                        ``-``     ``%-20d``                                Coloca o valor em um campo de 20 caracteres, justificado à esquerda
                        ``+``     ``%+20d``                                 Coloca o valor em um campo de 20 caracteres, justificado à direita
                        ``0``     ``%020d``                       Coloca o valor em um campo de 20 caracteres, preenchido com zeros à esquerda
                        ``.``    ``%20.2f``           Coloca o valor em um campo de 20 caracteres, com 2 caracteres à direita do ponto decimal
                   ``(nome)``  ``%(nome)d``                               Coloca o valor associado à chave ``nome`` de um dicionário fornecido
    ========================= ============= ==================================================================================================


..  The right side of the format operator is a collection of values that
    will be inserted into the format string. The collection will be either a
    tuple or a dictionary. If the collection is a tuple, the values are
    inserted in order of position. That is, the first element in the tuple
    corresponds to the first format character in the format string. If the
    collection is a dictionary, the values are inserted according to their
    keys. In this case all format characters must use the ``(name)``
    modifier to specify the name of the key.

O lado direito do operador de formatação é uma coleção de valores que
será inserido na string de formatação. A coleção deve ser uma
tupla ou um dicionário. Se a coleção for uma tupla, os valores são
inseridos na mesma ordem da tupla. Ou seja, o primeiro elemento na tupla
corresponde ao primeiro caractere de conversão na string de formatação. Se a
coleção for um dicionário, os valores são inseridos de acordo com sua
chaves. Neste caso, todos os caracteres de formato devem usar o modificador
``(nome)`` para especificar o nome da chave.

::

    >>> preço = 24
    >>> item = "banana"
    >>> print("O preço do kilo de %s é %d reais"%(item,preço))
    O preço do kilo de banana é 24 reais
    >>> print("O preço do kilo de %+10s é %5.2d reais"%(item,preço))
    O preço do kilo de     banana é 24.00 reais
    >>> print("O preço do kilo de %+10s é %10.2f reais"%(item,preço))
    O preço do kilo de     banana é      24.00 reais
    >>> dicio = {"item":"banana","preço":24}
    >>> print("O preço do kilo de %(item)s é %(preço)7.1f reais"%dicio)
    O preço do kilo de banana é    24.0 reais
    >>>

..  In addition to format strings that use format characters and format
    modifiers, Python strings also include a ``format`` method that can be
    used in conjunction with a new ``Formatter`` class to implement complex
    string formatting. More about these features can be found in the Python
    library reference manual.

Além das strings de formatação que usam caracteres de conversão e modificadores
de formato, as strings do Python também incluem um método ``format`` que pode ser
usado em conjunto com uma nova classe ``Formatter`` para implementar 
formatações mais complexas. Mais sobre esses recursos podem ser encontrados
no manual de referência do Python.
