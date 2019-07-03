..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


.. What Is Computer Science?

O que é Ciência da Computação?
------------------------------

..  Computer science is often difficult to define. This is probably due to
    the unfortunate use of the word “computer” in the name. As you are
    perhaps aware, computer science is not simply the study of computers.
    Although computers play an important supporting role as a tool in the
    discipline, they are just that–tools.

Ciência da computação é muitas vezes difícil de definir. Isto é provavelmente devido
ao infeliz uso da palavra “computador” no nome. Como você está
talvez consciente, ciência da computação não é simplesmente o estudo de computadores.
Embora os computadores desempenhem um importante papel de apoio como ferramenta na
disciplina, eles são apenas isso - ferramentas.

..  Computer science is the study of problems, problem-solving, and the
    solutions that come out of the problem-solving process. Given a problem,
    a computer scientist’s goal is to develop an **algorithm**, a
    step-by-step list of instructions for solving any instance of the
    problem that might arise. Algorithms are finite processes that if
    followed will solve the problem. Algorithms are solutions.

A ciência da computação é o estudo de problemas, resolução de problemas e
soluções que surgem do processo de resolução de problemas. Dado um problema,
o objetivo de um cientista da computação é desenvolver um **algoritmo**, uma
lista passo-a-passo de instruções para resolver qualquer instância do
problema que possa surgir. Algoritmos são processos finitos que se
seguidos irão resolver o problema. Algoritmos são soluções.

..  Computer science can be thought of as the study of algorithms. However,
    we must be careful to include the fact that some problems may not have a
    solution. Although proving this statement is beyond the scope of this
    text, the fact that some problems cannot be solved is important for
    those who study computer science. We can fully define computer science,
    then, by including both types of problems and stating that computer
    science is the study of solutions to problems as well as the study of
    problems with no solutions.

A ciência da computação pode ser pensada como o estudo de algoritmos. Contudo,
devemos ter cuidado para considerar o fato de que alguns problemas podem não ter
solução. Embora provar esta afirmação esteja além do escopo deste
texto, o fato de que alguns problemas não podem ser resolvidos é importante para
aqueles que estudam ciência da computação. Podemos então definir ciência da computação,
de forma completa, incluindo os dois tipos de problemas e afirmando que a ciência da
computação é o estudo de soluções para problemas, bem como o estudo de
problemas sem nenhuma solução.

..  It is also very common to include the word **computable** when
    describing problems and solutions. We say that a problem is computable
    if an algorithm exists for solving it. An alternative definition for
    computer science, then, is to say that computer science is the study of
    problems that are and that are not computable, the study of the
    existence and the nonexistence of algorithms. In any case, you will note
    that the word “computer” did not come up at all. Solutions are
    considered independent from the machine.

Também é muito comum incluir a palavra ** computável**quando
descrevendo problemas e soluções. Nós dizemos que um problema é computável
se existe um algoritmo para resolvê-lo. Uma definição alternativa para
ciência da computação, então, é dizer que a ciência da computação é o estudo de
problemas que são e que não são computáveis, o estudo da
existência e inexistência de algoritmos. Note 
que a palavra "computador" não surgiu em nenhuma dessas definições. 
Soluções são consideradas independentes da máquina.

..  Computer science, as it pertains to the problem-solving process itself,
    is also the study of **abstraction**. Abstraction allows us to view the
    problem and solution in such a way as to separate the so-called logical
    and physical perspectives. The basic idea is familiar to us in a common
    example.

Ciência da computação, no que se refere ao próprio processo de resolução de problemas,
é também o estudo de **abstrações**. A abstração nos permite ver o
problema e solução de tal forma a separar as assim chamadas
perspectivas lógicas e físicas. 
A idéia básica deve-lhe ser familiar no seguinte exemplo.

..  Consider the automobile that you may have driven to school or work
    today. As a driver, a user of the car, you have certain interactions
    that take place in order to utilize the car for its intended purpose.
    You get in, insert the key, start the car, shift, brake, accelerate, and
    steer in order to drive. From an abstraction point of view, we can say
    that you are seeing the logical perspective of the automobile. You are
    using the functions provided by the car designers for the purpose of
    transporting you from one location to another. These functions are
    sometimes also referred to as the **interface**.

Considere o automóvel que você pode ter dirigido para a escola ou para o trabalho
hoje. Como motorista, um usuário do carro, você tem certas interações
que acontecem para utilizar o carro para o propósito pretendido.
Você entra, insere a chave, liga o carro, desliga, freia, acelera e controla 
a direção. Do ponto de vista da abstração, podemos dizer
que você está vendo a perspectiva lógica do automóvel. Você está
usando as funções fornecidas pelos projetistas do veículo com a finalidade de
transportar você de um local para outro. Essas funções são
às vezes também chamado de **interface**.

