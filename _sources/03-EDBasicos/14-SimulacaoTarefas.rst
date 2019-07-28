..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


Simulação: Tarefas de Impressão
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Uma simulação mais interessante nos permite estudar o comportamento de uma
fila de impressão descrita anteriormente nesta seção. Lembre-se que como
as alunas e os alunos enviam tarefas de impressão para uma impressora compartilhada,
as tarefas são colocadas em uma fila para ser processada de maneira que a primeiro
a chegar seja a primeiro a ser atendida.
Muitas perguntas surgem com esta configuração.
A mais importante delas pode ser se a impressora é capaz de lidar com uma certa quantidade de
trabalhos.
Se não for possível, as alunos e os alunos aguardarão muito tempo pela impressão e
pode perder a próxima aula.

Considere a seguinte situação em um laboratório de ciência da computação.
Em qualquer dia en média cerca de 10 alunas ou alunos estão trabalhando no laboratório
em uma dado hora qualquer. Essas alunas e alunos costumam imprimir até duas vezes
durante esse período e o tamamho dessas tarefas varia de 1 a 20 páginas.
A impressora no laboratório é antiga, capaz de processar 10 páginas por minuto em qualidade de rascunho.
A impressora pode ser trocada para oferecer melhor qualidade, mas
produziria apenas cinco páginas por minuto. A velocidade de impressão mais lenta
poderia fazer as alunas e os alunos esperarem demais.
Qual frequência de impressão deve ser usada?

Poderíamos decidir em construir uma simulação que modela o laboratório.
Nós precisará construir representações para as alunas e alunos,
para astarefas de impressão e para a impressora (:ref:`Figura 4 <fig_qulabsim>`).
À medida que as alunas e alunos enviam tarefas de impressão,
vamos adicioná-las a uma lista de espera, uma fila de tarefas de impressão associada a impressora.
Quando a impressora concluir uma tarefa, ela examinará a
fila para ver se há alguma tarefa restante a ser processada.
De interesse para nós é a quantidade média de tempo que as alunas e alunos vão esperar
para que seus trabalhos sejam impressos.
Isso é igual à quantidade média de tempo que uma tarefa aguarda na fila.


.. _fig_qulabsim:

.. figure:: Figures/simulationsetup.png
   :align: center

   Figure 4: Fila de Impressão do Laboratório de Ciência da Computação


Para modelar essa situação, precisamos usar algumas probabilidades.
Por exemplo, as alunas e os alunos podem imprimir um documento de 1 a 20 páginas.
Se cada comprimento de 1 a 20 é igualmente provável, a duração de uma tarefa
de impressão pode ser simulada usando um número aleatório entre 1 e 20 inclusive.
Isto significa que há chance igual de qualquer comprimento de impressão de 1 a 20 entrar na fila.

Se houver 10 alunas e alunos no laboratório e cada uma delas e deles imprimir duas vezes,
haverá 20 tarefas de impressão por hora, em média. Qual é a probabilidade de que a qualquer
dado segundo, uma tarefa de impressão será criada?
A maneira de responder isso é considerar a razão de tarefas para o tempo.
20 tarefas por hora significa que, em média, haverá uma tarefa a cada 180 segundos:

:math:`\frac {20\ tarefas}{1\ hora} \times \frac {1\ hora}  {60\ minutos} \times \frac {1\ minuto} {60\ segundos}=\frac {1\ task} {180\ segundos}`

Para cada segundo podemos simular a chance de que uma tarefa de impressão ocorra
gerando um número aleatório entre 1 e 180 inclusive. Se o número for
180, dizemos que uma tarefa foi criada.
Note que é possível que muitas tarefas sejam criadas em seguida ou podemos esperar um bom tempo
para uma nova tarefa aparecer. Essa é a natureza da simulação. Você quer simular o
situação real, tanto quanto possível, dado que você sabe alguns parâmetros gerais.

Principais Passos da Simulação
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Aqui está a simulação principal.

#. Crie uma fila de tarefas de impressão. Cada tarefa será associada ao instante que chegou na fila (*timestamp*).
   Inicialmente a fila está vazia.

#. Para cada segundo (``currentSecond``):

   - Uma nova tarefa de impressão é criada? Em caso afirmativo, adicione-a à fila com
      o ``currentSecond`` como o instante associado.

   - Se a impressora não estiver ocupada e se uma tarefa estiver aguardando,

      - Remova a próxima tarefa da fila de impressão e atribua-a a impressora.

      - Subtrai o instante associado a tarefa do ``currentSecond`` para computar
         o tempo de espera para essa tarefa.

      - Anexe o tempo de espera dessa tarefa a uma lista para mais tarde ser
         processada.

      - Com base no número de páginas da tarefa de impressão, calcule o tempo será necessário
        para imprimi-la.

   - A impressora agora faz um segundo de impressão, se necessário. Também é 
      subtraido um segundo do tempo necessário para essa tarefa.

   - Se a tarefa foi concluída, em outras palavras, o tempo necessário
      chegou a zero, a impressora passa a estaar desocupada.

