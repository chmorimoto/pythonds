..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Notação O
~~~~~~~~~

Ao tentar caracterizar a eficiência de um algoritmo em termos de
tempo de execução, independente de qualquer programa ou computador em particular, é
importante quantificar o número de operações ou passos que o
algoritmo irá requerer. Se cada uma dessas etapas for considerada
unidade básica de computação, o tempo de execução de um algoritmo pode
ser expresso como o número de passos necessárias para resolver o problema.
Decidir sobre uma unidade básica apropriada de computação pode ser um
problema complicado e vai depender de como o algoritmo é implementado.

Uma boa unidade básica de computação para comparar os algoritmos de soma
mostrado anteriormente pode ser contar o número de instruções de atribuição
realizadas para calcular a soma. Na função ``sumOfN()``, o número de
instruções de atribuição é 1 (:math:`theSum = 0`)
mais o valor de *n* (o número de vezes que realizamos
:math:`theSum = theSum + i`). Podemos denotar isso por uma função, chame de T,
onde :math:`T (n) = 1 + n`. O parâmetro *n* é geralmente chamado de
o "tamanho do problema", e podemos ler isso como "T(n) é o tempo
gasto ou consumido para resolver um problema de tamanho n, ou seja, 1+n passos.”

Nas funções que representa o número de somas dada acima, faz sentido usar o número
de termos no somatório para denotar o tamanho do problema. Nós podemos então
dizer que a soma dos primeiros 100 mil inteiros é uma instância maior para
o problema da soma dos primeiros 1 mil. Por causa disso,
pode parecer razoável que o tempo necessário para resolver o problema maior
seja maior do que para o problema menor. Nosso objetivo, então, é mostrar como
o tempo de execução do algoritmo muda em relação ao tamanho do
problema, no caso *n*.

Cientistas de computação preferem levar essa técnica de análise um passo
mais distante. Acontece que o número exato de operações não é tão
importante como determinar a parte mais dominante da função :math:`T (n)`.
Em outras palavras, à medida que o problema aumenta, alguma parte
da função :math:`T (n)` tende a dominar o resto. Esta dominante
termo é o que, no final, é usado para comparação. A função **ordem de
magnitude**  descreve a parte de :math:`T (n)` que aumenta
mais rápidamente a medida que o valor de *n* cresce.
Ordem de magnitude é frequentemente chamado de notação **O grande** (*Big-O*), O de ordem,  e escrita como
:math:`O(f(n))`. Ela fornece uma aproximação útil para o número real
de passos o operações. A função :math:`f (n)` fornece
uma representação simples da parte dominante da função original :math:`T(n)`.

No exemplo acima, :math:`T (n) = 1 + n`. Quando *n* fica grande,
a constante 1 se tornará cada vez menos significativa para o resultado final.
E se estamos procurando uma aproximação para :math:`T (n)`, então podemos omitir
o 1 e simplesmente dizer que o tempo de execução é :math:`O (n)`.
É importante notar que o 1 é certamente significativo para
:math:`T(n)`. No entanto, como *n* fica grande, nossa aproximação será
igualmente preciso sem ele.

Como outro exemplo, suponha que, para algum algoritmo, o número exato de
passos é :math:`T(n) = 5n^{2} + 27n + 1005`.
Quando *n* é pequeno, digamos 1 ou 2, a constante 1005 parece ser a parte dominante da função.
No entanto, quando *n* fica maior, o termo :math:`n^{2}` torna-se o mais
importante. De fato, quando *n* é muito grande, os outros dois termos se tornam
insignificantes no papel que desempenham na determinação do
resultado e, no caso, consumo de tempo. Mais uma vez, para aproximar :math:`T(n)`
quando *n* fica grande, nós podemos
ignorar os outros termos e nos concentrar em :math:`5n^{2}`.
Além disso, o coeficiente :math:`5` torna-se insignificante quando *n* fica grande.
Nós diremos então que a função :math:`T (n)` tem uma ordem de magnitude
:math:`f(n)=n^{2}`, ou simplesmente que é :math:`O(n^{2})`.

