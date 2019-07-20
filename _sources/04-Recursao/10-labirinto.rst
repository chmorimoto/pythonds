..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Exploring a Maze

Explorando um Labirinto
-----------------------

..  In this section we will look at a problem that has relevance to the
    expanding world of robotics: How do you find your way out of a maze? If you have
    a Roomba vacuum cleaner for your dorm room (don’t all college students?)
    you will wish that you could reprogram it using what you have learned in
    this section. The problem we want to solve is to help our turtle find
    its way out of a virtual maze. The maze problem has roots as deep as the
    Greek myth about Theseus who was sent into a maze to kill the minotaur.
    Theseus used a ball of thread to help him find his way back out again
    once he had finished off the beast. In our problem we will assume that
    our turtle is dropped down somewhere into the middle of the maze and
    must find its way out. Look at :ref:`Figure 2 <fig_mazescreen>` to get an idea of
    where we are going in this section.

Nesta seção, veremos um problema que tem relevância para o
mundo da robótica que está em rápida expansão: 
como você encontra o caminho para sair de um labirinto? Se você tem
um aspirador de pó Roomba para limpar o seu dormitório 
(como todos estudantes universitários?)
você vai querer poder reprogramá-lo usando o que você aprender nesta seção. 
O problema que queremos resolver é ajudar a nossa tartaruga a encontrar
a saída de um labirinto virtual. O problema do labirinto tem raízes tão profundas quanto
o mito grego sobre Teseu, que foi enviado a um labirinto para matar o minotauro.
Teseu usou uma bola de linha para ajudá-lo a encontrar o caminho de volta
depois de matar a fera. Em nosso problema, vamos supor que
nossa tartaruga é largada em algum lugar no meio do labirinto e
deve encontrar a saída. Veja a :ref:`Figura 2 <fig_mazescreen>` para ter uma ideia
do que faremos nesta seção.

.. _fig_mazescreen:

.. figure:: Figures/maze.png
   :align: center

   Figura 2: O Final do Programa de Busca da Saída do Labirinto


..  To make it easier for us we will assume that our maze is divided up into
    “squares.” Each square of the maze is either open or occupied by a
    section of wall. The turtle can only pass through the open squares of
    the maze. If the turtle bumps into a wall it must try a different
    direction. The turtle will require a systematic procedure to find its
    way out of the maze. Here is the procedure:
    -  From our starting position we will first try going North one square
    and then recursively try our procedure from there.
    -  If we are not successful by trying a Northern path as the first step
    then we will take a step to the South and recursively repeat our
    procedure.
    -  If South does not work then we will try a step to the West as our
    first step and recursively apply our procedure.
    -  If North, South, and West have not been successful then apply the
    procedure recursively from a position one step to our East.
    -  If none of these directions works then there is no way to get out of
    the maze and we fail.

Para simplificar o problema, vamos supor que o nosso labirinto é dividido em
"Quadrados". Cada quadrado do labirinto é aberto ou ocupado por uma
parede. A tartaruga só pode passar pelos quadrados abertos do 
labirinto. Se a tartaruga se chocar contra uma parede, ela deve tentar uma
outra direção. A tartaruga vai exigir um procedimento sistemático para encontrar
uma saída do labirinto. Aqui está o procedimento:

- Da nossa posição inicial, vamos primeiro tentar ir para o norte de um quadrado e depois recursivamente tentar o nosso procedimento a partir daí.

- Se não formos bem sucedidos, tentando um caminho pelo Norte como o primeiro passo, então vamos dar um passo para o sul e repetir nosso procedimento recursivamente.

- Se pelo sul não funcionar, então tentaremos dar um passo para o oeste e aplicar recursivamente o nosso procedimento.

- Se pelo norte, sul e oeste não acharmos um caminho até uma saída, então vamos aplicar o procedimento recursivamente a partir de um passo para o leste.

