..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.

Exemplos de Árvores
-------------------

Agora que já conhecemos estruturas de dados lineares, como pilhas e filas,
e também adquirimos alguma experiência com recursão, nós iremos estudar
uma estrutura de dados muito comum chamada **árvore**. Árvores são usadas
em várias áreas da ciência da computação, incluindo sistemas operacionais,
computação gráfica, bancos de dados e redes. Estruturas de dados de árvores
têm muita coisa em comum com suas primas do mundo botânico. Toda árvore,
como estrutura de dados, tem uma raiz, ramificações e folhas. A diferença
entre uma árvore na natureza e uma árvore na ciência da computação é que
estruturas de dados de árvores têm sua raiz no topo e as folhas na base.

Antes de começarmos a estudar estruturas de dados de árvores, vamos dar
uma olhada em alguns exemplos recorrentes. Nosso primeiro exemplo de
árvore é uma árvore taxonômica da biologia. A :ref:`Figura 1 < fig_biotree>`
mostra um exemplo de classificação biológica de alguns animais. A partir
desse exemplo simples, podemos aprender diversas propriedades das
árvores. A primeira que esse exemplo demonstra é que árvores são
estruturas hierárquicas. Com isso, queremos dizer que árvores são
estruturadas em níveis, com as coisas mais gerais próximas ao topo
e as mais específicas próximas da base. O topo da hierarquia é o Reino,
o próximo nível da árvore (os "filhos" do nível superior) é o Filo,
depois a Classe, e assim por diante. Contudo, não importa o quanto
descemos na árvore taxonômica: todos os organismos sempre são animais.


.. _fig_biotree:

.. figure:: Figures/biology.png
   :scale: 50%
   :align: center
   :alt: image


   Figura 1: Taxonomia de Alguns Animais Comuns Mostrada como uma Árvore

Note que você pode começar pelo topo da árvore e descer por um caminho
definido por círculos e setas até a base. A cada nível da árvore podemos
fazer uma pergunta e seguir o caminho que está de acordo com a resposta
que procuramos. Por exemplo, podemos perguntar: "Este animal é um
Cordado ou um Artrópode?" Se a resposta for "Cordado", então seguimos
por esse caminho. Em seguida, podemos perguntar: "Este Cordado é um 
Mamífero?" Se não for, não temos mais como descer na árvore (pelo menos 
neste exemplo simplificado). Se estivermos no nível de Mamífero, podemos
perguntar: "Este Mamífero é um Primata ou um Carnívoro?" Nós podemos
continuar seguindo pelo caminho até que cheguemos às folhas da árvore,
onde está o nome comum.

Uma segunda propriedade das árvores é que todos os filhos de um nó são
independentes dos filhos de um outro nó. Por exemplo, o Gênero Felis
tem como filhos Domestica e Leo. O Gênero Musca também tem um filho
denominado Domestica, mas trata-se de um nó diferente, não relacionado
com o filho Domestica de Felis. Isso significa que nós podemos mudar o
nó filho de Musca sem afetar os filhos de Felis.

Uma terceira propriedade é que folha é única. Nós podemos especificar um
caminho da raiz da árvore até uma folha que identifica univocamente
cada espécie do reino animal. Por exemplo: Animalia
:math:`\rightarrow` Chordate :math:`\rightarrow` Mammal
:math:`\rightarrow` Carnivora :math:`\rightarrow` Felidae
:math:`\rightarrow` Felis :math:`\rightarrow` Domestica.

Outro exemplo de uma estrutura em árvore que você provavelmente utiliza
todo dia é a de um sistema de arquivos. Em um sistema de arquivos, diretórios
(ou pastas) estão estruturados como uma árvore. A :ref:`Figura 2 <fig_filetree>`
ilustra uma pequena amostra da hierarquia de um sistema de arquivos da
família Unix.

.. _fig_filetree:

.. figure:: Figures/directory.png
   :scale: 50%
   :align: center
   :alt: image

   Figura 2: Uma amostra da hierarquia de um sistema de arquivos Unix

A árvore do sistema de arquivos tem muito em comum com a árvore taxonômica.
Você pode seguir um caminho da raiz até qualquer diretório. Esse caminho
irá identificar univocamente esse subdiretório (e todos os arquivos
contidos nele). Uma outra propriedade importante das árvores, derivada
da sua natureza hierárquica, é que você pode mover porções inteiras de uma
árvore (chamada **subárvore**) para algum outro braço sem afetar seus níveis
hierárquicos inferiores. Por exemplo, nós poderíamos pegar a subárvore
com raiz em /etc/, desacoplar o diretório etc/ da raiz e reacoplá-lo
dentro de /usr/. Isso iria mudar o caminho que leva à pasta httpd de 
/etc/httpd para /usr/etc/httpd, mas não iria afetar o conteúdo ou os filhos
do diretório httpd.

Um último exemplo de um árvore é uma página web. O exemplo a seguir mostra
uma simples página web escrita em HTML. A :ref:`Figura 3 <fig_html>` mostra
a árvore que corresponde a cada tag HTML usada para criar a página. 

::

    <html xmlns="http://www.w3.org/1999/xhtml" 
	  xml:lang="en" lang="en">
    <head>
	<meta http-equiv="Content-Type" 
	      content="text/html; charset=utf-8" />
	<title>simple</title>
    </head>
    <body>
    <h1>A simple web page</h1>
    <ul>
	<li>List item one</li>
	<li>List item two</li>
    </ul>
    <h2><a href="http://www.cs.luther.edu">Luther CS </a><h2>
    </body>
    </html>


.. _fig_html:

.. figure:: Figures/htmltree.png
   :align: center
   :alt: image

   Figure 4: Uma árvore criada a partir de elementos de marcação de uma página web

O código fonte HTML e a árvore que acompanha esse código ilustram outro
tipo de hierarquia. Note que cada nível da árvore corresponde a uma nível de
aninhamento dentro das tags HTML. A primeira tag no código é ``<html>``
e a última é ``</html>``. Todas as demais tags na página estão contidas
dentro desse par. Se você verificar, irá constatar que essa propriedade
hierárquica de aninhamento vale para todos os níveis da árvore.