#. Após a conclusão da simulação, calcule o tempo médio de espera
   da lista de tempos de espera gerados.

Implementação em Python 
^^^^^^^^^^^^^^^^^^^^^^^

Para projetar esta simulação, criaremos classes para os três
objetos do mundo real descritos acima: ``Printer`` (Impressora), ``Task`` (Tarefa) e
``PrintQueue`` (Fila de impressão).

A classe ``Printer`` (:ref:`Listagem 2 <lst_printer>`) precisará rverificar se
há uma tarefa a ser impressa. Em caso afirmativo, ela está ocupado (linhas 13 a 17) e o
tempo necessário pode ser calculado a partir do número de páginas da tarefa.
O construtor também permitirá que a configuração de páginas por minuto seja
inicializada. O método ``tick`` diminui o representa o cronômetro interno e
determina que a impressora fique inativa (linha 11) se a tarefa tiver sido concluída.

.. _lst_printer:

**Listagem 2**

.. highlight:: python
    :linenothreshold: 5

::

   class Printer:
       def __init__(self, ppm):
           self.pagerate = ppm
           self.currentTask = None
           self.timeRemaining = 0

       def tick(self):
           if self.currentTask != None:
               self.timeRemaining = self.timeRemaining - 1
               if self.timeRemaining <= 0:
                   self.currentTask = None

       def busy(self):
           if self.currentTask != None:
               return True
           else:
               return False

       def startNext(self,newtask):
           self.currentTask = newtask
           self.timeRemaining = newtask.getPages() * 60/self.pagerate
                                
.. highlight:: python
    :linenothreshold: 500

A classe Task (:ref:`Listagem 3 <lst_task>`) representará uma única tarefa de impressão.
Quando a tarefa é criada, um gerador de números aleatórios fornecerá um
comprimento de 1 a 20 páginas. Nós escolhemos usar para isso a função ``randrange()``
do módulo ``random``.

::

    >>> import random
    >>> random.randrange(1,21)
    18
    >>> random.randrange(1,21)
    8
    >>> 

Cada tarefa também precisará manter o instante em que foi criada (*timestamp*) a ser usado para
computar o tempo de espera. Esse registro de data e hora representará o tempo em que a tarefa foi
criada e colocada na fila da impressora. O método ``waitTime()`` pode
então ser usado para recuperar a quantidade de tempo gasto na fila antes
a impressão começar.

.. _lst_task:

**Listagem 3**

.. highlight:: python
    :linenothreshold: 5

::

   import random
   
   class Task:
       def __init__(self,time):
           self.timestamp = time
           self.pages = random.randrange(1,21)

       def getStamp(self):
           return self.timestamp

       def getPages(self):
           return self.pages

       def waitTime(self, currenttime):
           return currenttime - self.timestamp
           
.. highlight:: python
   :linenothreshold: 500

A simulação principal (:ref:`Listagem 4 <lst_qumainsim>`) implementa o algoritmo
descrito acima. O objeto ``printQueue`` é uma instância da nossa TDA
fila (``queue``) existente. Uma função auxiliar booleana, ``newPrintTask()``, decide
se uma nova tarefa de impressão foi criada. Nós decidimos usar novamente
a função ``randrange()`` do módulo ``random`` para retornar um
inteiro aleatório entre 1 e 180. As tarefas de impressão chegam uma vez a cada 180
segundos. Ao escolher arbitrariamente 180 do intervalo de inteiros aleatórios
(linha 28), podemos simular esse evento aleatório. A função de simulação
nos permite definir o tempo total e as páginas por minuto para o
impressora.

.. _lst_qumainsim:

**Listagem 4**

.. highlight:: python
    :linenothreshold: 5

::

   from pythonds.basic.queue import Queue

   import random

   def simulation(numSeconds, pagesPerMinute):
       labprinter = Printer(pagesPerMinute)
       printQueue = Queue()
       waitingtimes = []

       for currentSecond in range(numSeconds):

         if newPrintTask():
            task = Task(currentSecond)
            printQueue.enqueue(task)

         if (not labprinter.busy()) and (not printQueue.isEmpty()):
           nexttask = printQueue.dequeue()
           waitingtimes.append(nexttask.waitTime(currentSecond))
           labprinter.startNext(nexttask)

         labprinter.tick()

       averageWait=sum(waitingtimes)/len(waitingtimes)
       print("Average Wait %6.2f secs %3d tasks remaining."
             %(averageWait,printQueue.size())) 

   def newPrintTask():
       num = random.randrange(1,181)
       if num == 180:
           return True
       else:
           return False

   for i in range(10):
       simulation(3600,5)
       