- Se nenhuma dessas direções funcionar, então não há como sair do labirinto e nós falhamos.

..  Now, that sounds pretty easy, but there are a couple of details to talk
    about first. Suppose we take our first recursive step by going North. By
    following our procedure our next step would also be to the North. But if
    the North is blocked by a wall we must look at the next step of the
    procedure and try going to the South. Unfortunately that step to the
    south brings us right back to our original starting place. If we apply
    the recursive procedure from there we will just go back one step to the
    North and be in an infinite loop. So, we must have a strategy to
    remember where we have been. In this case we will assume that we have a
    bag of bread crumbs we can drop along our way. If we take a step in a
    certain direction and find that there is a bread crumb already on that
    square, we know that we should immediately back up and try the next
    direction in our procedure. As we will see when we look at the code for
    this algorithm, backing up is as simple as returning from a recursive
    function call.

Agora, isso parece muito fácil, mas há alguns detalhes que devemos mencionar. 
Suponha que nosso primeiro passo recursivo foi para o norte.
Seguindo nosso procedimento, nosso próximo passo também seria para o norte. 
Mas se o norte estiver bloqueado por uma parede, devemos olhar para o próximo passo do
procedimento e tentar ir para o sul. Infelizmente esse passo para o
o sul nos traz de volta ao nosso ponto de partida original. Se aplicarmos
o procedimento recursivo a partir daí vamos apenas voltar um passo para o
norte e entrar em um loop infinito. Então, devemos ter uma estratégia para
que possamos lembrar das posições onde já estivemos. Neste caso, vamos supor que temos um
saco de migalhas de pão que podemos deixar cair ao longo do nosso caminho. 
Se dermos um passo em uma certa direção e acharmos uma migalha de pão no 
quadrado, sabemos que devemos voltar imediatamente e tentar a próxima
direção em nosso procedimento. Como veremos no código deste algoritmo, 
a volta é tão simples como retornar de uma chamada de função recursiva.

..  As we do for all recursive algorithms let us review the base cases. Some
    of them you may already have guessed based on the description in the
    previous paragraph. In this algorithm, there are four base cases to
    consider:

Como fazemos para todos os algoritmos recursivos, vamos revisar os casos base. 
Alguns deles você pode já ter adivinhado com base na descrição dada no
parágrafo anterior. Nesse algoritmo, há quatro casos base a serem
considerados:

..  #. The turtle has run into a wall. Since the square is occupied by a
    wall no further exploration can take place.
    #. The turtle has found a square that has already been explored. We do
    not want to continue exploring from this position or we will get into
    a loop.
    #. We have found an outside edge, not occupied by a wall. In other words
    we have found an exit from the maze.
    #. We have explored a square unsuccessfully in all four directions.

#. A tartaruga bateu em uma parede. Como o quadrado é ocupado por uma parede, não é possível seguir nessa direção.

#. A tartaruga encontrou um quadrado que já foi explorado. Não queremos continuar explorando a partir desta posição para não entraremos em loop.

#. Nós encontramos uma borda externa, não ocupada por uma parede. Em outras palavras, encontramos uma saída do labirinto.

#. Nós exploramos um quadrado em todas as quatro direções sem sucesso.

..  For our program to work we will need to have a way to represent the
    maze. To make this even more interesting we are going to use the turtle
    module to draw and explore our maze so we can watch this algorithm in
    action. The maze object will provide the following methods for us to use
    in writing our search algorithm:

Para que o nosso programa funcione, precisamos ter uma maneira de representar o
labirinto. Para tornar isso ainda mais interessante, vamos usar o módulo turtle
para desenhar e explorar o nosso labirinto para que possamos assistir o algoritmo em
ação. O objeto maze (labirinto) fornecerá os seguintes métodos para usarmos
no nosso algoritmo de busca:

- ``__init__`` lê um arquivo com um labirinto, inicializa a representação interna do labirinto, e define a posição inicial da tartaruga.