Apesar de não vermos isso no exemplo da soma, às vezes o
o desempenho de um algoritmo depende dos valores exatos dos dados
em vez de simplesmente do tamanho do problema. Para esses tipos de
algoritmos que precisamos para caracterizar seu desempenho em termos de
**melhor caso**, **pior caso** ou **desempenho de caso médio**. O desempenho de pior caso
refere-se a um conjunto de dados específico em que o algoritmo tem um desempenho ruim.
Considerando que um conjunto diferente de dados para o mesmo algoritmo pode ter um desempenho
extraordinariamente bom. No entanto, na maioria
das vezes, o desempenho do algoritmo executa é entre esses dois extremos
(caso médio). É importante para um cientista da computação entender
essas distinções para que não sejam enganadas por um caso particular.


Algumas funções de ordem de grandeza são muito comuns quando estudamos o consumo de tempo
de algoritmos. Elas são mostradas em :ref:`Tabela 1 <tbl_fntable>`.
Para decidir qual dessas funções é a parte dominante de qualquer
função :math:`T (n)`, devemos ver como eles se comparam umas com os outras
a medida que *n* cresce.

.. _tbl_fntable: 

.. table:: **Tabela 1: Função comuns para notação O**

    ================= =============
             **f(n)**      **Nome**
    ================= =============
          :math:`1`      Constante
     :math:`\log n`    Logaritmica
          :math:`n`        Linear
    :math:`n\log n`    Log Linear
      :math:`n^{2}`    Quadrática
      :math:`n^{3}`        Cubica
      :math:`2^{n}`   Exponential
    ================= =============


:ref:`Figura 1 <fig_graphfigure>` mostra gráficos das funções comuns na
:ref:`Tabela 1 <tbl_fntable>`. Note que quando é pequeno, as funções não se diferenciam muito.
É difícil dizer qual é a dominante. Entretanto, quando *n* cresce, é fácil ver como elas se diferenciam
umas com as outras.

.. _fig_graphfigure:

.. figure:: Figures/newplot.png

   Figura 1: Gráfico de funções comuns como O grande


Como um exemplo final, suponha que temos o fragmento de código Python mostrado em
:ref:`Listagem 2 <lst_dummycode>`. Apesar desse programa não fazer nada de relevante é instrutivo de ve como examinamos um códio e analizamos o seu desempenho.

.. _lst_dummycode:

**Listagem 2**

::

    a=5
    b=6
    c=10
    for i in range(n):
       for j in range(n):
          x = i * i
          y = j * j
          z = i * j
    for k in range(n):
       w = a*k + 45
       v = b*b
    d = 33

O número de operações de atribuição é a soma de quatro termos.
O primeiro termo é a constante 3, representando as três instruções de atribuição no
começo do fragmento.
O segundo termo é :math:`3n^{2}`, pois há 
três fragmentos que são executados :math:`n^{2}` vezes devido
as iterações aninhadas. O terceiro termo é :math:`2n`, dois comandos
iterados *n* vezes. Finalmente, o quarto termo é a constante 1,
representando o último comando de atribuição. Isso nos dá
:math:`T(n)=3+3n^{2}+2n+1=3n^{2}+2n+4`. Ao olhar para os expoentes,
podemos ver facilmente que o termo :math:`n^{2}` é o dominante e
portanto o consumo de tempo desse fragmento de código é :math:`O(n^{2})`.
Note que todos os outros termos, bem como o coeficiente do termo dominante podem ser
ignorado a medida que  *n* cresce.

.. _fig_graphfigure2:

.. figure:: Figures/newplot2.png

   Figura 2: Comparação :math:`T(n)` com funções O grande comuns


ref:`Figura 2 <fig_graphfigure2>` mostra algumas das funções comuns como O grande
comparadas com a função :math:`T (n)` discutida acima. Observe que
:math:`T (n)` é inicialmente maior que a função cúbica. No entanto, a medida que 
n cresce, a função cúbica alcança rapidamente :math:`T (n)`. É fácil
ver que :math:`T (n)` então segue a função quadrática a medida que 
:math:`n` continua crescendo.


.. admonition:: Verifique a sua compreensão

    Escreva duas funções em Python para encontrar o número mínimo em uma lista. A primeira função deve comparar cada número com todos os demais números da lista. :math:`O(n^2)`. A segunda função deve ser linear :math:`O(n)`.

.. video::  findMinVid
   :controls:
   :thumb: ../_static/function_intro.png

   http://media.interactivepython.org/pythondsVideos/findmin.mov
   http://media.interactivepython.org/pythondsVideos/findmin.webm