..  On the other hand, the mechanic who must repair your automobile takes a
    very different point of view. She not only knows how to drive but must
    know all of the details necessary to carry out all the functions that we
    take for granted. She needs to understand how the engine works, how the
    transmission shifts gears, how temperature is controlled, and so on.
    This is known as the physical perspective, the details that take place
    “under the hood.”

Por outro lado, o mecânico que deve reparar o seu automóvel tem um
ponto de vista muito diferente. Ela não só sabe dirigir, mas deve
conhecer todos os detalhes necessários para realizar todas as funções que nós
nem consideramos. Ela precisa entender como o motor funciona, como o
a transmissão muda as marchas, como a temperatura é controlada e assim por diante.
Isso é conhecido como a perspectiva física, os detalhes que ocorrem
"sob o capô."


..  The same thing happens when we use computers. Most people use computers
    to write documents, send and receive email, surf the web, play music,
    store images, and play games without any knowledge of the details that
    take place to allow those types of applications to work. They view
    computers from a logical or user perspective. Computer scientists,
    programmers, technology support staff, and system administrators take a
    very different view of the computer. They must know the details of how
    operating systems work, how network protocols are configured, and how to
    code various scripts that control function. They must be able to control
    the low-level details that a user simply assumes.

A mesma coisa acontece quando usamos computadores. A maioria das pessoas usa computadores
para escrever documentos, enviar e receber e-mails, navegar na web, tocar música,
armazenar imagens e jogar jogos sem qualquer conhecimento dos detalhes que
ocorrer para permitir que esses tipos de aplicativos funcionem. Eles veem
computadores de uma perspectiva lógica ou de usuário. Cientistas da computação,
programadores, equipe de suporte tecnológico e administradores de sistemas tem uma
visão muito diferente do computador. Eles devem saber os detalhes de como
funcionam os sistemas operacionais, como os protocolos de rede são configurados e como
codificar vários scripts que controlam o funcionamento. Eles devem ser capazes de controlar
os detalhes de baixo nível que um usuário simplesmente assume.


..  The common point for both of these examples is that the user of the
    abstraction, sometimes also called the client, does not need to know the
    details as long as the user is aware of the way the interface works.
    This interface is the way we as users communicate with the underlying
    complexities of the implementation. As another example of abstraction,
    consider the Python ``math`` module. Once we import the module, we can
    perform computations such as

O ponto comum para ambos os exemplos é que o usuário da
abstração, às vezes também chamado de cliente, não precisa conhecer os
detalhes, desde que o usuário esteja ciente da maneira como a interface funciona.
Essa interface é a maneira como nós, como usuários, nos comunicamos com as
complexidades inerentes da implementação. Como outro exemplo de abstração,
considere o módulo ``math`` do Python. Uma vez que importamos o módulo, podemos
realizar cálculos como


::

    >>> import math
    >>> math.sqrt(16)
    4.0
    >>>

..  This is an example of **procedural abstraction**. We do not necessarily
    know how the square root is being calculated, but we know what the
    function is called and how to use it. If we perform the import
    correctly, we can assume that the function will provide us with the
    correct results. We know that someone implemented a solution to the
    square root problem but we only need to know how to use it. This is
    sometimes referred to as a “black box” view of a process. We simply
    describe the interface: the name of the function, what is needed (the
    parameters), and what will be returned. The details are hidden inside
    (see :ref:`Figure 1 <fig_procabstraction>`).

Este é um exemplo de **abstração procedimental**. Nós não necessariamente
sabemos como a raiz quadrada está sendo calculada, mas sabemos o nome da
função e como usá-la. Se executarmos a importação
corretamente, podemos supor que a função nos fornecerá os
resultados corretos. Sabemos que alguém implementou uma solução para o
problema da raiz quadrada, mas só precisamos saber como usá-la. Isto é
às vezes referido como uma visão de “caixa preta” de um processo. Nós simplesmente
descrevemos a interface: o nome da função, o que é necessário (os
parâmetros) e o que será retornado. Os detalhes ficam escondidos 
(veja: ref: `Figura 1 <fig_procabstraction>`).


.. _fig_procabstraction:

.. figure::  Figures/blackbox.png
   :scale: 50 %
   :align: center

   Figura 1: Abstração Procedimental