- ``drawMaze`` desenha o labirinto em uma janela na tela.

- ``updatePosition`` atualiza a representação interna do labirinto e altera a posição da tartaruga na janela.

- ``isExit`` verifica se a posição atual é uma saída do labirinto.

..  -  ``__init__`` Reads in a data file representing a maze, initializes
    the internal representation of the maze, and finds the starting
    position for the turtle.
    -  ``drawMaze`` Draws the maze in a window on the screen.
    -  ``updatePosition`` Updates the internal representation of the maze
    and changes the position of the turtle in the window.
    -  ``isExit`` Checks to see if the current position is an exit from the
    maze.

..  The ``Maze`` class also overloads the index operator ``[]`` so that our
    algorithm can easily access the status of any particular square.

A classe ``Maze`` também sobrescreve o operador de indexação ``[]`` para que nosso
algoritmo possa acessar facilmente o estado de qualquer quadrado em particular.

..  Let’s examine the code for the search function which we call
    ``searchFrom``. The code is shown in :ref:`Listing 3 <lst_mazesearch>`. Notice
    that this function takes three parameters: a maze object, the starting
    row, and the starting column. This is important because as a recursive
    function the search logically starts again with each recursive call.

Vamos examinar o código da função de procura que chamamos ``searchFrom``. 
O código é mostrado na :ref:`Listagem 3 <lst_mazesearch>`. Note
que esta função recebe três parâmetros: um objeto labirinto, a linha inicial 
e a coluna inicial. 
Isto é importante pois, como função recursiva,
a busca começa novamente com cada chamada recursiva.


.. _lst_mazesearch:

.. highlight:: python
    :linenothreshold: 5
    
**Listagem 3**

::

    def searchFrom(maze, startRow, startColumn):
        maze.updatePosition(startRow, startColumn)
       #  Check for base cases:
       #  1. We have run into an obstacle, return false
       if maze[startRow][startColumn] == OBSTACLE :
            return False
        #  2. We have found a square that has already been explored
        if maze[startRow][startColumn] == TRIED:
            return False
        # 3. Success, an outside edge not occupied by an obstacle
        if maze.isExit(startRow,startColumn):
            maze.updatePosition(startRow, startColumn, PART_OF_PATH)
            return True
        maze.updatePosition(startRow, startColumn, TRIED)

        # Otherwise, use logical short circuiting to try each 
        # direction in turn (if needed)
        found = searchFrom(maze, startRow-1, startColumn) or \
                searchFrom(maze, startRow+1, startColumn) or \
                searchFrom(maze, startRow, startColumn-1) or \
                searchFrom(maze, startRow, startColumn+1)
        if found:
            maze.updatePosition(startRow, startColumn, PART_OF_PATH)
        else:
            maze.updatePosition(startRow, startColumn, DEAD_END)
        return found

..  As you look through the algorithm you will see that the first thing the
    code does (line 2) is call ``updatePosition``. This is simply to help
    you visualize the algorithm so that you can watch exactly how the turtle
    explores its way through the maze. Next the algorithm checks for the
    first three of the four base cases: Has the turtle run into a wall (line
    5)? Has the turtle circled back to a square already explored (line 8)?
    Has the turtle found an exit (line 11)? If none of these conditions is
    true then we continue the search recursively.

Olhando o algoritmo, você verá que a primeira coisa que o código faz
(linha 2) é chamar o método ``updatePosition``. Isto serve para ajudar
você a visualizar o algoritmo para que você possa assistir exatamente como a tartaruga
explora seus caminhos no labirinto. Em seguida, o algoritmo verifica os
primeiros três dos quatro casos base: A tartaruga bateu numa parede (linha
5)? A tartaruga voltou para um quadrado já explorado (linha 8)?
A tartaruga encontrou uma saída (linha 11)? Se nenhuma dessas condições for
verdadeira então continuamos a busca recursivamente.

