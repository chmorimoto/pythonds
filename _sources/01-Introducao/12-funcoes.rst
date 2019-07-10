..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


..  Defining Functions

Definindo Funções
~~~~~~~~~~~~~~~~~

..  The earlier example of procedural abstraction called upon a Python
    function called ``sqrt`` from the math module to compute the square
    root. In general, we can hide the details of any computation by defining
    a function. A function definition requires a name, a group of
    parameters, and a body. It may also explicitly return a value. For
    example, the simple function defined below returns the square of the
    value you pass into it.

O exemplo anterior de abstração procedural chamou uma
função do Python chamada ``sqrt`` da biblioteca de funções matemáticas (``math``)  
para calcular a raiz quadrada.
Em geral, podemos ocultar os detalhes de qualquer computação definindo
uma função. Uma definição de função requer um nome, um grupo de
parâmetros e um corpo. Também pode retornar explicitamente um valor. 
Por exemplo, a função simples definida abaixo retorna o quadrado do
valor que você passa para ele.

::

    >>> def quadrado(n):
    ...    return n**2
    ...
    >>> quadrado(3)
    9
    >>> quadrado(quadrado(3))
    81
    >>>

..  The syntax for this function definition includes the name, ``square``,
    and a parenthesized list of formal parameters. For this function, ``n``
    is the only formal parameter, which suggests that ``square`` needs only
    one piece of data to do its work. The details, hidden “inside the box,”
    simply compute the result of ``n**2`` and return it. We can invoke or
    call the ``square`` function by asking the Python environment to
    evaluate it, passing an actual parameter value, in this case, ``3``.
    Note that the call to ``square`` returns an integer that can in turn be
    passed to another invocation.

A sintaxe para esta definição de função inclui o nome, ``quadrado``,
e uma lista de parâmetros formais entre parênteses. Para esta função, ``n``
é o único parâmetro formal, que sugere que ``quadrado`` precisa de apenas
um dado para fazer o seu trabalho. Os detalhes, escondidos "dentro da caixa"
simplesmente calcula o resultado de ``n ** 2`` e o retorna. Nós podemos invocar ou
chamar a função ``quadrado`` pedindo ao ambiente Python para
avaliá-lo, passando um valor como argumento, neste caso, ``3``.
Note que a chamada para ``quadrado`` retorna um inteiro que por sua vez pode ser
passado para outra chamada.

..  We could implement our own square root function by using a well-known
    technique called “Newton’s Method.” Newton’s Method for approximating
    square roots performs an iterative computation that converges on the
    correct value. The equation
    :math:`newguess = \frac {1}{2} * (oldguess + \frac {n}{oldguess})`
    takes a value :math:`n` and repeatedly guesses the square root by
    making each :math:`newguess` the :math:`oldguess` in the subsequent
    iteration. The initial guess used here is :math:`\frac {n}{2}`.
    :ref:`Listing 1 <lst_root>` shows a function definition that accepts a value
    :math:`n` and returns the square root of :math:`n` after making 20
    guesses. Again, the details of Newton’s Method are hidden inside the
    function definition and the user does not have to know anything about
    the implementation to use the function for its intended purpose.
    :ref:`Listing 1 <lst_root>` also shows the use of the # character as a comment
    marker. Any characters that follow the # on a line are ignored.

Poderíamos implementar nossa própria função de raiz quadrada usando uma
técnica chamada “Método de Newton”. O método de Newton para a aproximação
de raízes quadradas realiza um cálculo iterativo que converge para o
valor correto. A equação
:math:`raiz\_nova = \frac {1}{2} * (raiz\_anterior + \frac {n}{raiz\_anterior})`
assume um valor :math:`n` e aproxima repetidamente a raiz quadrada 
fazendo cada :math:`raiz\_nova` igual a  :math:`raiz\_anterior` na iteração seguinte.
O palpite inicial usado aqui é :math:`\frac {n}{2}`.
A :ref:`Listagem 1 <lst_root>` mostra uma definição de função que aceita um valor
:math:`n` e retorna a raiz quadrada de :math:`n` depois de fazer 20 aproximações.
Mais uma vez, os detalhes do Método de Newton estão escondidos dentro da
definição da função e o usuário não precisa saber nada sobre
a implementação para usar a função para o propósito pretendido.
A :ref:`Listagem 1 <lst_root>` também mostra o uso do caractere # como 
um marcador de comentário.
Quaisquer caracteres que seguem o # em uma linha são ignorados.




.. _lst_root:

**Listagem 1**

.. sourcecode:: python

    def raiz_quadrada(n):
        raiz = n/2    # chute inicial será 1/2 de n
        for k in range(20):
            raiz = (1/2)*(raiz + (n / raiz))

        return raiz


::

    >>>raiz_quadrada(9)
    3.0
    >>>raiz_quadrada(4563)
    67.549981495186216
    >>>

.. admonition:: Auto Avaliação

   Aqui está um auto-teste que realmente cobre tudo até agora. Você pode ter ouvido falar do teorema do macaco infinito? O teorema afirma que um macaco apertando teclas aleatoriamente em um teclado de máquina de escrever por um período infinito de tempo quase certamente digitará um determinado texto como as obras completas de William Shakespeare. Bem, suponha que substituímos um macaco por uma função Python. Quanto tempo você acha que seria necessário para uma função Python gerar apenas uma frase de Shakespeare? A frase que vamos tentar em inglês é: "methinks it is like a weasel" ("parece que é como uma doninha").   
   
   Você não vai querer rodar essa função no navegador, então abra seu IDE Python favorito. A maneira como vamos simular isso é escrever uma função que gera uma cadeia de 28 caracteres, escolhendo letras aleatórias das 26 letras do alfabeto inglês mais o espaço. Vamos escrever outra função que irá avaliar cada string gerada comparando a string gerada aleatoriamente com a meta.
   
   Uma terceira função irá chamar repetidamente as funções gerar e avaliar e, quando 100% das letras estiverem corretas, nós terminamos. Se as letras não estiverem corretas, geraremos uma string totalmente nova. Para facilitar o acompanhamento do progresso do programa, essa terceira função deve imprimir a melhor string gerada até agora e sua pontuação a cada 1000 tentativas.


.. admonition:: Auto Avaliação - Desafio

    Veja se você pode melhorar o programa na autoverificação mantendo as letras corretas e modificando apenas um caractere na melhor string até o momento. Este é um tipo de algoritmo da classe 'Hill Climbing', ou seja, só mantemos o resultado se for melhor que o anterior.

.. video:: monkeyvid
   :controls:
   :thumb: ../_static/videothumb.png

   http://media.interactivepython.org/pythondsVideos/monkeys.mov
   http://media.interactivepython.org/pythondsVideos/monkeys.webm


