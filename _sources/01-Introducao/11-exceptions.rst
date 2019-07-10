..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Exception Handling

Tratamento de Exceções
~~~~~~~~~~~~~~~~~~~~~~

..  There are two types of errors that typically occur when writing
    programs. The first, known as a syntax error, simply means that the
    programmer has made a mistake in the structure of a statement or
    expression. For example, it is incorrect to write a for statement and
    forget the colon.

Existem dois tipos de erros que normalmente ocorrem ao escrever
programas. O primeiro, conhecido como erro de sintaxe, significa simplesmente que
programador cometeu um erro na estrutura de um comando ou
expressão. Por exemplo, é incorreto escrever um comado for e
esquecer os dois pontos.

::

    >>> for i in range(10)
    SyntaxError: invalid syntax (<pyshell#61>, line 1)

..  In this case, the Python interpreter has found that it cannot complete
    the processing of this instruction since it does not conform to the
    rules of the language. Syntax errors are usually more frequent when you
    are first learning a language.

Nesse caso, o interpretador Python descobriu que não pode concluir
o processamento desta instrução, uma vez que não está em conformidade com as
regras da linguagem. Erros de sintaxe são geralmente mais frequentes quando você
estão aprendendo uma linguagem.

..  The other type of error, known as a logic error, denotes a situation
    where the program executes but gives the wrong result. This can be due
    to an error in the underlying algorithm or an error in your translation
    of that algorithm. In some cases, logic errors lead to very bad
    situations such as trying to divide by zero or trying to access an item
    in a list where the index of the item is outside the bounds of the list.
    In this case, the logic error leads to a runtime error that causes the
    program to terminate. These types of runtime errors are typically called
    **exceptions**.

O outro tipo de erro, conhecido como erro lógico, denota uma situação
onde o programa é executado, mas dá o resultado errado. Isso pode ser devido
a um erro no algoritmo ou a um erro na sua tradução
do algoritmo. Em alguns casos, erros lógicos levam a 
situações muito ruins como tentar dividir por zero ou tentar acessar um item
de uma lista em que o índice do item está fora dos limites da lista.
Neste caso, o erro lógico leva a um erro de execução que faz com que o
programa termine. Esses tipos de erro em tempo de execução são geralmente chamados
de **exceções**.

..  Most of the time, beginning programmers simply think of exceptions as
    fatal runtime errors that cause the end of execution. However, most
    programming languages provide a way to deal with these errors that will
    allow the programmer to have some type of intervention if they so
    choose. In addition, programmers can create their own exceptions if they
    detect a situation in the program execution that warrants it.

Na maioria das vezes, os programadores iniciantes simplesmente pensam em exceções como
erros fatais em tempo de execução que causam o fim da execução. No entanto, a maioria
das linguagens de programação fornecem uma maneira de lidar com esses erros que
permitem ao programador algum tipo de intervenção, se assim desejarem.
Além disso, os programadores podem criar suas próprias exceções se
detectarem situações na execução do programa que as justifiquem.

..  When an exception occurs, we say that it has been “raised.” You can
    “handle” the exception that has been raised by using a ``try``
    statement. For example, consider the following session that asks the
    user for an integer and then calls the square root function from the
    math library. If the user enters a value that is greater than or equal
    to 0, the print will show the square root. However, if the user enters a
    negative value, the square root function will report a ``ValueError``
    exception.

Quando ocorre uma exceção, dizemos que ela foi "levantada". Você pode
"tratar" a exceção que foi levantada usando um comando ``try``.
Por exemplo, considere o seguinte fragmento de código que pergunta ao
usuário para digitar um inteiro e, em seguida, chama a função raiz quadrada (``sqrt``) da
biblioteca matemática (``math``). Se o usuário inserir um valor maior ou igual a
para 0, a impressão mostrará a raiz quadrada. No entanto, se o usuário inserir um
valor negativo, a função raiz quadrada irá reportar uma exceção do tipo ``ValueError``.

::

    >>> num = int(input("Digite um número inteiro: "))
    Digite um número inteiro: -23
    >>> print(math.sqrt(num))
    Traceback (most recent call last):
      File "<pyshell#102>", line 1, in <module>
        print(math.sqrt(num))
    ValueError: math domain error
    >>>

..  We can handle this exception by calling the print function from within a
    ``try`` block. A corresponding ``except`` block “catches” the exception
    and prints a message back to the user in the event that an exception
    occurs. For example:

Podemos lidar com essa exceção chamando a função print de dentro de um
bloco ``try``. Um bloco ``except`` correspondente "captura" a exceção
e imprime uma mensagem de volta ao usuário caso uma exceção
ocorra. Por exemplo:

::

    >>> try:
           print(math.sqrt(num))
        except:
           print("Valor impróprio para raiz quadrada")
           print("Usando valor absoluto em seu lugar")
           print(math.sqrt(abs(num)))

    Valor impróprio para raiz quadrada
    Usando valor absoluto em seu lugar
    4.79583152331
    >>>

..  will catch the fact that an exception is raised by ``sqrt`` and will
    instead print the messages back to the user and use the absolute value
    to be sure that we are taking the square root of a non-negative number.
    This means that the program will not terminate but instead will continue
    on to the next statements.

vai pegar o fato de que uma exceção é levantada por ``sqrt`` e vai
em vez disso, imprimir as mensagens de volta para o usuário e usar o valor absoluto
para ter certeza de que estamos pegando a raiz quadrada de um número não negativo.
Isso significa que o programa não terminará, mas continuará a executar 
os comandos seguintes.

..  It is also possible for a programmer to cause a runtime exception by
    using the ``raise`` statement. For example, instead of calling the
    square root function with a negative number, we could have checked the
    value first and then raised our own exception. The code fragment below
    shows the result of creating a new ``RuntimeError`` exception. Note that
    the program would still terminate but now the exception that caused the
    termination is something explicitly created by the programmer.

Também é possível para um programador causar uma exceção em tempo de execução
usando o comando ``raise``. Por exemplo, em vez de chamar a função
raiz quadrada com um número negativo, poderíamos primeiro ter verificado o
valor e, em seguida, levantar nossa própria exceção. O fragmento de código abaixo
mostra o resultado da criação de uma nova exceção do tipo ``RuntimeError`` (erro 
em tempo de execução). Observe que
o programa ainda terminaria, mas agora a exceção que causa o término
é algo explicitamente criado pelo programador.

::

    >>> if num < 0:
    ...    raise RuntimeError("Você não pode usar um valor negativo")
    ... else:
    ...    print(math.sqrt(num))
    ...
    Traceback (most recent call last):
      File "<stdin>", line 2, in <module>
    RuntimeError: Você não pode usar um valor negativo
    >>>

..  There are many kinds of exceptions that can be raised in addition to the
    ``RuntimeError`` shown above. See the Python reference manual for a list
    of all the available exception types and for how to create your own.

Existem muitos tipos de exceção que podem ser levantados além do
``RuntimeError`` mostrado acima. Veja o manual de referência do Python para uma lista
de todos os tipos de exceção disponíveis e de como criar suas próprias exceções.