..  You will notice that in the recursive step there are four recursive
    calls to ``searchFrom``. It is hard to predict how many of these
    recursive calls will be used since they are all connected by ``or``
    statements. If the first call to ``searchFrom`` returns ``True`` then
    none of the last three calls would be needed. You can interpret this as
    meaning that a step to ``(row-1,column)`` (or North if you want to think
    geographically) is on the path leading out of the maze. If there is not
    a good path leading out of the maze to the North then the next recursive
    call is tried, this one to the South. If South fails then try West, and
    finally East. If all four recursive calls return false then we have
    found a dead end. You should download or type in the whole program and
    experiment with it by changing the order of these calls.

Você vai notar que na etapa recursiva há quatro chamadas
para ``searchFrom``. É difícil prever quantas dessas
chamadas recursivas serão usadas já que todas elas são conectadas por
operadores lógicos ``or``.
Se a primeira chamada para ``searchFrom`` retornar ``True`` então não é necessário
fazer nenhuma das três últimas chamadas.
Isso significa que um passo para ``(row-1, column)`` (ou norte se você quiser pensar
geograficamente) está no caminho que leva para fora do labirinto. Se não houver
um caminho pelo norte para fora do labirinto, a próxima chamada recursiva
é tentada, neste caso para o sul. Se essa chamada falhar, tenta-se pelo oeste e
finalmente pelo leste. Se todas as quatro chamadas recursivas falharem, então
encontramos um beco sem saída. Você pode baixar ou digitar todo o programa e
investigar o que ocorre quando a ordem dessas chamadas é alterada.

..  The code for the ``Maze`` class is shown in :ref:`Listing 4 <lst_maze>`, 
    :ref:`Listing 5 <lst_maze1>`, and :ref:`Listing 6 <lst_maze2>`. 
    The ``__init__`` method takes the name of a file as its
    only parameter. This file is a text file that represents a maze by using
    “+” characters for walls, spaces for open squares, and the letter “S” to
    indicate the starting position. :ref:`Figure 3 <fig_exmaze>` is an example of a
    maze data file. The internal representation of the maze is a list of
    lists. Each row of the ``mazelist`` instance variable is also a list.
    This secondary list contains one character per square using the
    characters described above. For the data file in :ref:`Figure 3 <fig_exmaze>` the
    internal representation looks like the following:

O código para a classe ``Maze`` (labirinto) 
é mostrado na :ref:`Listagem 4 <lst_maze>`,
:ref:`Listagem 5 <lst_maze1>`, e :ref:`Listagem 6 <lst_maze2>`.
O método ``__init__`` recebe o nome de um arquivo como seu
único parâmetro. Este é um arquivo de texto que representa um labirinto usando
o caractere "+" para paredes, espaço para quadrados abertos e a letra "S" para
indicar a posição inicial. A :ref:`Figura 3 <fig_exmaze>` mostra um exemplo de
arquivo com um labirinto. Internamente um labirinto é representado por uma lista de
listas. Cada linha da variável ``mazelist`` também é uma lista.
Esta lista secundária contém um caractere por quadrado usando os
caracteres descritos acima. Para o arquivo da :ref:`Figura 3 <fig_exmaze>` 
a representação interna seria parecida com:

.. highlight:: python
    :linenothreshold: 500

::

    [ ['+','+','+','+',...,'+','+','+','+','+','+','+'],
      ['+',' ',' ',' ',...,' ',' ',' ','+',' ',' ',' '],
      ['+',' ','+',' ',...,'+','+',' ','+',' ','+','+'],
      ['+',' ','+',' ',...,' ',' ',' ','+',' ','+','+'],
      ['+','+','+',' ',...,'+','+',' ','+',' ',' ','+'],
      ['+',' ',' ',' ',...,'+','+',' ',' ',' ',' ','+'],
      ['+','+','+','+',...,'+','+','+','+','+',' ','+'],
      ['+',' ',' ',' ',...,'+','+',' ',' ','+',' ','+'],
      ['+',' ','+','+',...,' ',' ','+',' ',' ',' ','+'],
      ['+',' ',' ',' ',...,' ',' ','+',' ','+','+','+'],
      ['+','+','+','+',...,'+','+','+',' ','+','+','+']]