.. highlight:: python
   :linenothreshold: 500

Quando executamos a simulação, não devemos nos preocupar que o
os resultados são diferentes a cada vez. Isto é devido à natureza probabilística
dos números aleatórios. Estamos interessados ​​nas tendências que podem estar
ocorrendo como resultado dos ajustes dos parâmetros para a simulação.
Aqui estão alguns resultados.

Primeiro, executaremos a simulação por um período de 60 minutos (3.600
segundos) usando uma taxa de imperssão de cinco páginas por minuto.
Além disso, nós iremos executar 10 testes independentes.
Lembre-se que como a simulação
trabalha com números aleatórios cada execução retornará resultados diferentes.

::

    >>> for i in range(10):
          simulation(3600,5)

    Average Wait 165.38 secs 2 tasks remaining.
    Average Wait  95.07 secs 1 tasks remaining.
    Average Wait  65.05 secs 2 tasks remaining.
    Average Wait  99.74 secs 1 tasks remaining.
    Average Wait  17.27 secs 0 tasks remaining.
    Average Wait 239.61 secs 5 tasks remaining.
    Average Wait  75.11 secs 1 tasks remaining.
    Average Wait  48.33 secs 0 tasks remaining.
    Average Wait  39.31 secs 3 tasks remaining.
    Average Wait 376.05 secs 1 tasks remaining.

Depois de executar nossos 10 testes, podemos ver que o tempo médio  de espera (``Average Wait``)
é 122,09 segundos.
Você também pode ver que há uma grande variação no tempo médio de espera com um mínimo de 17,27
segundos e um máximo de 376,05 segundos.
Você também pode notar que em apenas dois dos casos foram todas as tarefas concluídas.

Agora, ajustaremos a taxa de páginas para 10 páginas por minuto e executaremos as 10
testes novamente, com uma frequência maior de páginas por segundo,
nossa esperança seria que mais tarefas seria concluídas no período de uma hora.

::

    >>>for i in range(10):
          simulation(3600,10)

    Average Wait   1.29 secs 0 tasks remaining.
    Average Wait   7.00 secs 0 tasks remaining.
    Average Wait  28.96 secs 1 tasks remaining.
    Average Wait  13.55 secs 0 tasks remaining.
    Average Wait  12.67 secs 0 tasks remaining.
    Average Wait   6.46 secs 0 tasks remaining.
    Average Wait  22.33 secs 0 tasks remaining.
    Average Wait  12.39 secs 0 tasks remaining.
    Average Wait   7.27 secs 0 tasks remaining.
    Average Wait  18.17 secs 0 tasks remaining.
    
    
Você pode executar a simulação em ActiveCode 2.

.. activecode:: qumainsim
   :caption: Simulação da Fila de Impressão
   :nocodelens:

   from pythonds.basic.queue import Queue

   import random
   
   class Printer:
       def __init__(self, ppm):
           self.pagerate = ppm
           self.currentTask = None
           self.timeRemaining = 0

       def tick(self):
           if self.currentTask != None:
               self.timeRemaining = self.timeRemaining - 1
               if self.timeRemaining <= 0:
                   self.currentTask = None

       def busy(self):
           if self.currentTask != None:
               return True
           else:
               return False

       def startNext(self,newtask):
           self.currentTask = newtask
           self.timeRemaining = newtask.getPages() * 60/self.pagerate   

   class Task:
       def __init__(self,time):
           self.timestamp = time
           self.pages = random.randrange(1,21)

       def getStamp(self):
           return self.timestamp

       def getPages(self):
           return self.pages

       def waitTime(self, currenttime):
           return currenttime - self.timestamp


   def simulation(numSeconds, pagesPerMinute):

       labprinter = Printer(pagesPerMinute)
       printQueue = Queue()
       waitingtimes = []

       for currentSecond in range(numSeconds):

         if newPrintTask():
            task = Task(currentSecond)
            printQueue.enqueue(task)

         if (not labprinter.busy()) and (not printQueue.isEmpty()):
           nexttask = printQueue.dequeue()
           waitingtimes.append( nexttask.waitTime(currentSecond))
           labprinter.startNext(nexttask)

         labprinter.tick()

       averageWait=sum(waitingtimes)/len(waitingtimes)
       print("Average Wait %6.2f secs %3d tasks remaining."%(averageWait,printQueue.size()))

   def newPrintTask():
       num = random.randrange(1,181)
       if num == 180:
           return True
       else:
           return False

   for i in range(10):
       simulation(3600,5)

