..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.

..  Programming Exercises
    #. Implement the simple methods ``getNum`` and ``getDen`` that will
    return the numerator and denominator of a fraction.
    #. In many ways it would be better if all fractions were maintained in
    lowest terms right from the start. Modify the constructor for the
    ``Fraction`` class so that ``GCD`` is used to reduce fractions
    immediately. Notice that this means the ``__add__`` function no
    longer needs to reduce. Make the necessary modifications.
    #. Implement the remaining simple arithmetic operators (``__sub__``,
    ``__mul__``, and ``__truediv__``).'
    #. Implement the remaining relational operators (``__gt__``,
    ``__ge__``, ``__lt__``, ``__le__``, and ``__ne__``)
    #. Modify the constructor for the fraction class so that it checks to
    make sure that the numerator and denominator are both integers. If
    either is not an integer the constructor should raise an exception.
    #. In the definition of fractions we assumed that negative fractions
    have a negative numerator and a positive denominator. Using a
    negative denominator would cause some of the relational operators to
    give incorrect results. In general, this is an unnecessary
    constraint. Modify the constructor to allow the user to pass a
    negative denominator so that all of the operators continue to work
    properly.
    #. Research the ``__radd__`` method. How does it differ from
    ``__add__``? When is it used? Implement ``__radd__``.
    #. Repeat the last question but this time consider the ``__iadd__``
    method.
    #. Research the ``__repr__`` method. How does it differ from
    ``__str__``? When is it used? Implement ``__repr__``.
    #. Research other types of gates that exist (such as NAND, NOR, and
   XOR). Add them to the circuit hierarchy. How much additional coding
   did you need to do?
    #. The most simple arithmetic circuit is known as the half-adder.
    Research the simple half-adder circuit. Implement this circuit.
    #. Now extend that circuit and implement an 8 bit full-adder.
    #. The circuit simulation shown in this chapter works in a backward
    direction. In other words, given a circuit, the output is produced by
    working back through the input values, which in turn cause other
    outputs to be queried. This continues until external input lines are
    found, at which point the user is asked for values. Modify the
    implementation so that the action is in the forward direction; upon
    receiving inputs the circuit produces an output.
    #. Design a class to represent a playing card. Now design a class to
    represent a deck of cards. Using these two classes, implement a
    favorite card game.
    #. Find a Sudoku puzzle in the local newspaper. Write a program to solve
    the puzzle.



Exercícios de Programação
-------------------------

#. Implemente os métodos ``getNum`` e ``getDen`` para retornar o numerador e o denominador de uma fração.

#. De muitas maneiras, seria melhor se todas as frações fossem mantidas em sua forma irredutível desde o início. Modifique o construtor da classe ``Fraction`` para que o ``MDC`` seja usado para reduzir as frações imediatamente. Note que isso significa que a função ``__add__`` não mais precisa reduzir. Faça as modificações necessárias.    

#. Implemente os operadores aritméticos restantes (``__sub__``, ``__mul__`` e ``__truediv__``). 

#. Implemente os operadores relacionais restantes (``__gt__``, ``__ge__``, ``__lt__``, ``__le__`` e ``__ne__``). 

#. Modifique o construtor da classe ``Fraction`` para que seja verificado que tanto o numerador quanto o denominador sejam ambos inteiros. Caso algum não for inteiro, o construtor deve levantar uma exceção.

#. Na definição de frações, assumimos que as frações negativas tem um numerador negativo e um denominador positivo. Usando um denominador negativo faria com que alguns dos operadores relacionais forneçam resultados incorretos. Em geral, essa é uma restrição desnecessária. Modifique o construtor para permitir que o usuário passe um denominador negativo para que todos os operadores continuem a funcionar devidamente.

#. Pesquise o método ``__radd__``. Qual a diferença para o ``__add__``? Quando ele é usado? Implemente o método ``__radd__``. 

#. Faça o mesmo para o método ``__iadd__``. 

#. Pesquise o método ``__repr__``. Qual a diferença para o ``__str__``? Quando ele é usado? Implemente o método ``__repr__``. 

#. Pesquise outros tipos de portas existentes (tal como NAND, NOR, e XOR). Inclua-os na hierarquia de circuitos. Quanto código a mais você precisou fazer?

#. O circuito aritmético mais simples é conhecido como meio somador (*half-adder*). Pesquise    sobre esse circuito e o implemente.


#. Agora estenda o circuito e implemente um somador completo (*full-adder*) de 8 bits.

#. A simulação de circuito mostrada neste capítulo trabalha o resultado na direção reversa (para trás). Em outras palavras, dado um circuito, a saída é produzida trabalhando da saída e voltando na direção dos valores de entrada, causando outras saídas a serem consultadas. Isso continua até que as linhas de entrada externas sejam encontradas. Nesse ponto os valores são solicitados ao usuário. Modifique o implementação de modo que a ação esteja na direção para frente; ao receber as entradas, o circuito produz uma saída.

#. Escreva uma classe que represente uma carta de baralho. Agora escreva uma classe que represente um baralho completo. Usando essas duas classes, implemente o seu jogo favorito de cartas. 

#. Encontre um jogo de Sudoku (em um jornal, revista, online, etc). Escreva um programa para resolvê-lo. 