..  The ``drawMaze`` method uses this internal representation to draw the
    initial view of the maze on the screen.

O método ``drawMaze`` usa esta representação interna para desenhar
o labirinto inicial na tela.

.. _fig_exmaze:


Figura 3: Um Exemplo de Arquivo com um Labirinto

::
    
      ++++++++++++++++++++++
      +   +   ++ ++     +   
      + +   +       +++ + ++
      + + +  ++  ++++   + ++
      +++ ++++++    +++ +  +
      +          ++  ++    +
      +++++ ++++++   +++++ +
      +     +   +++++++  + +
      + +++++++      S +   +
      +                + +++
      ++++++++++++++++++ +++


..  The ``updatePosition`` method, as shown in :ref:`Listing 5 <lst_maze1>` uses the
    same internal representation to see if the turtle has run into a wall.
    It also updates the internal representation with a “.” or “-” to
    indicate that the turtle has visited a particular square or if the
    square is part of a dead end. In addition, the ``updatePosition`` method
    uses two helper methods, ``moveTurtle`` and ``dropBreadCrumb``, to
    update the view on the screen.

O método ``updatePosition`` (atualiza posição), 
como mostrado na :ref:`Listagem 5 <lst_maze1>`, usa a
mesma representação interna para ver se a tartaruga bateu em uma parede.
Também atualiza a representação interna com um “.” ou “-” para
indicar que a tartaruga já visitou um determinado quadrado ou se o 
quadrado faz parte de um beco sem saída. Além disso, o método ``updatePosition``
usa dois métodos auxiliares, ``moveTurtle`` (move tartaruga) e 
``dropBreadCrumb`` (joga migalha), para atualizar a exibição na tela.

..  Finally, the ``isExit`` method uses the current position of the turtle
    to test for an exit condition. An exit condition is whenever the turtle
    has navigated to the edge of the maze, either row zero or column zero,
    or the far right column or the bottom row.

Finalmente, o método ``isExit`` (é saída) usa a posição atual da tartaruga
para testar uma condição de saída. Uma condição de saída é verdadeira quando 
a tartaruga alcança uma borda do labirinto, como a linha ou coluna zero,
ou a última linha (mais inferior) ou última coluna (extrema direita).

.. _lst_maze:

**Listagem 4**

.. highlight:: python
    :linenothreshold: 500

::

    class Maze:
        def __init__(self,mazeFileName):
            rowsInMaze = 0
            columnsInMaze = 0
            self.mazelist = []
            mazeFile = open(mazeFileName,'r')
            rowsInMaze = 0
            for line in mazeFile:
                rowList = []
                col = 0
                for ch in line[:-1]:
                    rowList.append(ch)
                    if ch == 'S':
                        self.startRow = rowsInMaze
                        self.startCol = col
                    col = col + 1
                rowsInMaze = rowsInMaze + 1
                self.mazelist.append(rowList)
                columnsInMaze = len(rowList)

            self.rowsInMaze = rowsInMaze
            self.columnsInMaze = columnsInMaze
            self.xTranslate = -columnsInMaze/2
            self.yTranslate = rowsInMaze/2
            self.t = Turtle(shape='turtle')
            setup(width=600,height=600)
            setworldcoordinates(-(columnsInMaze-1)/2-.5,
                                -(rowsInMaze-1)/2-.5,
                                (columnsInMaze-1)/2+.5,
                                (rowsInMaze-1)/2+.5)

.. _lst_maze1:

**Listagem 5**