Discussão
^^^^^^^^^

Nós estávamos tentando responder a uma pergunta sobre se a impressora 
poderia realmente lidar com a carga de tarefas se fosse configurado para imprimir
com uma melhor qualidade e taxa de página mais lenta.
A abordagem que tomamos foi escrever uma simulação que modelou as tarefas de
impressão como eventos aleatórios de vários comprimentos e
horários de chegada.

O resultado acima mostra que, com impressão de 5 páginas por minuto, o
tempo médio de espera variou de uma de 17 segundos para uma alta de 376
segundos (cerca de 6 minutos). Com uma taxa de impressão mais rápida, a variação 
foi de 1 segundo com um máximo de apenas 28 segundos. Além disso, com 5 páginas por minuto,
em 8 das 10 testes  havia tarefas de impressão ainda esperando na fila ao final da hora.

Portanto, talvez tenhamos sido persuadidos que diminuir a velocidade da impressora
para melhorar qualidade pode não ser uma boa ideia.
Estudantes não podem se dar ao luxo de esperar
por muito tempo por suas papeis, especialmente quando eles precisam ir para a próxima aula.
Uma espera de seis minutos seria simplesmente longa demais.

Este tipo de análise de simulação nos permite responder a muitas perguntas,
comumente conhecido como  perguntas do tipo "se" ("*what if*").
Tudo o que precisamos fazer é variar os parâmetros utilizados pela simulação e
podemos simular qualquer número de comportamentos interessantes. Por exemplo,

- E se o número médio de alunas e alunos  aumenta em 20?

- E se for sábado e os estudantes não precisarem ir para a aula? Eles podem se dar ao luxo de esperar?

- E se o tamanho da tarefa de impressão média diminuir desde que o Python é uma linguagem e programas tão poderosos tendem a ser muito mais curtos?

Todas estas questões podem ser respondidas modificando a simulação acima.
No entanto, é importante lembrar que a simulação é tão boa quanto
são as suposições  usadas para construí-lo. Dados reais sobre o número
de tarefas de impressão por hora e o número de alunas e alunos por hora era
necessário construir uma simulação robusta.

.. admonition:: Teste o seu conhecimento

   Como você modificaria a simulação da impressora para refletir um número maior de estudantes?  Suponha que o número de estudantes tenha dobrado.  Você precisa fazer algumas suposições razoáveis ​​sobre como essa simulação foi montada, mas o que você mudaria? Modifique o código. Suponha também que a duração da tarefa de impressão média tenha sido reduzida pela metade.  Altere o código para refletir essa alteração.  Finalmente, como você poderia parametrizar o número de alunos, em vez de alterar o código que gostaríamos?  Gostaríamos de tornar o número de estudantes um parâmetro da simulação. 

   .. actex:: print_sim_selfcheck
         :nocodelens:

         from pythonds.basic.queue import Queue

         import random

         class Printer:
             def __init__(self, ppm):
                 self.pagerate = ppm
                 self.currentTask = None
                 self.timeRemaining = 0

             def tick(self):
                 if self.currentTask != None:
                     self.timeRemaining = self.timeRemaining - 1
                     if self.timeRemaining <= 0:
                         self.currentTask = None

             def busy(self):
                 if self.currentTask != None:
                     return True
                 else:
                     return False

             def startNext(self,newtask):
                 self.currentTask = newtask
                 self.timeRemaining = newtask.getPages() * 60/self.pagerate

         class Task:
             def __init__(self,time):
                 self.timestamp = time
                 self.pages = random.randrange(1,21)

             def getStamp(self):
                 return self.timestamp

             def getPages(self):
                 return self.pages

             def waitTime(self, currenttime):
                 return currenttime - self.timestamp


         def simulation(numSeconds, pagesPerMinute):

             labprinter = Printer(pagesPerMinute)
             printQueue = Queue()
             waitingtimes = []

             for currentSecond in range(numSeconds):

               if newPrintTask():
                  task = Task(currentSecond)
                  printQueue.enqueue(task)

               if (not labprinter.busy()) and (not printQueue.isEmpty()):
                 nexttask = printQueue.dequeue()
                 waitingtimes.append(nexttask.waitTime(currentSecond))
                 labprinter.startNext(nexttask)

               labprinter.tick()

             averageWait=sum(waitingtimes)/len(waitingtimes)
             print("Average Wait %6.2f secs %3d tasks remaining." % (averageWait,printQueue.size()))

         def newPrintTask():
             num = random.randrange(1,181)
             if num == 180:
                 return True
             else:
                 return False

         for i in range(10):
             simulation(3600,5)