::

        def drawMaze(self):
            for y in range(self.rowsInMaze):
                for x in range(self.columnsInMaze):
                    if self.mazelist[y][x] == OBSTACLE:
                        self.drawCenteredBox(x+self.xTranslate,
                                             -y+self.yTranslate,
                                             'tan')
            self.t.color('black','blue')

        def drawCenteredBox(self,x,y,color):
            tracer(0)
            self.t.up()
            self.t.goto(x-.5,y-.5)
            self.t.color('black',color)
            self.t.setheading(90)
            self.t.down()
            self.t.begin_fill()
            for i in range(4):
                self.t.forward(1)
                self.t.right(90)
            self.t.end_fill()
            update()
            tracer(1)

        def moveTurtle(self,x,y):
            self.t.up()
            self.t.setheading(self.t.towards(x+self.xTranslate,
                                             -y+self.yTranslate))
            self.t.goto(x+self.xTranslate,-y+self.yTranslate)

        def dropBreadcrumb(self,color):
            self.t.dot(color)

        def updatePosition(self,row,col,val=None):
            if val:
                self.mazelist[row][col] = val
            self.moveTurtle(col,row)

            if val == PART_OF_PATH:
                color = 'green'
            elif val == OBSTACLE:
                color = 'red'
            elif val == TRIED:
                color = 'black'
            elif val == DEAD_END:
                color = 'red'
            else:
                color = None
                
            if color:
                self.dropBreadcrumb(color)

.. _lst_maze2:

**Listagem 6**

::

       def isExit(self,row,col):
            return (row == 0 or
                    row == self.rowsInMaze-1 or
                    col == 0 or
                    col == self.columnsInMaze-1 )

       def __getitem__(self,idx):
            return self.mazelist[idx]


..  The complete program is shown in ActiveCode 1.  
    This program uses the data file ``maze2.txt`` shown below.
    Note that it is a much more simple example file in that the exit is very close to the starting position of the turtle.

O programa completo é mostrado no ActiveCode 1. 
Este programa usa o arquivo de dados ``maze2.txt`` mostrado abaixo.
Note que esse exemplo é muito mais simples
pois a saída é muito próxima da posição inicial da tartaruga.

.. raw:: html

	<pre id="maze2.txt">
  ++++++++++++++++++++++
  +   +   ++ ++        +
        +     ++++++++++
  + +    ++  ++++ +++ ++
  + +   + + ++    +++  +
  +          ++  ++  + +
  +++++ + +      ++  + +
  +++++ +++  + +  ++   +
  +          + + S+ +  +
  +++++ +  + + +     + +
  ++++++++++++++++++++++
    </pre>

.. activecode:: completemaze
    :caption: Solução Completa do Labirinto
    :nocodelens:
    :timelimit: off

    import turtle

    PART_OF_PATH = 'O'
    TRIED = '.'
    OBSTACLE = '+'
    DEAD_END = '-'

    class Maze:
        def __init__(self,mazeFileName):
            rowsInMaze = 0
            columnsInMaze = 0
            self.mazelist = []
            mazeFile = open(mazeFileName,'r')
            rowsInMaze = 0
            for line in mazeFile:
                rowList = []
                col = 0
                for ch in line[:-1]:
                    rowList.append(ch)
                    if ch == 'S':
                        self.startRow = rowsInMaze
                        self.startCol = col
                    col = col + 1
                rowsInMaze = rowsInMaze + 1
                self.mazelist.append(rowList)
                columnsInMaze = len(rowList)

            self.rowsInMaze = rowsInMaze
            self.columnsInMaze = columnsInMaze
            self.xTranslate = -columnsInMaze/2
            self.yTranslate = rowsInMaze/2
            self.t = turtle.Turtle()
            self.t.shape('turtle')
            self.wn = turtle.Screen()
            self.wn.setworldcoordinates(-(columnsInMaze-1)/2-.5,-(rowsInMaze-1)/2-.5,(columnsInMaze-1)/2+.5,(rowsInMaze-1)/2+.5)

        def drawMaze(self):
            self.t.speed(10)
            self.wn.tracer(0)        
            for y in range(self.rowsInMaze):
                for x in range(self.columnsInMaze):
                    if self.mazelist[y][x] == OBSTACLE:
                        self.drawCenteredBox(x+self.xTranslate,-y+self.yTranslate,'orange')
            self.t.color('black')
            self.t.fillcolor('blue')
            self.wn.update()
            self.wn.tracer(1)

        def drawCenteredBox(self,x,y,color):
            self.t.up()
            self.t.goto(x-.5,y-.5)
            self.t.color(color)
            self.t.fillcolor(color)
            self.t.setheading(90)
            self.t.down()
            self.t.begin_fill()
            for i in range(4):
                self.t.forward(1)
                self.t.right(90)
            self.t.end_fill()

        def moveTurtle(self,x,y):
            self.t.up()
            self.t.setheading(self.t.towards(x+self.xTranslate,-y+self.yTranslate))
            self.t.goto(x+self.xTranslate,-y+self.yTranslate)

        def dropBreadcrumb(self,color):
            self.t.dot(10,color)

        def updatePosition(self,row,col,val=None):
            if val:
                self.mazelist[row][col] = val
            self.moveTurtle(col,row)

            if val == PART_OF_PATH:
                color = 'green'
            elif val == OBSTACLE:
                color = 'red'
            elif val == TRIED:
                color = 'black'
            elif val == DEAD_END:
                color = 'red'
            else:
                color = None

            if color:
                self.dropBreadcrumb(color)

        def isExit(self,row,col):
            return (row == 0 or
                    row == self.rowsInMaze-1 or
                    col == 0 or
                    col == self.columnsInMaze-1 )
        
        def __getitem__(self,idx):
            return self.mazelist[idx]


    def searchFrom(maze, startRow, startColumn):
        # try each of four directions from this point until we find a way out.
        # base Case return values:
        #  1. We have run into an obstacle, return false
        maze.updatePosition(startRow, startColumn)
        if maze[startRow][startColumn] == OBSTACLE :
            return False
        #  2. We have found a square that has already been explored
        if maze[startRow][startColumn] == TRIED or maze[startRow][startColumn] == DEAD_END:
            return False
        # 3. We have found an outside edge not occupied by an obstacle
        if maze.isExit(startRow,startColumn):
            maze.updatePosition(startRow, startColumn, PART_OF_PATH)
            return True
        maze.updatePosition(startRow, startColumn, TRIED)
        # Otherwise, use logical short circuiting to try each direction 
        # in turn (if needed)
        found = searchFrom(maze, startRow-1, startColumn) or \
                searchFrom(maze, startRow+1, startColumn) or \
                searchFrom(maze, startRow, startColumn-1) or \
                searchFrom(maze, startRow, startColumn+1)
        if found:
            maze.updatePosition(startRow, startColumn, PART_OF_PATH)
        else:
            maze.updatePosition(startRow, startColumn, DEAD_END)
        return found


    myMaze = Maze('maze2.txt')
    myMaze.drawMaze()
    myMaze.updatePosition(myMaze.startRow,myMaze.startCol)

    searchFrom(myMaze, myMaze.startRow, myMaze.startCol)

..  Modify the maze search program so that the calls to searchFrom are in a different order.  Watch the program run. Can you explain why the behavior is different?  Can you predict what path the turtle will follow for a given change in order?

.. admonition:: Auto Avaliação

    Modifique o programa de procura no labirinto para que as chamadas para ``searchFrom`` estejam em uma ordem diferente. Veja o programa sendo executado. Você pode explicar porque o comportamento é diferente? Você pode prever qual caminho a tartaruga seguirá dada uma ordem determinada?

